# RabbitMQ Foundation Q&A

### Level 1: Remembering

#### Q_LEVEL1_1001: What is RabbitMQ?

**Question:**
en: What is RabbitMQ?
vi: RabbitMQ là gì?

**Answer:**
en: RabbitMQ is an open-source message broker that accepts messages from producers, routes them through exchanges, and delivers them to queues for consumers.
vi: RabbitMQ là một message broker mã nguồn mở, nhận message từ producer, định tuyến chúng qua exchange và chuyển vào queue cho consumer.

#### Q_LEVEL1_1002: What is a queue in RabbitMQ?

**Question:**
en: What is a queue in RabbitMQ?
vi: Queue trong RabbitMQ là gì?

**Answer:**
en: A queue is a buffer that stores messages until a consumer receives and processes them.
vi: Queue là nơi đệm để lưu message cho đến khi consumer nhận và xử lý chúng.

#### Q_LEVEL1_1003: What is an exchange in RabbitMQ?

**Question:**
en: What is an exchange in RabbitMQ?
vi: Exchange trong RabbitMQ là gì?

**Answer:**
en: An exchange is the routing component that receives published messages and decides which queue or queues should receive them.
vi: Exchange là thành phần định tuyến nhận message được publish và quyết định queue nào sẽ nhận message đó.

#### Q_LEVEL1_1004: What is a binding?

**Question:**
en: What is a binding in RabbitMQ?
vi: Binding trong RabbitMQ là gì?

**Answer:**
en: A binding is the relationship between an exchange and a queue, often configured with a routing rule such as a routing key pattern.
vi: Binding là mối liên kết giữa exchange và queue, thường được cấu hình với một quy tắc định tuyến như routing key pattern.

#### Q_LEVEL1_1005: What is a routing key?

**Question:**
en: What is a routing key in RabbitMQ?
vi: Routing key trong RabbitMQ là gì?

**Answer:**
en: A routing key is a string attached to a published message that exchanges can use to decide where that message should go.
vi: Routing key là chuỗi gắn với message khi publish để exchange dùng nó quyết định message sẽ được gửi đi đâu.

#### Q_LEVEL1_1006: What are the main exchange types?

**Question:**
en: What are the common exchange types in RabbitMQ?
vi: Các loại exchange phổ biến trong RabbitMQ là gì?

**Answer:**
en: The common exchange types are `direct`, `fanout`, `topic`, and `headers`, each using a different routing strategy.
vi: Các loại exchange phổ biến là `direct`, `fanout`, `topic` và `headers`, mỗi loại dùng một chiến lược định tuyến khác nhau.

#### Q_LEVEL1_1007: What is message acknowledgment?

**Question:**
en: What is message acknowledgment in RabbitMQ?
vi: Message acknowledgment trong RabbitMQ là gì?

**Answer:**
en: An acknowledgment is the signal from a consumer to RabbitMQ that the message was processed successfully and can be removed from the queue.
vi: Acknowledgment là tín hiệu từ consumer gửi cho RabbitMQ để xác nhận message đã được xử lý thành công và có thể bị xóa khỏi queue.

#### Q_LEVEL1_1008: What is message durability?

**Question:**
en: What does durability mean in RabbitMQ?
vi: Durability trong RabbitMQ nghĩa là gì?

**Answer:**
en: Durability means the broker is configured to survive restarts by using durable queues, durable exchanges, and persistent messages where needed.
vi: Durability nghĩa là broker được cấu hình để sống sót qua việc restart bằng cách dùng queue durable, exchange durable và persistent message khi cần.

#### Q_LEVEL1_1009: What is prefetch count?

**Question:**
en: What is prefetch count in RabbitMQ?
vi: Prefetch count trong RabbitMQ là gì?

**Answer:**
en: Prefetch count limits how many unacknowledged messages RabbitMQ can send to a consumer at one time.
vi: Prefetch count giới hạn số lượng message chưa được ack mà RabbitMQ có thể gửi cho một consumer tại cùng một thời điểm.

#### Q_LEVEL1_1010: What is a dead-letter exchange?

**Question:**
en: What is a dead-letter exchange in RabbitMQ?
vi: Dead-letter exchange trong RabbitMQ là gì?

**Answer:**
en: A dead-letter exchange is the exchange that receives messages rejected, expired, or over-delivered beyond configured limits, so they can be inspected or handled separately.
vi: Dead-letter exchange là exchange nhận các message bị reject, hết hạn hoặc vượt quá giới hạn phân phối đã cấu hình để chúng có thể được kiểm tra hoặc xử lý riêng.

### Level 2: Understanding

#### Q_LEVEL2_1101: Why do teams choose RabbitMQ?

**Question:**
en: Why do teams adopt RabbitMQ in distributed systems?
vi: Vì sao các team sử dụng RabbitMQ trong hệ thống phân tán?

**Answer:**
en: Teams use RabbitMQ to decouple services, absorb traffic spikes, distribute background work, and support asynchronous communication patterns more reliably than direct synchronous calls.
vi: Các team dùng RabbitMQ để giảm coupling giữa service, hấp thụ traffic tăng đột biến, phân phối background work và hỗ trợ giao tiếp bất đồng bộ đáng tin cậy hơn so với gọi đồng bộ trực tiếp.

#### Q_LEVEL2_1102: Direct vs fanout vs topic

**Question:**
en: How do `direct`, `fanout`, and `topic` exchanges differ?
vi: `direct`, `fanout` và `topic` exchange khác nhau như thế nào?

**Answer:**
en: A `direct` exchange routes by exact routing key match, `fanout` broadcasts to all bound queues, and `topic` routes using wildcard patterns such as `order.*` or `payment.#`.
vi: `direct` exchange định tuyến theo routing key khớp chính xác, `fanout` broadcast đến mọi queue đã bind, còn `topic` định tuyến bằng pattern có wildcard như `order.*` hoặc `payment.#`.

#### Q_LEVEL2_1103: Why are acknowledgments important?

**Question:**
en: Why are acknowledgments important in RabbitMQ consumer design?
vi: Vì sao acknowledgment quan trọng trong thiết kế consumer của RabbitMQ?

**Answer:**
en: Acknowledgments control message lifecycle. If consumers ack too early, messages can be lost after failures. If they never ack, messages will be redelivered and can block throughput.
vi: Acknowledgment kiểm soát vòng đời của message. Nếu consumer ack quá sớm, message có thể bị mất khi có lỗi. Nếu không ack, message sẽ bị redeliver và có thể làm nghẽn throughput.

#### Q_LEVEL2_1104: Why does prefetch matter?

**Question:**
en: Why does prefetch configuration affect throughput and fairness?
vi: Vì sao cấu hình prefetch ảnh hưởng đến throughput và fairness?

**Answer:**
en: A high prefetch can improve throughput by keeping consumers busy, but it may also let one slow consumer hold too many messages. A lower prefetch improves fairness and backpressure at the cost of raw throughput.
vi: Prefetch cao có thể tăng throughput vì giữ consumer luôn bận, nhưng cũng có thể khiến một consumer chậm giữ quá nhiều message. Prefetch thấp cải thiện fairness và backpressure nhưng phải đánh đổi throughput thuần.

#### Q_LEVEL2_1105: Persistent messages are not enough

**Question:**
en: Why is marking messages as persistent not a complete reliability strategy?
vi: Vì sao chỉ đánh dấu message là persistent vẫn chưa đủ cho reliability?

**Answer:**
en: Persistent messages help survive broker restarts, but reliability still depends on durable queues, publisher confirms, consumer acknowledgments, and safe retry or DLQ handling.
vi: Persistent message giúp sống sót qua broker restart, nhưng reliability vẫn còn phụ thuộc vào durable queue, publisher confirm, consumer acknowledgment và cơ chế retry hoặc DLQ an toàn.

### Level 3: Applying

#### Q_LEVEL3_1201: Apply publisher confirms

**Question:**
en: How would you publish a RabbitMQ message more safely from a C# producer?
vi: Bạn sẽ publish một RabbitMQ message an toàn hơn từ C# producer như thế nào?

**Answer:**
en: Declare the exchange and queue durably, publish persistent messages, and enable publisher confirms so the producer knows whether RabbitMQ accepted the message.
vi: Hãy khai báo exchange và queue ở chế độ durable, publish persistent message và bật publisher confirm để producer biết RabbitMQ đã chấp nhận message hay chưa.

```csharp
using RabbitMQ.Client;
using System.Text;

var factory = new ConnectionFactory { HostName = "localhost" };
using var connection = await factory.CreateConnectionAsync();
using var channel = await connection.CreateChannelAsync();

await channel.ExchangeDeclareAsync("orders.direct", ExchangeType.Direct, durable: true);
await channel.QueueDeclareAsync("orders.created", durable: true, exclusive: false, autoDelete: false);
await channel.QueueBindAsync("orders.created", "orders.direct", "order.created");

var body = Encoding.UTF8.GetBytes("""{"orderId":"A1001","status":"Created"}""");
var properties = new BasicProperties
{
    Persistent = true
};

await channel.ConfirmSelectAsync();
await channel.BasicPublishAsync(
    exchange: "orders.direct",
    routingKey: "order.created",
    mandatory: true,
    basicProperties: properties,
    body: body);
await channel.WaitForConfirmsOrDieAsync();
```

#### Q_LEVEL3_1202: Apply safe consumer acknowledgment

**Question:**
en: How would you design a RabbitMQ consumer to ack only after successful processing?
vi: Bạn sẽ thiết kế RabbitMQ consumer như thế nào để chỉ ack sau khi xử lý thành công?

**Answer:**
en: Process the message first, commit the business effect, and only then send `BasicAck`. If processing fails, reject or requeue based on whether the failure is transient or unrecoverable.
vi: Hãy xử lý message trước, commit hiệu ứng nghiệp vụ, sau đó mới gửi `BasicAck`. Nếu xử lý thất bại, hãy reject hoặc requeue tùy theo lỗi là tạm thời hay không thể phục hồi.

```csharp
using RabbitMQ.Client;
using RabbitMQ.Client.Events;
using System.Text;

var factory = new ConnectionFactory { HostName = "localhost" };
using var connection = await factory.CreateConnectionAsync();
using var channel = await connection.CreateChannelAsync();

await channel.BasicQosAsync(prefetchSize: 0, prefetchCount: 10, global: false);
var consumer = new AsyncEventingBasicConsumer(channel);

consumer.ReceivedAsync += async (_, ea) =>
{
    var json = Encoding.UTF8.GetString(ea.Body.ToArray());

    try
    {
        await ProcessOrderAsync(json);
        await channel.BasicAckAsync(ea.DeliveryTag, multiple: false);
    }
    catch (ValidationException)
    {
        await channel.BasicRejectAsync(ea.DeliveryTag, requeue: false);
    }
    catch
    {
        await channel.BasicNackAsync(ea.DeliveryTag, multiple: false, requeue: true);
    }
};

await channel.BasicConsumeAsync("orders.created", autoAck: false, consumer);
```
