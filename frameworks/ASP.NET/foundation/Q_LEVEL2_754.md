**Question 1:** Kênh đường ống pipeline xử lý middleware hoạt động ra sao trong ASP.NET? (nói theo ngôn ngữ kĩ thuật)

**Anser:** Trong ASP.NET Core, **Middleware Pipeline** là một cấu trúc thiết kế theo pattern **Chain of Responsibility**, nơi các thành phần phần mềm (middleware) được xâu chuỗi lại với nhau để xử lý HTTP Request và HTTP Response.

Dưới đây là cơ chế hoạt động chi tiết dưới góc độ kỹ thuật:

---

## 1. Kiến trúc Tuyến tính Hai chiều (Bidirectional Pipeline)

Pipeline hoạt động theo mô hình **LIFO (Last-In, First-Out)** đối với Response và **FIFO (First-In, First-Out)** đối với Request. Một cách dễ hiểu, nó giống như một hành lang với nhiều cửa kiểm soát: bạn phải đi qua hết các cửa để vào trong (Request) và đi ngược lại chính những cửa đó để ra ngoài (Response).

---

## 2. Luồng thực thi và Delegate `RequestDelegate`

Mỗi thành phần middleware trong pipeline bao gồm hai phần logic chính:

1.  **Logic tiền xử lý (Pre-processing):** Thực hiện trước khi yêu cầu được chuyển đến middleware tiếp theo.
2.  **Logic hậu xử lý (Post-processing):** Thực hiện sau khi các middleware phía sau đã hoàn tất công việc.

Cốt lõi của cơ chế này là delegate **`RequestDelegate`**, đại diện cho một hàm `async Task Process(HttpContext context)`.

- Mỗi middleware nhận vào một tham số `next` (cũng là một `RequestDelegate`).
- Khi middleware gọi `await next(context)`, nó đang tạm dừng thực thi của chính nó và chuyển quyền điều khiển cho middleware kế tiếp.
- Nếu một middleware **không** gọi `next(context)`, luồng xử lý bị "ngắt mạch" (**Short-circuiting**).

---

## 3. Cơ chế Ngắt mạch (Short-circuiting)

Đây là một tính năng kỹ thuật quan trọng để tối ưu hiệu năng và bảo mật.

- **Ví dụ:** Middleware xác thực (Authentication). Nếu Request không có Token hợp lệ, middleware này sẽ trả về ngay lập tức status code `401 Unauthorized` và không gọi `next()`.
- Khi đó, các middleware phía sau (như Routing, Endpoints) sẽ không bao giờ được khởi chạy, giúp tiết kiệm tài nguyên hệ thống.

---

## 4. Thứ tự đăng ký (Order of Execution)

Thứ tự bạn gọi các phương thức `app.Use...` trong file `Program.cs` chính là thứ tự mà Request sẽ đi qua. Một pipeline tiêu biểu thường có cấu hình như sau:

| Thứ tự | Middleware                   | Vai trò kỹ thuật                                                                       |
| :----- | :--------------------------- | :------------------------------------------------------------------------------------- |
| **1**  | **ExceptionHandler**         | Bọc ngoài cùng để bắt Exception từ tất cả các middleware bên trong.                    |
| **2**  | **HSTS / HTTPS Redirection** | Đảm bảo giao thức an toàn.                                                             |
| **3**  | **Static Files**             | Trả về file (CSS, JS) và ngắt mạch nếu tìm thấy file, không cần đi sâu vào Controller. |
| **4**  | **Routing**                  | Phân tích URL để khớp với Endpoint.                                                    |
| **5**  | **CORS**                     | Kiểm tra quyền truy cập từ domain khác.                                                |
| **6**  | **Authentication**           | Xác định danh tính người dùng (`User.Identity`).                                       |
| **7**  | **Authorization**            | Kiểm tra quyền hạn của người dùng đối với tài nguyên.                                  |
| **8**  | **Endpoint**                 | Thực thi logic nghiệp vụ (Controller/Minimal API) - Đây thường là "đích" của Pipeline. |

---

## 5. Cấu trúc mã nguồn (Middleware Pattern)

Về mặt kỹ thuật, một Middleware tiêu chuẩn thường được triển khai dưới dạng một Class với phương thức `InvokeAsync`:

```csharp
public class CustomMiddleware
{
    private readonly RequestDelegate _next;

    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(HttpContext context)
    {
        // 1. Logic tiền xử lý (ví dụ: Logging Request)

        await _next(context); // Chuyển giao cho middleware tiếp theo

        // 2. Logic hậu xử lý (ví dụ: Thêm Header vào Response)
    }
}
```

**Tóm lại:** Pipeline trong ASP.NET Core là một chuỗi các hàm callback không đồng bộ, cho phép can thiệp sâu vào vòng đời của một HTTP Request từ lúc nó vừa chạm tới server cho đến khi phản hồi được gửi trả lại client.
