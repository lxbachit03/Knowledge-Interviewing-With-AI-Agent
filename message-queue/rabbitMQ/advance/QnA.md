# RabbitMQ Advance Q&A

### Level 4: Analyzing

#### Q_LEVEL4_1301: Analyze queue vs publish-subscribe fit

**Question:**
en: Analyze when RabbitMQ should be used as a work queue versus a publish-subscribe backbone.
vi: Phân tích khi nào RabbitMQ nên được dùng như work queue và khi nào nên dùng như publish-subscribe backbone.

**Answer:**
en: RabbitMQ is a strong fit as a work queue when tasks must be distributed across competing consumers for background processing, such as email sending or image resizing. It is a good publish-subscribe backbone when multiple independent consumers need the same event, but the team must still manage routing design, replay limitations, and schema evolution carefully.
vi: RabbitMQ phù hợp làm work queue khi tác vụ cần được phân phối cho các competing consumer để xử lý nền, ví dụ gửi email hoặc resize ảnh. Nó cũng phù hợp làm publish-subscribe backbone khi nhiều consumer độc lập cần cùng một event, nhưng team vẫn phải quản lý cẩn thận routing design, replay limitation và schema evolution.

#### Q_LEVEL4_1302: Analyze durability trade-offs

**Question:**
en: Analyze the trade-off between maximum durability and maximum throughput in RabbitMQ.
vi: Phân tích trade-off giữa độ bền tối đa và throughput tối đa trong RabbitMQ.

**Answer:**
en: Higher durability usually means durable queues, persistent messages, confirms, mirrored or quorum-style replication, and more disk I/O, which lowers peak throughput and increases latency. Pushing only for throughput can improve speed, but it increases the chance of message loss during broker failure or restart.
vi: Độ bền cao thường đòi hỏi durable queue, persistent message, confirm, replication kiểu mirrored hoặc quorum và nhiều disk I/O hơn, nên làm giảm throughput cực đại và tăng latency. Nếu chỉ tối ưu cho throughput thì tốc độ có thể tăng, nhưng nguy cơ mất message khi broker lỗi hoặc restart cũng cao hơn.

#### Q_LEVEL4_1303: Analyze requeue behavior

**Question:**
en: Why can naive requeue behavior create production instability in RabbitMQ?
vi: Vì sao requeue ngây thơ có thể gây bất ổn production trong RabbitMQ?

**Answer:**
en: If consumers requeue every failed message immediately, poison messages can circulate endlessly, hot partitions can form around bad payloads, and downstream dependencies can get hammered repeatedly. Stable systems separate transient failures from invalid messages and move unrecoverable payloads to a DLQ path.
vi: Nếu consumer requeue ngay mọi message lỗi, poison message có thể quay vòng vô tận, các payload xấu có thể tạo điểm nóng và downstream dependency sẽ bị đập lặp đi lặp lại. Hệ thống ổn định phải tách lỗi tạm thời khỏi message không hợp lệ và chuyển payload không thể phục hồi sang luồng DLQ.

### Level 5: Evaluating

#### Q_LEVEL5_1401: Evaluate RabbitMQ against direct HTTP calls

**Question:**
en: Evaluate RabbitMQ against direct HTTP communication between services.
vi: Đánh giá RabbitMQ so với giao tiếp HTTP trực tiếp giữa các service.

**Answer:**
en: Direct HTTP is simpler when one service needs an immediate response and failure handling can remain synchronous. RabbitMQ is the better choice when decoupling, buffering, workload smoothing, and asynchronous recovery matter more than immediate consistency and simpler debugging.
vi: HTTP trực tiếp đơn giản hơn khi một service cần phản hồi ngay và xử lý lỗi vẫn có thể giữ ở dạng đồng bộ. RabbitMQ là lựa chọn tốt hơn khi giảm coupling, buffer workload, làm mượt tải và phục hồi bất đồng bộ quan trọng hơn so với nhất quán tức thì và việc debug đơn giản.

#### Q_LEVEL5_1402: Evaluate RabbitMQ for event sourcing or long-term replay

**Question:**
en: Is RabbitMQ the best choice when the system needs long-term event retention and repeated replay?
vi: RabbitMQ có phải là lựa chọn tốt nhất khi hệ thống cần lưu giữ event lâu dài và replay nhiều lần không?

**Answer:**
en: Usually no. RabbitMQ is excellent for message delivery and workflow decoupling, but it is not primarily designed as a long-term event log. If the core requirement is durable retention with repeated consumer replay, another platform or an additional storage strategy is often a better fit.
vi: Thường là không. RabbitMQ rất tốt cho việc giao message và tách rời workflow, nhưng nó không được thiết kế chủ yếu như một event log lưu trữ dài hạn. Nếu yêu cầu cốt lõi là giữ event bền lâu và replay lặp lại nhiều lần, một nền tảng khác hoặc chiến lược lưu trữ bổ sung thường phù hợp hơn.

#### Q_LEVEL5_1403: Evaluate operational complexity

**Question:**
en: Evaluate whether RabbitMQ is a good choice for a team with weak operational maturity.
vi: Đánh giá liệu RabbitMQ có phải lựa chọn tốt cho một team có năng lực vận hành còn yếu hay không.

**Answer:**
en: It depends on the criticality and scale, but teams should not treat RabbitMQ as a free abstraction. Reliable use requires monitoring queue depth, consumer lag, connection health, redelivery patterns, dead-letter flow, and broker capacity. Without that discipline, RabbitMQ can hide failures until they become serious incidents.
vi: Điều đó còn tùy vào mức độ quan trọng và quy mô, nhưng team không nên xem RabbitMQ như một abstraction miễn phí. Để dùng đáng tin cậy, cần theo dõi queue depth, consumer lag, connection health, redelivery pattern, dead-letter flow và capacity của broker. Nếu thiếu kỷ luật này, RabbitMQ có thể che giấu lỗi cho đến khi chúng trở thành sự cố nghiêm trọng.
