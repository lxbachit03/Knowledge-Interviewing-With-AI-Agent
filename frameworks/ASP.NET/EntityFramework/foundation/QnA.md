# Entity Framework Core Foundation Q&A

### Level 1: Remembering

#### Q_LEVEL1_101: What is Entity Framework Core?

**Question:**
en: What is Entity Framework Core?
vi: Entity Framework Core là gì?

**Answer:**
en: Entity Framework Core, or EF Core, is Microsoft's modern object-relational mapper for .NET. It lets developers work with databases using C# classes and LINQ instead of writing raw SQL for every operation.
vi: Entity Framework Core, hay **EF Core**, là ORM hiện đại của Microsoft cho .NET. Nó cho phép lập trình viên làm việc với database bằng class C# và LINQ thay vì phải viết SQL thuần cho mọi thao tác.

#### Q_LEVEL1_112: What is a DbContext?

**Question:**
en: What is a `DbContext` in EF Core?
vi: `DbContext` trong EF Core là gì?

**Answer:**
en: `DbContext` is the main class that coordinates EF Core operations with the database. It manages entity tracking, change detection, queries, and saving updates.
vi: `DbContext` là class trung tâm điều phối các thao tác của EF Core với database. Nó quản lý việc theo dõi entity, phát hiện thay đổi, truy vấn dữ liệu và lưu cập nhật.

#### Q_LEVEL1_126: What is a DbSet?

**Question:**
en: What is a `DbSet<T>` in EF Core?
vi: `DbSet<T>` trong EF Core là gì?

**Answer:**
en: `DbSet<T>` represents a collection of entities of one type in a `DbContext`. It is commonly used to query and modify rows for that entity type.
vi: `DbSet<T>` đại diện cho tập hợp entity cùng một kiểu trong `DbContext`. Nó thường được dùng để truy vấn và thay đổi các dòng dữ liệu của kiểu entity đó.

#### Q_LEVEL1_139: What are migrations?

**Question:**
en: What are migrations in EF Core?
vi: Migration trong EF Core là gì?

**Answer:**
en: Migrations are versioned descriptions of schema changes. EF Core uses them to create, update, and keep the database structure aligned with the application's entity model.
vi: **Migration** là các bản mô tả có phiên bản cho những thay đổi của schema. EF Core dùng chúng để tạo, cập nhật và giữ cấu trúc database đồng bộ với model entity của ứng dụng.

#### Q_LEVEL1_154: What is change tracking?

**Question:**
en: What is change tracking in EF Core?
vi: **Change tracking** trong EF Core là gì?

**Answer:**
en: Change tracking is EF Core's mechanism for remembering which entities were loaded and what changed on them. This allows `SaveChanges()` to generate the necessary database updates.
vi: **Change tracking** là cơ chế EF Core ghi nhớ entity nào đã được tải và có gì thay đổi trên chúng. Nhờ đó `SaveChanges()` có thể tạo ra các lệnh cập nhật database cần thiết.

#### Q_LEVEL1_168: What does SaveChanges do?

**Question:**
en: What does `SaveChanges()` do in EF Core?
vi: `SaveChanges()` trong EF Core làm gì?

**Answer:**
en: `SaveChanges()` gathers the tracked inserts, updates, and deletes in the current `DbContext` and sends them to the database in one unit of work.
vi: `SaveChanges()` gom các thao tác thêm, sửa và xóa đang được theo dõi trong `DbContext` hiện tại rồi gửi chúng xuống database như một đơn vị công việc.

---

### Level 2: Understanding

#### Q_LEVEL2_211: Explain how LINQ becomes SQL.

**Question:**
en: How does EF Core turn LINQ queries into SQL?
vi: EF Core chuyển truy vấn LINQ thành SQL như thế nào?

**Answer:**
en: EF Core reads the LINQ expression tree, translates supported parts into SQL, sends that SQL to the database, and then materializes the result back into .NET objects. Not every .NET method can be translated, so unsupported logic may fail or require client-side processing.
vi: EF Core đọc cây biểu thức LINQ, dịch các phần được hỗ trợ sang SQL, gửi SQL đó xuống database rồi materialize kết quả thành object .NET. Không phải mọi method .NET đều dịch được, nên logic không được hỗ trợ có thể lỗi hoặc buộc phải xử lý phía ứng dụng.

#### Q_LEVEL2_228: Explain tracking vs no-tracking queries.

**Question:**
en: What is the difference between tracking and no-tracking queries in EF Core?
vi: Sự khác nhau giữa truy vấn tracking và no-tracking trong EF Core là gì?

**Answer:**
en: Tracking queries keep returned entities in the `DbContext` so EF Core can detect later changes. No-tracking queries skip that bookkeeping, which is usually faster and lighter for read-only endpoints.
vi: Truy vấn tracking giữ các entity trả về trong `DbContext` để EF Core có thể phát hiện thay đổi về sau. Truy vấn no-tracking bỏ qua phần ghi nhớ đó, nên thường nhanh và nhẹ hơn cho các API chỉ đọc.

#### Q_LEVEL2_243: Explain eager, lazy, and explicit loading.

**Question:**
en: Explain eager loading, lazy loading, and explicit loading in EF Core.
vi: Giải thích eager loading, lazy loading và explicit loading trong EF Core.

**Answer:**
en: Eager loading fetches related data up front, usually with `Include`. Lazy loading fetches related data only when a navigation property is accessed. Explicit loading means the code asks for related data manually at a chosen time. Each approach trades simplicity, control, and query count differently.
vi: **Eager loading** tải dữ liệu liên quan ngay từ đầu, thường bằng `Include`. **Lazy loading** chỉ tải khi code chạm vào navigation property. **Explicit loading** là tự gọi lệnh để tải dữ liệu liên quan ở thời điểm mình chọn. Mỗi cách đánh đổi khác nhau giữa sự đơn giản, khả năng kiểm soát và số lượng query.

#### Q_LEVEL2_257: Explain code-first and database-first.

**Question:**
en: What is the difference between code-first and database-first in EF Core?
vi: Code-first và database-first trong EF Core khác nhau thế nào?

**Answer:**
en: In code-first, the entity classes and configuration drive the database schema, usually with migrations. In database-first, the database already exists and code is generated or shaped from that schema. The choice depends on whether code or database design is the main source of truth.
vi: Với **code-first**, class entity và cấu hình trong code là nguồn tạo ra schema database, thường đi cùng migration. Với **database-first**, database đã tồn tại trước và code được sinh ra hoặc điều chỉnh theo schema đó. Việc chọn cách nào phụ thuộc vào việc code hay database là nguồn sự thật chính.

#### Q_LEVEL2_274: Explain concurrency control.

**Question:**
en: How does EF Core help handle optimistic concurrency?
vi: EF Core hỗ trợ xử lý optimistic concurrency như thế nào?

**Answer:**
en: EF Core can use a concurrency token, such as a row version column, to detect that another update changed the same row first. If the original value no longer matches, `SaveChanges()` throws a concurrency exception instead of silently overwriting data.
vi: EF Core có thể dùng **concurrency token**, như cột row version, để phát hiện rằng một cập nhật khác đã thay đổi cùng dòng dữ liệu trước đó. Nếu giá trị gốc không còn khớp, `SaveChanges()` sẽ ném ra concurrency exception thay vì âm thầm ghi đè dữ liệu.

