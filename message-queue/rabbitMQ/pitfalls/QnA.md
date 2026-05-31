# RabbitMQ Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_1501: What is the auto-ack mistake?

**Question:**
en: What is a common mistake when using `autoAck` in RabbitMQ consumers?
vi: Lỗi phổ biến khi dùng `autoAck` trong RabbitMQ consumer là gì?

**Answer:**
en: The mistake is enabling `autoAck` for important workloads, which can lose messages if the consumer crashes after receiving the message but before completing the business work.
vi: Lỗi phổ biến là bật `autoAck` cho workload quan trọng, điều này có thể làm mất message nếu consumer bị crash sau khi nhận message nhưng trước khi hoàn thành xử lý nghiệp vụ.

#### Q_LEVEL1_1502: What is the queue-as-database mistake?

**Question:**
en: What is the mistake in treating RabbitMQ like a permanent data store?
vi: Lỗi gì xảy ra khi xem RabbitMQ như một nơi lưu dữ liệu vĩnh viễn?

**Answer:**
en: The mistake is assuming messages will act like a durable business archive forever. RabbitMQ is a broker for delivery, not a general-purpose historical source of truth.
vi: Lỗi là giả định message sẽ đóng vai trò như kho lưu trữ nghiệp vụ bền vững mãi mãi. RabbitMQ là broker để giao message, không phải nguồn sự thật lịch sử dùng chung cho mọi mục đích.

### Level 2: Understanding

#### Q_LEVEL2_1601: Why is one huge queue a scaling trap?

**Question:**
en: Why can pushing too many unrelated workloads into one queue become a scaling and debugging trap?
vi: Vì sao dồn quá nhiều workload không liên quan vào một queue có thể trở thành bẫy về scaling và debugging?

**Answer:**
en: One huge queue mixes priorities, hides ownership, and makes it hard to tune prefetch, retry, and consumer concurrency for different workload shapes. Over time, one bad message pattern can affect many unrelated jobs.
vi: Một queue khổng lồ sẽ trộn lẫn priority, làm mờ ownership và khiến việc tinh chỉnh prefetch, retry và consumer concurrency cho các workload khác nhau trở nên khó khăn. Theo thời gian, chỉ một pattern message xấu cũng có thể ảnh hưởng đến nhiều job không liên quan.

#### Q_LEVEL2_1602: Why is skipping publisher confirms risky?

**Question:**
en: Why is publishing without confirms a reliability risk?
vi: Vì sao publish không dùng confirms lại là rủi ro về reliability?

**Answer:**
en: Without publisher confirms, the producer may assume the message was accepted even when the broker did not persist or route it successfully. That creates silent data-loss scenarios that are difficult to detect later.
vi: Nếu không có publisher confirm, producer có thể tưởng rằng message đã được chấp nhận dù broker chưa persist hoặc chưa route thành công. Điều đó tạo ra các tình huống mất dữ liệu âm thầm rất khó phát hiện về sau.

#### Q_LEVEL2_1603: Why is no DLQ strategy dangerous?

**Question:**
en: Why is running RabbitMQ without a dead-letter strategy dangerous?
vi: Vì sao vận hành RabbitMQ mà không có chiến lược dead-letter lại nguy hiểm?

**Answer:**
en: Without a DLQ or dead-letter exchange path, poisoned or invalid messages may loop forever, block healthy traffic, or disappear after repeated failures depending on the handling code.
vi: Nếu không có DLQ hoặc luồng dead-letter exchange, các message lỗi hoặc không hợp lệ có thể quay vòng vô tận, chặn traffic khỏe mạnh hoặc biến mất sau nhiều lần lỗi tùy theo code xử lý.

### Level 3: Applying

#### Q_LEVEL3_1701: Apply a dead-letter queue configuration

**Question:**
en: How would you configure a RabbitMQ queue so rejected messages flow to a dead-letter queue?
vi: Bạn sẽ cấu hình RabbitMQ queue như thế nào để các message bị reject được chuyển sang dead-letter queue?

**Answer:**
en: Declare the main queue with `x-dead-letter-exchange`, bind a dead-letter queue to that exchange, and reject unrecoverable messages without requeueing them. That keeps poison messages out of the hot path while preserving them for investigation.
vi: Hãy khai báo main queue với `x-dead-letter-exchange`, bind một dead-letter queue vào exchange đó và reject các message không thể phục hồi mà không requeue. Cách này giữ poison message ra khỏi luồng nóng nhưng vẫn bảo toàn chúng để điều tra.

```csharp
using RabbitMQ.Client;

var factory = new ConnectionFactory { HostName = "localhost" };
using var connection = await factory.CreateConnectionAsync();
using var channel = await connection.CreateChannelAsync();

await channel.ExchangeDeclareAsync("orders.dlx", ExchangeType.Direct, durable: true);
await channel.QueueDeclareAsync("orders.created.dlq", durable: true, exclusive: false, autoDelete: false);
await channel.QueueBindAsync("orders.created.dlq", "orders.dlx", "orders.created.dead");

var arguments = new Dictionary<string, object?>
{
    ["x-dead-letter-exchange"] = "orders.dlx",
    ["x-dead-letter-routing-key"] = "orders.created.dead"
};

await channel.QueueDeclareAsync(
    queue: "orders.created",
    durable: true,
    exclusive: false,
    autoDelete: false,
    arguments: arguments);
```

#### Q_LEVEL3_1702: Apply idempotent consumer protection

**Question:**
en: How would you protect a RabbitMQ consumer from duplicate delivery?
vi: Bạn sẽ bảo vệ RabbitMQ consumer như thế nào trước việc nhận trùng lặp?

**Answer:**
en: Persist a stable message ID or business key in the same consistency boundary as the side effect, then skip repeated deliveries that carry the same identity. RabbitMQ can redeliver, so idempotency belongs in the consumer design rather than in wishful assumptions about the broker.
vi: Hãy lưu một message ID ổn định hoặc business key trong cùng ranh giới nhất quán với side effect, rồi bỏ qua các lần giao lặp mang cùng danh tính đó. RabbitMQ có thể redeliver, nên idempotency phải nằm trong thiết kế consumer chứ không nên dựa vào kỳ vọng mơ hồ về broker.

```csharp
public sealed class ShipmentCreatedConsumer
{
    private readonly ShippingDbContext _db;

    public ShipmentCreatedConsumer(ShippingDbContext db)
    {
        _db = db;
    }

    public async Task HandleAsync(ShipmentCreatedMessage message, CancellationToken cancellationToken)
    {
        var alreadyProcessed = await _db.ProcessedMessages
            .AnyAsync(x => x.MessageId == message.MessageId, cancellationToken);

        if (alreadyProcessed)
        {
            return;
        }

        _db.ProcessedMessages.Add(new ProcessedMessage
        {
            MessageId = message.MessageId,
            ProcessedAtUtc = DateTime.UtcNow
        });

        _db.Shipments.Add(new Shipment
        {
            OrderId = message.OrderId,
            TrackingCode = message.TrackingCode
        });

        await _db.SaveChangesAsync(cancellationToken);
    }
}
```
