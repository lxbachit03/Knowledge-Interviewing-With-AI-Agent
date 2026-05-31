# TypeScript Foundation Q&A

### Level 1: Remembering

#### Q_LEVEL1_101: What is TypeScript?

**Question:**
en: What is TypeScript?
vi: TypeScript là gì?

**Answer:**
en: TypeScript is a strongly typed programming language that builds on JavaScript, giving you better tooling at any scale. It adds optional static typing to the language.
vi: TypeScript là một ngôn ngữ lập trình có kiểu dữ liệu mạnh (strongly typed) được xây dựng dựa trên JavaScript, cung cấp cho bạn các công cụ tốt hơn ở bất kỳ quy mô nào. Nó bổ sung thêm tính năng kiểm tra kiểu tĩnh (static typing) tùy chọn vào ngôn ngữ.

#### Q_LEVEL1_102: How do you define a variable with a specific type in TypeScript?

**Question:**
en: How do you define a variable with a specific type in TypeScript?
vi: Làm thế nào để định nghĩa một biến với một kiểu cụ thể trong TypeScript?

**Answer:**
en: You can use a colon followed by the type name after the variable name.
vi: Bạn có thể sử dụng dấu hai chấm theo sau là tên kiểu dữ liệu sau tên biến.

```typescript
let count: number = 10;
let name: string = "TypeScript";
```

#### Q_LEVEL1_103: What are the basic types in TypeScript?

**Question:**
en: What are the basic types in TypeScript?
vi: Các kiểu dữ liệu cơ bản trong TypeScript là gì?

**Answer:**
en: The basic types include `number`, `string`, `boolean`, `null`, `undefined`, `any`, `void`, `never`, `unknown`, `enum`, `tuple`, and `array`.
vi: Các kiểu cơ bản bao gồm `number`, `string`, `boolean`, `null`, `undefined`, `any`, `void`, `never`, `unknown`, `enum`, `tuple`, và `array`.

#### Q_LEVEL1_104: What is the `any` type?

**Question:**
en: What is the `any` type?
vi: Kiểu `any` là gì?

**Answer:**
en: The `any` type allows a variable to hold any value, effectively opting out of type checking for that variable.
vi: Kiểu `any` cho phép một biến chứa bất kỳ giá trị nào, về cơ bản là bỏ qua việc kiểm tra kiểu cho biến đó.

#### Q_LEVEL1_105: What is the `void` type?

**Question:**
en: What is the `void` type?
vi: Kiểu `void` là gì?

**Answer:**
en: `void` is used as the return type for functions that do not return a value.
vi: `void` được sử dụng làm kiểu trả về cho các hàm không trả về giá trị nào.

#### Q_LEVEL1_106: How do you define an array of strings in TypeScript?

**Question:**
en: How do you define an array of strings in TypeScript?
vi: Làm thế nào để định nghĩa một mảng các chuỗi trong TypeScript?

**Answer:**
en: You can use `string[]` or `Array<string>`.
vi: Bạn có thể sử dụng `string[]` hoặc `Array<string>`.

```typescript
let list: string[] = ["a", "b", "c"];
let otherList: Array<string> = ["x", "y", "z"];
```

#### Q_LEVEL1_107: What is an Interface in TypeScript?

**Question:**
en: What is an Interface in TypeScript?
vi: Interface trong TypeScript là gì?

**Answer:**
en: An interface is a way to define the shape of an object, specifying the properties and their types that an object must have.
vi: Một interface là một cách để định nghĩa cấu trúc (shape) của một đối tượng, chỉ định các thuộc tính và kiểu dữ liệu của chúng mà một đối tượng phải có.

#### Q_LEVEL1_108: What is a Type Alias?

**Question:**
en: What is a Type Alias?
vi: Type Alias là gì?

**Answer:**
en: A type alias allows you to create a new name for a type using the `type` keyword.
vi: Type alias cho phép bạn tạo một tên mới cho một kiểu dữ liệu bằng cách sử dụng từ khóa `type`.

#### Q_LEVEL1_109: What is the `unknown` type?

**Question:**
en: What is the `unknown` type?
vi: Kiểu `unknown` là gì?

**Answer:**
en: `unknown` is a type-safe counterpart of `any`. You can assign anything to `unknown`, but you cannot perform operations on it without narrowing the type first.
vi: `unknown` là một phiên bản an toàn hơn của `any`. Bạn có thể gán bất cứ thứ gì cho `unknown`, nhưng bạn không thể thực hiện các thao tác trên nó mà không thu hẹp kiểu (narrowing) trước.

#### Q_LEVEL1_110: What is an Enum?

**Question:**
en: What is an Enum?
vi: Enum là gì?

**Answer:**
en: Enums allow a developer to define a set of named constants. TypeScript provides both numeric and string-based enums.
vi: Enum cho phép nhà phát triển định nghĩa một tập hợp các hằng số có tên. TypeScript cung cấp cả enum dựa trên số và chuỗi.

#### Q_LEVEL1_111: What is a Tuple?

**Question:**
en: What is a Tuple?
vi: Tuple là gì?

**Answer:**
en: A tuple is a type that allows you to express an array with a fixed number of elements whose types are known, but need not be the same.
vi: Tuple là một kiểu dữ liệu cho phép bạn biểu diễn một mảng với số lượng phần tử cố định mà kiểu của chúng đã biết, nhưng không nhất thiết phải giống nhau.

#### Q_LEVEL1_112: How do you make a property optional in an interface?

**Question:**
en: How do you make a property optional in an interface?
vi: Làm thế nào để làm cho một thuộc tính trở thành tùy chọn (optional) trong một interface?

**Answer:**
en: You can add a question mark (`?`) after the property name.
vi: Bạn có thể thêm dấu hỏi chấm (`?`) sau tên thuộc tính.

```typescript
interface User {
  id: number;
  name: string;
  email?: string; // Optional property
}
```

#### Q_LEVEL1_113: What is the `never` type?

**Question:**
en: What is the `never` type?
vi: Kiểu `never` là gì?

**Answer:**
en: The `never` type represents the type of values that never occur. It is often used as the return type for functions that always throw an error or never terminate.
vi: Kiểu `never` đại diện cho kiểu giá trị không bao giờ xảy ra. Nó thường được sử dụng làm kiểu trả về cho các hàm luôn ném ra lỗi hoặc không bao giờ kết thúc.

#### Q_LEVEL1_114: What is Type Inference?

**Question:**
en: What is Type Inference?
vi: Type Inference (Suy luận kiểu) là gì?

**Answer:**
en: Type inference is the process where TypeScript automatically determines the type of a variable based on the value assigned to it.
vi: Type inference là quá trình mà TypeScript tự động xác định kiểu của một biến dựa trên giá trị được gán cho nó.

#### Q_LEVEL1_115: What is a Union Type?

**Question:**
en: What is a Union Type?
vi: Union Type là gì?

**Answer:**
en: A union type allows a variable to hold values of multiple types, separated by the pipe (`|`) symbol.
vi: Union type cho phép một biến chứa các giá trị của nhiều kiểu dữ liệu khác nhau, được phân tách bằng ký hiệu ống dẫn (`|`).

#### Q_LEVEL1_116: What is an Intersection Type?

**Question:**
en: What is an Intersection Type?
vi: Intersection Type là gì?

**Answer:**
en: An intersection type combines multiple types into one, using the ampersand (`&`) symbol. The resulting type has all the features of all combined types.
vi: Intersection type kết hợp nhiều kiểu thành một, sử dụng ký hiệu và (`&`). Kiểu kết quả sẽ có tất cả các đặc tính của tất cả các kiểu được kết hợp.

#### Q_LEVEL1_117: What is the `readonly` modifier?

**Question:**
en: What is the `readonly` modifier?
vi: Modifier `readonly` là gì?

**Answer:**
en: The `readonly` modifier makes a property of an object or an element of an array immutable after it is initialized.
vi: Modifier `readonly` làm cho một thuộc tính của một đối tượng hoặc một phần tử của một mảng không thể thay đổi (immutable) sau khi nó được khởi tạo.

#### Q_LEVEL1_118: What is a Literal Type?

**Question:**
en: What is a Literal Type?
vi: Literal Type là gì?

**Answer:**
en: Literal types allow you to specify exact values that a string, number, or boolean must have.
vi: Literal types cho phép bạn chỉ định các giá trị chính xác mà một chuỗi, số hoặc boolean phải có.

#### Q_LEVEL1_119: What is the purpose of `tsconfig.json`?

**Question:**
en: What is the purpose of `tsconfig.json`?
vi: Mục đích của `tsconfig.json` là gì?

**Answer:**
en: The `tsconfig.json` file specifies the root files and the compiler options required to compile the project.
vi: File `tsconfig.json` chỉ định các file gốc và các tùy chọn trình biên dịch (compiler options) cần thiết để biên dịch dự án.

#### Q_LEVEL1_120: How do you perform Type Assertion in TypeScript?

**Question:**
en: How do you perform Type Assertion in TypeScript?
vi: Làm thế nào để thực hiện Type Assertion (Khẳng định kiểu) trong TypeScript?

**Answer:**
en: You can use the `as` keyword or the angle-bracket `< >` syntax to tell the compiler to treat a value as a specific type.
vi: Bạn có thể sử dụng từ khóa `as` hoặc cú pháp ngoặc nhọn `< >` để nói với trình biên dịch coi một giá trị là một kiểu cụ thể.

```typescript
let someValue: unknown = "this is a string";
let strLength: number = (someValue as string).length;
```

---

### Level 2: Understanding

#### Q_LEVEL2_201: Compare Interface and Type Alias.

**Question:**
en: Compare Interface and Type Alias. When should you use one over the other?
vi: So sánh Interface và Type Alias. Khi nào bạn nên sử dụng cái này thay vì cái kia?

**Answer:**
en: Interfaces are better for defining object shapes and support declaration merging. Type aliases are more flexible and can represent unions, primitives, and tuples. Use interfaces for public APIs and object structures; use types for complex combinations.
vi: Interface tốt hơn cho việc định nghĩa cấu trúc đối tượng và hỗ trợ gộp khai báo (declaration merging). Type alias linh hoạt hơn và có thể biểu diễn union, primitive, và tuple. Sử dụng interface cho các API công khai và cấu trúc đối tượng; sử dụng type cho các kết hợp phức tạp.

#### Q_LEVEL2_202: Explain the difference between `any` and `unknown`.

**Question:**
en: Explain the difference between `any` and `unknown`.
vi: Giải thích sự khác biệt giữa `any` và `unknown`.

**Answer:**
en: `any` turns off all type checking, allowing any operation. `unknown` is the type-safe version; it allows any value but requires type narrowing (e.g., using `typeof` or `instanceof`) before you can access properties or call methods on it.
vi: `any` tắt tất cả việc kiểm tra kiểu, cho phép mọi thao tác. `unknown` là phiên bản an toàn; nó cho phép mọi giá trị nhưng yêu cầu thu hẹp kiểu (ví dụ: sử dụng `typeof` hoặc `instanceof`) trước khi bạn có thể truy cập các thuộc tính hoặc gọi các phương thức trên nó.

#### Q_LEVEL2_203: How does TypeScript's Structural Typing differ from Nominal Typing?

**Question:**
en: How does TypeScript's Structural Typing differ from Nominal Typing?
vi: Hệ thống kiểu cấu trúc (Structural Typing) của TypeScript khác với Nominal Typing như thế nào?

**Answer:**
en: Structural typing (duck typing) means two types are compatible if they have the same members. Nominal typing (like in C# or Java) requires types to be explicitly related by name or inheritance.
vi: Structural typing (kiểu cấu trúc) có nghĩa là hai kiểu tương thích nếu chúng có cùng các thành phần. Nominal typing (như trong C# hoặc Java) yêu cầu các kiểu phải có quan hệ rõ ràng theo tên hoặc kế thừa.

#### Q_LEVEL2_204: What is Type Narrowing and why is it important?

**Question:**
en: What is Type Narrowing and why is it important?
vi: Type Narrowing (Thu hẹp kiểu) là gì và tại sao nó lại quan trọng?

**Answer:**
en: Type narrowing is the process of refining a broader type into a more specific type within a conditional block. It is essential for safely working with union types and `unknown`.
vi: Type narrowing là quá trình tinh chỉnh một kiểu rộng thành một kiểu cụ thể hơn trong một khối điều kiện. Nó rất quan trọng để làm việc an toàn với các union type và kiểu `unknown`.

#### Q_LEVEL2_205: Explain "Declaration Merging" in TypeScript.

**Question:**
en: Explain "Declaration Merging" in TypeScript.
vi: Giải thích "Declaration Merging" (Gộp khai báo) trong TypeScript.

**Answer:**
en: Declaration merging is where the compiler merges two or more separate declarations with the same name into a single definition. This is most commonly seen with interfaces.
vi: Gộp khai báo là khi trình biên dịch gộp hai hoặc nhiều khai báo riêng biệt có cùng tên thành một định nghĩa duy nhất. Điều này thường thấy nhất với các interface.

#### Q_LEVEL2_206: What are Generics and what problem do they solve?

**Question:**
en: What are Generics and what problem do they solve?
vi: Generics là gì và chúng giải quyết vấn đề gì?

**Answer:**
en: Generics allow you to create reusable components that work with a variety of types while maintaining type safety. They solve the problem of code duplication when the logic is the same but types differ.
vi: Generics cho phép bạn tạo các thành phần có thể tái sử dụng hoạt động với nhiều kiểu dữ liệu khác nhau trong khi vẫn duy trì tính an toàn kiểu. Chúng giải quyết vấn đề lặp lại code khi logic giống nhau nhưng kiểu dữ liệu khác nhau.

#### Q_LEVEL2_207: Explain the `keyof` operator.

**Question:**
en: Explain the `keyof` operator.
vi: Giải thích toán tử `keyof`.

**Answer:**
en: The `keyof` operator takes an object type and produces a string or numeric literal union of its keys.
vi: Toán tử `keyof` lấy một kiểu đối tượng và tạo ra một union của các literal chuỗi hoặc số từ các key của đối tượng đó.

#### Q_LEVEL2_208: What is the `typeof` operator in a type context?

**Question:**
en: What is the `typeof` operator in a type context?
vi: Toán tử `typeof` trong ngữ cảnh kiểu (type context) là gì?

**Answer:**
en: In a type context, `typeof` is used to refer to the type of a variable or property. It's different from the runtime `typeof` in JavaScript.
vi: Trong ngữ cảnh kiểu, `typeof` được sử dụng để tham chiếu đến kiểu của một biến hoặc thuộc tính. Nó khác với `typeof` lúc runtime trong JavaScript.

#### Q_LEVEL2_209: Explain "Mapped Types".

**Question:**
en: Explain "Mapped Types".
vi: Giải thích "Mapped Types".

**Answer:**
en: Mapped types allow you to create new types based on the properties of an existing type by iterating over its keys.
vi: Mapped types cho phép bạn tạo các kiểu mới dựa trên các thuộc tính của một kiểu hiện có bằng cách lặp qua các key của nó.

#### Q_LEVEL2_210: What is the difference between `null` and `undefined` in TypeScript?

**Question:**
en: What is the difference between `null` and `undefined` in TypeScript?
vi: Sự khác biệt giữa `null` và `undefined` trong TypeScript là gì?

**Answer:**
en: In TypeScript, they are both types and values. `undefined` usually means a variable has been declared but not assigned. `null` is an intentional absence of value. With `strictNullChecks` enabled, they are not assignable to other types.
vi: Trong TypeScript, cả hai đều là kiểu và giá trị. `undefined` thường có nghĩa là một biến đã được khai báo nhưng chưa được gán. `null` là sự vắng mặt có ý định của giá trị. Khi bật `strictNullChecks`, chúng không thể được gán cho các kiểu khác.

#### Q_LEVEL2_211: Explain the `readonly` modifier in classes vs interfaces.

**Question:**
en: Explain the `readonly` modifier in classes vs interfaces.
vi: Giải thích modifier `readonly` trong class so với interface.

**Answer:**
en: In both, it prevents reassignment after initialization. In a class, it can be initialized in the constructor. In an interface, it's a contract for the implementing object.
vi: Ở cả hai, nó ngăn chặn việc gán lại sau khi khởi tạo. Trong một class, nó có thể được khởi tạo trong constructor. Trong một interface, nó là một ràng buộc cho đối tượng thực thi.

#### Q_LEVEL2_212: What is "Discriminated Unions"?

**Question:**
en: What is "Discriminated Unions" (Tagging)?
vi: "Discriminated Unions" (Gộp có phân biệt) là gì?

**Answer:**
en: It's a pattern where multiple types have a common literal property (the "discriminant") used to distinguish between them, allowing for safe type narrowing.
vi: Đó là một pattern trong đó nhiều kiểu có một thuộc tính literal chung (gọi là "discriminant") được sử dụng để phân biệt giữa chúng, cho phép thu hẹp kiểu an toàn.

#### Q_LEVEL2_213: Explain "Const Assertions" (`as const`).

**Question:**
en: Explain "Const Assertions" (`as const`).
vi: Giải thích "Const Assertions" (`as const`).

**Answer:**
en: `as const` tells the compiler to treat an expression as the most specific literal type possible, and makes objects/arrays deeply readonly.
vi: `as const` nói với trình biên dịch coi một biểu thức là kiểu literal cụ thể nhất có thể, và làm cho các đối tượng/mảng trở thành readonly sâu.

#### Q_LEVEL2_214: What are "Utility Types"? Give examples.

**Question:**
en: What are "Utility Types"? Give examples.
vi: "Utility Types" là gì? Cho ví dụ.

**Answer:**
en: Utility types are built-in types that facilitate common type transformations. Examples: `Partial<T>`, `Readonly<T>`, `Pick<T, K>`, `Record<K, T>`.
vi: Utility types là các kiểu được xây dựng sẵn giúp tạo điều kiện cho các chuyển đổi kiểu phổ biến. Ví dụ: `Partial<T>`, `Readonly<T>`, `Pick<T, K>`, `Record<K, T>`.

#### Q_LEVEL2_215: Explain the difference between `module` and `namespace`.

**Question:**
en: Explain the difference between `module` and `namespace`.
vi: Giải thích sự khác biệt giữa `module` và `namespace`.

**Answer:**
en: Namespaces are a TypeScript-specific way to organize code. Modules are the standard ES6 way to organize code using `import`/`export`. Modules are preferred in modern development.
vi: Namespaces là một cách riêng của TypeScript để tổ chức code. Modules là cách tiêu chuẩn của ES6 để tổ chức code bằng `import`/`export`. Modules được ưu tiên hơn trong phát triển hiện đại.

---

### Level 3: Applying

#### Q_LEVEL3_301: Implement a Generic Function to wrap a value in an array.

**Question:**
en: Implement a generic function `toArray<T>(value: T): T[]` that wraps any given value in an array.
vi: Thực hiện một hàm generic `toArray<T>(value: T): T[]` để bao bọc bất kỳ giá trị nào được đưa vào trong một mảng.

**Answer:**
en: This function uses a type parameter `T` to capture the input type and return an array of that type.
vi: Hàm này sử dụng một tham số kiểu `T` để nắm bắt kiểu đầu vào và trả về một mảng của kiểu đó.

```typescript
function toArray<T>(value: T): T[] {
  return [value];
}

const numArr = toArray(123); // number[]
const strArr = toArray("hello"); // string[]
```

#### Q_LEVEL3_302: Create a Discriminated Union for API Responses.

**Question:**
en: Create a discriminated union to represent a successful or failed API response.
vi: Tạo một discriminated union để đại diện cho một phản hồi API thành công hoặc thất bại.

**Answer:**
en: We use a `status` property as the discriminant.
vi: Chúng ta sử dụng thuộc tính `status` làm discriminant.

```typescript
interface SuccessResponse {
  status: "success";
  data: string[];
}

interface ErrorResponse {
  status: "error";
  message: string;
}

type ApiResponse = SuccessResponse | ErrorResponse;

function handleResponse(response: ApiResponse) {
  if (response.status === "success") {
    console.log(response.data); // TypeScript knows it's SuccessResponse
  } else {
    console.error(response.message); // TypeScript knows it's ErrorResponse
  }
}
```

#### Q_LEVEL3_303: Use `Pick` and `Partial` to create a subset of an interface.

**Question:**
en: Given an `User` interface, create a type for updating a user that only allows changing `name` or `email`, and makes them optional.
vi: Cho một interface `User`, hãy tạo một kiểu để cập nhật người dùng mà chỉ cho phép thay đổi `name` hoặc `email`, và làm cho chúng trở thành tùy chọn.

**Answer:**
en: Combine `Partial` and `Pick` utility types.
vi: Kết hợp các utility type `Partial` và `Pick`.

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

type UpdateUserDto = Partial<Pick<User, "name" | "email">>;

const update: UpdateUserDto = {
  name: "New Name"
};
```

#### Q_LEVEL3_304: Implement a Type Guard for a custom class.

**Question:**
en: Implement a type guard function to check if an object is an instance of a `Bird` class.
vi: Thực hiện một hàm type guard để kiểm tra xem một đối tượng có phải là một instance của class `Bird` hay không.

**Answer:**
en: Use the `is` keyword in the return type.
vi: Sử dụng từ khóa `is` trong kiểu trả về.

```typescript
class Bird {
  fly() { console.log("Flying..."); }
}

class Fish {
  swim() { console.log("Swimming..."); }
}

function isBird(animal: Bird | Fish): animal is Bird {
  return (animal as Bird).fly !== undefined;
}

const myPet: Bird | Fish = new Bird();
if (isBird(myPet)) {
  myPet.fly(); // Safely call fly()
}
```

#### Q_LEVEL3_305: Use `keyof` and Generics to create a safe property getter.

**Question:**
en: Write a generic function `getProperty` that takes an object and a key, and returns the value of that property safely.
vi: Viết một hàm generic `getProperty` nhận vào một đối tượng và một key, và trả về giá trị của thuộc tính đó một cách an toàn.

**Answer:**
en: Use `K extends keyof T` to ensure the key exists on the object.
vi: Sử dụng `K extends keyof T` để đảm bảo key tồn tại trên đối tượng.

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = { id: 1, name: "Alice" };
const userName = getProperty(user, "name"); // string
// const invalid = getProperty(user, "age"); // Error: Argument of type '"age"' is not assignable...
```
