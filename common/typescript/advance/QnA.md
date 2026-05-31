# TypeScript Advance Q&A

### Level 4: Analyzing

#### Q_LEVEL4_401: Analyze the trade-offs of using `enum` vs `const enum` vs `union of literals`.

**Question:**
en: Analyze the trade-offs of using `enum`, `const enum`, and `union of literal types` in TypeScript.
vi: Phân tích sự đánh đổi khi sử dụng `enum`, `const enum`, và `union of literal types` trong TypeScript.

**Answer:**
en: 
- `enum`: Generates a real object at runtime, supporting reverse mapping (for numeric enums). Increases bundle size.
- `const enum`: Completely removed during compilation; values are inlined. No runtime overhead, but doesn't support reverse mapping and can cause issues with isolated modules.
- `union of literals`: Purely a type-level construct. Zero runtime overhead. Highly flexible and works well with type narrowing. Often preferred in modern TS.
vi:
- `enum`: Tạo ra một đối tượng thực sự lúc runtime, hỗ trợ reverse mapping (cho numeric enum). Làm tăng kích thước bundle.
- `const enum`: Được loại bỏ hoàn toàn trong quá trình biên dịch; các giá trị được chèn trực tiếp (inlined). Không có chi phí runtime, nhưng không hỗ trợ reverse mapping và có thể gây ra vấn đề với các module bị cô lập (isolated modules).
- `union of literals`: Hoàn toàn là một cấu trúc ở cấp độ kiểu. Không tốn chi phí runtime. Rất linh hoạt và hoạt động tốt với việc thu hẹp kiểu. Thường được ưu tiên trong TS hiện đại.

#### Q_LEVEL4_402: Compare `interface` and `type` for extending complex types.

**Question:**
en: Analyze how `interface` and `type` handle extension and merging of complex types.
vi: Phân tích cách `interface` và `type` xử lý việc mở rộng và gộp các kiểu phức tạp.

**Answer:**
en: Interfaces use `extends` for inheritance and support declaration merging (multiple interfaces with the same name are joined). Types use intersection (`&`) for combining. Interfaces are generally faster for the compiler to check because they are cached by name, whereas intersections require recursive checking.
vi: Interface sử dụng `extends` để kế thừa và hỗ trợ gộp khai báo (nhiều interface cùng tên sẽ được gộp lại). Type sử dụng intersection (`&`) để kết hợp. Interface thường nhanh hơn để trình biên dịch kiểm tra vì chúng được lưu đệm (cached) theo tên, trong khi các intersection yêu cầu kiểm tra đệ quy.

#### Q_LEVEL4_403: Investigate the implications of `strict` mode in `tsconfig.json`.

**Question:**
en: Investigate the most significant flags enabled by the `strict` setting in `tsconfig.json` and their impact on code quality.
vi: Điều tra các flag quan trọng nhất được bật bởi cài đặt `strict` trong `tsconfig.json` và tác động của chúng đến chất lượng code.

**Answer:**
en: 
- `noImplicitAny`: Prevents accidental use of `any`.
- `strictNullChecks`: Forces explicit handling of `null` and `undefined`.
- `strictFunctionTypes`: Ensures function parameters are checked more strictly (contravariance).
- `strictPropertyInitialization`: Ensures class properties are initialized in the constructor.
These flags collectively eliminate entire classes of runtime errors by moving them to compile-time.
vi:
- `noImplicitAny`: Ngăn chặn việc sử dụng vô ý kiểu `any`.
- `strictNullChecks`: Buộc phải xử lý rõ ràng `null` và `undefined`.
- `strictFunctionTypes`: Đảm bảo các tham số hàm được kiểm tra chặt chẽ hơn (contravariance).
- `strictPropertyInitialization`: Đảm bảo các thuộc tính class được khởi tạo trong constructor.
Các flag này cùng nhau loại bỏ toàn bộ các loại lỗi runtime bằng cách chuyển chúng về thời điểm biên dịch.

#### Q_LEVEL4_404: Analyze the behavior of `this` in TypeScript classes and how to type it.

**Question:**
en: Analyze how TypeScript handles the typing of `this` and how to prevent "lost context" errors.
vi: Phân tích cách TypeScript xử lý việc định kiểu cho `this` và cách ngăn chặn lỗi "mất ngữ cảnh" (lost context).

**Answer:**
en: TypeScript allows explicit `this` parameters in functions to define what `this` should be. In classes, arrow functions capture `this` lexically, preventing it from changing when the method is passed as a callback.
vi: TypeScript cho phép các tham số `this` rõ ràng trong các hàm để định nghĩa `this` nên là gì. Trong các class, arrow functions nắm bắt `this` theo ngữ cảnh (lexically), ngăn nó thay đổi khi phương thức được truyền dưới dạng callback.

```typescript
class MyClass {
  name = "TS";
  // Arrow function to preserve 'this'
  printName = () => {
    console.log(this.name);
  };
  
  // Explicit 'this' parameter
  logName(this: MyClass) {
    console.log(this.name);
  }
}
```

#### Q_LEVEL4_405: Contrast "Variance" (Covariance and Contravariance) in TypeScript.

**Question:**
en: Contrast how Covariance and Contravariance apply to function types in TypeScript.
vi: Đối chiếu cách Covariance và Contravariance áp dụng cho các kiểu hàm trong TypeScript.

**Answer:**
en: In TypeScript, function return types are covariant (you can return a more specific type). Function parameters are contravariant (you can pass a function that accepts a more general type) when `strictFunctionTypes` is enabled. This ensures that the function can safely handle any input it's given.
vi: Trong TypeScript, các kiểu trả về của hàm là covariant (bạn có thể trả về một kiểu cụ thể hơn). Các tham số hàm là contravariant (bạn có thể truyền một hàm chấp nhận một kiểu tổng quát hơn) khi `strictFunctionTypes` được bật. Điều này đảm bảo rằng hàm có thể xử lý an toàn bất kỳ đầu vào nào được cung cấp.

---

### Level 5: Evaluating

#### Q_LEVEL5_501: Evaluate the use of `any` in a legacy JavaScript migration project.

**Question:**
en: Evaluate the strategy of using `any` versus `unknown` or `Object` when migrating a large legacy JavaScript codebase to TypeScript.
vi: Đánh giá chiến lược sử dụng `any` so với `unknown` hoặc `Object` khi chuyển đổi một codebase JavaScript cũ lớn sang TypeScript.

**Answer:**
en: Using `any` is a quick way to get the project compiling but defers type safety. `unknown` is better as it forces developers to perform type checks later. A phased approach using `allowJs: true` and gradually introducing types is often better than a mass `any` conversion.
vi: Sử dụng `any` là một cách nhanh chóng để dự án có thể biên dịch được nhưng lại trì hoãn tính an toàn kiểu. `unknown` tốt hơn vì nó buộc các nhà phát triển phải thực hiện kiểm tra kiểu sau đó. Một cách tiếp cận theo từng giai đoạn sử dụng `allowJs: true` và dần dần đưa vào các kiểu dữ liệu thường tốt hơn là chuyển đổi hàng loạt sang `any`.

#### Q_LEVEL5_502: Critique the pattern of using Decorators in TypeScript.

**Question:**
en: Critique the use of Decorators in TypeScript (experimental vs. stage 3). Should they be used in production?
vi: Phê bình việc sử dụng Decorator trong TypeScript (experimental vs. stage 3). Có nên sử dụng chúng trong môi trường production không?

**Answer:**
en: Decorators provide a clean declarative syntax for meta-programming (common in Angular/NestJS). However, the "experimental" implementation differs from the official ECMAScript proposal. Using them ties the project to a specific compiler behavior. For production, they are acceptable if the framework (like NestJS) relies on them, but one should be aware of the migration effort if the standard changes.
vi: Decorator cung cấp một cú pháp khai báo sạch sẽ cho lập trình meta (phổ biến trong Angular/NestJS). Tuy nhiên, triển khai "experimental" khác với đề xuất chính thức của ECMAScript. Sử dụng chúng sẽ gắn chặt dự án vào một hành vi trình biên dịch cụ thể. Đối với production, chúng có thể chấp nhận được nếu framework (như NestJS) dựa vào chúng, nhưng cần lưu ý về nỗ lực chuyển đổi nếu tiêu chuẩn thay đổi.

#### Q_LEVEL5_503: Justify the choice of TypeScript over vanilla JavaScript for a small team.

**Question:**
en: Justify the investment in TypeScript for a small team (2-3 developers) building a medium-sized web application.
vi: Bào chữa cho việc đầu tư vào TypeScript cho một team nhỏ (2-3 dev) đang xây dựng một ứng dụng web quy mô trung bình.

**Answer:**
en: Even for small teams, the "self-documenting" nature of TS and the immediate feedback from the IDE reduce communication overhead and debugging time. The cost of setup and learning is quickly offset by the reduction in runtime bugs and the ease of refactoring as the application grows.
vi: Ngay cả đối với các team nhỏ, bản chất "tự tài liệu hóa" của TS và phản hồi tức thì từ IDE giúp giảm chi phí giao tiếp và thời gian debugging. Chi phí thiết lập và học tập nhanh chóng được bù đắp bằng việc giảm các lỗi runtime và sự dễ dàng khi refactor khi ứng dụng phát triển.

#### Q_LEVEL5_504: Appraise the effectiveness of "Branded Types" (Nominal Typing simulation).

**Question:**
en: Appraise the effectiveness of using "Branded Types" to simulate nominal typing in TypeScript.
vi: Thẩm định hiệu quả của việc sử dụng "Branded Types" để mô phỏng nominal typing trong TypeScript.

**Answer:**
en: Branded types (using an intersection with a unique property) effectively prevent accidental mixing of logically different but structurally identical types (e.g., `UserId` vs `OrderId`). They are highly effective for domain-driven design but add some complexity to object creation and casting.
vi: Branded types (sử dụng intersection với một thuộc tính duy nhất) ngăn chặn hiệu quả việc trộn lẫn vô tình các kiểu khác nhau về logic nhưng giống nhau về cấu trúc (ví dụ: `UserId` so với `OrderId`). Chúng rất hiệu quả cho domain-driven design nhưng thêm một chút phức tạp vào việc tạo đối tượng và ép kiểu.

```typescript
type Brand<K, T> = K & { __brand: T };
type UserId = Brand<string, "UserId">;
type OrderId = Brand<string, "OrderId">;

let u: UserId = "123" as UserId;
let o: OrderId = "123" as OrderId;
// u = o; // Error: Type 'OrderId' is not assignable to type 'UserId'
```

#### Q_LEVEL5_505: Evaluate the trade-offs of using `Template Literal Types` for complex string manipulation.

**Question:**
en: Evaluate the trade-offs of using `Template Literal Types` to create complex string-based types (like CSS selectors or path routing).
vi: Đánh giá sự đánh đổi khi sử dụng `Template Literal Types` để tạo các kiểu dựa trên chuỗi phức tạp (như CSS selectors hoặc path routing).

**Answer:**
en: Template literal types enable incredibly powerful type safety for strings. However, they can significantly slow down the compiler if they generate too many permutations (combinatorial explosion). They should be used sparingly for critical parts of the API, not for every string manipulation.
vi: Template literal types cho phép tính an toàn kiểu cực kỳ mạnh mẽ cho các chuỗi. Tuy nhiên, chúng có thể làm chậm đáng kể trình biên dịch nếu chúng tạo ra quá nhiều hoán vị (bùng nổ tổ hợp). Chúng nên được sử dụng tiết kiệm cho các phần quan trọng của API, không phải cho mọi thao tác chuỗi.
