**Question 1:** `UseRouting` và `UseEndpoints` trong ASP.NET hoạt động như thế nào (giải thích theo ngôn ngữ kĩ thuật)

**Answer:** Trong ASP.NET Core (từ phiên bản 3.0 trở đi), cơ chế Routing đã được tách ra khỏi MVC và trở thành một hệ thống độc lập gọi là **Endpoint Routing**. Việc hiểu cách `UseRouting` và `UseEndpoints` tương tác là chìa khóa để nắm bắt vòng đời của một Request.

Dưới đây là phân tích kỹ thuật về vai trò và sự khác biệt giữa hai Middleware này:

---

## 1. `UseRouting` – Cơ chế "Khớp lệnh" (Matching)

Khi Request đi vào Middleware này, hệ thống sẽ thực hiện việc phân tích URL và các HTTP Metadata khác để xác định xem Request này thuộc về **Endpoint** nào.

- **Nhiệm vụ chính:** Quét qua danh sách các Endpoint đã được đăng ký trong ứng dụng (thông qua `UseEndpoints`) và tìm ra mục phù hợp nhất.
- **Kết quả:** Nếu tìm thấy kết quả phù hợp, nó sẽ đính kèm (attach) một đối tượng `Endpoint` vào `HttpContext` của Request hiện tại thông qua `IEndpointFeature`.
- **Lưu ý quan trọng:** Ở giai đoạn này, **Endpoint chưa được thực thi**. Nó mới chỉ được "gắn nhãn" để các Middleware tiếp theo biết Request này đang đi đâu.

---

## 2. Các Middleware trung gian (The "In-Between")

Điểm đột phá của Endpoint Routing là cho phép các Middleware khác (như **Authorization** hoặc **CORS**) truy cập vào thông tin của Endpoint trước khi nó thực sự chạy.

Ví dụ:

```csharp
app.UseRouting();

app.UseCors();          // Biết được Endpoint này có cho phép CORS hay không
app.UseAuthentication();
app.UseAuthorization(); // Biết được Endpoint này yêu cầu Role gì

app.UseEndpoints(...);
```

Nếu không có `UseRouting` đi trước, các Middleware như `UseAuthorization` sẽ không biết Request này dẫn tới Controller nào để kiểm tra quyền truy cập.

---

## 3. `UseEndpoints` – Cơ chế "Thực thi" (Execution)

Đây là điểm cuối của hành trình. Tại đây, bạn định nghĩa danh sách các Endpoint khả dụng và thực hiện logic xử lý.

- **Nhiệm vụ chính:** Đọc đối tượng `Endpoint` đã được `UseRouting` gán vào `HttpContext` và gọi delegate xử lý tương ứng (như gọi Action trong Controller, thực thi Razor Page, hoặc một Lambda function).
- **Đăng ký Route:** Đây là nơi bạn cấu hình các mẫu URL (Route patterns).

```csharp
app.UseEndpoints(endpoints =>
{
    // Đăng ký các Endpoint vào bảng định tuyến toàn cục
    endpoints.MapControllers();
    endpoints.MapGet("/", async context => {
        await context.Response.WriteAsync("Hello World!");
    });
});
```

---

## Tóm tắt sự khác biệt về mặt kỹ thuật

| Đặc điểm                  | `UseRouting`                                                  | `UseEndpoints`                                                   |
| :------------------------ | :------------------------------------------------------------ | :--------------------------------------------------------------- |
| **Thời điểm**             | Chạy sớm để xác định mục tiêu.                                | Chạy cuối để thực thi logic.                                     |
| **Dữ liệu**               | Gán `Endpoint` vào `HttpContext`.                             | Đọc `Endpoint` từ `HttpContext`.                                 |
| **Logic**                 | So khớp URL Pattern bằng thuật toán (Tree-based routing).     | Triệu gọi (Invoke) Request Delegate.                             |
| **Middleware trung gian** | Cho phép Middleware phía sau biết được metadata của Endpoint. | Thường không có Middleware nào phía sau nó (vì nó là điểm cuối). |

### Mô hình toán học đơn giản:

Nếu gọi $R$ là tập hợp các Route, và $req$ là Request đến:

1.  **UseRouting**: $f(req, R) \rightarrow endpoint$ (Tìm kiếm).
2.  **Middleware khác**: $g(endpoint) \rightarrow allow/deny$ (Kiểm tra điều kiện).
3.  **UseEndpoints**: $h(endpoint) \rightarrow response$ (Thực thi).

---

**Bạn có muốn đi sâu vào cách thuật toán của `UseRouting` tối ưu hóa việc tìm kiếm URL khi ứng dụng có hàng nghìn Endpoint không?**
