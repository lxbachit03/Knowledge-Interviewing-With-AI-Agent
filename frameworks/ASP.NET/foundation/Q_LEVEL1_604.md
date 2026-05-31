**Question 1:** Razor Pages là gì?

**Answer:** **Razor Pages** là một mô hình lập trình hướng trang (page-focused) được giới thiệu từ phiên bản ASP.NET Core 2.0. Nó được thiết kế để giúp việc xây dựng các giao diện web trở nên đơn giản, gọn nhẹ và dễ bảo trì hơn so với mô hình MVC (Model-View-Controller) truyền thống.

Nói một cách hóm hỉnh thì nếu MVC là một bộ máy cồng kềnh với nhiều bộ phận tách biệt, thì Razor Pages giống như một "căn hộ studio" tiện nghi – mọi thứ bạn cần đều nằm gọn trong một không gian hợp lý.

---

## 1. Cấu trúc của Razor Pages

Điểm đặc trưng nhất của Razor Pages là cấu trúc tệp tin. Thay vì chia nhỏ vào các thư mục `Controllers`, `Views` và `Models` riêng biệt, một "trang" trong Razor Pages thường bao gồm hai tệp đi kèm với nhau:

- **Tệp `.cshtml` (View):** Chứa mã HTML và cú pháp Razor để hiển thị giao diện.
- **Tệp `.cshtml.cs` (PageModel):** Chứa mã C# (code-behind) để xử lý logic, dữ liệu và các sự kiện (như khi người dùng nhấn nút).

---

## 2. Cách thức hoạt động

Razor Pages sử dụng cơ chế **Handler Methods** để xử lý các yêu cầu HTTP (GET, POST, ...). Thay vì tìm đến một Action trong Controller, hệ thống sẽ tự động tìm các phương thức tương ứng trong `PageModel`:

- **OnGet():** Chạy khi trang được tải lần đầu.
- **OnPost():** Chạy khi người dùng gửi form dữ liệu.

---

## 3. Tại sao nên dùng Razor Pages?

| Đặc điểm             | Mô tả                                                                                                                                |
| :------------------- | :----------------------------------------------------------------------------------------------------------------------------------- |
| **Gọn gàng**         | Logic và giao diện của một tính năng nằm sát cạnh nhau, không phải nhảy qua lại giữa nhiều thư mục.                                  |
| **Routing tự động**  | Đường dẫn (URL) được xác định dựa trên cấu trúc thư mục của tệp tin. Ví dụ: `/Pages/Contact.cshtml` sẽ tự động có URL là `/Contact`. |
| **Phù hợp cho CRUD** | Rất lý tưởng cho các ứng dụng quản lý dữ liệu (Thêm, Sửa, Xóa) vì mỗi trang thường chỉ phục vụ một mục đích cụ thể.                  |
| **Dễ học**           | Đối với những người mới bắt đầu hoặc chuyển từ ASP.NET Web Forms sang, Razor Pages có đường cong học tập thấp hơn MVC.               |

---

## 4. So sánh nhanh với MVC

Mặc dù Razor Pages chạy trên nền tảng của MVC, nhưng tư duy tổ chức lại khác nhau:

- **MVC:** Thích hợp cho các ứng dụng cực lớn với hệ thống điều hướng phức tạp, nơi một Controller có thể quản lý rất nhiều View khác nhau.
- **Razor Pages:** Thích hợp cho hầu hết các ứng dụng web thông thường, nơi mỗi trang web có một nhiệm vụ riêng biệt.

> **Lưu ý nhỏ:** Bạn hoàn toàn có thể sử dụng cả Razor Pages và MVC trong cùng một dự án ASP.NET Core. Chúng không hề "đánh nhau" mà bổ trợ cho nhau rất tốt!

Bạn đang có ý định bắt đầu một dự án mới bằng Razor Pages hay đang tìm hiểu để chuyển đổi từ một công nghệ khác sang?
