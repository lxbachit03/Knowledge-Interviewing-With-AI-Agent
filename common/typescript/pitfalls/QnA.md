# TypeScript Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_901: Excessive use of `any`.

**Question:**
en: Why is the excessive use of `any` considered a pitfall, and how can it be avoided?
vi: Tại sao việc sử dụng quá mức `any` được coi là một sai lầm, và làm thế nào để tránh nó?

**Answer:**
en: `any` effectively disables type checking, leading to runtime errors that TypeScript was meant to prevent. Avoid it by using `unknown` for values of unknown types, or by defining proper interfaces and union types. Enable `noImplicitAny` in `tsconfig.json`.
vi: `any` vô hiệu hóa việc kiểm tra kiểu, dẫn đến các lỗi runtime mà TypeScript đáng lẽ phải ngăn chặn. Tránh nó bằng cách sử dụng `unknown` cho các giá trị không rõ kiểu, hoặc bằng cách định nghĩa các interface và union type phù hợp. Hãy bật `noImplicitAny` trong `tsconfig.json`.

#### Q_LEVEL1_902: Ignoring `strictNullChecks`.

**Question:**
en: Why is disabling `strictNullChecks` a dangerous pitfall?
vi: Tại sao việc tắt `strictNullChecks` là một sai lầm nguy hiểm?

**Answer:**
en: Without `strictNullChecks`, `null` and `undefined` are assignable to every type, leading to the infamous "Cannot read property 'x' of undefined" runtime errors. Keeping it enabled forces you to handle these cases explicitly.
vi: Nếu không có `strictNullChecks`, `null` và `undefined` có thể được gán cho mọi kiểu dữ liệu, dẫn đến các lỗi runtime nổi tiếng "Cannot read property 'x' of undefined". Việc bật nó buộc bạn phải xử lý các trường hợp này một cách rõ ràng.

#### Q_LEVEL1_903: Misusing `Non-null Assertion Operator` (`!`).

**Question:**
en: What are the risks of using the `!` operator frequently?
vi: Rủi ro khi sử dụng toán tử `!` (khẳng định không null) thường xuyên là gì?

**Answer:**
en: The `!` operator tells the compiler that a value is definitely not null or undefined. If you are wrong, it results in a runtime crash. It should only be used when you are 100% sure the value exists due to logic the compiler can't see.
vi: Toán tử `!` nói với trình biên dịch rằng một giá trị chắc chắn không phải là null hoặc undefined. Nếu bạn sai, nó sẽ dẫn đến crash lúc runtime. Nó chỉ nên được sử dụng khi bạn chắc chắn 100% rằng giá trị tồn tại do logic mà trình biên dịch không thể thấy được.

---

### Level 2: Understanding

#### Q_LEVEL2_904: Misunderstanding `as` (Type Assertions).

**Question:**
en: What is the risk of using type assertions (`as Type`) frequently?
vi: Rủi ro khi sử dụng khẳng định kiểu (`as Type`) thường xuyên là gì?

**Answer:**
en: Type assertions tell the compiler "trust me, I know what I'm doing," which can hide actual type mismatches. If the runtime value doesn't match the asserted type, code will fail silently or crash. Prefer type guards or proper type definitions over assertions.
vi: Khẳng định kiểu nói với trình biên dịch "tin tôi đi, tôi biết mình đang làm gì", điều này có thể che giấu sự không khớp kiểu thực tế. Nếu giá trị runtime không khớp với kiểu được khẳng định, code sẽ thất bại âm thầm hoặc bị crash. Hãy ưu tiên sử dụng type guards hoặc định nghĩa kiểu phù hợp thay vì dùng assertion.

#### Q_LEVEL2_905: Over-complicating Generics.

**Question:**
en: When do Generics become a pitfall in TypeScript?
vi: Khi nào Generics trở thành một sai lầm trong TypeScript?

**Answer:**
en: Over-using generics for simple functions or creating deeply nested generic structures makes code unreadable and hard to maintain. If a generic isn't used to relate two or more values or types, it might be unnecessary.
vi: Sử dụng quá mức generics cho các hàm đơn giản hoặc tạo ra các cấu trúc generic lồng nhau sâu sắc làm cho code trở nên khó đọc và khó bảo trì. Nếu một generic không được sử dụng để liên kết hai hoặc nhiều giá trị hoặc kiểu, nó có thể không cần thiết.

#### Q_LEVEL2_906: Confusion between `interface` and `class`.

**Question:**
en: What is the common mistake when using interfaces to represent runtime data?
vi: Sai lầm phổ biến khi sử dụng interface để đại diện cho dữ liệu runtime là gì?

**Answer:**
en: Interfaces do not exist at runtime. You cannot use `instanceof` with an interface. If you need runtime checks or default values, use a `class`.
vi: Interface không tồn tại lúc runtime. Bạn không thể sử dụng `instanceof` với một interface. Nếu bạn cần kiểm tra runtime hoặc các giá trị mặc định, hãy sử dụng một `class`.

#### Q_LEVEL2_907: Structural Typing Surprises.

**Question:**
en: How can TypeScript's structural typing lead to unexpected behavior?
vi: Hệ thống kiểu cấu trúc của TypeScript có thể dẫn đến hành vi không mong muốn như thế nào?

**Answer:**
en: Because TypeScript is structural, an object with *extra* properties can still satisfy an interface. This can lead to bugs if you iterate over keys or spread the object into a database call that doesn't expect extra fields.
vi: Vì TypeScript dựa trên cấu trúc, một đối tượng có *thêm* các thuộc tính vẫn có thể thỏa mãn một interface. Điều này có thể dẫn đến lỗi nếu bạn lặp qua các key hoặc spread đối tượng vào một lời gọi database không mong đợi các trường thừa.

#### Q_LEVEL2_908: Not Using `readonly` for Immutable Data.

**Question:**
en: Why is neglecting `readonly` a pitfall in large applications?
vi: Tại sao việc bỏ qua `readonly` là một sai lầm trong các ứng dụng lớn?

**Answer:**
en: Without `readonly`, state can be mutated accidentally anywhere in the app, making debugging difficult. Using `readonly` or `ReadonlyArray` ensures that data remains immutable and changes are intentional.
vi: Nếu không có `readonly`, trạng thái có thể bị thay đổi vô ý ở bất kỳ đâu trong ứng dụng, làm cho việc debugging trở nên khó khăn. Sử dụng `readonly` hoặc `ReadonlyArray` đảm bảo rằng dữ liệu vẫn không thay đổi và các thay đổi là có chủ ý.
