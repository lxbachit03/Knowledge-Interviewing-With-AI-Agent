**Question 1:** Trước và sau khi dùng nguyên tắc SOLID và tại sao dùng. Demo bằng C# (nhớ DEMO cả 5 nguyên tắc)

**Answer:**

### 3. L - Liskov Substitution Principle (LSP)

**Class con phải thay thế được class cha mà không làm hỏng ứng dụng.**

**❌ Trước khi dùng (Vi phạm):** Một ví dụ kinh điển khi làm việc với thao tác ghi/đọc dữ liệu. Cả Database thường và Read-Only Database đều kế thừa từ `Database`, nhưng Read-Only lại ném ra lỗi nếu gọi hàm `Save()`.

```csharp
public class Database
{
    public virtual void Read() { /* ... */ }
    public virtual void Save() { /* ... */ }
}

public class ReadOnlyDatabase : Database
{
    public override void Read() { /* Đọc dữ liệu */ }

    public override void Save()
    {
        // Vi phạm LSP: Class con thay đổi hành vi chuẩn của class cha bằng cách ném Exception
        throw new NotImplementedException("Không thể ghi vào Read-Only DB");
    }
}
```

**✅ Sau khi dùng:** Tách biệt các hành vi thông qua Interface để đảm bảo class con chỉ implement những gì nó thực sự làm được.

```csharp
public interface IReadable { void Read(); }
public interface IWritable { void Save(); }

public class RegularDatabase : IReadable, IWritable
{
    public void Read() { /* ... */ }
    public void Save() { /* ... */ }
}

public class ReadOnlyDatabase : IReadable
{
    public void Read() { /* ... */ }
    // Không hề có hàm Save(), hoàn toàn an toàn khi gọi
}
```

---

**Question 2:**

```csharp
class Product {
    caculateTax() {
        return 0;
    }
}

class ElectricProduct extends Product {
    caculateTax() {
        return 10;
    }
}

class ClothingProduct extends Product {
    caculateTax() {
        return 5;
    }
}
```

vs

```csharp
public interface IDiscountStrategy
{
    double Calculate(double amount);
}

public class StandardDiscount : IDiscountStrategy
{
    public double Calculate(double amount) => amount * 0.05;
}

public class VIPDiscount : IDiscountStrategy
{
    public double Calculate(double amount) => amount * 0.10;
}

// Giờ đây thêm class VVIPDiscount : IDiscountStrategy rất dễ dàng
```

2 cái này khác nhau như thế nào?

**Answer:** Đây là một sự so sánh rất xuất sắc. Bạn đang chạm đến một chủ đề kinh điển trong thiết kế kiến trúc phần mềm: **Kế thừa (Inheritance)** so với **Khuôn mẫu Chiến lược (Strategy Pattern / Composition)**.

Mặc dù cả hai đoạn code này đều giúp bạn tận dụng tính **Đa hình (Polymorphism)** và phần nào thoả mãn nguyên tắc **Open/Closed Principle (OCP)** (có thể thêm logic mới bằng cách tạo class mới), nhưng triết lý thiết kế và độ linh hoạt của chúng hoàn toàn khác biệt.

Dưới đây là sự khác nhau chi tiết giữa hai cách tiếp cận này:

### 1. Bản chất cốt lõi: "Is-A" vs "Has-A"

- **Đoạn code trong ảnh (Kế thừa - Inheritance):** Sử dụng mối quan hệ **"Is-A" (Là một)**. Cụ thể, `ElectronicProduct` _là một_ `Product`. Bạn đang "nhúng" trực tiếp thuật toán tính thuế (`calculateTax`) vào cấu trúc định nghĩa của chính thực thể (Entity) đó.
- **Đoạn code C# (Giao diện - Strategy Pattern):** Bóc tách hoàn toàn hành vi ra khỏi thực thể. Việc giảm giá không nằm chết trong class `Order` hay `User`, mà nó được định nghĩa thành một "chiến lược" (Strategy) riêng biệt. Điều này tạo ra mối quan hệ **"Has-A" (Có một)**: Một đơn hàng _có một_ chiến lược giảm giá.

### 2. Sự bùng nổ cấu trúc (Class Explosion)

- **Code trong ảnh (Kế thừa):** Khi logic nghiệp vụ phức tạp lên, hệ thống sẽ rất dễ bị phình to cây kế thừa. Giả sử sản phẩm điện tử (`ElectronicProduct`) lại được chia thành hàng nội địa và hàng nhập khẩu với mức thuế khác nhau, bạn sẽ phải tiếp tục đẻ ra các class như `DomesticElectronicProduct` và `ImportedElectronicProduct`.
- **Code C# (Giao diện):** Ngăn chặn được sự bùng nổ này. Các thuật toán tính toán được chia nhỏ thành các module độc lập. Nếu sau này có sự kết hợp (ví dụ: vừa là Standard, vừa có Voucher dịp lễ), bạn chỉ cần viết thêm một Strategy mới chuyên xử lý logic gộp đó mà không làm rối cấu trúc các class cũ.

### 3. Tính linh hoạt khi chương trình đang chạy (Runtime Flexibility)

- **Code trong ảnh (Kế thừa):** Rất cứng nhắc (Tight Coupling). Khi bạn khởi tạo một đối tượng `new ClothingProduct()`, thuật toán tính thuế của nó bị đóng đinh là `0.05`. Bạn không thể thay đổi hành vi này trong lúc chương trình đang chạy (runtime) nếu không tạo ra một đối tượng hoàn toàn mới.
- **Code C# (Giao diện):** Cực kỳ linh hoạt (Loose Coupling). Vì logic tính toán được đưa vào một object riêng (ví dụ `StandardDiscount`), hệ thống có thể dễ dàng thay đổi (swap) thuật toán bất kỳ lúc nào. Ví dụ: Người dùng đang ở hạng `Standard`, ngay khi họ mua đủ doanh số, chương trình chỉ cần gán lại `currentDiscount = new VIPDiscount()` và mọi tính toán ngay lập tức thay đổi mà không cần phải can thiệp vào object của người dùng đó.

### Tổng kết: Khi nào dùng cái nào?

Sự so sánh này dẫn đến một nguyên lý vô cùng nổi tiếng trong lập trình: **"Favor Composition over Inheritance"** (Ưu tiên Composition / Interface hơn là Kế thừa).

- **Dùng Kế thừa (Code trong ảnh):** Phù hợp khi bạn có một hệ thống phân cấp tự nhiên, bền vững và thực sự cần tái sử dụng mã nguồn (thuộc tính, các phương thức chung) từ class cha, nơi mà đặc tính "Là một" không bao giờ thay đổi.
- **Dùng Interface / Strategy (Code C#):** Nên dùng khi bạn nhận thấy một "hành vi", "thuật toán" hay "luật tính toán" có khả năng biến đổi linh hoạt, nhiều phiên bản khác nhau. Cách này giúp code dễ test hơn (Unit Test), dễ bảo trì hơn và tránh được việc class phải ôm đồm quá nhiều trách nhiệm (tuân thủ tốt cả SRP và DIP trong SOLID).

===========

**Question 3:** "Các object của class con phải có thể thay thế được các object của class cha" là sao? giải thích chi tiết hơn

**Answer:** Câu hỏi rất hay! Nguyên lý **Liskov Substitution Principle (LSP)** thường được đánh giá là nguyên lý "khó nhằn" và mang tính triết lý nhất trong 5 nguyên lý SOLID.

Để hiểu rõ câu nói _"Các object của class con phải có thể thay thế được các object của class cha"_, chúng ta hãy bóc tách nó qua lăng kính thực tế và code.

### 1. Hiểu qua góc nhìn đời thực (Bản Hợp Đồng)

Khi bạn định nghĩa một **Class Cha**, bạn đang tạo ra một **"Bản hợp đồng"** về hành vi. Bất kỳ **Class Con** nào kế thừa Class Cha đều phải tuân thủ nghiêm ngặt bản hợp đồng đó, không được gây bất ngờ cho người sử dụng.

**Ví dụ:** Chiếc điều khiển TV của bạn cần lắp **Pin AA (Class Cha)**.

- Bạn ra siêu thị mua **Pin AA Energizer (Class Con 1)** -> Lắp vào chạy tốt. (Tuân thủ)
- Bạn mua **Pin AA Panasonic (Class Con 2)** -> Lắp vào chạy tốt. (Tuân thủ)
- Bạn mua một cục **Pin AA "Tàu" (Class Con 3)**, nhưng cục pin này lại được thiết kế... chảy nước nếu bấm nút quá nhanh. Bạn lắp vào, bấm nhanh, điều khiển hỏng. -> **Vi phạm LSP!** Dù Pin "Tàu" mang hình dáng của Pin AA (kế thừa), nhưng nó đã phá vỡ hành vi kỳ vọng (bản hợp đồng) của một cục pin tiêu chuẩn.

### 2. Hiểu qua Code (Ví dụ kinh điển: Hình vuông và Hình chữ nhật)

Trong toán học, **Hình vuông là một Hình chữ nhật** (có 2 cạnh bằng nhau). Nghe rất hợp lý để cho class `HinhVuong` kế thừa class `HinhChuNhat`. Nhưng trong lập trình, điều này sẽ gây ra thảm họa vi phạm LSP.

Hãy xem điều gì xảy ra:

```csharp
// Class Cha: Bản hợp đồng nói rằng Chiều Rộng và Chiều Cao là độc lập.
public class HinhChuNhat
{
    public virtual int ChieuRong { get; set; }
    public virtual int ChieuCao { get; set; }

    public int TinhDienTich() => ChieuRong * ChieuCao;
}

// Class Con: Cố gắng bẻ cong hợp đồng để phù hợp với nó
public class HinhVuong : HinhChuNhat
{
    // Bắt buộc Rộng và Cao phải bằng nhau
    public override int ChieuRong
    {
        get => base.ChieuRong;
        set { base.ChieuRong = value; base.ChieuCao = value; }
    }

    public override int ChieuCao
    {
        get => base.ChieuCao;
        set { base.ChieuRong = value; base.ChieuCao = value; }
    }
}
```

Mọi thứ có vẻ ổn cho đến khi một function khác sử dụng Class Cha:

```csharp
public void KiemTraDienTich(HinhChuNhat hcn)
{
    hcn.ChieuRong = 5;
    hcn.ChieuCao = 4;

    // Theo logic thông thường của Hình Chữ Nhật, diện tích phải là 20.
    int dienTich = hcn.TinhDienTich();

    Console.WriteLine($"Diện tích mong đợi: 20, Thực tế: {dienTich}");
}
```

**Lỗi vi phạm Liskov xảy ra ở đây:**
Nếu bạn truyền một object `HinhChuNhat` bình thường vào hàm `KiemTraDienTich`, kết quả là 20 (Đúng).
Nhưng nếu bạn **"thay thế object của class cha bằng object của class con"** (truyền `HinhVuong` vào):

1. `hcn.ChieuRong = 5` (Cả rộng và cao của hình vuông thành 5).
2. `hcn.ChieuCao = 4` (Cả rộng và cao của hình vuông bị đổi lại thành 4).
3. Kết quả diện tích in ra là **16**!

Chương trình của bạn sẽ chạy sai logic (hoặc văng lỗi) vì `HinhVuong` đã bí mật thay đổi cách hoạt động của `HinhChuNhat`. Người gọi hàm `KiemTraDienTich` không hề biết điều đó và ăn một con bug từ trên trời rơi xuống.

### 3. Dấu hiệu nhận biết bạn đang vi phạm LSP

Nếu trong code của bạn xuất hiện những đặc điểm sau, 90% là bạn đang vi phạm Liskov:

- **Class con ném ra Exception (lỗi) cho một hàm của class cha:** Ví dụ class cha có hàm `LuuVaodatabase()`, class con là `BanGhiChiDoc` (Read-only) nên ghi đè hàm đó và `throw new Exception("Không được phép lưu")`.
- **Phải dùng `if/else` để kiểm tra Type:** Nếu trong một vòng lặp xử lý class cha, bạn phải viết `if (object.GetType() == typeof(ClassCon))` để xử lý riêng biệt, thì class con đó chưa thể "thay thế" hoàn hảo cho class cha được.
- **Class con để trống (không làm gì cả) trong hàm của class cha:** Ghi đè hàm của class cha nhưng bên trong hàm không viết code gì vì class con không cần chức năng đó.

Tóm lại, kế thừa (`extends` / `:`) chỉ nên được dùng khi hành vi của class con **mở rộng** class cha, chứ không phải **thay đổi** những quy luật cơ bản của class cha.

Tuyệt vời! Cách giải quyết bài toán Hình vuông - Hình chữ nhật chính là việc chúng ta phải thay đổi góc nhìn về mối quan hệ "kế thừa" (Inheritance) sang "trừu tượng" (Abstraction).

Thay vì ép buộc "Hình vuông là một Hình chữ nhật" (kế thừa trực tiếp) dẫn đến việc vi phạm các đặc tính của Hình chữ nhật, chúng ta lùi lại một bước và nhận ra: **Cả hai đều là Hình Học (Shape), và đặc điểm chung duy nhất của chúng là có thể tính được diện tích.**

Dưới đây là cách thiết kế lại bằng C# tuân thủ nghiêm ngặt nguyên tắc Liskov (LSP):

### 1. Tạo "Bản hợp đồng" chung (Interface)

Chúng ta định nghĩa một interface `IHinhHoc` chỉ chứa duy nhất một hành vi chung mà mọi hình học đều làm được: Tính diện tích.

```csharp
public interface IHinhHoc
{
    double TinhDienTich();
}
```

### 2. Triển khai Class một cách độc lập

Bây giờ, Hình chữ nhật và Hình vuông sẽ hoạt động theo đúng bản chất tự nhiên của chúng, không ai dẫm chân lên ai.

```csharp
// Hình chữ nhật có 2 chiều độc lập
public class HinhChuNhat : IHinhHoc
{
    public double ChieuRong { get; set; }
    public double ChieuCao { get; set; }

    public double TinhDienTich()
    {
        return ChieuRong * ChieuCao;
    }
}

// Hình vuông bản chất chỉ có 1 cạnh
public class HinhVuong : IHinhHoc
{
    public double Canh { get; set; }

    public double TinhDienTich()
    {
        return Canh * Canh;
    }
}
```

### 3. Tại sao thiết kế này giải quyết triệt để lỗi LSP?

Hãy xem lại ví dụ hàm kiểm tra lúc nãy. Bây giờ chúng ta có 2 kịch bản sử dụng rất an toàn:

**Kịch bản 1: Hàm chỉ quan tâm đến diện tích**
Hàm này nhận vào `IHinhHoc`. Bạn truyền Hình vuông hay Hình chữ nhật vào đều chạy đúng, không ai thay đổi logic của ai. Đây chính là đỉnh cao của Đa hình (Polymorphism).

```csharp
public void InDienTich(IHinhHoc hinh)
{
    // Nó không quan tâm bạn lấy Cao x Rộng hay Canh x Canh
    // Nó chỉ cần biết kết quả
    Console.WriteLine($"Diện tích là: {hinh.TinhDienTich()}");
}
```

**Kịch bản 2: Hàm muốn thay đổi kích thước (Chiều rộng / Chiều cao)**
Hàm này sẽ yêu cầu **đích danh** `HinhChuNhat`.

```csharp
public void ThayDoiKichThuoc(HinhChuNhat hcn)
{
    hcn.ChieuRong = 5;
    hcn.ChieuCao = 4;
}
```

Lúc này, nếu một lập trình viên khác cố tình truyền `HinhVuong` vào hàm `ThayDoiKichThuoc()`, **trình biên dịch (Compiler) sẽ báo lỗi đỏ rực ngay lập tức** vì `HinhVuong` không còn là `HinhChuNhat` nữa.

Lỗi được chặn ngay từ lúc viết code (Compile-time) thay vì gây ra bug ngầm lúc ứng dụng đang chạy (Runtime). Đó chính là sức mạnh của việc tuân thủ nguyên tắc Liskov!

---

Việc lạm dụng kế thừa dẫn đến vi phạm LSP là một trong những lỗi phổ biến nhất của các lập trình viên OOP. Trong các dự án thực tế bạn từng làm, bạn đã bao giờ gặp tình trạng phải dùng những câu lệnh kiểu như `if (object is ClassCon) { // Xử lý riêng }` để "chữa cháy" cho một thiết kế kế thừa sai lầm chưa?

===============

**Question 4:** Code demo cho 3 trường hợp vi phạm đó

**Answer:** Chào bạn, đây là minh họa cụ thể bằng code C# cho 3 "dấu hiệu đỏ" (red flags) cho thấy bạn đang vi phạm nguyên tắc **Liskov Substitution Principle (LSP)**.

### 1. Class con ném ra Exception (Lỗi khi gọi phương thức cha)

Đây là trường hợp phổ biến nhất. Hành vi này khiến lập trình viên sử dụng class cha không thể an tâm gọi phương thức mà không kèm theo `try-catch`.

```csharp
public class Document {
    public virtual void Save() => Console.WriteLine("Đã lưu vào Database.");
}

public class ReadOnlyDocument : Document {
    public override void Save() {
        // VI PHẠM: Hành vi này phá vỡ hợp đồng của lớp cha
        throw new InvalidOperationException("Không được phép lưu tài liệu này!");
    }
}
```

---

### 2. Phải dùng `if/else` hoặc `is/as` để kiểm tra Type

Nếu bạn phải kiểm tra kiểu dữ liệu để quyết định xem có nên gọi hàm đó hay không, chứng tỏ class con không thực sự thay thế được class cha một cách trọn vẹn.

```csharp
public void ProcessDocuments(List<Document> documents) {
    foreach (var doc in documents) {
        // VI PHẠM: Phải kiểm tra kiểu để tránh ném lỗi
        if (!(doc is ReadOnlyDocument)) {
            doc.Save();
        } else {
            Console.WriteLine("Bỏ qua tài liệu chỉ đọc.");
        }
    }
}
```

---

### 3. Class con để trống (Ghi đè nhưng không làm gì)

Trường hợp này xảy ra khi lớp cha ép buộc lớp con phải thừa kế một chức năng mà lớp con không hề có nhu cầu sử dụng (Thường là dấu hiệu của việc vi phạm cả **Interface Segregation Principle**).

```csharp
public class Bird {
    public virtual void Fly() => Console.WriteLine("Chim đang bay.");
}

public class Ostrich : Bird {
    public override void Fly() {
        // VI PHẠM: Đà điểu không biết bay, hàm để trống hoặc làm gì đó vô nghĩa
        // Điều này làm người dùng class Bird lầm tưởng Ostrich cũng biết bay
    }
}
```

---

### Lời khuyên để khắc phục:

Để tránh 3 trường hợp trên, giải pháp tốt nhất là **tách Interface (Interface Segregation)** thay vì cố gắng dùng kế thừa lớp.

**Ví dụ khắc phục cho trường hợp 1 & 3:**

- Thay vì dùng `Document`, hãy tạo `IStorable` (Interface cho các thứ có thể lưu).
- Thay vì dùng `Bird`, hãy tạo `IFlyable`.
- Chỉ các class nào thực sự cần tính năng đó mới implement interface tương ứng.

Khi đó, code của bạn sẽ không bao giờ phải ném `Exception` hay dùng `if/else` để kiểm tra kiểu dữ liệu nữa. Bạn có thấy cách tiếp cận sử dụng Interface giúp code của mình trở nên "trong suốt" và dễ quản lý hơn so với việc dùng kế thừa lớp không?

===============

**Question 4:** 1 Ví dụ về lớp con kế thừa lớp cha hoàn toàn và 1 ví dụ về class con mở rộng class cha, kèm theo code ví dụ

**Answer:** Dưới đây là 2 ví dụ phân biệt rõ ràng giữa việc **kế thừa hoàn toàn** (chỉ sử dụng lại code của cha) và **mở rộng** (thêm tính năng mới vào class con) trong C#.

Cả hai cách này, nếu áp dụng đúng, đều tuân thủ rất tốt nguyên tắc **Liskov Substitution Principle (LSP)** vì class con không hề phá vỡ hay thay đổi sai lệch những gì class cha đã định nghĩa.

---

### 1. Ví dụ: Class con kế thừa hoàn toàn lớp cha

**Đặc điểm:** Class con không khai báo thêm bất kỳ thuộc tính hay phương thức nào mới. Nó trống rỗng.
**Mục đích:** Thường được dùng để **phân loại kiểu dữ liệu** (Type typing) cho rõ ràng về mặt nghiệp vụ (Domain Logic) hoặc để chuẩn bị cho việc mở rộng trong tương lai.

**Ví dụ thực tế:** Hệ thống gửi Báo cáo.

```csharp
using System;

// LỚP CHA: Chứa logic cốt lõi chung cho mọi báo cáo
public class Report
{
    public string Title { get; set; }
    public string Content { get; set; }

    public void PrintReport()
    {
        Console.WriteLine($"=== {Title} ===");
        Console.WriteLine(Content);
    }
}

// LỚP CON 1: Báo cáo tháng
public class MonthlyReport : Report
{
    // Để trống. Không thêm thuộc tính hay hàm nào mới.
    // Nó kế thừa hoàn toàn 100% từ class Report.
}

// LỚP CON 2: Báo cáo năm
public class AnnualReport : Report
{
    // Tương tự, cũng kế thừa hoàn toàn.
}

class Program
{
    static void Main()
    {
        // Sử dụng class con y hệt như class cha
        MonthlyReport reportThang4 = new MonthlyReport();
        reportThang4.Title = "Báo Cáo Tháng 4/2026";
        reportThang4.Content = "Doanh thu tăng 20%";

        reportThang4.PrintReport();
    }
}
```

_Lưu ý: Dù `MonthlyReport` không có code gì bên trong, nhưng khi dùng, ta vẫn phân biệt được nó với `AnnualReport`. Nếu sau này có hàm `GuiBaoCao(MonthlyReport r)`, hàm đó sẽ chỉ nhận báo cáo tháng chứ không nhận báo cáo năm._

---

### 2. Ví dụ: Class con mở rộng lớp cha

**Đặc điểm:** Class con nhận toàn bộ di sản của class cha, nhưng nó "giàu có" hơn vì nó **khai báo thêm** những thuộc tính và phương thức đặc thù riêng của nó.
**Mục đích:** Tái sử dụng code chung, đồng thời thêm các tính năng chuyên biệt mà chỉ nhóm đối tượng đó mới có (Đúng với bản chất của Kế thừa trong OOP).

**Ví dụ thực tế:** Hệ thống Quản lý Người dùng (User). Mọi người dùng đều có thể đăng nhập, nhưng chỉ Admin mới có quyền khóa tài khoản người khác.

```csharp
using System;

// LỚP CHA: Người dùng thông thường
public class User
{
    public string Username { get; set; }
    public string Email { get; set; }

    // Tính năng chung ai cũng có
    public void Login()
    {
        Console.WriteLine($"[Hệ thống] {Username} vừa đăng nhập thành công.");
    }
}

// LỚP CON: Mở rộng từ User
public class AdminUser : User
{
    // 1. MỞ RỘNG THÊM THUỘC TÍNH: Lớp cha không có thuộc tính này
    public int AdminLevel { get; set; }

    // 2. MỞ RỘNG THÊM PHƯƠNG THỨC: Lớp cha không có chức năng này
    public void BanAccount(string targetUsername)
    {
        if (AdminLevel >= 2)
        {
            Console.WriteLine($"[Cảnh báo] Admin {Username} đã KHÓA tài khoản của {targetUsername}!");
        }
        else
        {
            Console.WriteLine($"[Lỗi] Admin {Username} không đủ quyền để khóa tài khoản.");
        }
    }
}

class Program
{
    static void Main()
    {
        // --- Sử dụng User bình thường ---
        User normalUser = new User() { Username = "NguyenVanA" };
        normalUser.Login();
        // normalUser.BanAccount(...) -> Báo lỗi ngay vì User không có tính năng này

        Console.WriteLine("-------------------------");

        // --- Sử dụng AdminUser (Bản mở rộng) ---
        AdminUser superAdmin = new AdminUser();

        // Kế thừa: Sử dụng lại thuộc tính và phương thức của cha
        superAdmin.Username = "BossTong";
        superAdmin.Login();

        // Mở rộng: Sử dụng các thuộc tính và phương thức mới của con
        superAdmin.AdminLevel = 5;
        superAdmin.BanAccount("NguyenVanA");
    }
}
```

### Mối liên hệ với nguyên tắc Liskov (LSP):

Bạn hãy để ý class `AdminUser`. Nó mở rộng thêm hàm `BanAccount`, **nhưng nó không hề làm thay đổi hay phá hỏng hàm `Login()` của class cha**.

Nếu có một function yêu cầu truyền vào một `User` để thực hiện việc ghi log đăng nhập:

```csharp
public void GhiLogDangNhap(User u)
{
    u.Login();
}
```

Bạn hoàn toàn có thể truyền `superAdmin` vào function này, và nó vẫn chạy đúng hàm `Login()` một cách an toàn. Đây chính là minh chứng cho câu: _"Các object của class con phải có thể thay thế được các object của class cha mà không làm hỏng ứng dụng"_.

===============

**Question 5:** trong ví dụ về so sánh đoạn code trong hình và đoạn code cung cấp, 2 đoạn đó có vi phạm LSP không?

**Answer:** Câu trả lời ngắn gọn là: **Cả hai đoạn code đó đều KHÔNG vi phạm nguyên tắc Liskov (LSP).**

Thực tế, cả hai đoạn code đều là những ví dụ chuẩn mực về việc tuân thủ LSP, chỉ là chúng dùng hai kỹ thuật khác nhau (Kế thừa class và Thực thi interface).

Dưới đây là lý giải chi tiết tại sao chúng không vi phạm:

### 1. Đoạn code trong hình (Sử dụng Kế thừa - Inheritance)

```javascript
class Product {
  calculateTax() {
    return 0;
  }
}
class ElectronicProduct extends Product {
  calculateTax() {
    return 0.15;
  }
}
```

**Tại sao tuân thủ LSP?**

- **Bản hợp đồng:** Class cha `Product` hứa hẹn rằng: _"Bất cứ ai gọi hàm `calculateTax()` trên tôi, tôi sẽ trả về một con số (mức thuế)"_.
- **Class con thực hiện:** `ElectronicProduct` và `ClothingProduct` khi thay thế class cha, chúng vẫn trả về một con số (0.15 và 0.05). Chúng không hề đổi tên hàm, không đổi kiểu dữ liệu trả về thành chuỗi (string), và quan trọng nhất là **không ném ra Exception (lỗi)** để từ chối việc tính thuế.
- **Kết luận:** Nếu bạn có một vòng lặp duyệt qua một mảng chứa đủ loại `Product` và gọi `.calculateTax()`, chương trình vẫn chạy trơn tru mượt mà. Lớp con thay thế hoàn hảo lớp cha.

### 2. Đoạn code C# (Sử dụng Interface - Strategy Pattern)

```csharp
public interface IDiscountStrategy { double Calculate(double amount); }
public class VIPDiscount : IDiscountStrategy { ... }
```

**Tại sao tuân thủ LSP?**

- **Bản hợp đồng:** Interface `IDiscountStrategy` là một hợp đồng cực kỳ chặt chẽ: _"Phải có hàm `Calculate` nhận vào một số `double` và trả ra một số `double`"_.
- **Class con thực hiện:** Các class như `StandardDiscount` hay `VIPDiscount` đều implement đúng y hệt bản hợp đồng này. Chức năng tính toán bên trong có thể khác nhau (nhân 0.05 hay nhân 0.10), nhưng _hành vi giao tiếp_ với bên ngoài không hề thay đổi.
- **Kết luận:** Bất kỳ class nào trong hệ thống yêu cầu một `IDiscountStrategy` đều có thể nhận `VIPDiscount` hoặc `StandardDiscount` mà không sợ bị sập chương trình. Bản thân khuôn mẫu Strategy Pattern hoạt động được chính là nhờ dựa trên nền tảng của nguyên tắc Liskov.

---

**Điểm mấu chốt cần nhớ:**
Việc ở phần trước chúng ta so sánh và ưu tiên dùng **Interface (Đoạn C#)** hơn **Kế thừa (Đoạn trong hình)** là để giải quyết bài toán về **sự linh hoạt (Loose Coupling)** và tránh vi phạm **OCP (Open/Closed Principle)** khi hệ thống phình to, chứ không phải vì đoạn code kế thừa trong hình bị sai logic hay vi phạm Liskov.

==============

**Question 6:** Nhưng mà ElectronicProduct và ClothingProduct hard code trả về khác nhau, trông khi class cha return 0. Cái này có gọi là thay đổi hành vi không?

**Answer:** Câu hỏi của bạn **cực kỳ sắc sảo!** Bạn đã chạm đến đúng ranh giới mỏng manh nhất giữa **Tính Đa hình (Polymorphism)** và sự **Vi phạm Liskov (LSP)** trong lập trình hướng đối tượng.

Nhiều người khi mới học cũng có thắc mắc y hệt như bạn: _"Cha trả về 0, con trả về 0.15, rõ ràng là nó hoạt động khác đi rồi, sao lại nói là không thay đổi hành vi?"_

Để trả lời, chúng ta cần làm rõ khái niệm **"Hành vi" (Behavior)** trong nguyên lý Liskov. Liskov không cấm class con trả về **dữ liệu/kết quả** khác với class cha, mà Liskov cấm class con phá vỡ **"Bản hợp đồng" (Contract)** mà class cha đã ký với hệ thống.

Đây là giải thích chi tiết:

### 1. Phân biệt "Thay đổi dữ liệu" và "Thay đổi bản chất hành vi"

- **Tính đa hình (Được phép):** Là việc các class con thực hiện **cùng một mục đích** nhưng đưa ra **kết quả đặc thù** của riêng nó.
  - _Ví dụ:_ Lớp cha `DongVat` có hàm `Keu()`. Lớp `Cho` trả về "Gâu gâu", lớp `Meo` trả về "Meo meo". Dù kết quả khác nhau, nhưng chúng đều đang thực hiện đúng bản chất hành vi "kêu phát ra tiếng".
  - Quay lại code của bạn: Mục đích của hàm `calculateTax()` là **trả về mức thuế dưới dạng một con số**. Việc `ElectronicProduct` trả về `0.15` là nó đang cung cấp dữ liệu đặc thù của nó, hoàn toàn tuân thủ mục đích này.

- **Vi phạm Liskov (Không được phép):** Là khi class con làm sai lệch hẳn mục đích, điều kiện đầu vào (pre-condition), hoặc điều kiện đầu ra (post-condition) của hàm.
  - _Ví dụ vi phạm:_ Nếu `ElectronicProduct` ghi đè hàm `calculateTax()`, nhưng thay vì trả về mức thuế, nó lại thực hiện hành động **trừ tiền trong thẻ tín dụng của khách hàng** rồi mới return 0.15. Hoặc nó `throw new Exception("Lỗi không tính được")`. Lúc này, bản chất hành vi đã bị bẻ cong.

### 2. Vấn đề thực sự nằm ở chữ "return 0" của class cha

Sự cấn cá của bạn rất chính xác. Nó không đến từ việc vi phạm LSP, mà nó đến từ việc **Thiết kế class cha chưa tối ưu (Bad Design)**.

Việc class `Product` để sẵn `return 0` gây ra một sự tối nghĩa (ambiguity):

- Nó có nghĩa là _"Mặc định mọi sản phẩm đều miễn thuế (0%)"_?
- Hay nó có nghĩa là _"Tôi chưa biết sản phẩm này là gì nên tôi tạm để là 0"_?

Nếu theo nghĩa thứ hai, lập trình viên khác dùng class `Product` có thể hiểu lầm và tính sai tiền.

**Cách khắc phục:** Trong thực tế, để tránh sự khó hiểu này và làm cho thiết kế hoàn hảo 100%, người ta sẽ không viết `return 0` ở class cha. Thay vào đó, họ biến `Product` thành một **Class Trừu tượng (Abstract Class)**.

```javascript
// Biến Product thành Abstract Class
abstract class Product {
    // Không có thân hàm, không return 0.
    // Ép buộc mọi class con PHẢI tự định nghĩa mức thuế của mình.
    abstract calculateTax();
}

class ElectronicProduct extends Product {
    calculateTax() { return 0.15; }
}

class ClothingProduct extends Product {
    calculateTax() { return 0.05; }
}
```

Khi bạn dùng Abstract (như đoạn code trên) hoặc Interface (như đoạn code C# tôi cung cấp ở trên), class cha không hề cung cấp một giá trị mặc định nào cả. Nó chỉ tạo ra một cái "vỏ" (hợp đồng). Lúc này, thắc mắc _"con thay đổi giá trị của cha"_ của bạn sẽ tan biến hoàn toàn, vì cha đâu có giá trị nào để mà thay đổi!

**Tóm lại:** Đoạn code `return 0.15` không vi phạm LSP vì nó đang thể hiện sức mạnh của **Tính đa hình** (trả về kết quả phù hợp với ngữ cảnh của class con) chứ không phải đang phá hoại cấu trúc của chương trình. Tuy nhiên, linh cảm của bạn rất tốt vì việc `return 0` ở class cha đúng là một "code smell" (mùi code xấu) cần được cấu trúc lại bằng `abstract` hoặc `interface`.

=============== Câu hỏi phụ

**Question 7:** Vậy thì abstract class khác gì interface?

**Answer:**

**Giống nhau:** Abstract và Interface đều liên quan đến tính trừu tượng, đều dùng để định nghĩa một "hợp đồng" mà các class con hoặc các class implement interface phải tuân theo. Cả hai đều không thể khởi tạo trực tiếp mà phải thông qua class con kế thừa hoặc implement nó.

**Khác nhau:**
Mặc dù cả **Abstract Class (Lớp trừu tượng)** và **Interface (Giao diện)** đều dùng để tạo ra các "bản hợp đồng" nhằm áp dụng tính Đa hình và tuân thủ nguyên tắc SOLID, nhưng bản chất triết lý và cách sử dụng của chúng hoàn toàn khác nhau.

Cách dễ hiểu nhất để phân biệt là qua hai cụm từ: **"Is-A" (Là một)** và **"Can-Do" (Có thể làm)**.

---

### 1. Phân biệt qua góc nhìn đời thực

- **Abstract Class đại diện cho Bản sắc (Identity - "Là một"):**
  Nó định nghĩa bản chất cốt lõi của một nhóm đối tượng có chung huyết thống.
  _Ví dụ:_ `ĐiệnThoại` là một Abstract Class. Nó định nghĩa rằng đã là điện thoại thì phải có CPU, có màn hình, và có chức năng `GoiDien()`. iPhone hay Samsung đều **là một** chiếc điện thoại. Bạn không thể vừa là Điện Thoại, vừa là Cái Tủ Lạnh được (chỉ có thể kế thừa 1 Abstract Class).

- **Interface đại diện cho Khả năng/Hành vi (Capability - "Có thể làm"):**
  Nó chỉ quan tâm đến việc đối tượng _làm được gì_, chứ không quan tâm đối tượng _là ai_.
  _Ví dụ:_ `IChupAnh` là một Interface. Chiếc iPhone _có thể chụp ảnh_, chiếc Máy ảnh Canon _có thể chụp ảnh_, và thậm chí Vệ tinh nhân tạo cũng _có thể chụp ảnh_. Ba thứ này bản chất hoàn toàn khác nhau, nhưng chúng cùng chung một khả năng (có thể implement nhiều Interface).

---

### 2. So sánh chi tiết về mặt Kỹ thuật (C#)

| Tiêu chí                       | Abstract Class (Lớp trừu tượng)                                                           | Interface (Giao diện)                                                                                                                                       |
| :----------------------------- | :---------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Mối quan hệ**                | **"Is-A"** (Kế thừa bản chất)                                                             | **"Can-Do"** (Cam kết hành vi)                                                                                                                              |
| **Số lượng kế thừa**           | Đơn kế thừa (Một class **chỉ được kế thừa 1** Abstract class)                             | Đa kế thừa (Một class **được implement nhiều** Interface cùng lúc)                                                                                          |
| **Chứa Code thực tế**          | **Được phép.** Có thể chứa các hàm đã viết code xử lý sẵn (dùng chung cho các class con). | **Không được phép.** Chỉ chứa chữ ký hàm (tên hàm, tham số). _(_) Từ C# 8.0 có tính năng Default Implementation nhưng bản chất thiết kế vẫn hạn chế dùng.\* |
| **Biến (Fields) & Trạng thái** | Có thể khai báo biến (field) để lưu trạng thái.                                           | Không được phép chứa biến (field). Chỉ được chứa Property (Get/Set).                                                                                        |
| **Constructor (Hàm tạo)**      | Có Constructor (Dùng để khởi tạo các giá trị mặc định cho class con).                     | Không có Constructor.                                                                                                                                       |
| **Phạm vi truy cập**           | Tự do (`public`, `protected`, `private`).                                                 | Mặc định tất cả đều là `public`.                                                                                                                            |

---

### 3. Demo Code: Sự kết hợp hoàn hảo

Để thấy rõ sự khác biệt, hãy xem ví dụ này. Chú chó và Chim đại bàng đều là Động vật, nhưng chỉ Chim và Máy bay mới biết bay.

```csharp
using System;

// 1. ABSTRACT CLASS: Định nghĩa bản sắc chung
public abstract class DongVat
{
    // Có biến lưu trạng thái
    protected string Ten;

    // Có Constructor
    public DongVat(string ten)
    {
        Ten = ten;
    }

    // Có code thực tế: Đã là động vật thì đều ngủ như nhau
    public void Ngu()
    {
        Console.WriteLine($"{Ten} đang ngủ Zzz...");
    }

    // Hàm abstract (Bắt buộc class con phải tự định nghĩa)
    public abstract void PhatRaTiengKieu();
}

// 2. INTERFACE: Định nghĩa một khả năng
public interface IBietBay
{
    // Chỉ có tên hàm, không có code bên trong
    void Bay();
}

// --- TRIỂN KHAI ---

// Con Chó: LÀ MỘT động vật, nhưng KHÔNG BIẾT BAY
public class ConCho : DongVat
{
    public ConCho() : base("Cậu Vàng") { }

    public override void PhatRaTiengKieu() => Console.WriteLine("Gâu gâu!");
}

// Đại Bàng: LÀ MỘT động vật, VÀ CÓ THỂ BAY
public class DaiBang : DongVat, IBietBay
{
    public DaiBang() : base("Đại Bàng Hói") { }

    public override void PhatRaTiengKieu() => Console.WriteLine("Quác quác!");

    public void Bay() => Console.WriteLine("Đại bàng vỗ cánh bay vút lên trời!");
}

// Máy Bay: KHÔNG PHẢI động vật, NHƯNG CÓ THỂ BAY
public class MayBay : IBietBay
{
    // Máy bay không kế thừa DongVat, nó chỉ cần cam kết có khả năng bay
    public void Bay() => Console.WriteLine("Máy bay nổ động cơ và cất cánh!");
}
```

### Tổng kết: Khi nào dùng cái nào?

- **Hãy dùng Abstract Class khi:** Bạn muốn tạo ra một "khuôn mẫu gốc" chia sẻ chung các đoạn code, biến, và logic cho các class có liên quan mật thiết với nhau (Ví dụ: `BaseController`, `BaseRepository`, `Entity`).
- **Hãy dùng Interface khi:** Bạn muốn định nghĩa các "phích cắm" chức năng. Bạn muốn các class hoàn toàn không liên quan gì đến nhau (như Đại bàng và Máy bay) có thể giao tiếp thông qua chung một hợp đồng (Ví dụ: `ILogger`, `IDisposable`, `IComparable`).

Thực tế trong các dự án C# hiện đại, người ta thường **ưu tiên sử dụng Interface nhiều hơn** để thiết kế kiến trúc (như đã thấy ở Dependency Injection trong nguyên tắc SOLID), và chỉ dùng Abstract class ở một vài lớp base (nền tảng) của hệ thống.

=============== Câu hỏi phụ

**Question 8:**
ở vài đoạn code phía trên:

public class Database
{
public virtual void Read() { /_ ... _/ }
public virtual void Save() { /_ ... _/ }
}  

tôi thấy bạn có dùng virtual? virtual là gì và tại sao lại dùng

**Answer:** Bạn quan sát rất tinh tế! Từ khóa `virtual` là một mảnh ghép cực kỳ quan trọng để tạo nên tính **Đa hình (Polymorphism)** trong lập trình hướng đối tượng (OOP) của C#.

Dưới đây là giải thích chi tiết về `virtual` và lý do tại sao chúng ta lại dùng nó:

### 1. `virtual` là gì?

Trong C#, theo mặc định, một class con khi kế thừa class cha sẽ **không được phép** thay đổi (viết lại) code của các hàm đã có sẵn trong class cha.

Tuy nhiên, khi bạn gắn từ khóa `virtual` (ảo) vào trước một phương thức của class cha, bạn đang đưa ra một thông điệp cho các class con:

> _"Đây là cách xử lý mặc định của tôi. Bạn có thể dùng nguyên bản cách này, hoặc nếu bạn muốn, bạn **được phép viết lại (ghi đè)** nó theo cách riêng của bạn bằng từ khóa `override`."_

### 2. Tại sao lại dùng `virtual`? (Ví dụ thực tế)

Giả sử bạn đang viết phần mềm tính lương cho công ty.

**Lớp cha (Nhân Viên):** Có một công thức tính lương chuẩn cho tất cả mọi người (Lương cơ bản \* Ngày công).
**Lớp con (Nhân Viên Sale):** Vẫn là nhân viên, nhưng cách tính lương của họ lại khác (cộng thêm hoa hồng bán hàng).
**Lớp con (Nhân Viên Bảo Vệ):** Không có hoa hồng, dùng đúng cách tính lương cơ bản của công ty.

Lúc này, `virtual` chính là cứu tinh:

```csharp
using System;

// CLASS CHA
public class NhanVien
{
    public string Ten { get; set; }
    public double LuongCoBan { get; set; } = 5000000;

    // Dùng 'virtual' để cho phép class con tự do thay đổi nếu cần
    public virtual double TinhLuong()
    {
        return LuongCoBan;
    }
}

// CLASS CON 1: Không cần đổi cách tính lương
public class NhanVienBaoVe : NhanVien
{
    // Không dùng override, tự động xài luôn hàm TinhLuong() của cha
}

// CLASS CON 2: Muốn đổi cách tính lương
public class NhanVienSale : NhanVien
{
    public double HoaHong { get; set; } = 2000000;

    // Dùng 'override' để "ghi đè" (đá văng) hàm TinhLuong của cha
    // và thay bằng logic riêng của Sale
    public override double TinhLuong()
    {
        // Có thể gọi lại logic của cha (base.TinhLuong()) rồi cộng thêm hoa hồng
        return base.TinhLuong() + HoaHong;
    }
}
```

### 3. Phân biệt nhanh `virtual` và `abstract`

Ở câu trả lời trước, chúng ta có nhắc đến `abstract`. Cả `virtual` và `abstract` đều cho phép class con dùng `override` để ghi đè, nhưng chúng có một điểm khác biệt cốt lõi:

- **`virtual` (Có thể ghi đè):** Class cha **đã có sẵn code xử lý mặc định** bên trong (như ví dụ `Database` có code lưu mặc định). Class con _muốn thì ghi đè, không muốn thì xài đồ của cha_.
- **`abstract` (Bắt buộc ghi đè):** Class cha **hoàn toàn trống rỗng**, không có code bên trong. Nó chỉ mang tính chất ép buộc: _"Tao không biết làm, mày đã kế thừa tao thì mày PHẢI tự viết code cho hàm này!"_

Trong đoạn code về Database mà bạn trích dẫn:

```csharp
public class Database
{
    public virtual void Read() { /* Logic đọc DB mặc định */ }
    public virtual void Save() { /* Logic lưu DB mặc định */ }
}
```

Lý do dùng `virtual` ở đây là người viết code muốn cung cấp một cơ chế kết nối Database tiêu chuẩn. Hầu hết các class con kế thừa nó cứ thế mà xài. Chỉ những class đặc biệt (như `EncryptedDatabase` - DB cần mã hóa trước khi lưu) mới cần `override` lại hàm `Save()` để thêm logic mã hóa.
