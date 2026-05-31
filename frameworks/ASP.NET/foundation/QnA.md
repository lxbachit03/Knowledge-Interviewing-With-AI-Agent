# ASP.NET Core Foundation Q&A

[?][record trong C# ASP.NET có nói "so sánh theo giá trị" điều này có nghĩa là sao?]
[?][viết thủ công hàm so sánh Equals cho một class là sao?]
[?][nói rõ hơn về GetHashCode trong C# ASP.NET]

### Level 1: Remembering

#### Q_LEVEL1_481: What is ASP.NET Core?

**Question:**
en: What is ASP.NET Core?
vi: ASP.NET Core là gì?

**Answer:**
en: ASP.NET Core is a cross-platform, high-performance, open-source framework for building modern, cloud-based, Internet-connected applications.
vi: ASP.NET Core là một framework mã nguồn mở, hiệu năng cao và đa nền tảng (cross-platform) dùng để xây dựng các ứng dụng hiện đại kết nối Internet dựa trên đám mây.

#### Q_LEVEL1_152: What is Kestrel?

**Question:**
en: What is Kestrel in ASP.NET Core?
vi: Kestrel trong ASP.NET Core là gì?

**Answer:**
en: Kestrel is a cross-platform, incredibly lightweight web server specifically built for ASP.NET Core out-of-the-box.
vi: Kestrel là một web server đa nền tảng, siêu nhẹ và siêu nhanh được tích hợp sẵn (out-of-the-box) chạy mặc định cho ASP.NET Core.

#### Q_LEVEL1_349: What is the Program.cs file?

**Question:**
en: What is the purpose of the `Program.cs` file?
vi: Mục đích của file `Program.cs` là gì?

**Answer:**
en: It serves as the main entry point to configure the dependency injection container, the application request pipeline, and host execution.
vi: Nó là điểm bắt đầu (entry point) khởi động app, dùng để cấu hình Dependency Injection, xây dựng pipeline request và chạy Host.

#### Q_LEVEL1_552: What is Dependency Injection?

**Question:**
en: What is Dependency Injection (DI) in ASP.NET Core?
vi: Dependency Injection (DI) trong ASP.NET Core là gì?

**Answer:**
en: DI is a core software design pattern built natively into ASP.NET Core aiming to achieve Inversion of Control (IoC) between classes and their dependencies.
vi: DI là một design pattern được tích hợp sẵn bắt buộc trong cốt lõi ASP.NET Core, nhằm đạt được Inversion of Control phân ly sự phụ thuộc.

#### Q_LEVEL1_810: What are the DI Lifetimes?

**Question:**
en: What are the three Service Lifetimes in ASP.NET Core DI?
vi: Ba vòng đời dịch vụ (Lifetimes) trong ASP.NET Core DI là gì?

**Answer:**
en: They are Transient (created each time requested), Scoped (created once per client request/connection), and Singleton (created once per application lifetime).
vi: Chúng gồm Transient (tạo mới mỗi lần gọi), Scoped (tạo mới một lần cho mỗi chu kỳ HTTP Request), và Singleton (tạo đúng một lần tồn tại song song tuổi thọ app).

#### Q_LEVEL1_811: What is Captive Dependency?

**Question:**
en: What is a Captive Dependency in ASP.NET Core DI?
vi: Captive Dependency trong ASP.NET Core DI là gì?

**Answer:**
en: ...
vi: Captive Dependency xảy ra khi một service có vòng đời dài hơn, thường là Singleton, giữ tham chiếu đến một dependency có vòng đời ngắn hơn như Scoped, làm object ngắn hạn bị "giam giữ" sống lâu hơn không cần thiết. Ví dụ: Singleton service giữ tham chiếu đến Scoped service, thì lúc này Scoped service sẽ bất đắc dĩ sống lâu bằng Singleton.

#### Q_LEVEL1_114: What is a Controller?

**Question:**
en: What is an MVC Controller?
vi: MVC Controller là gì?

**Answer:**
en: A Controller is a class that handles incoming HTTP requests, performs business operations, and returns responses back to the client.
vi: Controller là một class chịu trách nhiệm tiếp nhận HTTP request, có thể xử lý logic và trả về response cho client.

#### Q_LEVEL1_496: What is a Minimal API?

**Question:**
en: What is a Minimal API?
vi: Minimal API là gì?

**Answer:**
en: Introduced in .NET 6, Minimal APIs are simplified architectures to create HTTP APIs with low ceremony and no Controller classes needed.
vi: Ra mắt từ .NET 6, Minimal API là cách thiết kế tinh gọn để tạo các API mà không cần rườm rà viết cấu trúc Controller.

#### Q_LEVEL1_118: What does sealed mean? (C# 1.0/.NET Framework 1.0)

**Question:**
en: What does the `sealed` keyword mean in C# and ASP.NET Core code?
vi: Từ khóa `sealed` có nghĩa là gì trong code C# và ASP.NET Core?

**Answer:**
en: `sealed` means a class cannot be inherited by another class. In ASP.NET Core code, it is often used when a type is meant to have a fixed behavior, avoid subclassing, or communicate that inheritance is not part of its design.
vi: `sealed` có nghĩa là một class không thể bị kế thừa bởi class khác. Trong code ASP.NET Core, nó thường được dùng khi một kiểu dữ liệu cần có hành vi cố định, tránh bị subclass hoặc muốn thể hiện rõ rằng inheritance không nằm trong thiết kế của nó.

#### Q_LEVEL1_504: What is a record? (C# 9.0/.NET 5)

**Question:**
en: What is a `record` in C# and why is it common in ASP.NET Core?
vi: `record` trong C# là gì và vì sao nó hay được dùng trong ASP.NET Core?

**Answer:**
en: A `record` is a C# reference type designed for immutable-style data models and value-based equality. In ASP.NET Core, records are commonly used for request and response DTOs because they are concise, readable, and fit data-carrying objects well.
vi: `record` là một kiểu tham chiếu trong C# được thiết kế cho các model dữ liệu theo phong cách bất biến và so sánh theo giá trị. Trong ASP.NET Core, record thường được dùng cho request DTO và response DTO vì cú pháp gọn, dễ đọc và rất phù hợp với các object chủ yếu dùng để mang dữ liệu.

Lưu ý thú vị: Bạn có thể kết hợp cả hai để tạo ra một sealed record. Điều này cực kỳ phổ biến trong C# hiện đại để đảm bảo tính bất biến tối đa và hiệu suất tối ưu cho các Data Transfer Objects (DTOs).

**Details:** ./frameworks/ASP.NET/foundation/Q_LEVEL1_504.md

#### Q_LEVEL1_621: What is Model Binding?

**Question:**
en: What is Model Binding?
vi: Model Binding là gì?

**Answer:**
en: Model Binding automatically maps data from HTTP requests (query strings, forms, JSON body) to action method parameters.
vi: Thuật toán tự động đọc dữ liệu từ HTTP (query, form, JSON body...) rồi nhét vào biến tham số đầu vào của các Action.

#### Q_LEVEL1_832: What is a Middleware, Filter, Pipeline?

**Question:**
en: What is a Middleware, Filter, Pipeline?
vi: Middleware, Filter, Pipeline là gì?

**Answer:**
en: ...
vi: Action method là endpoint (nơi xử lý logic chính) trong controller, còn middleware và filter là các thành phần xử lý request và response. Cụ thể hơn như sau:

- Middlewares là các thành phần xử lý request và response trên toàn cục.
- Filters là các thành phần xử lý request và response trong phạm vi của controller. Cho phép code chạy trước hoặc sau các giai đoạn cụ thể trong chu kỳ thực thi của một Action Method.
- Pipeline là toàn bộ quy trình luân chuyển của Request thông qua Middleware và Filter.

**DETAILS:** frameworks/ASP.NET/foundation/Q_LEVEL1_832.md

#### Q_LEVEL1_319: What is CORS?

**Question:**
en: What is CORS?
vi: CORS là gì?

**Answer:**
en: Cross-Origin Resource Sharing (CORS) is a W3C standard that allows a server to relax the same-origin policy, dictating which external domains can call the API.

vi: CORS là một cơ chế bảo mật của trình duyệt giúp kiểm soát các truy cập tài nguyên trên một trang web được truy cập từ một tên miền (domain) khác. Nó nới lỏng chính sách Same-Origin Policy (SOP) một cách an toàn, cho phép frontend (ví dụ: a.com) gọi API từ backend (ví dụ: api.b.com) khi được máy chủ cho phép.

Các đặc điểm chính của CORS:

- Cơ chế hoạt động: Trình duyệt gửi yêu cầu (thường là OPTIONS - preflight request) đến máy chủ để hỏi xem tên miền đang yêu cầu có được quyền truy cập tài nguyên hay không.
- Tiêu đề (Header) quan trọng: Máy chủ xác nhận quyền bằng cách trả về header Access-Control-Allow-Origin, kèm theo domain được phép hoặc dấu \* cho phép tất cả.
- Lỗi CORS (Blocked by CORS policy): Xảy ra khi máy chủ backend chưa cấu hình cho phép tên miền frontend gọi đến, khiến trình duyệt chặn phản hồi để bảo mật.
- Vai trò: Giúp tích hợp các dịch vụ bên thứ ba (như font, video, API) mà không vi phạm an ninh trình duyệt.

Cách khắc phục lỗi CORS:
Giải pháp triệt để nhất là cấu hình ở phía server backend, thêm các HTTP header cần thiết (Access-Control-Allow-Origin, Access-Control-Allow-Methods) để cho phép nguồn gốc frontend.

**DETAILS:** frameworks/ASP.NET/foundation/Q_LEVEL1_319.md

**Resources:** [CORS là gì?][https://viblo.asia/p/cors-la-gi-Qbq5Q0j3lD8]

#### Q_LEVEL1_744: What is appsettings.json?

**Question:**
en: What is `appsettings.json`?
vi: `appsettings.json` dùng để làm gì?

**Answer:**
en: It is the standard JSON configuration file used to store application-level settings like database connection strings and custom parameters.
vi: Đây là tệp cấu hình trung tâm định dạng JSON lưu các biến kỹ thuật như chuỗi kết nối database (connection strings) hay các settings hệ thống.

#### Q_LEVEL1_381: What is an Action?

**Question:**
en: What is an Action Method?
vi: Action Method là gì?

**Answer:**
en: An Action is a public method on a Controller that responds to an HTTP request routed to it.

vi: Action method thường được gọi ngắn là **Action**. Ngoài ra mình còn có thể gọi là endpoint, cụ thể hơn là 1 phương thức public bên trong **Controller**, hàm này sẽ được thực thi khi 1 HTTP request được ánh xạ (route) **routing** tới phương thức đó.

#### Q_LEVEL1_536: What is Routing?

**Question:**
en: What is Routing?
vi: Routing là gì?

**Answer:**
en: Routing is the process of mapping incoming HTTP request URLs to the executable code (endpoints/controllers).
vi: Routing là cơ chế định tuyến phân tích URL HTTP gửi tới và ánh xạ nó đi tìm đúng hàm (endpoint/controller) để chạy.

#### Q_LEVEL1_198: What are Tag Helpers?

**Question:**
en: What are Tag Helpers?
vi: Tag Helpers là gì?

**Answer:**
en: They allow back-end code to participate in creating and rendering HTML elements within Razor views dynamically.
vi: Cung cấp tính năng để nhúng mã back-end C# vào quá trình biên dịch nhằm sinh ra các thẻ HTML động trên View HTML Razor.

#### Q_LEVEL1_604: What is Razor Pages?

**Question:**
en: What is Razor Pages?
vi: Razor Pages là gì?

**Answer:**
en: A page-focused architectural paradigm in ASP.NET Core that encapsulates both the view template and page logic model in a single folder.
vi: Razor Pages là mô hình lập trình hướng **trang (page-focused)**. **Đặc điểm đặc trưng** nhất của Razor Page là tệp tin. _Thay vì chia nhỏ vào các thư mục_ `Views`, `Controllers`, `Models` thì cấu trúc của 1 Razor Page gồm 2 thành phần luôn đi kèm với nhau là:

- Tệp .cshtml (View): Chứa mã HTML và cú pháp Razor để hiển thị giao diện.

- Tệp .cshtml.cs (PageModel): Chứa mã C# (code-behind) để xử lý logic, dữ liệu và các sự kiện (như khi người dùng nhấn nút).

Một mô hình kiến trúc tập trung vào "Trang", gom giao diện HTML (View) và code xử lý C# (PageModel) dính liền với nhau để dễ bảo trì.

Lưu ý nhỏ: Bạn hoàn toàn có thể sử dụng cả Razor Pages và MVC trong cùng một dự án ASP.NET Core. Chúng không hề "đánh nhau" mà bổ trợ cho nhau rất tốt!

**Details:** frameworks/ASP.NET/Q_LEVEL1_604.md

#### Q_LEVEL1_792: What is Entity Framework Core?

**Question:**
en: What is Entity Framework Core?
vi: Entity Framework Core là gì?

**Answer:**
en: It is the standard Microsoft lightweight, extensible, cross-platform Object-Relational Mapper (O/RM) for .NET.
vi: Đây là công cụ hệ sinh thái chuẩn của Microsoft cung cấp giải pháp lập trình CSDL bằng đối tượng (O/RM) cực nhanh và nhẹ.

#### Q_LEVEL1_417: What is ViewComponent?

**Question:**
en: What is a ViewComponent?
vi: ViewComponent là gì?

**Answer:**
en: Think of them as partial views with logic attached; they render HTML chunks based on encapsulated independent dependencies.
vi: Có thể hiểu ViewComponent như một View con (partial) được nhúng code Logic hoàn chỉnh bên trong để tự render mà không cần Controller truyền dữ liệu xuống.

#### Q_LEVEL1_265: What is Environment Variable?

**Question:**
en: What is the ASPNETCORE_ENVIRONMENT variable?
vi: Biến môi trường ASPNETCORE_ENVIRONMENT là gì?

**Answer:**
en: It tells ASP.NET Core the runtime environment (Development, Staging, Production) so code can conditionally execute setup features.
vi: Cho dự án biết nó đang chạy ở môi trường nào (Development, Production) thông qua đó C# có thể bật tắt các setting (ví dụ: Log tắt ở Prod, bật ở Dev).

#### Q_LEVEL1_734: What is a `CancellationToken`?

**Question:**
en: What does a `CancellationToken` represent in ASP.NET Core?
vi: `CancellationToken` đại diện cho điều gì trong ASP.NET Core?

**Answer:**
en: It is a cooperative signal that tells running work to stop when the request is aborted, times out, or the application is shutting down. It helps avoid wasting CPU, memory, and database connections on work nobody needs anymore.
vi: Nó là tín hiệu hủy theo kiểu cooperative, báo cho đoạn xử lý đang chạy biết là nên dừng lại khi request bị hủy, timeout hoặc app đang shutdown. **Mục tiêu** là không tiêu tốn CPU, bộ nhớ và kết nối DB cho công việc đã không còn ai cần nữa.

---

### Level 2: Understanding

#### Q_LEVEL2_754: Pipeline processing - DONE

**Question:**
en: How does the request processing middleware pipeline work?
vi: Kênh đường ống pipeline xử lý middleware hoạt động ra sao?

**Answer:**
en: HTTP Requests travel sequentially through registered middlewares. Each middleware processes the request, optionally calls `next()`, and processes the response backward as the call stack unwinds.
vi: HTTP request sẽ đi qua tuần tự các middleware. Từng tầng sẽ xử lý logic nhất định sau đó gọi lệnh `next()` để chuyển HTTP request cho tầng middleware tiếp theo.

Request HTTP đi tuần tự qua từng middleware. Từng tầng sẽ chạy lệnh, gọi `next()` nhường quyền cho tầng kế, sau đó khi trả Response lại đi ngược lại theo chuẩn Return Stack nghĩa là sau khi action method xử lý xong sẽ trả về response và response đó sẽ đi ngược ra qua những middlewares đó.

**Details:** ./frameworks/ASP.NET/foundation/Q_LEVEL2_754.md

#### Q_LEVEL2_840: AddScoped vs AddTransient vs AddSingleton - DONE

**Question:**
en: Explain the fundamental difference between `AddScoped`, `AddTransient`, and `AddSingleton`.
vi: Giải thích điểm khác nhau cốt lõi giữa `AddScoped`, `AddTransient` và `AddSingleton`.

**Answer:**
en: Transient creates a new instance every single injection. Scoped creates one instance shared strictly across a single HTTP request lifecycle. Singleton creates one persistent instance shared globally forever.
vi: Transient khởi tạo object mới bất kể ở đâu gọi (hao tài nguyên). Scoped giữ duy nhất một bản sao trong một chu kỳ sống của HTTP Request. Singleton tạo ra duy nhất một bản độc tôn trường tồn mãi cho đến khi tắt Server.

#### Q_LEVEL2_841: Why is Captive Dependency dangerous? - DONE

**Question:**
en: Why is Captive Dependency considered a dangerous lifetime mismatch?
vi: Vì sao Captive Dependency được xem là lỗi lệch vòng đời nguy hiểm?

**Answer:**
en: ...
vi: Vì nó phá vỡ ranh giới vòng đời đã thiết kế. Một Singleton có thể vô tình giữ lại state riêng của từng request, dùng sai các object Scoped đã hết hạn, nghĩa là dùng lại dữ liệu của request cũ.

**DETAILS ->** ./frameworks/ASP.NET/foundation/Q_LEVEL2_841_DETAILS.md

#### Q_LEVEL2_183: Model Validation

**Question:**
en: How does Model Validation work?
vi: Cơ chế Xác thực dữ liệu Model (Validation) hoạt động ra sao?

**Answer:**
en: It validates incoming data automatically prior to executing the action logic using Data Annotations (like `[Required]`). If failed, `ModelState.IsValid` flips false.
vi: Framework sử dụng tính năng Data Annotations (vd: `[Required]`, `[EmailAddress]`) gán trên class. Khi dữ liệu vào, nó quét và nếu lỗi thì đánh cờ `ModelState.IsValid = false`.

#### Q_LEVEL2_526: Controller vs Minimal API

**Question:**
en: Compare Minimal APIs with MVC Controllers.
vi: So sánh Minimal API và MVC Controller.

**Answer:**
en: Minimal APIs optimize for raw performance and extreme code brevity by defining routes dynamically as lambdas, omitting the heavy inheritance and filters native to MVC Controller architectures.
vi: Minimal API vứt bỏ tối đa các class thừa, viết route bằng lambda, cực nhanh nhẹ và dễ đọc. MVC Controller hỗ trợ cấu trúc phân tầng, kế thừa và Filter chuyên sâu, phù hợp cho các dự án phức tạp.

#### Q_LEVEL2_577: ASP.NET Core vs ASP.NET MVC vs ASP.NET Framework - DONE

**Question:**
en: What is different between ASP.NET Core and ASP.NET MVC?
vi: ASP.NET Core và ASP.NET MVC khác nhau ở điểm nào?

**Answer:**
en: ASP.NET Core is the modern, cross-platform, open-source framework that runs on Windows, Linux, and macOS, with built-in dependency injection, unified hosting, and better performance. Classic ASP.NET MVC belongs to the older .NET Framework stack, mainly targets Windows, and depends on the older `System.Web` pipeline. In practice, ASP.NET Core is the current platform for new applications, while classic ASP.NET MVC is the legacy framework many older applications still use.
vi:
**ASP.NET Framework (cũ nhất):** là _phiên bản cũ nhất_ trong lịch sử tiến hóa của hệ sinh thái .NET. Nó được thiết kế _chặt chẽ_ với _Windows_ và _máy chủ IIS_ (Internet Information Services). Đặc điểm:
Runtime: Chạy trên CLR (Common Language Runtime).
Kiến trúc: Dựa trên thư viện hệ thống System.Web.dll, vốn chứa nhiều thành phần nặng nề và bị phụ thuộc vào Windows APIs.
Deployment: Chỉ chạy trên Windows Server.
App Model: Bao gồm Web Forms (kéo thả UI) và sau này tích hợp thêm MVC.

**ASP.NET Core:** là _phiên bản hiện đại nhất_ từ _ASP.NET 5_ trở lên. _Lưu ý:_ Nó không phải là bản cập nhật của ASP.NET Framework mà là _framework hoàn toàn mới_. Đặc điểm:
_Runtime_: Chạy trên .NET Core (hoặc sau này là .NET 5/6/7/8+), sử dụng CoreCLR.
_Đa nền tảng_: Chạy trên Windows, Linux và macOS.
_Hiệu năng_: Loại bỏ System.Web.dll, thay bằng hệ thống các gói NuGet nhỏ gọn. Nó sử dụng web server nội bộ tên là Kestrel, được tối ưu hóa cho tốc độ cực cao.
_Dependency Injection (DI)_: Được tích hợp sẵn vào core của framework (trong khi bản cũ phải dùng thư viện bên thứ 3).

**ASP.NET MVC:** Là một _Pattern_ không phải một nền tàng riêng biệt như 2 frameworks trên nhưng có thể triển khai Pattern này trên cả 2 frameworks trên. Đặc điểm:
_Cốt lõi_: Tách biệt ứng dụng thành 3 thành phần: Model (Dữ liệu), View (Giao diện), và Controller (Điều hướng).
_Trong ASP.NET Framework_: MVC đời đầu (từ v1 đến v5) chạy trên nền tảng ASP.NET Framework cũ.
_Trong ASP.NET Core_: MVC được viết lại hoàn toàn, nhẹ hơn và tích hợp sẵn như một middleware.

**Details:** ./frameworks/ASP.NET/foundation/Q_LEVEL2_577.md

#### Q_LEVEL2_891: UseRouting vs UseEndpoints - DONE

**Question:**
en: Explain the difference between `UseRouting` and `UseEndpoints` logic.
vi: Mạch logic của `UseRouting` khác `UseEndpoints` ở điểm nào?

**Answer:**
en: `UseRouting` parses the request URL to determine the intended endpoint execution target. `UseEndpoints` represents the end of the pipeline that actively executes the previously resolved target.
vi: `UseRouting` và `UseEndpoints` là 2 middlewares luôn đi cặp với nhau tương tác với nhau, hiểu được 2 middlewares tương tác với nhau là chìa khóa để nắm bắt vòng đời của 1 Request.
**UseRouting:** _Khi Request đi qua middleware này_, hệ thống sẽ thực hiện phân tích URL và các HTTP metadata (như header, query string, method) để xác định xem Request này phù hợp nhất với Endpoint nào.
Nhiệm vụ chính: Quét qua danh sách các Endpoint đã được đăng ký trong ứng dụng (thông qua UseEndpoints) và tìm ra mục phù hợp nhất.
_Kết quả_: Nếu tìm thấy kết quả phù hợp, nó sẽ đính kèm (attach) một đối tượng Endpoint vào HttpContext của Request hiện tại thông qua IEndpointFeature.
_Lưu ý quan trọng_: Ở giai đoạn này, Endpoint chưa được thực thi. _Nó mới chỉ được "gắn nhãn" để các Middleware tiếp theo biết Request này đang đi đâu._

**UseEndpoints:** Đây là điểm cuối của _Pipeline_. Tại đây, chúng ta sẽ định nghĩa _endpoints khả dụng_ và _thực hiện xử lý logic_.

- _Nhiệm vụ chính:_ _Đọc đối tượng `Endpoint` đã được `UseRouting` gán vào `HttpContext` và gọi delegate xử lý tương ứng_ (như gọi Action trong Controller, thực thi Razor Page, hoặc một Lambda function).
- _Đăng ký Route:_ Đây là nơi bạn cấu hình các mẫu URL (Route patterns).

```csharp
app.UseEndpoints(endpoints =>
{
    // Đăng ký các Endpoint vào bảng định tuyến toàn cục
    endpoints.MapControllers();
    endpoints.MapGet("/", async context => {
        await context.Response.WriteAsync("Hello World!");
    });
});
```

**Details:** ./frameworks/ASP.NET/foundation/Q_LEVEL2_891.md

#### Q_LEVEL2_394: Formulating Content Negotiation.

**Question:**
en: What is Content Negotiation in API formulation?
vi: Khái niệm Content Negotiation (đàm phán cấu trúc) trong API là gì?

**Answer:**
en: It's the process where the API returns different payload formats (e.g. JSON vs XML) based primarily on what the client specifically asks for using the `Accept` HTTP header.
vi: Là tính năng tự nhận dạng header `Accept` của bộ gọi client. Nếu client muốn nhận `application/xml` API tự nhả XML, nếu đòi JSON API tự nhả JSON thay vi hard-code.

#### Q_LEVEL2_114: Synchronous vs Asynchronous Actions - DONE

**Question:**
en: Contrast synchronous and asynchronous Controller action methods.
vi: So sánh hành vi gọi Action Synchronous (đồng bộ) so với Asynchronous (bất đồng bộ) trên Controller.

**Answer:**
en: Sync actions block the runtime execution thread completely while waiting for lengthy I/O operations (like database hits). Async actions (`async/await`) surrender the thread to process other server requests until the I/O bottleneck completes.
vi: Sync Action giam lỏng luôn Thread máy chủ lúc truy xuất DB làm app bị tắc nghẽn cục bộ. Async (`async/await`) lập tức thả Thread đi phục vụ người khác trong lúc chờ DB, giúp thông luồng xử lý hàng ngàn request cùng lúc.

#### Q_LEVEL2_602: The User object (ClaimsPrincipal) - DONE

**Question:**
en: What is the purpose of the generic `User` object property present in the HttpContext?
vi: Phân tích mục đích của object `User` có mặt mặc định trong HTTP Context?

**Answer:**
en: It holds the `ClaimsPrincipal` describing the actively authenticated user making the HTTP request, containing parsed access claims (roles, permissions, name) decoded from the Authentication middleware schema.
vi: Nó chứa dữ liệu `ClaimsPrincipal` cấu thành định danh của User đang gọi đến. Khi token (như JWT) giải mã thành công, middleware tự bóc cờ (Claims - như roles, tên gốc) ra chèn vào object này để bạn xét duyệt phân quyền.

#### Q_LEVEL2_753: Sessions in Core

**Question:**
en: How is server-side session state handled safely?
vi: Cách cơ chế Session state (phiên bộ nhớ) được thi hành như thế nào?

**Answer:**
en: Sessions are implemented via added middleware and backed by an `IDistributedCache` storing values server-side while relaying an encrypted session-ID via client tracking cookie.
vi: C# quản lý Session thông qua middleware tiêm `IDistributedCache`. Bản chất nó lưu dữ liệu nằm bên Server, rồi gán một Cookie mã hóa (chỉ ghi chuỗi ID) tống sang trình duyệt Client giữ để tham chiếu.

#### Q_LEVEL2_482: Strongly Typed Configurations - DONE

**Question:**
en: Describe how the Options Pattern (`IOptions<T>`) binds configuration parameters.
vi: Mô tả Pattern Options (`IOptions<T>`) gói cấu hình hệ thống ra sao?

**Answer:**
en: It binds loosely typed structural fields from `appsettings.json` into strongly typed C# instantiated classes utilizing the framework DI resolving mechanism implicitly.
vi: Nó kết nối cấu trúc rườm rà của `appsettings.json` rồi ráp giá trị bọc thành một cái Class C# định dạng chặt chẽ. Sau đó sử dụng DI để inject bộ Setting này cho bất kỳ đâu cần.

#### Q_LEVEL2_219: Developer Exception Page

**Question:**
en: How does the framework intercept unhandled application exceptions fundamentally?
vi: Làm thế nào Framework Core giải trình chặn bắt các Exception crash hệ thống ngầm?

**Answer:**
en: Utilizing `UseExceptionHandler` or `UseDeveloperExceptionPage`, it isolates the pipeline stack, traps any bubbling fatal exceptions natively halting crashes, and renders a localized friendly status stack trace.
vi: Framework sử dụng ngầm các middleware bắt Exception (như `UseDeveloperExceptionPage`), trùm lên toàn bộ pipeline chặn các lỗi crash xuyên thấu, đồng thời tự xử lý in ra cái bảng Stack Trace đầy màu để Developer quan sát lỗi.

#### Q_LEVEL2_901: Authentication vs Authorization

**Question:**
en: Contrast Identity Authentication from Access Authorization structurally.
vi: Tách bạch rõ vai trò của Authentication (Xác thực) và Authorization (Phân quyền).

**Answer:**
en: Authentication proves WHO the exact calling request user fundamentally is (e.g. verifying JWT tokens). Authorization proves WHAT that specifically authenticated entity is legitimately permitted to do (e.g. evaluating Roles).
vi: Authentication là cửa ải kiểm chứng gốc BẠN LÀ AI (vd soi mã token người dùng). Dù đã vào nhà, Authorization là cửa kiểm chứng BẠN CÓ QUYỀN ĐƯỢC LÀM NHỮNG GÌ (vd không phải admin cấm gọi hành động xóa gốc).

#### Q_LEVEL2_458: ApplicationBuilder vs EndpointRouteBuilder

**Question:**
en: Explain fundamentally the `IApplicationBuilder` opposed to `IEndpointRouteBuilder`.
vi: Phân tích sự kiện `IApplicationBuilder` đối nghịch với `IEndpointRouteBuilder`.

**Answer:**
en: The `IApplicationBuilder` is utilized globally structuring the comprehensive middleware stack. `IEndpointRouteBuilder` defines exact route configurations exclusively targeting precise endpoints processing maps.
vi: Thể thức `IApplicationBuilder` đóng vai trò vĩ mô giúp cấu trúc lắp ghép đường ống Middleware. Ở đầu kia, `IEndpointRouteBuilder` nằm trong vi mô định nghĩa các trạm dừng thiết lập địa chỉ maps cho API.

#### Q_LEVEL2_663: IActionResult

**Question:**
en: What is the benefit of returning `IActionResult` over simple strings or objects?
vi: Cái lợi của việc Controller Return `IActionResult` thay cho string/object chay là gì?

**Answer:**
en: `IActionResult` supports extensive RESTful HTTP representations natively standardizing explicit response structures like `NotFound()`, `BadRequest()`, or status OK with payloads uniformly.
vi: Khai báo `IActionResult` cho phép hàm trả ra những chỉ định HTTP chuẩn REST cực kỳ chuyên nghiệp như trạng thái mã hóa 404 Not Found, 400 Bad Request một cách rõ ràng rành mạch.

#### Q_LEVEL2_137: Startup vs Program

**Question:**
en: Discuss the architectural consolidation of `Startup.cs` moving to `Program.cs`.
vi: Thảo luận việc hợp nhất hoàn toàn `Startup.cs` biến mất dồn vào file `Program.cs` duy nhất từ .NET 6.

**Answer:**
en: Using top-level statements, modern .NET coalesced configuring the services pipeline into the `Program.cs` implicitly establishing an ultra-lightweight entry point mitigating ceremonial class bloat.
vi: Dùng tính năng Top-level statements, .NET đời mới ép chết `Startup.cs` cồng kềnh, quy gọn mọi thiết lập service và pipeline vào điểm vào duy nhất `Program.cs` làm app sạch sẽ tối giản 90% dòng class dư thừa cũ.

#### Q_LEVEL2_846: Middleware ordering and exception handling

**Question:**
en: Why does middleware ordering matter so much, especially for exception handling, authentication, authorization, and CORS?
vi: Vì sao thứ tự middleware lại quan trọng, đặc biệt với exception handling, authentication, authorization và CORS?

**Answer:**
en: Middleware runs in registration order, so putting one in the wrong place changes behavior. For example, exception handling should be early so it can catch downstream failures, authentication must run before authorization, and CORS must run before endpoints that need its headers. A large number of “it works locally but fails in production” issues come from incorrect middleware order.
vi: Middleware chạy theo đúng thứ tự đăng ký, nên đặt sai vị trí là hành vi ứng dụng đổi ngay. Ví dụ middleware bắt lỗi phải đặt sớm để chụp được lỗi phía sau, authentication phải chạy trước authorization, còn CORS phải đứng trước endpoint nếu muốn response có header phù hợp. Rất nhiều lỗi kiểu “máy em chạy được” thật ra đến từ việc sắp pipeline sai thứ tự.

#### Q_LEVEL2_333:

**Question:**

en: Type Casting
vi: Ép kiểu (Type Casting) trong C#

**Answer:**

en:
vi:

---

### Level 3: Applying

#### Q_LEVEL3_854: Register and use custom Middleware

**Question:**
en: Demonstrate defining and executing a customized HTTP middleware in the runtime pipeline.
vi: Triển khai một file Middleware tự viết để can thiệp luồng pipeline.

**Answer:**
en: Create a class capturing the `RequestDelegate`, implement an `InvokeAsync` interceptor to log or manipulate execution, and `Use` it explicitly inside `Program.cs`.
vi: Viết lớp nhận `RequestDelegate`, trỏ hàm `InvokeAsync` can thiệp logic (ví dụ in thông tin Console) trước khi gọi hàm kế `await _next()`. Cuối cùng gọi Extension bằng `app.Use...`

```csharp
public class CustomAuditMiddleware
{
    private readonly RequestDelegate _next;
    public CustomAuditMiddleware(RequestDelegate next) => _next = next;

    public async Task InvokeAsync(HttpContext context)
    {
        Console.WriteLine("Before Request Processing => auditing");
        await _next(context); // Advance pipeline
        Console.WriteLine("After Request Unwinding");
    }
}

// In Program.cs:
// app.UseMiddleware<CustomAuditMiddleware>();
```

#### Q_LEVEL3_207: Create a Minimal API Endpoint

**Question:**
en: Show the syntax creating a typical RESTful Minimal API endpoint.
vi: Viết code cho ra API RESTful siêu tốc sử dụng kỹ thuật Minimal API.

**Answer:**
en: You simply utilize `.MapGet()` extensions on the dynamic runtime `WebApplication` object passing lamda expression actions without demanding distinct controller structuring templates.
vi: Bạn chỉ việc lôi cổ `app` gọi trực tiếp `.MapGet()` ép biểu thức lamda xử lí vào đó là xong, không dùng class Controller nào cả.

```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/api/greetings/{name}", (string name) =>
{
    return Results.Ok(new { message = $"Hello, {name}!" });
});

app.Run();
```

#### Q_LEVEL3_942: Inject DbContext to Controller

**Question:**
en: Demonstrate how DI provides an EF `DbContext` into a Controller constructor seamlessly.
vi: Minh họa cách kỹ thuật Tiêm (DI) nhét cái CSDL C# (`DbContext`) vào cấu trúc thiết lập hàm khởi tạo của Controller C#.

**Answer:**
en: Register the exact context defining the driver connection string within setup, then declare the object type statically as a read-only parameter constructor.
vi: Chỉ lệnh cài cắm ở Program, sau đó ghi hẳn đối tượng kết nối EF vào hàm Constructor, Dependency sẽ tự động mò nhét tham chiếu DbContext vào.

```csharp
[ApiController]
[Route("[controller]")]
public class InventoryController : ControllerBase
{
    private readonly ApplicationDbContext _db;

    // Auto-injected context by default Core mechanics
    public InventoryController(ApplicationDbContext context)
    {
        _db = context;
    }

    [HttpGet]
    public IActionResult FetchItems() => Ok(_db.Items.ToList());
}
```

#### Q_LEVEL3_943: Fix a Captive Dependency

**Question:**
en: Show how to fix a Captive Dependency when a Singleton needs to work with a Scoped service.
vi: Minh họa cách sửa Captive Dependency khi một Singleton cần làm việc với một Scoped service.

**Answer:**
en: The fix is usually to align lifetimes correctly. If the service truly depends on request-scoped data, make that service Scoped too. If a Singleton only occasionally needs scoped work, create a scope explicitly using `IServiceScopeFactory`.
vi: Cách sửa chuẩn là căn chỉnh lại vòng đời cho đúng. Nếu service thật sự phụ thuộc dữ liệu theo request thì hãy đổi service đó thành Scoped. Nếu Singleton chỉ thỉnh thoảng mới cần xử lý với Scoped service thì phải tự tạo scope mới bằng `IServiceScopeFactory`.

```csharp
public interface IRequestAuditService
{
    Task WriteAsync(string message);
}

public class RequestAuditService : IRequestAuditService
{
    private readonly ApplicationDbContext _db;

    public RequestAuditService(ApplicationDbContext db)
    {
        _db = db;
    }

    public async Task WriteAsync(string message)
    {
        _db.AuditLogs.Add(new AuditLog { Message = message });
        await _db.SaveChangesAsync();
    }
}

public class BackgroundReporter
{
    private readonly IServiceScopeFactory _scopeFactory;

    public BackgroundReporter(IServiceScopeFactory scopeFactory)
    {
        _scopeFactory = scopeFactory;
    }

    public async Task ReportAsync(string message)
    {
        using var scope = _scopeFactory.CreateScope();
        var auditService = scope.ServiceProvider.GetRequiredService<IRequestAuditService>();
        await auditService.WriteAsync(message);
    }
}

// Program.cs
builder.Services.AddDbContext<ApplicationDbContext>(options => { });
builder.Services.AddScoped<IRequestAuditService, RequestAuditService>();
builder.Services.AddSingleton<BackgroundReporter>();
```

#### Q_LEVEL3_613: Writing a custom Action Filter

**Question:**
en: Demonstrate authoring a personalized Action Filter logic processing execution steps explicitly.
vi: Triển khai một Action Filter tùy chỉnh bọc trên hành vi truy cập.

**Answer:**
en: Implementing native `IActionFilter` interfaces exposes `OnActionExecuting` overriding mechanisms halting requests before controller instantiation logic.
vi: Gắn cờ kế thừa interface lõi là `IActionFilter`. Triển khai đè hàm chặn cổng `OnActionExecuting` giúp cấm đoạt logic trước khi gọi ruột Controller.

```csharp
public class RejectEmptyHeaderFilter : IActionFilter
{
    public void OnActionExecuting(ActionExecutingContext context)
    {
        if (!context.HttpContext.Request.Headers.ContainsKey("X-Required-Agent"))
        {
            // Halts pipeline completely assigning block response
            context.Result = new BadRequestObjectResult("Missing Agent Header!");
        }
    }
    public void OnActionExecuted(ActionExecutedContext context) { }
}

// Use via attribute: [ServiceFilter(typeof(RejectEmptyHeaderFilter))]
```

#### Q_LEVEL3_485: Configuring CORS Protocol

**Question:**
en: Demonstrate declaring explicitly allowed external origins configuring strict CORS definitions smoothly.
vi: Viết mẫu cấu hình định dạng giới nghiêm trình dịch CORS cho phép những domain được cấp quyền gọi App.

**Answer:**
en: Declare CORS policy templates specifying dynamic hosts securely inside services setup natively prior to registering URL routing bindings.
vi: Khai rành mạch hệ quy tắc Policy ấn định mảng Domain tuyệt đối ngay trong lòng Services setup trước khi cài routing.

```csharp
// Program.cs setup constraints
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowPortalPolicy",
        policy => policy.WithOrigins("https://my-portal.com")
                        .AllowAnyHeader()
                        .AllowAnyMethod());
});

var app = builder.Build();

// Interject to pipeline
app.UseCors("AllowPortalPolicy");
```

#### Q_LEVEL3_764: Fix middleware ordering

**Question:**
en: Show a correct middleware ordering example for exception handling, routing, authentication, authorization, and endpoints.
vi: Hãy minh họa một thứ tự middleware đúng cho exception handling, routing, authentication, authorization và endpoints.

**Answer:**
en: Put global exception handling early, then routing, then authentication, then authorization, and finally map endpoints. This order ensures errors are caught, the user identity is established before policy checks, and endpoints execute after the request has been fully prepared.
vi: Cách sắp xếp an toàn là đặt middleware bắt lỗi toàn cục lên sớm, sau đó đến routing, rồi authentication, tiếp theo là authorization và cuối cùng mới map endpoint. Thứ tự này giúp lỗi phía sau vẫn bị chặn, danh tính user được dựng xong trước khi kiểm tra quyền, và endpoint chỉ chạy khi pipeline đã chuẩn bị đầy đủ.

```csharp
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddAuthentication("Bearer")
    .AddJwtBearer();
builder.Services.AddAuthorization();

var app = builder.Build();

// Catch exceptions from downstream middleware and endpoints.
app.UseExceptionHandler("/error");

app.UseRouting();

// Build HttpContext.User before authorization checks.
app.UseAuthentication();
app.UseAuthorization();

app.MapControllers();

app.Run();
```

#### Q_LEVEL3_781: Use `IHttpClientFactory` with cancellation

**Question:**
en: Demonstrate the recommended way to call an external API using `IHttpClientFactory` and a `CancellationToken`.
vi: Hãy minh họa cách gọi API ngoài bằng `IHttpClientFactory` và `CancellationToken` theo hướng được khuyến nghị.

**Answer:**
en: Inject `IHttpClientFactory`, create a client from it, and pass the incoming `CancellationToken` down to `GetAsync` or `SendAsync`. That avoids the common `new HttpClient()` anti-pattern and lets the outbound request stop when the original HTTP request is cancelled.
vi: Cách làm chuẩn là inject `IHttpClientFactory`, tạo client từ factory và truyền `CancellationToken` của request xuống `GetAsync` hoặc `SendAsync`. Như vậy bạn tránh được anti-pattern `new HttpClient()` liên tục, đồng thời request đi ra ngoài cũng dừng theo khi request gốc bị hủy.

```csharp
public class WeatherGateway
{
    private readonly IHttpClientFactory _httpClientFactory;

    public WeatherGateway(IHttpClientFactory httpClientFactory)
    {
        _httpClientFactory = httpClientFactory;
    }

    public async Task<string> GetForecastAsync(CancellationToken cancellationToken)
    {
        var client = _httpClientFactory.CreateClient("weather");

        // The outbound call is cancelled if the request is aborted.
        using var response = await client.GetAsync("/forecast", cancellationToken);
        response.EnsureSuccessStatusCode();

        return await response.Content.ReadAsStringAsync(cancellationToken);
    }
}
```

#### Q_LEVEL3_805: Make a singleton service thread-safe

**Question:**
en: Show how to fix a thread-safety mistake in a Singleton service that stores mutable shared data.
vi: Hãy minh họa cách sửa một lỗi thread-safety trong Singleton khi service này lưu mutable shared data.

**Answer:**
en: Avoid storing shared data in normal collections like `Dictionary<TKey, TValue>` without synchronization. Use thread-safe primitives such as `ConcurrentDictionary`, or redesign the service so it stays stateless. The interview point is not just “make it compile”, but “make shared state safe under concurrent requests”.
vi: Sai lầm thường gặp là để `Singleton` giữ shared state trong các collection bình thường như `Dictionary<TKey, TValue>` mà không có đồng bộ hóa. Cách sửa cơ bản là dùng primitive thread-safe như `ConcurrentDictionary`, hoặc tốt hơn là thiết kế service theo hướng stateless. Điểm ăn tiền trong phỏng vấn không phải chỉ là “code chạy được”, mà là “shared state có an toàn dưới tải đồng thời hay không”.

```csharp
public class RequestCounter
{
    // Safe for concurrent access across many requests.
    private readonly ConcurrentDictionary<string, int> _counts = new();

    public int Increment(string route)
    {
        return _counts.AddOrUpdate(
            route,
            addValueFactory: _ => 1,
            updateValueFactory: (_, current) => current + 1);
    }
}

// Program.cs
builder.Services.AddSingleton<RequestCounter>();
```
