# Entity Framework Core Advance Q&A

### Level 4: Analyzing

#### Q_LEVEL4_311: Analyze N+1 query problems.

**Question:**
en: Analyze how an N+1 query problem happens in EF Core.
vi: Phân tích cách lỗi **N+1 query** xảy ra trong EF Core.

**Answer:**
en: N+1 happens when code loads a list of parent rows and then triggers an extra query for related data per row, often by careless navigation access or lazy loading. The result is many small database round trips, which can destroy API latency under load. The fix is to shape the query intentionally with projection, `Include`, or a different aggregation strategy.
vi: **N+1** xảy ra khi code tải danh sách bản ghi cha rồi lại phát sinh thêm một query cho dữ liệu liên quan của từng bản ghi, thường do truy cập navigation thiếu kiểm soát hoặc lazy loading. Kết quả là database phải xử lý rất nhiều lần round-trip nhỏ, làm độ trễ API tăng mạnh khi có tải. Cách xử lý là thiết kế truy vấn có chủ đích bằng projection, `Include` hoặc chiến lược gom dữ liệu khác.

#### Q_LEVEL4_327: Analyze large object graphs and over-fetching.

**Question:**
en: Analyze why loading large entity graphs can hurt EF Core application performance.
vi: Phân tích vì sao việc tải graph entity quá lớn có thể làm ứng dụng EF Core chậm đi.

**Answer:**
en: Pulling entire entities plus multiple related collections increases SQL complexity, memory usage, and tracking cost. Often the API only needs a small DTO, but the query loads far more data than necessary. A careful design uses projection and smaller read models so the database returns only the fields required by that use case.
vi: Việc kéo nguyên entity cùng nhiều collection liên quan làm câu SQL phức tạp hơn, tốn bộ nhớ hơn và tăng chi phí tracking. Nhiều khi API chỉ cần một DTO nhỏ nhưng truy vấn lại tải quá nhiều dữ liệu không cần thiết. Thiết kế tốt hơn là dùng projection và read model nhỏ để database chỉ trả về đúng các trường cần cho use case đó.

#### Q_LEVEL4_346: Analyze DbContext lifetime and thread-safety.

**Question:**
en: Analyze why `DbContext` lifetime and thread-safety matter in EF Core applications.
vi: Phân tích vì sao lifetime và thread-safety của `DbContext` quan trọng trong ứng dụng EF Core.

**Answer:**
en: `DbContext` is designed for a short unit of work and is not thread-safe. Reusing one context for too long can accumulate tracked state, stale entities, and memory cost, while sharing it across threads can cause concurrency failures. In web applications, the usual pattern is one scoped context per request or one explicit context per background operation.
vi: `DbContext` được thiết kế cho một unit of work ngắn và không thread-safe. Dùng một context quá lâu có thể làm tích tụ state theo dõi, entity cũ và chi phí bộ nhớ, còn chia sẻ nó giữa nhiều thread dễ gây lỗi truy cập đồng thời. Trong web app, pattern thông dụng là một context theo từng request hoặc một context tường minh cho mỗi background operation.

#### Q_LEVEL4_362: Analyze transactions and SaveChanges boundaries.

**Question:**
en: Analyze how transaction boundaries affect EF Core correctness.
vi: Phân tích cách ranh giới transaction ảnh hưởng tới tính đúng đắn trong EF Core.

**Answer:**
en: Developers often think only about `SaveChanges()`, but correctness depends on where the business unit of work starts and ends. If related updates are split across multiple saves or external calls without a clear transaction strategy, partial failure can leave the system inconsistent. The right approach depends on whether the work is purely database-local or crosses service boundaries.
vi: Nhiều người chỉ nghĩ tới `SaveChanges()`, nhưng tính đúng đắn thật sự phụ thuộc vào việc unit of work nghiệp vụ bắt đầu và kết thúc ở đâu. Nếu các cập nhật liên quan bị chia thành nhiều lần save hoặc xen với external call mà không có chiến lược transaction rõ ràng, lỗi giữa chừng có thể làm hệ thống rơi vào trạng thái không nhất quán. Cách làm đúng phụ thuộc vào việc công việc đó chỉ nằm trong database hay còn đi qua ranh giới service khác.

### Level 5: Evaluating

#### Q_LEVEL5_411: Evaluate repository abstractions over EF Core.

**Question:**
en: Evaluate when adding a repository layer on top of EF Core is useful versus redundant.
vi: Đánh giá khi nào thêm repository layer lên trên EF Core là hữu ích và khi nào là thừa.

**Answer:**
en: A repository layer is useful when it captures real domain-specific query logic, enforces boundaries, or isolates infrastructure in a way the system genuinely needs. It becomes redundant when it only wraps `DbSet` with generic CRUD methods and hides EF Core features such as projection, includes, batching, and query composition. The real test is whether the abstraction simplifies the domain or merely adds ceremony.
vi: Repository layer hữu ích khi nó đóng gói logic truy vấn theo domain thật sự, áp ranh giới rõ ràng hoặc cô lập hạ tầng theo nhu cầu thực tế của hệ thống. Nó trở nên thừa khi chỉ bọc `DbSet` bằng vài hàm CRUD chung chung và che khuất các khả năng của EF Core như projection, include, batching và query composition. Bài kiểm tra quan trọng là abstraction đó có làm domain đơn giản hơn hay chỉ làm code nhiều nghi thức hơn.

