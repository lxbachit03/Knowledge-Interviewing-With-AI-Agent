# SOLID Foundation Q&A

### Level 1: Remembering

#### Q1: What does each letter in SOLID stand for?

**Question:**
en: What does each letter in the SOLID acronym stand for?
vi: Mỗi chữ cái trong từ viết tắt SOLID đại diện cho điều gì?

**Answer:**
en:

- **S**: Single Responsibility Principle (SRP) - "A class should do one thing."
- **O**: Open/Closed Principle (OCP) - "Add behavior without changing code."
- **L**: Liskov Substitution Principle (LSP) - "Subclasses must be usable as parents."
- **I**: Interface Segregation Principle (ISP) - "Smaller, specific interfaces over one large one."
- **D**: Dependency Inversion Principle (DIP) - "Depend on abstractions, not concretions."

vi:

- **S**: Nguyên tắc đơn trách nhiệm (SRP) - "Một lớp chỉ nên làm một việc."
- **O**: Nguyên tắc Đóng/Mở (OCP) - "Thêm hành vi mới mà không cần sửa đổi mã nguồn cũ."
- **L**: Nguyên tắc thay thế Liskov (LSP) - "Các lớp con phải có thể sử dụng thay thế hoàn toàn cho lớp cha."
- **I**: Nguyên tắc phân tách giao diện (ISP) - "Nên dùng nhiều giao diện nhỏ, chuyên biệt thay vì một giao diện lớn."
- **D**: Nguyên tắc đảo ngược phụ thuộc (DIP) - "Phụ thuộc vào trừu tượng (Interface), không phụ thuộc vào lớp cụ thể (Implementation)."

#### Q2: Define the Single Responsibility Principle (SRP)?

**Question:**
en: ...
vi: Định nghĩa thực tế của Nguyên tắc Đóng/Mở (OCP) là gì?

**Answer:**
en: ...
vi:
**Single Responsibility Principle (SRP):** "Một lớp chỉ nên có một, và chỉ một, lý do để thay đổi." Điều này có nghĩa là mỗi lớp nên tập trung vào một chức năng hoặc trách nhiệm duy nhất. **Mục tiêu** là giảm thiểu sự phức tạp trong 1 class và tăng khả năng bảo trì mã nguồn.
**Vấn đề:** Nếu mình có 1 class `User` có 2 chức năng vừa lưu vào DB, vừa gửi email thông báo. Thì khi thay đổi DB, mình phải sửa class `User`. Khi thay đổi cách gửi email, mình cũng phải sửa class `User`. Lúc này mình có 2 lý do để thay đổi class `User` điều này vi phạm SRP làm tăng sự phức tạp trong 1 class và giảm khả năng bảo trì mã nguồn.
**Giải pháp:** Tách chúng ra. 1 class UserRepository để lưu vào DB, 1 class EmailService để gửi email. Lúc này class User chỉ có 1 lý do để thay đổi là thay đổi các thuộc tính của người dùng và nghiệp vụ.

#### Q3: Define the Open/Closed Principle (OCP)?

**Question:**
en: What is the practical definition of the Open/Closed Principle (OCP)?
vi: Định nghĩa thực tế của Nguyên tắc Đóng/Mở (OCP) là gì?

**Answer:**
en: ...
vi:
**Open/Closed Principle (OCP):** "Các thực thể phần mềm (lớp, mô-đun, hàm, v.v.) nên được mở để mở rộng nhưng đóng đối với việc sửa đổi." Điều này cho phép chúng ta phát triển các tính năng của hệ thống bằng cách thêm các mô-đun mới thay vì viết lại các mô-đun cũ. **Mục tiêu** là giảm phát sinh rủi ro ở những chức năng đã có khi thêm chức năng mới. Tận dụng tính đa hình (Polymorphism) để hệ thống tự động nhận diện và thực thi code mới mà không cần can thiệp vào logic cũ.
**Vấn đề:** Khi có một yêu cầu mới, thường chúng ta sẽ vào sửa đổi trực tiếp vào mã nguồn của code cũ (thêm if/else hoặc switch/case). Điều này rất dễ sinh ra bug ngầm không mong muốn ngoài ra nếu có test case thì phải sửa lại test case cũ để test case mới hoạt động.
**Giải pháp:** Mình sẽ thiết kế sao cho có khả năng mở rộng bằng cách là tạo một class mới kế thừa (extend) hoặc thực thi (implement) các interface có sẵn hoặc tạo mới, mà không cần đụng vào code đang chạy tốt.
**Ví dụ**: Thay vì viết một hàm tính lương có if (loại_nhân_viên == "Fulltime") ... else if (loại_nhân_viên == "Parttime"), hãy tạo một interface NhanVien có hàm tinhLuong(). Các class NhanVienFulltime và NhanVienParttime sẽ tự triển khai logic tính lương của riêng mình.

=> Demo: ./DEMO_O.md

#### Q4: Define the Liskov Substitution Principle (LSP)?

**Question:**
en: ...
vi: Định nghĩa thực tế của Nguyên tắc thay thế Liskov Substitution (LSP) là gì?

**Answer:**
en: ...
vi:
**Nguyên tắc thay thế Liskov (LSP):** "Các object của class con phải có thể **thay thế** cho các object của class cha mà không làm thay đổi **tính đúng đắn** của chương trình". Điều này có nghĩa là các oject của class con hoạt động giống hệt như các object của class cha. Cụ thể hơn là khi class con kế thừa các thuộc tính, hàm từ class cha thì mình phải đảm bảo rằng class con không làm thay đổi hành vi của class cha mình chỉ có thể **mở rộng** hành vi của class con mà không làm thay đổi hành vi của class cha. Nếu vi phạm nguyên tắc này thì sẽ gây ra các lỗi không mong muốn và buộc phải sử dụng các cách kiểm tra kiểu dữ liệu phức tạp.
**Vấn đề:** Đôi khi chúng ta cho kế thừa một cách gượng ép. Ví dụ kinh điển: Class ChimCachCut kế thừa từ class Chim. Class Chim có hàm bay(). Nhưng chim cánh cụt không biết bay. Nếu chương trình gọi hàm bay() trên object ChimCachCut, nó sẽ văng lỗi (Exception).
**Giải pháp:** Để đảm bảo class con không thay đổi hành vi cốt lỗi của class cha. Nếu một hành động không áp dụng được cho mọi class con, hãy tách nó ra thành một interface riêng (ví dụ: IBietBay)

**DETAILS =>** SOLID/foundation/LV1_Q4.md

#### Q5: Define the Interface Segregation Principle (ISP)?

**Question:**
en: What is the practical definition of the Interface Segregation Principle (ISP)?
vi: Định nghĩa thực tế của Nguyên tắc phân tách giao diện (ISP) là gì?

**Answer:**
en: ...
vi:
**Nguyên lý Phân tách Interface**: Thay vì dùng interface lớn chứa mọi thứ, hãy tách nó ra thành nhiều interface nhỏ hơn với các mục đích cụ thể.
**Vấn đề:** Đừng ép 1 class phải implement (triển khai) những phương thức mà nó không cần dùng.
**Giải pháp:** Giả sử bạn có một interface IMachine có các hàm print(), scan(), fax(). Nếu bạn tạo một class MáyInĐenTrắng chỉ biết in, việc bắt nó implement cả scan() và fax() (rồi để trống hoặc ném lỗi) là thiết kế tồi. Hãy tách ra thành IPrinter, IScanner, IFax. Máy in đen trắng chỉ cần implement IPrinter.

#### Q6: Define the Dependency Inversion Principle (DIP)?

**Question:**
en: ...
vi: Định nghĩa thực tế của Nguyên tắc đảo ngược phụ thuộc (DIP) là gì?

**Answer:**
en: ...
vi:
**Nguyên tắc đảo ngược phụ thuộc (DIP):** Các module cấp cao không nên phụ thuộc vào các module cấp thấp. Cả hai nên phụ thuộc vào abstraction (interface hoặc abstract class) thay vì concrete class
**Vấn đề:** Nếu module cấp cao (ví dụ: class nghiệp vụ) phụ thuộc trực tiếp vào module cấp thấp (ví dụ: class Database), thì khi module cấp thấp thay đổi, module cấp cao cũng phải thay đổi theo. Điều này làm giảm tính linh hoạt của hệ thống. Cụ thể hơn là khởi tạo trực tiếp class cụ thể thay vì interface.
**Ví dụ:** Khởi tạo database trực tiếp bên trong class nghiệp vụ.
**Giải pháp:** Module cấp cao và module cấp thấp chỉ nên giao tiếp với nhau thông qua interface (ví dụ: IDabase). Phần triển khai cụ thể (MySQLDatabase hoặc MongoDBDatabase) sẽ được inject vào thông qua constructor hoặc setter. Kỹ thuật phổ biến nhất để thực hiện nguyên tắc này là Dependency Injection.

**DETAILS =>** SOLID/foundation/LV1_Q6.md

---

### Level 2: Understanding

#### Q: ...

**Question:**
en: ...
vi: Lợi ích của SOLID là gì?

**Answer:**
en: ...
vi:
**S - Single Responsibility Principle (SRP)**

- **Dễ dàng kiểm thử (Unit test):**
- **Giảm sự phụ thuộc (Coupling) và xung đột trong code:**
- **Dễ bảo trì và mở rộng:**

**O - Open/Closed Principle (OCP)**

- **Giảm thiểu phát sinh rủi ro ở các chức năng đã có khi thêm chức năng mới:**
- **Dễ mở rộng tính năng:**
- **Chỉ viết thêm unit mới cho tính năng mới:**

**L - Liskov Substitution Principle (LSP)**

- **Tái sử dụng code:**
- **Tận dụng tính kế thừa:**
- **Giảm xung đột trong code:**

**I - Interface Segregation Principle (ISP)**

- **Giảm sự phụ thuộc (Coupling) và xung đột trong code:**

**D - Dependency Inversion Principle (DIP)**

- **Các module cấp thấp có thể thay thế lẫn nhau:**
- **Khi thiết kế hệ thống giảm sự phụ thuộc (coupling) và xung đột trong code:**

#### Q: ...

**Question:**
en: ...
vi: Khi nào nên sử dụng SOLID?

**Answer:**
en: ...
vi:
**S - Single Responsibility Principle (SRP)**

- **Khi 1 class hoặc 1 module chứa nhiều nghiệp vụ khác nhau:**
- **Khi cần viết các bài kiểm thử tự động:**
  **=> Hầu như dự án nào cũng nên áp dụng (code convention)**

**O - Open/Closed Principle (OCP)**

- **Khi cần hệ thống cần mở rộng mà vẫn giữ tính ổn định:**
- **Khi muốn giảm nguy cơ phá vỡ các chức năng đã có khi thêm tính năng mới:**
- **Khi không muốn sửa đổi unit test đã có:**
- **Khi muốn hệ thống dễ bảo trì:**
  **=> Hầu như dự án nào cũng nên áp dụng (code convention)**

**L - Liskov Substitution Principle (LSP)**

- **Khi thiết kế hệ thống theo nguyên tắc kế thừa:**
- **Khi muốn tái sử dụng code:**
  **=>**

**I - Interface Segregation Principle (ISP)**

- **Khi có nhiều nghiệp vụ khác nhau trong 1 interface:**
- **Khi 1 class chỉ dùng 1 phần của nghiệp vụ:**

  **=> Hầu như dự án nào cũng nên áp dụng (code convention)**

**D - Dependency Inversion Principle (DIP)**

- **Khi có nhiều module cấp thấp có thể thay thế lẫn nhau:**
- **Khi thiết kế hệ thống giảm sự phụ thuộc (coupling) và xung đột trong code:**

  **=> Hầu như dự án nào cũng nên áp dụng (code convention)**

#### Q: ...

en: ...
vi: Trước và sau khi dùng nguyên tắc SOLID và tại sao dùng. Demo bằng C# (nhớ DEMO cả 5 nguyên tắc)

**=> DETAILS:** SOLID/foundation/LV2_Q6.md

#### Q: List two signs of "Bad Design" that SOLID aims to fix.

**Question:**
en: List two characteristics of "Bad Design" that SOLID principles aim to address.
vi: Liệt kê hai đặc điểm của "Thiết kế tồi" mà các nguyên tắc SOLID hướng tới giải quyết.

**Answer:**
en:

1. **Rigidity**: Every change causes a cascade of changes in other modules.
2. **Fragility**: A change in one place causes the system to break in unrelated places.

vi:

1. **Tính cứng nhắc (Rigidity)**: Mỗi thay đổi nhỏ đều kéo theo một loạt các thay đổi ở các mô-đun khác.
2. **Tính dễ vỡ (Fragility)**: Một thay đổi ở một nơi làm hệ thống bị hỏng ở những nơi hoàn toàn không liên quan.

#### Q: Explain why SRP helps in reducing code coupling.

**Question:**
en: Explain why the Single Responsibility Principle (SRP) helps in reducing code coupling.
vi: Giải thích tại sao Nguyên tắc đơn trách nhiệm (SRP) giúp giảm thiểu sự liên kết (coupling) trong mã nguồn.

**Answer:** ...

#### Q: Describe how OCP facilitates adding new features.

**Question:**
en: Describe how the Open/Closed Principle (OCP) facilitates adding new features to a system.
vi: Mô tả cách Nguyên tắc Đóng/Mở (OCP) tạo điều kiện thuận lợi cho việc thêm các tính năng mới vào một hệ thống.

**Answer:** ...

#### Q_LV2_423: Discuss the importance of LSP for polymorphism.

**Question:**
en: Discuss the importance of the Liskov Substitution Principle (LSP) for ensuring reliable polymorphism.
vi: Thảo luận về tầm quan trọng của Nguyên tắc thay thế Liskov (LSP) trong việc đảm bảo tính đa hình đáng tin cậy.

**Answer:**
en: LSP is about "trust." It ensures that any subclass can stand in for its parent without the client code knowing the difference. If a subclass violates the contract of the parent (e.g., by throwing an unexpected exception or ignoring a precondition), polymorphism breaks down. Without LSP, you end up with "if/else" or "instanceof" checks everywhere to handle specific subclass quirks, which defeats the whole purpose of using inheritance and makes the code fragile and hard to maintain.
vi: LSP nói về sự "tin cậy". Nó đảm bảo rằng bất kỳ lớp con nào cũng có thể thay thế cho lớp cha của nó mà mã nguồn client không nhận ra sự khác biệt. Nếu một lớp con vi phạm "hợp đồng" của lớp cha (ví dụ: ném ra một ngoại lệ không mong đợi hoặc bỏ qua một điều kiện tiên quyết), tính đa hình sẽ bị phá vỡ. Nếu không có LSP, bạn sẽ kết thúc với các kiểm tra "if/else" hoặc "instanceof" ở khắp mọi nơi để xử lý các đặc điểm riêng của lớp con, điều này làm mất đi mục đích của việc sử dụng kế thừa và làm cho mã nguồn trở nên dễ vỡ và khó bảo trì.

**DETAILS =>** SOLID/foundation/Q_LV2_423.md

#### Q: Explain the problem that Interface Segregation (ISP) aims to solve.

**Question:**
en: Explain the problem of "Fat Interfaces" that Interface Segregation (ISP) aims to solve.
vi: Giải thích vấn đề "Giao diện béo" (Fat Interfaces) mà Nguyên tắc phân tách giao diện (ISP) hướng tới giải quyết.

**Answer:**
en: "Fat Interfaces" occur when we pack too many methods into a single interface. This forces implementers to provide empty implementations or throw `NotImplementedException` for methods they don't actually need. This creates "unintended dependencies": if a method in the fat interface changes, all implementations must be updated and recompiled, even those that don't use that method. ISP solves this by breaking them into smaller, client-specific roles.
vi: "Giao diện béo" xảy ra khi chúng ta đóng gói quá nhiều phương thức vào một giao diện duy nhất. Điều này buộc những lớp thực thi phải cung cấp các bản thực thi rỗng hoặc ném ra `NotImplementedException` cho các phương thức mà chúng thực sự không cần. Điều này tạo ra các "phụ thuộc không mong muốn": nếu một phương thức trong giao diện béo thay đổi, tất cả các bản thực thi đều phải được cập nhật và biên dịch lại, ngay cả những lớp không sử dụng phương thức đó. ISP giải quyết vấn đề này bằng cách chia chúng thành các vai trò nhỏ hơn, cụ thể cho từng client.

#### Q: Describe the essence of Dependency Inversion (DIP).

**Question:**
en: Describe the essence of the Dependency Inversion Principle (DIP).
vi: Mô tả bản chất của Nguyên tắc đảo ngược phụ thuộc (DIP).

**Answer:**
en: DIP is about decoupling high-level policy (what the app does) from low-level details (how it does it). In traditional design, high-level code calls low-level code directly. DIP flips this: high-level code defines an abstraction (Interface), and low-level code implements it. This makes the high-level policy independent and reusable. If you want to switch from a SQL database to a NoSQL one, you just swap the implementation—the core business logic doesn't change because it depends on the "idea" (abstraction) of a database, not the "detail."
vi: DIP nói về việc tách biệt chính sách cấp cao (ứng dụng làm gì) khỏi các chi tiết cấp thấp (cách thức thực hiện). Trong thiết kế truyền thống, mã cấp cao gọi trực tiếp mã cấp thấp. DIP đảo ngược điều này: mã cấp cao định nghĩa một sự **trừu tượng (Interface)**, và mã cấp thấp thực thi nó. Điều này làm cho chính sách cấp cao trở nên độc lập và có thể tái sử dụng. Nếu bạn muốn chuyển từ cơ sở dữ liệu SQL sang NoSQL, bạn chỉ cần hoán đổi bản thực thi—logic nghiệp vụ cốt lõi không thay đổi vì nó phụ thuộc vào "ý tưởng" (trừu tượng) về một cơ sở dữ liệu, chứ không phải "chi tiết".

#### Q: Describe how LSP prevents "runtime type checking."

**Question:**
en: Describe how following the Liskov Substitution Principle (LSP) helps prevent excessive "runtime type checking" (like `instanceof` or `isType`).
vi: Mô tả cách việc tuân theo Nguyên tắc thay thế Liskov (LSP) giúp ngăn chặn việc "kiểm tra kiểu lúc chạy" quá mức (như `instanceof` hoặc `isType`).

**Answer:**
en: If subclasses consistently follow base class behavior, the client code doesn't need to ask "what specific type is this?" before calling a method, resulting in cleaner, polymorphic code.
vi: Nếu các lớp con tuân thủ nhất quán hành vi của lớp cha, mã nguồn client không cần hỏi "đây là kiểu cụ thể nào?" trước khi gọi một phương thức, dẫn đến mã nguồn đa hình sạch sẽ hơn.

#### Q: Discuss the relationship between Abstraction and OCP.

**Question:**
en: Discuss why "Abstraction" is the key to effectively applying the Open/Closed Principle (OCP).
vi: Thảo luận tại sao "Trừu tượng hóa" (Abstraction) là chìa khóa để áp dụng hiệu quả Nguyên tắc Đóng/Mở (OCP).

**Answer:**
en: Abstraction creates a stable interface that is "closed" for changes, while allowing different "open" implementations to be plugged in to change the application's behavior.
vi: Trừu tượng hóa tạo ra một giao diện ổn định "đóng" đối với các thay đổi, đồng thời cho phép các bản thực thi "mở" khác nhau được cắm vào để thay đổi hành vi của ứng dụng.

#### Q: Explain why DIP encourages the use of Interfaces/Abstract classes.

**Question:**
en: Explain why the Dependency Inversion Principle (DIP) encourages depending on Interfaces or Abstract classes rather than concrete implementations.
vi: Giải thích tại sao Nguyên tắc đảo ngược phụ thuộc (DIP) khuyến khích việc phụ thuộc vào Giao diện hoặc lớp Trừu tượng thay vì các bản thực thi cụ thể.

**Answer:**
en: Interfaces are more stable than concrete classes. Depending on an interface allows you to swap low-level implementations without changing the high-level policy code.
vi: Giao diện ổn định hơn các lớp cụ thể. Phụ thuộc vào một giao diện cho phép bạn hoán đổi các bản thực thi cấp thấp mà không cần thay đổi mã chính sách cấp cao.

---

### Level 3: Applying

#### Q1: Demonstrate SRP by refactoring a "Service" class.

**Question:**
en: Demonstrate SRP by refactoring a class that both processes payments and logs to a file.
vi: Minh họa SRP bằng cách tái cấu trúc một lớp vừa xử lý thanh toán vừa ghi log vào tệp.

**Answer:**
en: A class should have only one reason to change. If we need to change the logging format (e.g., from TXT to JSON), we shouldn't have to touch the payment logic class. By separating them, we make both classes smaller, more specialized, and easier to test in isolation.
vi: Một lớp chỉ nên có một lý do duy nhất để thay đổi. Nếu chúng ta cần thay đổi định dạng ghi log (ví dụ: từ TXT sang JSON), chúng ta không nên phải chạm vào lớp chứa logic thanh toán. Bằng cách tách biệt chúng, chúng ta làm cho cả hai lớp nhỏ hơn, chuyên biệt hơn và dễ dàng kiểm thử độc lập hơn.

```csharp
// Before: Violates SRP because it has two responsibilities (Payment and Logging)
public class PaymentService {
    public void Process(decimal amount) {
        // ... payment logic ...
        LogToFile($"Processed payment of {amount}");
    }
    private void LogToFile(string msg) { /* File I/O logic here */ }
}

// After: Each class has a single responsibility
public class PaymentProcessor {
    private readonly ILogger _logger;
    public PaymentProcessor(ILogger logger) { _logger = logger; }

    public void Process(decimal amount) {
        // ... payment logic ...
        _logger.Log($"Processed payment of {amount}");
    }
}

public class FileLogger : ILogger {
    public void Log(string msg) { /* Log to file logic */ }
}
```

#### Q2: Apply OCP to a discount calculation system.

**Question:**
en: Apply the Open/Closed Principle (OCP) to a discount calculation system that needs to support new discount types easily.
vi: Áp dụng Nguyên tắc Đóng/Mở (OCP) cho một hệ thống tính chiết khấu cần hỗ trợ các loại chiết khấu mới một cách dễ dàng.

**Answer:**
en: To follow OCP, we avoid using a big `switch` or `if/else` block inside the calculator. Instead, we use the Strategy Pattern. This way, if someone wants to add a "Black Friday" discount, they just create a new class—they don't have to touch the existing `DiscountCalculator` at all, ensuring we don't break existing discount logic.
vi: Để tuân thủ OCP, chúng ta tránh sử dụng các khối `switch` hoặc `if/else` lớn bên trong bộ tính toán. Thay vào đó, chúng ta sử dụng Strategy Pattern. Bằng cách này, nếu ai đó muốn thêm chiết khấu "Black Friday", họ chỉ cần tạo một lớp mới—họ hoàn toàn không phải chạm vào lớp `DiscountCalculator` hiện có, đảm bảo chúng ta không làm hỏng logic chiết khấu cũ.

```csharp
// Before: Violates OCP. Every new discount type requires modifying this class.
public class DiscountCalculator {
    public decimal Calculate(decimal price, string type) {
        if (type == "Flat") return price - 10;
        if (type == "Percent") return price * 0.9m;
        return price;
    }
}

// After: Open for extension, closed for modification.
public interface IDiscountStrategy {
    decimal ApplyDiscount(decimal price);
}

public class FlatDiscount : IDiscountStrategy {
    public decimal ApplyDiscount(decimal price) => price - 10;
}

public class PriceCalculator {
    public decimal Calculate(decimal price, IDiscountStrategy strategy) {
        return strategy.ApplyDiscount(price);
    }
}
```

#### Q3: Show an LSP violation and its fix.

**Question:**
en: Provide a code example of a Liskov Substitution Principle (LSP) violation (e.g., Square-Rectangle) and how to fix it.
vi: Cung cấp một ví dụ mã nguồn về vi phạm Nguyên tắc thay thế Liskov (LSP) (ví dụ: Hình vuông - Hình chữ nhật) và cách khắc phục.

**Answer:**
en: The classic violation occurs when a subclass overrides parent methods in a way that breaks expectations. A `Square` isn't truly a `Rectangle` in software because a Square's width and height must always be equal. If we pass a Square to a function expecting a Rectangle, and that function sets Width to 10 and Height to 5, the Square will be in an invalid state. The fix is to separate them or have them share a more general interface.
vi: Vi phạm điển hình xảy ra khi một lớp con ghi đè các phương thức của lớp cha theo cách phá vỡ các kỳ vọng ban đầu. Một `Square` không thực sự là một `Rectangle` trong phần mềm vì chiều rộng và chiều cao của Hình vuông phải luôn bằng nhau. Nếu chúng ta truyền một Square vào một hàm mong đợi một Rectangle, và hàm đó thiết lập Width là 10 và Height là 5, thì Square sẽ rơi vào trạng thái không hợp lệ. Giải pháp là tách chúng ra hoặc để chúng chia sẻ một giao diện chung tổng quát hơn.

```csharp
// Violation: Square behavior breaks Rectangle expectations
public class Rectangle {
    public virtual int Width { get; set; }
    public virtual int Height { get; set; }
}
public class Square : Rectangle {
    public override int Width { set { base.Width = base.Height = value; } }
    public override int Height { set { base.Height = base.Width = value; } }
}

// Fix: Use an abstraction that doesn't imply side effects
public interface IShape {
    int GetArea();
}
```

#### Q4: Refactor a "Fat Interface" into smaller ones (ISP).

**Question:**
en: Refactor an interface `Worker` that has `work()` and `eat()` for use by both Humans and Robots.
vi: Tái cấu trúc một giao diện `Worker` có `work()` và `eat()` để sử dụng cho cả Con người và Robot (áp dụng ISP).

**Answer:**
en: Robots don't eat, so forcing them to implement `Eat()` is "Interface Pollution." If we ever change the parameters of `Eat()`, we'd be forced to update the `Robot` class even though it doesn't care about eating. By splitting the interface, we ensure classes only implement what they actually use.
vi: Robot không ăn, vì vậy việc bắt chúng thực thi `Eat()` là "Ô nhiễm giao diện". Nếu chúng ta thay đổi tham số của `Eat()`, chúng ta sẽ buộc phải cập nhật lớp `Robot` mặc dù nó không quan tâm đến việc ăn uống. Bằng cách chia nhỏ giao diện, chúng ta đảm bảo các lớp chỉ thực thi những gì chúng thực sự sử dụng.

```csharp
// Before: Fat interface forces Robot to implement Eat()
public interface IWorker {
    void Work();
    void Eat();
}

// After: Split into role-specific interfaces
public interface IWorkable { void Work(); }
public interface IEatable { void Eat(); }

public class Human : IWorkable, IEatable {
    public void Work() { /* coding... */ }
    public void Eat() { /* lunch break... */ }
}

public class Robot : IWorkable {
    public void Work() { /* charging and working... */ }
}
```

#### Q5: Apply DIP to decouple a high-level `App` from a `Database`.

**Question:**
en: Apply the Dependency Inversion Principle (DIP) to decouple a high-level `Application` from a concrete `PostgreSQLDatabase`.
vi: Áp dụng Nguyên tắc đảo ngược phụ thuộc (DIP) để tách biệt lớp `Application` cao cấp khỏi lớp `PostgreSQLDatabase` cụ thể.

**Answer:**
en: If `Application` directly instantiates `PostgreSQLDatabase`, it is tightly coupled. If we want to unit test the application using a mock database, or switch to MongoDB later, it becomes difficult. DIP allows us to "invert" this: the Application defines the `repository` it needs, and the Database follows that definition.
vi: Nếu `Application` trực tiếp khởi tạo `PostgreSQLDatabase`, nó sẽ bị liên kết chặt chẽ. Nếu chúng ta muốn kiểm thử đơn vị ứng dụng bằng cơ sở dữ liệu giả (mock), hoặc chuyển sang MongoDB sau này, việc đó sẽ trở nên khó khăn. DIP cho phép chúng ta "đảo ngược" điều này: Application định nghĩa `repository` mà nó cần, và Database sẽ tuân theo định nghĩa đó.

```csharp
// After DIP: Application depends on Abstraction
public interface IRepository {
    void Save(string data);
}

public class Application {
    private readonly IRepository _repo;
    // We inject the dependency via constructor (Constructor Injection)
    public Application(IRepository repo) {
        _repo = repo;
    }
    public void Run() { _repo.Save("Important Data"); }
}

public class MySqlRepository : IRepository {
    public void Save(string data) { /* save to MySQL */ }
}
```

#### Q6: Refactor a class that violates ISP (Multi-function Printer).

**Question:**
en: Refactor an interface `SmartDevice` that has `print()`, `scan()`, and `fax()` to follow the Interface Segregation Principle (ISP).
vi: Tái cấu trúc một giao diện `SmartDevice` có `print()`, `scan()`, và `fax()` để tuân theo Nguyên tắc phân tách giao diện (ISP).

**Answer:**
en: A "Basic Printer" usually cannot scan or fax. If it implements `SmartDevice`, it has to include empty or error-throwing methods. By splitting `SmartDevice` into independent interfaces like `IPrinter`, `IScanner`, and `IFax`, we allow each device to implement only the capabilities it actually possesses.
vi: Một "Máy in cơ bản" thường không thể quét hoặc fax. Nếu nó thực thi `SmartDevice`, nó phải bao gồm các phương thức rỗng hoặc ném ra lỗi. Bằng cách chia nhỏ `SmartDevice` thành các giao diện độc lập như `IPrinter`, `IScanner`, và `IFax`, chúng ta cho phép mỗi thiết bị chỉ thực thi các khả năng mà nó thực sự sở hữu.

```csharp
// Better: Segregated interfaces
public interface IPrinter { void Print(); }
public interface IScanner { void Scan(); }
public interface IFax { void Fax(); }

public class MultiFunctionDevice : IPrinter, IScanner, IFax {
    public void Print() { /* printing... */ }
    public void Scan() { /* scanning... */ }
    public void Fax() { /* faxing... */ }
}

public class EconomyPrinter : IPrinter {
    public void Print() { /* only printing */ }
}
```

#### Q7: Demonstrate OCP using the "Strategy Pattern."

**Question:**
en: Demonstrate how to use the "Strategy Pattern" to apply the Open/Closed Principle (OCP) for a sorting algorithm.
vi: Minh họa cách sử dụng "Strategy Pattern" để áp dụng Nguyên tắc Đóng/Mở (OCP) cho một thuật toán sắp xếp.

**Answer:**
en: If we put multiple sorting algorithms inside one `Sorter` class, we have to modify that class every time we add a new algorithm. With the Strategy Pattern, the `Sorter` class remains closed for modification because it depends on an `ISortStrategy` interface. We can add as many new sorting classes as we want without ever changing the `Sorter` code.
vi: Nếu chúng ta đặt nhiều thuật toán sắp xếp bên trong một lớp `Sorter`, chúng ta phải sửa đổi lớp đó mỗi khi muốn thêm một thuật toán mới. Với Strategy Pattern, lớp `Sorter` vẫn đóng đối với việc sửa đổi vì nó phụ thuộc vào giao diện `ISortStrategy`. Chúng ta có thể thêm bao nhiêu lớp sắp xếp mới tùy ý mà không bao giờ phải thay đổi mã nguồn của lớp `Sorter`.

```csharp
public interface ISortStrategy {
    void Sort(int[] data);
}

public class QuickSort : ISortStrategy {
    public void Sort(int[] data) { /* logic for QuickSort */ }
}

public class Sorter {
    private ISortStrategy _strategy;
    public void SetStrategy(ISortStrategy strategy) { _strategy = strategy; }
    public void ExecuteSort(int[] data) { _strategy.Sort(data); }
}
```

#### Q8: Correct a DIP violation for manual instantiation.

**Question:**
en: Provide a fix for a class `UserService` that manually instantiates a `UserRepository` inside its constructor, violating DIP.
vi: Cung cấp giải pháp khắc phục cho một lớp `UserService` tự khởi tạo một `UserRepository` bên trong hàm tạo của nó (vi phạm DIP).

**Answer:**
en: Hardcoding `new UserRepository()` inside `UserService` creates a tight coupling to a concrete class. This makes it impossible to swap repositories for testing or other environments. The fix is to use Dependency Injection: the `UserService` asks for an `IUserRepository` through its constructor, allowing an external "container" or caller to provide the concrete implementation.
vi: Việc gán cứng `new UserRepository()` bên trong `UserService` tạo ra một sự liên kết chặt chẽ với một lớp cụ thể. Điều này khiến việc hoán đổi repository để kiểm thử hoặc cho các môi trường khác trở nên bất khả thi. Giải pháp là sử dụng Tiêm phụ thuộc (Dependency Injection): `UserService` yêu cầu một `IUserRepository` thông qua hàm tạo của nó, cho phép một "container" hoặc người gọi bên ngoài cung cấp bản thực thi cụ thể.

```csharp
// Fix: Inject the dependency
public class UserService {
    private readonly IUserRepository _repository;

    public UserService(IUserRepository repository) {
        _repository = repository; // Dependency is "Injected"
    }
}
```

#### Q9: Use SRP to extract logic from a UI Controller.

**Question:**
en: In a web application, use SRP to refactor a controller method that handles validation, database saving, and email notifications.
vi: Trong một ứng dụng web, sử dụng SRP để tái cấu trúc một phương thức controller xử lý việc xác thực, lưu cơ sở dữ liệu và thông báo qua email.

**Answer:**
en: A controller's job should be to route requests, not to contain business logic. By extracting validation to a `Validator`, persistence to a `Repository`, and notifications to a `Service`, we make the code modular. Now, we can change the database schema without touching the controller, or unit test the validation logic without spinning up a web server.
vi: Công việc của một controller nên là điều hướng các yêu cầu, chứ không phải chứa logic nghiệp vụ. Bằng cách tách việc xác thực sang một `Validator`, việc lưu trữ sang một `Repository`, và các thông báo sang một `Service`, chúng ta làm cho mã nguồn trở nên mô-đun. Giờ đây, chúng ta có thể thay đổi schema cơ sở dữ liệu mà không cần chạm vào controller, hoặc kiểm thử đơn vị logic xác thực mà không cần khởi chạy máy chủ web.

#### Q10: Apply LSP to a hierarchy involving File systems (Read-only vs Read-Write).

**Question:**
en: Apply LSP to a hierarchy where you have `ReadOnlyFile` and `ReadWriteFile`. Why is `ReadWriteFile` inheriting from `ReadOnlyFile` often better than vice-versa?
vi: Áp dụng LSP cho một phân cấp nơi bạn có `ReadOnlyFile` và `ReadWriteFile`. Tại sao `ReadWriteFile` kế thừa từ `ReadOnlyFile` thường tốt hơn là ngược lại?

**Answer:**
en: LSP states that a subtype must be substitutable for its base type. A `ReadWriteFile` can do everything a `ReadOnlyFile` can (read content). However, a `ReadOnlyFile` cannot do everything a `ReadWriteFile` can (it can't write). If `ReadOnlyFile` inherits from `ReadWriteFile`, it would have to throw a `NotSupportedException` in the `Write()` method, which breaks the contract and violates LSP. Proper inheritance reflects real capabilities without breaking base type expectations.
vi: LSP phát biểu rằng một kiểu con phải có khả năng thay thế cho kiểu cơ sở của nó. Một `ReadWriteFile` có thể làm mọi thứ mà một `ReadOnlyFile` có thể làm (đọc nội dung). Tuy nhiên, một `ReadOnlyFile` không thể làm mọi thứ mà một `ReadWriteFile` có thể làm (nó không thể ghi). Nếu `ReadOnlyFile` kế thừa từ `ReadWriteFile`, nó sẽ phải ném ra `NotSupportedException` trong phương thức `Write()`, điều này phá vỡ hợp đồng và vi phạm LSP. Kế thừa đúng đắn phản ánh các khả năng thực tế mà không phá vỡ kỳ vọng của kiểu cơ sở.
