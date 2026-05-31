# Entity Framework Core Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_611: What is a common DbContext misuse?

**Question:**
en: What is a common misuse of `DbContext` in EF Core?
vi: Lỗi dùng `DbContext` phổ biến trong EF Core là gì?

**Answer:**
en: A common misuse is treating `DbContext` as a long-lived shared object. It should usually be short-lived, scoped to one unit of work, and never shared across threads.
vi: Lỗi phổ biến là xem `DbContext` như một object dùng chung lâu dài. Thông thường nó nên sống ngắn, gắn với một unit of work và không bao giờ bị chia sẻ giữa nhiều thread.

#### Q_LEVEL1_624: What is a common migration mistake?

**Question:**
en: What is a common migration mistake in EF Core projects?
vi: Lỗi migration thường gặp trong dự án EF Core là gì?

**Answer:**
en: A common mistake is changing entity classes and forgetting to create or review the migration carefully. That can make the code model and the real database drift apart.
vi: Lỗi thường gặp là sửa class entity rồi quên tạo hoặc rà soát migration cẩn thận. Điều đó làm model trong code và database thực tế dần lệch khỏi nhau.

### Level 2: Understanding

#### Q_LEVEL2_641: Explain early ToList mistakes.

**Question:**
en: Why is calling `ToList()` too early a common EF Core mistake?
vi: Vì sao gọi `ToList()` quá sớm là lỗi thường gặp trong EF Core?

**Answer:**
en: Calling `ToList()` too early materializes data before filtering, projection, pagination, or aggregation finishes. That moves extra work and memory usage into the application instead of letting the database do it efficiently.
vi: Gọi `ToList()` quá sớm sẽ materialize dữ liệu trước khi filter, projection, pagination hoặc aggregation hoàn tất. Điều đó đẩy thêm việc và thêm chi phí bộ nhớ sang phía ứng dụng thay vì để database xử lý hiệu quả hơn.

#### Q_LEVEL2_658: Explain missing AsNoTracking.

**Question:**
en: Why can forgetting `AsNoTracking()` hurt read-only EF Core endpoints?
vi: Vì sao quên `AsNoTracking()` có thể làm endpoint chỉ đọc trong EF Core chậm đi?

**Answer:**
en: Without `AsNoTracking()`, EF Core spends extra effort tracking returned entities even when the request will never modify them. On read-heavy endpoints, that extra tracking can waste memory and CPU.
vi: Nếu không dùng `AsNoTracking()`, EF Core vẫn tốn thêm công để theo dõi các entity trả về dù request đó không hề sửa chúng. Trên các endpoint đọc nhiều, phần tracking thừa này có thể làm hao bộ nhớ và CPU.

#### Q_LEVEL2_676: Explain why client-side evaluation assumptions are risky.

**Question:**
en: Why is assuming every LINQ expression translates cleanly to SQL a risky EF Core mistake?
vi: Vì sao việc cho rằng mọi biểu thức LINQ đều dịch sạch sang SQL là một lỗi rủi ro trong EF Core?

**Answer:**
en: Some methods, custom logic, or complex expressions cannot be translated by the provider. If developers assume translation will always work, they can hit runtime failures or accidentally move logic to the application layer in inefficient ways.
vi: Một số method, logic tự viết hoặc biểu thức phức tạp không thể được provider dịch sang SQL. Nếu lập trình viên mặc định rằng mọi thứ luôn dịch được, họ có thể gặp lỗi runtime hoặc vô tình đẩy logic sang tầng ứng dụng theo cách kém hiệu quả.

#### Q_LEVEL2_689: Explain why lazy loading can surprise teams.

**Question:**
en: Why can lazy loading become a dangerous performance trap in EF Core?
vi: Vì sao lazy loading có thể trở thành bẫy hiệu năng nguy hiểm trong EF Core?

**Answer:**
en: Lazy loading makes code look simple, but it can hide extra queries behind ordinary property access. In loops or serializers, that often turns into N+1 behavior and unpredictable database traffic.
vi: Lazy loading làm code nhìn rất gọn, nhưng nó có thể che giấu các query phát sinh phía sau việc truy cập property bình thường. Trong vòng lặp hoặc serializer, điều này rất dễ biến thành kiểu N+1 và tạo lưu lượng database khó đoán.

### Level 3: Applying

#### Q_LEVEL3_701: Apply a safer read query pattern.

**Question:**
en: How would you apply a safer EF Core pattern for a read-only list endpoint?
vi: Bạn sẽ áp dụng pattern EF Core an toàn hơn như thế nào cho một endpoint danh sách chỉ đọc?

**Answer:**
en: Use `AsNoTracking()`, project directly to a DTO, filter before materialization, and paginate intentionally. The key is to let SQL do the heavy lifting and only materialize the minimal data the endpoint needs.
vi: Hãy dùng `AsNoTracking()`, projection thẳng sang DTO, filter trước khi materialize và phân trang có chủ đích. Ý chính là để SQL gánh phần việc nặng và chỉ materialize lượng dữ liệu tối thiểu mà endpoint thật sự cần.

