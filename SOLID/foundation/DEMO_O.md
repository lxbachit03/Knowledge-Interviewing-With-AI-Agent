Chào bạn! Rất vui được đồng hành cùng bạn tìm hiểu về nguyên tắc **Open/Closed Principle (OCP)** – nguyên tắc thứ hai trong bộ 5 nguyên tắc SOLID, một nền tảng quan trọng để viết mã nguồn dễ bảo trì và mở rộng.

---

### 1. Vấn đề là gì?

Vấn đề nảy sinh khi bạn thiết kế các lớp (classes) mà **khi muốn thêm tính năng mới, bạn buộc phải sửa đổi code hiện có**.

- **Tại sao đây là vấn đề?** Khi bạn sửa code đã chạy ổn định để thêm tính năng mới, bạn đối mặt với rủi ro:
  - Làm hỏng (break) các tính năng cũ đang hoạt động.
  - Phải kiểm thử (test) lại toàn bộ hệ thống từ đầu.
  - Vi phạm nguyên tắc "Đóng-Mở" (Open-Closed).

---

### 2. Giải pháp

Nguyên tắc OCP phát biểu rằng: **"Các thực thể phần mềm (class, module, function...) nên mở cho việc mở rộng (open for extension) nhưng đóng cho việc sửa đổi (closed for modification)."**

**Cách thực hiện:** Thay vì sửa đổi code gốc, chúng ta sử dụng **Abstraction** (Interface hoặc Abstract Class). Khi cần thêm tính năng, ta chỉ việc tạo ra một lớp mới kế thừa hoặc triển khai (implement) từ các abstraction đó.

---

### 3. Code Demo (C# & ASP.NET Core)

Giả sử chúng ta đang xây dựng hệ thống tính phí giao hàng.

#### Trước khi áp dụng (Vi phạm OCP)

Bạn phải dùng `if-else` hoặc `switch` để kiểm tra loại giao hàng. Mỗi khi có thêm loại mới (ví dụ: giao hàng hỏa tốc), bạn phải sửa class `OrderProcessor`.

```csharp
public class OrderProcessor {
    public decimal CalculateShipping(string type) {
        if (type == "Standard") return 10.0m;
        else if (type == "Express") return 20.0m;
        // Nếu muốn thêm loại "SameDay", phải sửa vào đây -> VI PHẠM OCP
        return 0;
    }
}
```

#### Sau khi áp dụng (Tuân thủ OCP)

Chúng ta dùng `Interface` để tạo ra một "hợp đồng" chung.

```csharp
// 1. Tạo Abstraction
public interface IShippingStrategy {
    decimal Calculate(decimal amount);
}

// 2. Triển khai các chiến lược cụ thể
public class StandardShipping : IShippingStrategy {
    public decimal Calculate(decimal amount) => 10.0m;
}

public class ExpressShipping : IShippingStrategy {
    public decimal Calculate(decimal amount) => 20.0m;
}

// 3. Class xử lý không bao giờ phải sửa nữa
public class OrderProcessor {
    public decimal CalculateShipping(IShippingStrategy strategy, decimal amount) {
        return strategy.Calculate(amount);
    }
}
```

**Tại sao đây là OCP?**
Nếu bạn muốn thêm "SameDayShipping", bạn chỉ cần tạo một class mới:

```csharp
public class SameDayShipping : IShippingStrategy {
    public decimal Calculate(decimal amount) => 30.0m;
}
```

Bạn **không cần chạm vào code của `OrderProcessor`**. Nó đã được "đóng" đối với việc sửa đổi và "mở" cho việc mở rộng thông qua class mới.

---

### Lợi ích thực tế trong ASP.NET Core

Trong các dự án thực tế, bạn thường kết hợp OCP với **Dependency Injection (DI)**. Bạn đăng ký các service trong `Program.cs`:

```csharp
// Đăng ký vào DI Container
builder.Services.AddScoped<IShippingStrategy, StandardShipping>();
```

Khi đó, `OrderProcessor` sẽ nhận `IShippingStrategy` thông qua Constructor Injection, giúp code của bạn cực kỳ linh hoạt và dễ kiểm thử (Unit Test).
