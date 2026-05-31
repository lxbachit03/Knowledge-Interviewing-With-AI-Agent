**Question 1:** ASP.NET Core và ASP.NET MVC và ASP.NET Framework khác nhau ở điểm nào? (Giải thích theo ngôn ngữ kĩ thuật)

**Answer:** Để hiểu sự khác biệt giữa ba khái niệm này, chúng ta cần nhìn vào lịch sử tiến hóa của hệ sinh thái .NET từ một nền tảng đóng, phụ thuộc vào Windows sang một nền tảng mã nguồn mở, đa nền tảng.

Dưới đây là phân tích kỹ thuật chi tiết:

---

## 1. ASP.NET Framework (Cũ nhất)

Đây là phiên bản "ông tổ", ra mắt từ năm 2002. Nó được thiết kế chặt chẽ với hệ điều hành Windows và máy chủ IIS (Internet Information Services).

- **Runtime:** Chạy trên **CLR (Common Language Runtime)**.
- **Kiến trúc:** Dựa trên thư viện hệ thống `System.Web.dll`, vốn chứa nhiều thành phần nặng nề và bị phụ thuộc vào Windows APIs.
- **Deployment:** Chỉ chạy trên Windows Server.
- **App Model:** Bao gồm Web Forms (kéo thả UI) và sau này tích hợp thêm MVC.

## 2. ASP.NET MVC

Thực tế, **ASP.NET MVC không phải là một nền tảng riêng biệt** so với ASP.NET Framework hay ASP.NET Core. Nó là một **Pattern (Mô hình thiết kế)** được triển khai trên cả hai nền tảng đó.

- **Cốt lõi:** Tách biệt ứng dụng thành 3 thành phần: **Model** (Dữ liệu), **View** (Giao diện), và **Controller** (Điều hướng).
- **Trong ASP.NET Framework:** MVC đời đầu (từ v1 đến v5) chạy trên nền tảng ASP.NET Framework cũ.
- **Trong ASP.NET Core:** MVC được viết lại hoàn toàn, nhẹ hơn và tích hợp sẵn như một middleware.

## 3. ASP.NET Core (Hiện đại nhất)

Đây là bản tái thiết kế toàn diện (vốn được gọi là ASP.NET 5 trước khi đổi tên). Nó không phải là bản cập nhật của ASP.NET Framework mà là một framework mới hoàn toàn.

- **Runtime:** Chạy trên **.NET Core** (hoặc sau này là .NET 5/6/7/8+), sử dụng **CoreCLR**.
- **Đa nền tảng:** Chạy trên Windows, Linux và macOS.
- **Hiệu năng:** Loại bỏ `System.Web.dll`, thay bằng hệ thống các gói **NuGet** nhỏ gọn. Nó sử dụng web server nội bộ tên là **Kestrel**, được tối ưu hóa cho tốc độ cực cao.
- **Dependency Injection (DI):** Được tích hợp sẵn vào core của framework (trong khi bản cũ phải dùng thư viện bên thứ 3).

---

## Bảng so sánh kỹ thuật

| Tiêu chí        | ASP.NET Framework        | ASP.NET Core                              |
| :-------------- | :----------------------- | :---------------------------------------- |
| **Nền tảng**    | Chỉ Windows              | Windows, Linux, macOS                     |
| **Kiến trúc**   | Monolithic (Nguyên khối) | Modular (Dựa trên NuGet)                  |
| **Web Server**  | IIS                      | Kestrel, IIS, Apache, Nginx               |
| **Hiệu năng**   | Trung bình               | Rất cao (Top đầu trong các Web Framework) |
| **Open Source** | Không (Chỉ một phần)     | Hoàn toàn mã nguồn mở                     |
| **Cấu hình**    | `web.config` (XML)       | `appsettings.json` (JSON)                 |

---

## Tóm tắt mối quan hệ

1.  **ASP.NET Framework** là nền tảng cũ, chỉ chạy Windows.
2.  **ASP.NET Core** là nền tảng mới, đa nền tảng, hiệu năng cao.
3.  **ASP.NET MVC** là một cách tổ chức code (pattern). Bạn có thể viết "ASP.NET MVC" trên nền Framework cũ hoặc trên nền Core mới.

**Lời khuyên:** Nếu bạn bắt đầu dự án mới vào năm 2026, **ASP.NET Core** (hiện tại là các phiên bản .NET 8/9+) là lựa chọn duy nhất nên cân nhắc. ASP.NET Framework hiện chỉ còn được duy trì cho các hệ thống cũ (Legacy systems).
