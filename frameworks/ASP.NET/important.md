## record / class

-> C# 9.0: record (class) (Heap)
-> C# 10.0: record struct (Stack)
-> reference type nếu là `record class` và value type nếu là `record struct`
-> record: imutable (khởi tạo 1 lần)
-> record (struct): _value-based equality_ + _with expression_ != class: _reference-equality_
--> record: override equals() + GetHashCode() methods + "==" and "!=" operators
--> record: override "==" => nhanh, tiện hơn so với override "==" của class
-> record: with expression => copy object và thay đổi 1 thuộc tính
-> [use]record: Thường dùng với DTO + làm key trong Dictionary / HashSet + Value object in DDD
-> [+]record: có thể khai báo single-line
**NOTE**: record so sánh các giá trị khai báo public

- IEnumerable / IQueryable / ICollection / IList / Array

## yield return

-> Ra mắt từ C# 2.0
-> [characteristic] trình biên dịch sẽ tạo ra 1 _state machine (máy trạng thái)_ ngầm bên dưới. Thay vì chạy vì chạy toàn bộ hàm và trả về 1 danh sách `List<T>`, nó sẽ trả về 1 _iterator_ (`IEnumerable<T>`, `IEnumerator<T>`) và thực thi theo cơ chế **Lazy Evaluation** (đánh giá lười).
--> Cơ chế này khi hàm chạy tới `yield return`, nó sẽ trả về giá trị và tạm dừng thực thi (đánh dấu vị trí hiện tại)
-> [+] Tiết kiệm bộ nhớ: Ưa điểm cực lớn là tiết kiệm bộ nhớ (không cần phải khởi tạo `List<T>` hay `Array<T>` để chứa toàn bộ dữ liệu load hết vào bộ nhớ - RAM)
-> [+] Sử lý dữ liệu lớn hoặc luồng dữ liệu vô hạn: lấy dữ liệu từ hàng nghìn dòng từ database để stream dữ liệu cho client thay vì phải load hết vào RAM.
-> [+] Sử dụng trong bất đồng bộ lấy dữ liệu từ DB(`IAsyncEnumerable<T>` (giới thiệu từ C# 8.0)): giúp vừa đọc từ DB vừa trả dữ liệu cho client.

## `IAsyncEnumerable<T>`

-> Giới thiệu từ C# 8.0. Cho phép steam dữ liệu từ DB về phía Client ngay khi dữ liệu sẵn sàng thay vì chờ đợi load toàn bộ dữ liệu và trả về bộ nhớ server.
-> Là Async version của `IEnumerable<T>`
-> Sử dụng trong bất đồng bộ lấy dữ liệu từ DB(`yield return`)
-> [why?] Khi dùng `IEnumerable<T>`, nếu bên trong có các thao tác bất đồng bộ (như truy vấn DB), mình phải gọi `.ToList()` hoặc `.ToArray()` để đợi dữ liệu hoàn tất trước khi trả về
--> Tăng độ trễ (latency): Server phải đợi đến khi bản ghi cuối cùng được truy vấn xong mới trả về toàn bộ.
--> Tốn RAM: load vào `List<T>` => load vào RAM
==> với `IAsyncEnumerable<T>` và `yield return` dữ liệu sẽ được đẩy (stream) về client theo từng đợt nhỏ giúp phản hồi nhanh hơn và tiết kiệm RAM đáng kể.
-> [Note]
--> Không dùng trong mọi trường hợp: Nếu cần thực hiện các thao tác `Count()`, `OrderBy()` ngay trên DB => Cần phải **dùng `IQueryable()` trước** sau đó mới chuyển sang `IAsyncEnumerable()` để stream
--> Serialization: ASP.NET Core (System.Text.Json) hỗ trợ serialize `IAsyncEnumerable<T>` cực tốt. Khi trả về theo kiểu này, kết quả sẽ được tự động serialize dưới dạng mảng JSON và sẽ được gửi đi dưới dạng stream (HTTP Chunked Transfer Encoding)

## equals() / GetHashCode()

-> [default]: C# sẽ dùng logic của `System.Object` => so sánh địa chỉ bộ nhớ (reference-equality)
-> class: tự override Equals() và GetHashCode() nếu muốn tự định nghĩa logic
-> 2 objects bằng nhau (==) => GetHashCode() của 2 objects phải bằng nhau. Ngược lại nếu GetHashCode() bằng nhau thì 2 objects chưa chắc bằng nhau (phải so sánh thêm bằng Equals())
-> [+]GetHashCode(): dùng để tối ưu khi search trong Dictionary / HashSet nhưng không nên override Equals() nếu không override GetHashCode() => O(1)

- Value Types / Reference Types
  -> Value type: store on Stack (nếu là local), store on Heap (nếu là field của class/record) (int, double, float, bool, char, byte)
  -> Reference type: actual data store on Heap, reference store on Stack (class, record class, dynamic, delegate)
  -> String: là immutable reference type

## sealed

-> Ngăn cản kế thừa, override các method

## static class

-> Không thể khởi tạo bằng keywork `new`, chỉ có thể gọi trực tiếp thông qua tên class | Không thể kế thừa | Chỉ chứa các thành viên tĩnh (Tất cả các fields, properties, methods của nó đều phải là static) | _Chỉ có Static Constructor:_ Không tự định nghĩa constructor => duy nhất static constructor (không có tham số, không có access modifiers như public, private)
--> Bản chất: 2 modifier ẩn là `sealed` + `abstract`
--> Static field, method chỉ được khởi tạo 1 lần trong suốt vòng đời của ứng dụng.
---> CLR của ASP.NET gọi 1 lần duy nhất `static` constructor trước khi gọi bất kì members nào bên trong.
--> [use] _utillity, Helper class:_ Thường được dùng làm utillity, Helper class như `String.IsNullOrEmpty()`, `Math.Max()`. `DateTime.Now`,... | [use] _Extension Methods:_ Mở rộng 1 kiểu dữ liệu có sẵn bằng keyword `this` ở tham số đầu tiên như IServiceCollection, phương thức mở rộng bắt buộc là static method và nằm trong 1 static class. | [use] _Lưu trữ Global Constants:_

```CSharp
public static class StringHelper
using System;

namespace AspNetCoreDemo.Helpers
{
    // Định nghĩa một Static Class
    public static class StringHelper
    {
        // 1. Chỉ chứa static field / property
        public static string DefaultCulture = "vi-VN";

        // 2. Không thể có constructor thông thường, chỉ có static constructor để setup ban đầu
        static StringHelper()
        {
            // Được gọi 1 lần duy nhất bởi CLR
            Console.WriteLine("StringHelper initialized in memory.");
        }

        // 3. Chứa Static Method
        public static string ToTitleCase(string text)
        {
            ...
        }

        // 4. Ứng dụng làm Extension Method trong ASP.NET (từ khóa 'this' ở tham số đầu tiên)
        public static bool IsValidEmail(this string email)
        {
            return email.Contains("@");
        }
    }

    public class Program
    {
        public static void Main()
        {
            // LỖI BIÊN DỊCH (COMPILE-TIME ERROR): Không thể khởi tạo class tĩnh
            // StringHelper helper = new StringHelper();

            // CÁCH SỬ DỤNG ĐÚNG: Gọi trực tiếp thông qua tên Class
            string formatted = StringHelper.ToTitleCase("hELlo");
            Console.WriteLine(formatted); // Output: Hello

            // Sử dụng như một Extension Method
            string myEmail = "admin@example.com";
            bool check = myEmail.IsValidEmail();
        }
    }
}
```

## dynamic

-> ra mắt C# 4.0. Mang lại kiểu hoạt động linh hoạt giống như Javascript (không khắc khe về kiểu dữ liệu)
-> [characteristic] dynamic không được kiểm tra tại thời gian biên dịch (compile time), mà chỉ tại thời gian chạy (runtime)
-> [+] Khác với `object` phải dùng cách `obj.GetType().GetMethod("DoSomething").Invoke(...)` để check thuộc tính/phương thức / dynamic cho phép truy cập thuộc tính/phương thức của object mà không cần ép kiểu. Được hỗ trợ thông qua DLR (Dynamic Language Runtime).
-> [+] Làm việc với JSON không có cấu trúc cố định `dynamic data = JsonConvert.DeserializeObject(jsonString); string name = data.User.Profile.Name;`
-> [-] Dễ crash tại thời điểm runtime vì thời điểm biên dịch không kiểm tra giúp
-> [-] Đánh đổi hiệu năng: C# là 1 ngôn ngữ chạy nhanh vì mọi thứ (bộ nhớ, kiểu dữ liệu) đã được tính toán tại thời điểm biên dịch (compile time). Tuy nhiên, dynamic lại phải tính toán thêm tại thời điểm runtime (thông qua DLR), làm chậm đi hiệu năng của chương trình.
-> **Lưu ý**
--> [-]: Không nên lạm dụng `dynamic` để thay thế cho `var`
--> Nên gán vào biến có kiểu dữ liệu tường minh (explicit type) sau khi dùng dynamic để lấy dữ liệu từ JSON.

## tuple

-> [version] Giới thiệu từ C# 7 | Là _cấu trúc dữ liệu_ cho phép lưu tập hợp nhiều giá trị (có thể khác kiểu) trong cùng một object.
--> Tuple được tạo ra nhằm thay thế cho việc trả về nhiều giá trị từ một method.
--> [note] tối đa 7 phần tử (item 1 - item 8)
--> [use] _trả về nhiều giá trị từ một method_

```CSharp
// 1. Sử dụng Tuple cổ điển (Tuple<T1, T2>)
var person = Tuple.Create("Thao", 25);
Console.WriteLine(person.Item1); // Thao

// 2. Sử dụng ValueTuple (C# 7+) - Khuyên dùng
(string Name, int Age) user = ("Thao", 25);
Console.WriteLine(user.Name); // Thao
```

```CSharp
(string name, int age, bool isStudent) GetStudent()
{
    return ("John", 20, true);
}

var student = GetStudent();
Console.WriteLine(student.name);
Console.WriteLine(student.age);
Console.WriteLine(student.isStudent);
```

## object

-> alias của `System.Object`
-> base class của mọi kiểu dữ liệu trong C# (kiểu giá trị nguyên thủy: int, double, bool) hoặc (kiểu tham chiếu phức tạp: class, array, string)
-> [-]: hạn chế dùng vì mất đi type safe
--> không thể gọi các hàm của chuỗi `myObj.ToUpper()` hoặc `myObj.Length`

## array

-> Là data structure, có kích thước cố định (không thể thay đổi kích thước sau khi khởi tạo) và mỗi phần tử trong array có cùng dữ liệu (strongly-typed).
-> system-level:
--> Bản chất cấp phát bộ nhớ (Memory allocation): Array là một reference type, dữ liệu được lưu trên `Heap` và địa chỉ bộ nhớ được lưu trên `Stack`.
---> Dữ liệu trong array được lưu liên tiếp nhau trên heap, => vì vậy cho phép truy cập ngẫu nhiên với index (random access) với tốc độ O(1).
---> Kích thước là cố định sau khi khởi tạo. Nếu muốn mở rộng => Tạo array mới copy dữ liệu qua ==> **tốn thời gian (CPU cycles) và tài nguyên bộ nhớ** VÌ OS phải tìm kiếm vùng nhớ mới và liên tục và _Garbage collector_ sẽ dọn dẹp vùng nhớ cũ; việc garbage collector đi dọn rác cũ cũng làm tiêu tốn tài nguyên CPU.
----> Trường hợp của `List<T>`: Được xây dựng trên array, nhưng cho phép thay đổi kích thước khi thêm phần tử. Nếu vượt qua capacity => OS sẽ cấp phát bộ nhớ mới với kích thước gấp đôi.
-->

## Type casting

-> Ép kiểu ngầm định (Implicit Casting) / Ép kiểu tường minh (Explicit Casting) - Dùng dấu ()
--> Implicit Casting: khi chuyển dữ liệu nhỏ -> lớn (int -> long) hoặc lớp con -> lớp cha (derived -> base)
---> [note] không mất dữ liệu hoặc không bị exception
--> Explicit Casting: khi chuyển dữ liệu lớn -> nhỏ (double -> int) hoặc lớp cha -> lớp con (base -> derived)
---> [note] có nguy cơ mất dữ liệu hoặc lỗi runtime. **hạn chế** dùng (Type), Chỉ dùng khi chắc chắn giá trị hợp lệ. Thay vào đó nên dùng "as" hoặc "is" hoặc "is not null" + "?" để kiểm tra và ép kiểu.
-> `as` / `is`
--> `as`: ép kiểu an toàn, trả về `null` nếu ép kiểu thất bại thay vì throw exception. `var employee = person as Employee; if (employee != null) { ... } else { ... }`
--> `is` (pattern matching): kiểm tra kiểu, trả về true/false. `if (person is Employee employee) { ... }`
--> [note] Vừa kiểm tra vừa gán vào biến mới rất gọn gàng
-> [-]: hạn chế đùng `(Type)` => `as` và `is`
-> [-]: hạn chế dùng `int.Parse("123a")` => `int.TryParse("123a", out int resultVar)` hoặc dùng lớp `Convert` -> `Convert.ToInt32()` (an toàn hơn Parse vì Parse trả về `null` nếu lỗi còn Convert trả về số 0 nếu lỗi)

## streaming

->

## delegate

->

## IActionResult

->

## Task

->

## LINQ (Language Integrated Query)

->

## Entity Framework Core

->

## AddScoped vs AddTransient vs AddSingleton / Captive Dependency

->

## Struct / class

-> String là class, int là struct

## Abstract class

-> [characteristics] Không thể khởi tạo bằng keywork `new` **|** các methods, properties có thể đánh dấu là `abstract` sẽ không có thân hàm bất kì Class con kế thừa nào cũng phải ghi đè bằng keyword `override` **|** _Tái sử dụng:_ có thể chứa các fields, properties, methods hoàn chỉnh để class con có thể tái sử dụng.
--> có `constructor` nhưng class con phải gọi thông qua `base` => để khởi tạo những gì cần thiết (state nội bộ) trước khi class con được khởi tạo.
--> class con chỉ có thể kế thừa duy nhất 1 abstract class và có thể kế thừa nhiều interface.
--> [use] _Base Controllers (`abstract class BaseController : ControllerBase`)_ **|** _Base Repositories (`abstract class BaseRepository<T, TContext>`)_ **|** _Custom Exception Handling_
--> [note] keyword `virtual` có thể sử dụng được trong `abstract class` và `class`.

## Class

-> Là bản thiết kế (blueprint) hoặc là khuôn mẫu dùng để tạo ra các đối tượng (objects) cụ thể trong Heap.
-> [characteristics] _Định nghĩa trạng thái và hành vi:_ Class chứa các trạng thái như (fields, properties) và các hành vi như (methods, events). **|** _keyword `new`:_ Tạo ra thực thể (intance) của `class` bằng keyword `new` **|** _Tính đóng gói (Encapsulation):_ Class có thể che giấu thông tin bằng access modifiers (`private, protected, internal`) **|** _Tính kế thừa (Inheritance):_ Class có thể kế thừa duy nhất từ 1 class khác nhưng có thể implement nhiều interface.

## Interface

-> Là bản thiết kế hoặc là 1 "hợp đồng" (contract) hoặc là 1 khuôn mẫu để định nghĩa các thành phần như (fields, properties, methods, events) mà không cần cung cấp mã thực thi => class khi implement những interface thì cần phải cung cấp mã thực thi cho những thành phần này. **|** _Đa kế thừa:_ Class có thể kế thừa nhiều interface
--> Interface không thể khởi tạo bằng keyword `new`.
--> [note] Mặc định tất cả các thành phần trong interface đều là `public` trước C# 8.0. Từ C# 8.0 có thể sử dụng `private`, `protected`, `internal`, `protected internal`, `private protected`.

```Csharp
public interface ILogger
{
    // 1. PUBLIC (Mặc định): Hợp đồng bắt buộc Class phải implement
    void LogInfo(string message);

    // 2. PUBLIC kèm Default Method: Class có thể implement lại hoặc xài đồ mặc định
    public void LogError(string message)
    {
        // Gọi hàm private bên dưới
        LogToConsole("ERROR", message);
    }

    // 3. PRIVATE: Hàm helper nội bộ, giấu kín, Class implement sẽ kông nhìn thấy hàm này
    private void LogToConsole(string level, string message)
    {
        Console.WriteLine($"[{level}] - {DateTime.Now}: {message}");
    }

    // 4. PROTECTED: Cho phép các Interface con hoặc Class implement gọi được
    protected void LogWarning(string message)
    {
        LogToConsole("WARNING", message);
    }
}
```

--> [note] từ C# 8.0 interface có thể có `default implementations` (mặc định có thể cung cấp mã thực thi cho các thành phần trong interface)
--> [note] Không thể chứa các fields lưu trạng thái.

## Tính đóng gói (Encapsulation) Access Modifiers (`public, private, protected, internal`)

## Lock / Deadlock

-> _Lock:_ Là 1 cơ chế hay 1 quy tắc khóa tài nguyên (dữ liệu) trong CSDL để kiểm soát truy cập đồng thời, ngăn chặn 2 giao dịch (transactions) sửa đổi cùng một dữ liệu => đảm bảo tính toàn vẹn (ACID) ~ dữ liệu luôn nhất quán với nhau **Nhưng làm giảm hiệu năng xử lý song song**
--> [mechanism] cụ thể hơn là khi có nhiều luồng (threads) hoặc tiến trình (processes) cùng cố truy cập vào 1 tài nguyên đồng thời, lúc này thread yêu cầu lock nếu lock này đang trống -> thread đó sẽ sở hữu nó. Nếu lock này đang sở hữu bởi thread khác thì thread này sẽ chuyển sang trạng thái chờ cho đến khi lock được giải phóng (release).
---> [system_level(DB)]: _Cơ chế update:_ Dữ liệu được lưu ở file level (data files) trên ổ cứng. Khi update dữ liệu, OS sẽ load dữ liệu này lên bộ nhớ RAM (page buffer / data cache) để thực hiện việc sửa đổi, những thay đổi dữ liệu này sẽ được ghi LOG lại cho đến khi `commit`.
-----> [level_of_lock]: lock áp dụng cho cả **dữ liệu** (row record, table, Page/Block, Database, Index) và **không phải dữ liệu** (code, cấu trúc object).
-----> [note] leo thang lock
-----> [note] lock và foreign key
-----> [note] Việc đọc dữ liệu tùy vào việc thiết lập _mức cô lập (isolation level)_ mà hệ thống đang sử dụng: Pessimistic Locking: | Optimistic Locking: | Multi-Version Concurrency Control (MVCC): Đây là kỹ thuật được sử dụng trong các DB (PostgreSQL, MySQL)
------> [indexing]
-> _Deadlock:_ Là trạng thái khi mà 2 hoặc nhiều giao dịch/luồng (thread) bị kẹt vì mỗi bên giữ tài nguyên mà bên kia cần, dẫn đến chờ nhau mãi mãi.
--> [solutions]:

## race condition
