# Javascript Foundation Q&A

---

### Level 1: Remembering

#### Q_LEVEL1_101: What is JavaScript?

**Question:**
en: What is JavaScript?
vi: JavaScript là gì?

**Answer:**
en: JavaScript is a high-level, dynamic programming language mainly used to build interactive web applications. It runs in browsers and also on servers through environments such as Node.js.
vi: JavaScript là một ngôn ngữ lập trình bậc cao, linh hoạt, thường dùng để xây dựng ứng dụng web có tính tương tác. Nó chạy được cả trong trình duyệt lẫn phía server thông qua môi trường như Node.js.

#### Q_LEVEL1_102: What is ECMAScript?

**Question:**
en: What is ECMAScript?
vi: ECMAScript là gì?

**Answer:**
en: ECMAScript is the language specification that defines the standard behavior of JavaScript. JavaScript engines implement that specification with some environment-specific APIs.
vi: ECMAScript là bộ đặc tả chuẩn mô tả cách JavaScript phải hoạt động. Các JavaScript engine sẽ triển khai đặc tả đó rồi bổ sung thêm API riêng của môi trường chạy.

#### Q_LEVEL1_369: What is a JavaScript runtime?

**Question:**
en: What is a JavaScript runtime?
vi: **JavaScript runtime** là gì?

**Answer:**
en: A JavaScript runtime is the environment where JavaScript code executes. It usually includes a JavaScript engine plus extra APIs and features, such as the DOM in browsers or file system and process APIs in Node.js.
vi: **JavaScript runtime** là môi trường nơi code JavaScript được thực thi. Nó thường bao gồm JavaScript engine cùng với các API và tính năng bổ sung, như DOM trong trình duyệt hoặc API file system và process trong Node.js.

#### Q_LEVEL1_103: Name JavaScript primitive data types.

**Question:**
en: Name the primitive data types in JavaScript.
vi: Hãy kể tên các kiểu dữ liệu nguyên thủy trong JavaScript.

**Answer:**
en: The primitive types are `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, and `null`. They represent single immutable values.
vi: Các kiểu dữ liệu nguyên thủy gồm `string`, `number`, `bigint`, `boolean`, `undefined`, `symbol`, và `null`. Chúng đại diện cho giá trị đơn lẻ và về bản chất được xử lý như dữ liệu bất biến.

#### Q_LEVEL1_104: What does `typeof` do?

**Question:**
en: What does the `typeof` operator do?
vi: Toán tử `typeof` dùng để làm gì?

**Answer:**
en: `typeof` returns a string describing the type of a value at runtime. It is often used for quick type checks, although some results such as `typeof null` are historically surprising.
vi: `typeof` trả về chuỗi mô tả kiểu dữ liệu của một giá trị tại thời điểm chạy. Nó hữu ích để kiểm tra nhanh kiểu dữ liệu, dù có vài trường hợp gây nhầm lẫn như `typeof null`.

#### Q_LEVEL1_105: What is the DOM?

**Question:**
en: What is the DOM?
vi: DOM là gì?

**Answer:**
en: The DOM, or Document Object Model, is a tree-like representation of an HTML or XML document. JavaScript uses it to read, modify, create, and remove UI elements in the browser.
vi: DOM, viết tắt của Document Object Model, là mô hình cây biểu diễn tài liệu HTML hoặc XML. JavaScript dùng DOM để đọc, sửa, tạo mới hoặc xóa các phần tử giao diện trong trình duyệt.

#### Q_LEVEL1_106: What is an event in JavaScript?

**Question:**
en: What is an event in JavaScript?
vi: Event trong JavaScript là gì?

**Answer:**
en: An event is a signal that something happened, such as a click, key press, or network response. JavaScript can listen for these signals and run callback functions in response.
vi: Event là tín hiệu cho biết một hành động hoặc thay đổi đã xảy ra, ví dụ click chuột, nhấn phím, hoặc nhận phản hồi từ network. JavaScript có thể lắng nghe các tín hiệu đó và chạy hàm xử lý tương ứng.

#### Q_LEVEL1_107: What is a function?

**Question:**
en: What is a function in JavaScript?
vi: Function trong JavaScript là gì?

**Answer:**
en: A function is a reusable block of code that can accept inputs and return an output. In JavaScript, functions are first-class values, so they can be passed around like other variables.
vi: Function là một khối code có thể tái sử dụng, nhận đầu vào và trả về kết quả. Trong JavaScript, function là công dân hạng nhất nên có thể gán cho biến, truyền vào hàm khác hoặc trả về như một giá trị.

#### Q_LEVEL1_108: What is a closure?

**Question:**
en: What is a closure?
vi: Closure là gì?

**Answer:**
en: A closure is created when a function remembers variables from its outer scope even after that outer scope has finished executing. This allows data to stay accessible in a controlled way.
vi: Closure xuất hiện khi một function vẫn nhớ được biến ở scope bên ngoài ngay cả khi scope đó đã chạy xong. Cơ chế này giúp giữ trạng thái nội bộ mà không cần lộ dữ liệu ra ngoài trực tiếp.

#### Q_LEVEL1_109: What are `let`, `const`, and `var`?

**Question:**
en: What are `let`, `const`, and `var` used for?
vi: `let`, `const`, và `var` dùng để làm gì?

**Answer:**
en: They are keywords for declaring variables. `let` creates a block-scoped variable, `const` creates a block-scoped binding that cannot be reassigned, and `var` creates a function-scoped variable with older hoisting behavior.
vi: Đây là các từ khóa dùng để khai báo biến. `let` tạo biến theo block scope, `const` tạo binding theo block scope và không cho gán lại, còn `var` là kiểu cũ theo function scope với hành vi hoisting dễ gây lỗi hơn.

#### Q_LEVEL1_110: What is hoisting?

**Question:**
en: What is hoisting in JavaScript?
vi: Hoisting trong JavaScript là gì?

**Answer:**
en: Hoisting is JavaScript's behavior of processing declarations before execution. Function declarations are fully hoisted, while `var`, `let`, and `const` are treated differently during initialization.
vi: Hoisting là cách JavaScript xử lý khai báo trước khi code thật sự được thực thi. Function declaration được đưa lên đầy đủ, còn `var`, `let`, và `const` có cách khởi tạo khác nhau nên dễ tạo ra hành vi bất ngờ nếu hiểu sai.

#### Q_LEVEL1_111: What is the difference between `==` and `===`?

**Question:**
en: What is the difference between `==` and `===`?
vi: Sự khác nhau giữa `==` và `===` là gì?

**Answer:**
en: `==` compares values after type coercion, while `===` compares both value and type without coercion. `===` is usually preferred because it is more predictable.
vi: `==` so sánh sau khi ép kiểu, còn `===` so sánh cả giá trị lẫn kiểu dữ liệu mà không ép kiểu. Trong thực tế, `===` thường được ưu tiên vì ít gây hiểu nhầm hơn.

#### Q_LEVEL1_112: What is an array?

**Question:**
en: What is an array in JavaScript?
vi: Array trong JavaScript là gì?

**Answer:**
en: An array is an ordered collection of values. It can store items of different types and provides built-in methods such as `map`, `filter`, and `reduce`.
vi: Array là một tập hợp có thứ tự của nhiều giá trị. Nó có thể chứa nhiều kiểu dữ liệu khác nhau và đi kèm nhiều hàm tiện ích như `map`, `filter`, và `reduce`.

#### Q_LEVEL1_113: What is an object?

**Question:**
en: What is an object in JavaScript?
vi: Object trong JavaScript là gì?

**Answer:**
en: An object is a collection of key-value pairs. It is commonly used to model structured data and behavior in JavaScript applications.
vi: Object là tập hợp các cặp key-value. Đây là cấu trúc rất phổ biến để biểu diễn dữ liệu có cấu trúc và gom các hành vi liên quan trong ứng dụng JavaScript.

#### Q_LEVEL1_114: What is JSON?

**Question:**
en: What is JSON?
vi: JSON là gì?

**Answer:**
en: JSON stands for JavaScript Object Notation and is a lightweight data interchange format. It is widely used for APIs because it is easy for humans to read and machines to parse.
vi: JSON là viết tắt của JavaScript Object Notation, một định dạng trao đổi dữ liệu gọn nhẹ. Nó được dùng rất nhiều trong API vì dễ đọc, dễ parse và tương thích tốt giữa nhiều nền tảng.

#### Q_LEVEL1_115: What is a Promise?

**Question:**
en: What is a Promise in JavaScript?
vi: Promise trong JavaScript là gì?

**Answer:**
en: A Promise is an object that represents the eventual result of an asynchronous operation. It can be pending, fulfilled, or rejected.
vi: Promise là một đối tượng đại diện cho kết quả sẽ có trong tương lai của một tác vụ bất đồng bộ. Nó thường đi qua ba trạng thái chính là pending, fulfilled, và rejected.

#### Q_LEVEL1_116: What does `async` mean?

**Question:**
en: What does the `async` keyword mean in JavaScript?
vi: Từ khóa `async` trong JavaScript có ý nghĩa gì?

**Answer:**
en: `async` marks a function as asynchronous and makes it return a Promise automatically. It allows the use of `await` inside that function.
vi: `async` đánh dấu một hàm là bất đồng bộ và khiến hàm đó tự động trả về `Promise`. Nó cũng cho phép dùng `await` bên trong hàm đó để viết code dễ đọc hơn.

#### Q_LEVEL1_117: What does `await` do?

**Question:**
en: What does `await` do?
vi: `await` dùng để làm gì?

**Answer:**
en: `await` pauses the execution of an `async` function until a Promise settles, then returns the resolved value or throws the rejection reason. It helps write asynchronous code in a more synchronous style.
vi: `await` tạm dừng phần thực thi trong một hàm `async` cho tới khi `Promise` hoàn thành, rồi trả về giá trị resolve hoặc ném ra lỗi reject. Nhờ vậy code bất đồng bộ trở nên dễ đọc như code tuần tự.

#### Q_LEVEL1_118: What is scope?

**Question:**
en: What is scope in JavaScript?
vi: Scope trong JavaScript là gì?

**Answer:**
en: Scope defines where variables and functions are accessible in code. Common scopes include global scope, function scope, and block scope.
vi: Scope là phạm vi mà biến hoặc function có thể được truy cập trong code. Những loại phổ biến là global scope, function scope, và block scope.

#### Q_LEVEL1_119: What is the event loop?

**Question:**
en: What is the event loop?
vi: Event loop là gì?

**Answer:**
en: The event loop is the mechanism that coordinates the call stack, callback queues, and asynchronous tasks. It allows JavaScript to handle non-blocking operations even though the main thread executes one task at a time.
vi: Event loop là cơ chế điều phối giữa call stack, hàng đợi callback, và các tác vụ bất đồng bộ. Nhờ nó mà JavaScript có thể xử lý tác vụ không chặn dù luồng chính chỉ chạy từng tác vụ một.

**DETAILS =>** common/javascript/foundation/Q_LEVEL1_119.md
**RESOUCES:** [#1]

#### Q_LEVEL1_120: What is strict mode?

**Question:**
en: What is strict mode in JavaScript?
vi: Strict mode trong JavaScript là gì?

**Answer:**
en: Strict mode is a restricted variant of JavaScript enabled with `"use strict"`. It helps catch unsafe actions early, such as assigning to undeclared variables.
vi: Strict mode là chế độ thực thi nghiêm ngặt được bật bằng `"use strict"`. Nó giúp phát hiện sớm các hành vi không an toàn, ví dụ gán giá trị cho biến chưa khai báo.

---

### Level 2: Understanding

#### Q_LEVEL2_201: Explain why JavaScript is called single-threaded.

**Question:**
en: Explain why JavaScript is called a single-threaded language.
vi: Giải thích vì sao JavaScript thường được gọi là ngôn ngữ single-threaded.

**Answer:**
en: JavaScript executes its main code on a single call stack, so only one operation runs there at a time. It still handles concurrency by delegating work to browser or runtime APIs and then scheduling callbacks back through the event loop.
vi: JavaScript được gọi là single-threaded vì phần code chính chạy trên một call stack duy nhất, nên mỗi thời điểm chỉ xử lý một việc trên stack đó. Vấn đề là nhiều người hiểu nhầm nó không làm được concurrency, trong khi thực tế browser hoặc runtime sẽ xử lý phần việc nền rồi trả callback về qua event loop.

#### Q_LEVEL2_202: Explain the difference between `null` and `undefined`.

**Question:**
en: Explain the difference between `null` and `undefined`.
vi: Giải thích sự khác nhau giữa `null` và `undefined`.

**Answer:**
en: `undefined` usually means a value has not been assigned, while `null` is an intentional absence of value. The distinction matters because one often indicates a missing initialization and the other expresses a deliberate state.
vi: `undefined` thường mang ý nghĩa chưa có giá trị hoặc chưa được gán, còn `null` thể hiện chủ đích là không có dữ liệu. Vấn đề là nếu dùng lẫn lộn thì code rất khó đọc, nên cần thống nhất khi nào biểu diễn trạng thái trống có chủ đích.

#### Q_LEVEL2_203: Explain lexical scope.

**Question:**
en: Explain lexical scope in JavaScript.
vi: Giải thích lexical scope trong JavaScript.

**Answer:**
en: Lexical scope means variable access is determined by where code is written, not where a function is called. This is why inner functions can access variables from their outer declarations.
vi: Lexical scope nghĩa là phạm vi truy cập biến được quyết định tại lúc viết code chứ không phải lúc hàm được gọi. Nhờ vậy một hàm con có thể nhìn thấy biến của hàm cha nơi nó được khai báo, đây cũng là nền tảng để hiểu **closure**.

#### Q_LEVEL2_204: Describe how closures are useful.

**Question:**
en: Describe how closures are useful in real applications.
vi: Mô tả việc closure hữu ích như thế nào trong ứng dụng thực tế.

**Answer:**
en: Closures let functions keep private state, which is useful for encapsulation, factories, and callbacks. They help structure code without exposing every variable globally.
vi: Closure hữu ích vì nó cho phép giữ trạng thái riêng mà không cần làm biến đó thành global. Giải pháp này thường dùng trong factory function, callback, hoặc các module nhỏ cần che giấu dữ liệu nội bộ để tránh bị sửa ngoài ý muốn.

#### Q_LEVEL2_205: Compare function declarations and arrow functions.

**Question:**
en: Compare function declarations and arrow functions.
vi: So sánh function declaration và arrow function.

**Answer:**
en: Function declarations are hoisted and have their own `this`, `arguments`, and `prototype`. Arrow functions are more concise and capture `this` lexically, which makes them convenient for callbacks but unsuitable as constructors.
vi: Function declaration được hoist và có cơ chế `this`, `arguments`, `prototype` riêng. Arrow function ngắn gọn hơn và giữ `this` theo lexical scope, nên rất tiện cho callback nhưng không phù hợp để làm constructor.

#### Q_LEVEL2_206: Explain how prototype inheritance works.

**Question:**
en: Explain how prototype inheritance works in JavaScript.
vi: Giải thích cách prototype inheritance hoạt động trong JavaScript.

**Answer:**
en: Objects in JavaScript can inherit properties from another object through the prototype chain. When a property is not found on the object itself, the engine looks up the chain until it finds a match or reaches the end.
vi: JavaScript kế thừa thông qua prototype chain, nghĩa là object có thể truy xuất thuộc tính từ object cha liên kết ở phía sau. Khi không tìm thấy thuộc tính trên chính nó, engine sẽ lần lượt dò lên chuỗi prototype cho tới khi tìm được hoặc hết chuỗi.

#### Q_LEVEL2_207: Explain the purpose of promises over callbacks.

**Question:**
en: Explain why Promises are often preferred over deeply nested callbacks.
vi: Giải thích vì sao Promise thường được ưu tiên hơn callback lồng nhau quá sâu.

**Answer:**
en: Promises improve readability and error handling by allowing async steps to be chained in a structured way. They reduce callback nesting and make failure propagation more consistent.
vi: Vấn đề của callback lồng sâu là code khó đọc, khó bắt lỗi và dễ tạo ra tình trạng callback hell. Promise là giải pháp giúp chuỗi xử lý bất đồng bộ rõ ràng hơn, có thể gom luồng thành công và lỗi theo cách nhất quán hơn.

#### Q_LEVEL2_208: Explain the difference between synchronous and asynchronous code.

**Question:**
en: Explain the difference between synchronous and asynchronous code.
vi: Giải thích sự khác nhau giữa code đồng bộ và bất đồng bộ.

**Answer:**
en: Synchronous code runs step by step and waits for each operation to finish before moving on. Asynchronous code allows long-running work to happen without blocking the main flow, improving responsiveness.
vi: Code đồng bộ chạy tuần tự và phải chờ từng bước hoàn thành rồi mới đi tiếp. Code bất đồng bộ cho phép các tác vụ tốn thời gian diễn ra mà không chặn luồng chính, nhờ đó ứng dụng phản hồi tốt hơn với người dùng.

#### Q_LEVEL2_209: Why is immutability useful in JavaScript applications?

**Question:**
en: Why is immutability useful in JavaScript applications?
vi: Vì sao immutability hữu ích trong ứng dụng JavaScript?

**Answer:**
en: Immutability reduces accidental side effects because data is not modified in place. It makes state changes easier to reason about, especially in UI frameworks and debugging scenarios.
vi: Immutability hữu ích vì nó giảm nguy cơ sửa dữ liệu tại chỗ rồi gây side effect khó truy vết. Khi trạng thái được tạo mới thay vì sửa trực tiếp, việc debug, so sánh dữ liệu và quản lý state trong UI sẽ dễ hơn nhiều.

#### Q_LEVEL2_210: Explain truthy and falsy values.

**Question:**
en: Explain truthy and falsy values in JavaScript.
vi: Giải thích truthy và falsy trong JavaScript.

**Answer:**
en: JavaScript converts values to booleans in conditional contexts. Values like `false`, `0`, `""`, `null`, `undefined`, and `NaN` are falsy, while most other values are truthy.
vi: Trong biểu thức điều kiện, JavaScript sẽ ép giá trị sang boolean. Những giá trị như `false`, `0`, `""`, `null`, `undefined`, và `NaN` là falsy, còn phần lớn giá trị còn lại là truthy nên nếu không hiểu rõ rất dễ viết điều kiện sai.

#### Q_LEVEL2_211: Explain how destructuring improves code readability.

**Question:**
en: Explain how destructuring improves code readability.
vi: Giải thích cách destructuring giúp code dễ đọc hơn.

**Answer:**
en: Destructuring lets developers extract values from arrays or objects in a concise way. It reduces repetitive access syntax and makes the intended data shape clearer.
vi: Destructuring giúp lấy dữ liệu từ array hoặc object một cách ngắn gọn, thay vì phải truy cập từng thuộc tính lặp đi lặp lại. Điều này làm code rõ ý hơn, nhất là khi làm việc với dữ liệu trả về từ API hoặc hàm cấu hình.

#### Q_LEVEL2_212: Explain rest parameters and spread syntax.

**Question:**
en: Explain rest parameters and spread syntax.
vi: Giải thích rest parameters và spread syntax.

**Answer:**
en: Rest parameters gather multiple arguments into an array, while spread syntax expands an iterable or object into individual elements. Together they simplify function signatures and immutable updates.
vi: Rest parameters gom nhiều đối số thành một array, còn spread syntax trải các phần tử hoặc thuộc tính ra. Hai cú pháp này rất hữu ích khi viết hàm linh hoạt hoặc cập nhật dữ liệu theo kiểu không mutate trực tiếp.

#### Q_LEVEL2_213: Explain module usage in modern JavaScript.

**Question:**
en: Explain the purpose of modules in modern JavaScript.
vi: Giải thích mục đích của module trong JavaScript hiện đại.

**Answer:**
en: Modules split code into reusable, isolated files with explicit imports and exports. This improves maintainability, dependency management, and code organization.
vi: Module giúp tách code thành các file độc lập có `import` và `export` rõ ràng. Giải pháp này làm kiến trúc dễ bảo trì hơn, kiểm soát phụ thuộc tốt hơn và tránh việc mọi thứ dồn hết vào global scope.

#### Q_LEVEL2_214: Explain shallow copy versus deep copy.

**Question:**
en: Explain the difference between shallow copy and deep copy.
vi: Giải thích sự khác nhau giữa shallow copy và deep copy.

**Answer:**
en: A shallow copy duplicates only the top-level structure, so nested references are still shared. A deep copy recursively duplicates nested data, preventing accidental mutation of the original structure.
vi: Shallow copy chỉ sao chép lớp ngoài cùng nên các object lồng bên trong vẫn còn dùng chung tham chiếu. Deep copy thì sao chép sâu toàn bộ cấu trúc, nhờ đó tránh việc sửa dữ liệu mới nhưng vô tình làm thay đổi dữ liệu gốc.

#### Q_LEVEL2_215: Explain garbage collection at a high level.

**Question:**
en: Explain garbage collection in JavaScript at a high level.
vi: Giải thích garbage collection trong JavaScript ở mức tổng quan.

**Answer:**
en: Garbage collection automatically frees memory that is no longer reachable by the program. Developers still need to avoid unnecessary references because reachable objects cannot be collected.
vi: Garbage collection là cơ chế tự động giải phóng bộ nhớ cho những object không còn được chương trình tham chiếu tới. Tuy nhiên điều đó không có nghĩa là lập trình viên được bỏ qua quản lý tài nguyên, vì chỉ cần giữ tham chiếu sai cách thì object vẫn không được thu hồi.

---

### Level 3: Applying

#### Q_LEVEL3_301: Demonstrate variable scope safely.

**Question:**
en: Show how you would demonstrate safe block scoping similar to `let` and `const`.
vi: Hãy minh họa cách thể hiện block scope an toàn, tương tự tư duy dùng `let` và `const`.

**Answer:**
en: A good demonstration isolates variables inside the smallest possible scope and uses immutable bindings by default. The same design principle exists in C# when limiting variable lifetime and preferring readonly intent.
vi: Khi áp dụng tư duy scope an toàn, ta nên giới hạn biến trong phạm vi nhỏ nhất và ưu tiên binding không bị gán lại nếu không cần thiết. Dù ví dụ code theo chuẩn repo dùng C#, ý tưởng vẫn giống JavaScript: giảm phạm vi truy cập để tránh side effect và lỗi do tái sử dụng biến sai ngữ cảnh.

```csharp
using System;

public class ScopeDemo
{
    public static void Main()
    {
        const int maxRetries = 3; // Similar to a stable `const` binding in JS

        for (int attempt = 1; attempt <= maxRetries; attempt++)
        {
            // `message` only exists inside this block, similar to `let`
            string message = $"Attempt {attempt}";
            Console.WriteLine(message);
        }

        // `message` is not accessible here, which avoids leaking temporary state
    }
}
```

#### Q_LEVEL3_302: Demonstrate array transformation.

**Question:**
en: Demonstrate how you would transform a list of values without mutating the original collection.
vi: Hãy minh họa cách biến đổi một danh sách mà không làm thay đổi collection ban đầu.

**Answer:**
en: In JavaScript, developers often use `map` to create a new array instead of editing the original one. The same immutable mindset can be shown in C# with LINQ projections.
vi: Trong JavaScript, cách làm phổ biến là dùng `map` để tạo mảng mới thay vì sửa trực tiếp dữ liệu cũ. Giải pháp tương đương trong C# là dùng LINQ để biểu diễn rõ ý định biến đổi dữ liệu mà không gây mutate ngoài ý muốn.

```csharp
using System;
using System.Linq;

public class ArrayTransformDemo
{
    public static void Main()
    {
        var scores = new[] { 1, 2, 3, 4 };

        // Create a new sequence instead of mutating the original data
        var doubledScores = scores.Select(score => score * 2).ToArray();

        Console.WriteLine(string.Join(", ", scores));         // 1, 2, 3, 4
        Console.WriteLine(string.Join(", ", doubledScores)); // 2, 4, 6, 8
    }
}
```

#### Q_LEVEL3_303: Demonstrate closure-like behavior.

**Question:**
en: Demonstrate behavior similar to a JavaScript closure that preserves private state.
vi: Hãy minh họa hành vi tương tự closure của JavaScript để giữ trạng thái riêng.

**Answer:**
en: The key idea is to keep state hidden and expose only controlled behavior. In C#, a local function can capture outer variables, which mirrors the mental model of a JavaScript closure.
vi: Vấn đề cần giải quyết là giữ state nội bộ mà không cho phần khác của chương trình sửa bừa. Giải pháp là dùng hàm bên trong để capture biến ở scope ngoài, đây chính là tư duy giống với **closure** trong JavaScript.

```csharp
using System;

public class ClosureDemo
{
    public static void Main()
    {
        Func<int> counter = CreateCounter();

        Console.WriteLine(counter()); // 1
        Console.WriteLine(counter()); // 2
        Console.WriteLine(counter()); // 3
    }

    private static Func<int> CreateCounter()
    {
        int count = 0; // Private state captured by the returned function

        int Increment()
        {
            count++;
            return count;
        }

        return Increment;
    }
}
```

#### Q_LEVEL3_304: Show asynchronous flow with async and await.

**Question:**
en: Show how you would model an asynchronous flow similar to JavaScript `async` and `await`.
vi: Hãy minh họa luồng xử lý bất đồng bộ tương tự `async` và `await` trong JavaScript.

**Answer:**
en: The important part is to await asynchronous work instead of blocking the thread. This keeps the code readable and makes success and failure handling easier to follow.
vi: Khi áp dụng tư duy `async/await`, mục tiêu là chờ tác vụ bất đồng bộ theo cách không chặn luồng chính và vẫn giữ code dễ đọc. Cách này tốt hơn kiểu lồng callback vì luồng xử lý thành công hay lỗi đều rõ ràng hơn.

```csharp
using System;
using System.Threading.Tasks;

public class AsyncDemo
{
    public static async Task Main()
    {
        string result = await FetchMessageAsync();
        Console.WriteLine(result);
    }

    private static async Task<string> FetchMessageAsync()
    {
        // Simulate I/O work, similar to waiting on a Promise in JavaScript
        await Task.Delay(200);
        return "Data loaded";
    }
}
```

#### Q_LEVEL3_305: Show safe object copying before update.

**Question:**
en: Show how you would update structured data safely without mutating the original object.
vi: Hãy minh họa cách cập nhật dữ liệu có cấu trúc mà không sửa trực tiếp object ban đầu.

**Answer:**
en: In JavaScript, this is often done with object spread to create a new object before updating fields. The same idea in C# is to create a copy and then apply the change to the new instance.
vi: Trong JavaScript, ta thường dùng object spread để tạo bản sao rồi mới cập nhật thuộc tính. Tư duy này giúp tránh side effect và làm việc với state management an toàn hơn; trong C# có thể biểu diễn bằng record với `with` expression.

```csharp
using System;

public record UserProfile(string Name, string Role);

public class CopyUpdateDemo
{
    public static void Main()
    {
        var original = new UserProfile("An", "Developer");

        // Create a new object instead of mutating the existing one
        var updated = original with { Role = "Tech Lead" };

        Console.WriteLine(original); // UserProfile { Name = An, Role = Developer }
        Console.WriteLine(updated);  // UserProfile { Name = An, Role = Tech Lead }
    }
}
```
