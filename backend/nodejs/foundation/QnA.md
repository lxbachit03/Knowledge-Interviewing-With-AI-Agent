# NodeJS Foundation Q&A

### Level 1: Remembering

#### Q_LEVEL1_104: What is NodeJS?

**Question:**
en: What is NodeJS?
vi: NodeJS là gì?

**Answer:**
en: NodeJS is an open-source, cross-platform JavaScript runtime that runs JavaScript outside the browser. It is commonly used to build servers, APIs, command-line tools, and real-time applications.
vi: NodeJS là một **JavaScript runtime** mã nguồn mở, đa nền tảng, cho phép chạy JavaScript bên ngoài trình duyệt. Nó thường được dùng để xây dựng server, API, công cụ dòng lệnh và ứng dụng thời gian thực.

#### Q_LEVEL1_218: What JavaScript engine does NodeJS use?

**Question:**
en: What JavaScript engine does NodeJS use?
vi: NodeJS sử dụng JavaScript engine nào?

**Answer:**
en: NodeJS uses the V8 JavaScript engine, originally developed for Google Chrome. V8 compiles JavaScript into machine code for fast execution.
vi: NodeJS sử dụng **V8 JavaScript engine**, engine ban đầu được phát triển cho Google Chrome. **V8** biên dịch JavaScript thành mã máy để thực thi nhanh hơn.

#### Q_LEVEL1_337: What is the Event Loop?

**Question:**
en: What is the Event Loop in NodeJS?
vi: **Event Loop** trong NodeJS là gì?

**Answer:**
en: The Event Loop is the mechanism that lets NodeJS handle asynchronous operations without blocking the main JavaScript thread. It schedules callbacks when I/O, timers, or other async work completes.
vi: **Event Loop** là cơ chế giúp NodeJS xử lý các tác vụ bất đồng bộ mà không chặn luồng JavaScript chính. Khi I/O, timer hoặc tác vụ async hoàn tất, **Event Loop** sẽ điều phối callback tương ứng.

#### Q_LEVEL1_429: What is non-blocking I/O?

**Question:**
en: What is non-blocking I/O in NodeJS?
vi: **Non-blocking I/O** trong NodeJS là gì?

**Answer:**
en: Non-blocking I/O means NodeJS starts an input/output operation and continues running other code instead of waiting for that operation to finish.
vi: **Non-blocking I/O** nghĩa là NodeJS khởi chạy thao tác nhập/xuất rồi tiếp tục xử lý công việc khác thay vì đứng chờ thao tác đó hoàn tất.

#### Q_LEVEL1_512: What is npm?

**Question:**
en: What is npm?
vi: **npm** là gì?

**Answer:**
en: npm is the default package manager for NodeJS. It is used to install dependencies, run scripts, publish packages, and manage project metadata.
vi: **npm** là package manager mặc định của NodeJS. Nó dùng để cài dependency, chạy script, publish package và quản lý metadata của dự án.

#### Q_LEVEL1_638: What is package.json?

**Question:**
en: What is the purpose of `package.json`?
vi: Mục đích của file `package.json` là gì?

**Answer:**
en: `package.json` stores project metadata such as name, version, scripts, dependencies, dev dependencies, and module type.
vi: `package.json` lưu metadata của dự án như tên, phiên bản, script, dependency, dev dependency và kiểu module.

#### Q_LEVEL1_741: What is package-lock.json?

**Question:**
en: What is `package-lock.json` used for?
vi: `package-lock.json` dùng để làm gì?

**Answer:**
en: `package-lock.json` records the exact dependency tree installed by npm. It helps make installs reproducible across machines and environments.
vi: `package-lock.json` ghi lại chính xác cây dependency mà **npm** đã cài. File này giúp quá trình cài đặt nhất quán giữa các máy và môi trường khác nhau.

#### Q_LEVEL1_856: What is CommonJS?

**Question:**
en: What is CommonJS in NodeJS?
vi: **CommonJS** trong NodeJS là gì?

**Answer:**
en: CommonJS is the older NodeJS module system that uses `require()` to import modules and `module.exports` or `exports` to export values.
vi: **CommonJS** là hệ thống module cũ của NodeJS, dùng `require()` để import module và `module.exports` hoặc `exports` để export giá trị.

#### Q_LEVEL1_963: What are ES Modules?

**Question:**
en: What are ES Modules in NodeJS?
vi: **ES Modules** trong NodeJS là gì?

**Answer:**
en: ES Modules are the standard JavaScript module format using `import` and `export`. NodeJS supports them through `.mjs` files or `"type": "module"` in `package.json`.
vi: **ES Modules** là chuẩn module của JavaScript, dùng `import` và `export`. NodeJS hỗ trợ qua file `.mjs` hoặc cấu hình `"type": "module"` trong `package.json`.

#### Q_LEVEL1_127: What is a callback?

**Question:**
en: What is a callback in NodeJS?
vi: **Callback** trong NodeJS là gì?

**Answer:**
en: A callback is a function passed into another function to run later, often after an asynchronous operation finishes.
vi: **Callback** là một function được truyền vào function khác để chạy sau, thường là sau khi một tác vụ bất đồng bộ hoàn tất.

#### Q_LEVEL1_235: What is a Promise?

**Question:**
en: What is a Promise in NodeJS?
vi: **Promise** trong NodeJS là gì?

**Answer:**
en: A Promise represents the future result of an asynchronous operation. It can be pending, fulfilled, or rejected.
vi: **Promise** đại diện cho kết quả tương lai của một tác vụ bất đồng bộ. Nó có thể ở trạng thái pending, fulfilled hoặc rejected.

#### Q_LEVEL1_346: What is async await?

**Question:**
en: What are `async` and `await` used for?
vi: `async` và `await` dùng để làm gì?

**Answer:**
en: `async` and `await` provide a cleaner syntax for working with Promises, making asynchronous code read more like synchronous code.
vi: `async` và `await` cung cấp cú pháp dễ đọc hơn khi làm việc với **Promise**, giúp code bất đồng bộ nhìn gần giống code đồng bộ.

#### Q_LEVEL1_459: What is the fs module?

**Question:**
en: What is the `fs` module in NodeJS?
vi: Module `fs` trong NodeJS là gì?

**Answer:**
en: The `fs` module is a built-in module for interacting with the file system, such as reading, writing, deleting, and watching files.
vi: Module `fs` là module tích hợp sẵn để làm việc với file system, ví dụ đọc, ghi, xóa và theo dõi thay đổi của file.

#### Q_LEVEL1_566: What is the http module?

**Question:**
en: What is the `http` module used for?
vi: Module `http` dùng để làm gì?

**Answer:**
en: The `http` module provides APIs for creating HTTP servers and clients without installing a framework.
vi: Module `http` cung cấp API để tạo HTTP server và client mà không cần cài framework bên ngoài.

#### Q_LEVEL1_621: What are Event Emitters?

**Question:**
en: What are Event Emitters in NodeJS?
vi: **Event Emitters** trong NodeJS là gì?

**Answer:**
en: Event Emitters are objects that let code publish named events and let other parts of the program listen for them. They are commonly used in NodeJS for asynchronous and event-driven patterns through the built-in `EventEmitter` class from the `events` module.
vi: **Event Emitters** là các object cho phép code phát ra các sự kiện có tên và cho phép phần khác của chương trình lắng nghe các sự kiện đó. Chúng thường được dùng trong NodeJS cho các pattern bất đồng bộ và hướng sự kiện thông qua class `EventEmitter` có sẵn trong module `events`.

**DETAILS =>** backend/nodejs/foundation/Q_LEVEL1_621.md

**RESOURCES** [#1]

#### Q_LEVEL1_674: What is Express?

**Question:**
en: What is Express in the NodeJS ecosystem?
vi: **Express** trong hệ sinh thái NodeJS là gì?

**Answer:**
en: Express is a minimal web framework for NodeJS. It simplifies routing, middleware handling, request parsing, and HTTP response management.
vi: **Express** là một web framework tối giản cho NodeJS. Nó giúp đơn giản hóa routing, middleware, parse request và trả HTTP response.

#### Q_LEVEL1_781: What is middleware?

**Question:**
en: What is middleware in a NodeJS web application?
vi: **Middleware** trong ứng dụng web NodeJS là gì?

**Answer:**
en: Middleware is code that runs between receiving a request and sending a response. It can log, authenticate, validate, parse, or modify the request and response.
vi: **Middleware** là đoạn code chạy giữa lúc nhận request và lúc trả response. Nó có thể log, xác thực, validate, parse hoặc thay đổi request và response.

#### Q_LEVEL1_889: What is a stream?

**Question:**
en: What is a stream in NodeJS?
vi: **Stream** trong NodeJS là gì?

**Answer:**
en: A stream is an abstraction for reading or writing data piece by piece instead of loading everything into memory at once.
vi: **Stream** là abstraction để đọc hoặc ghi dữ liệu từng phần thay vì tải toàn bộ dữ liệu vào bộ nhớ cùng lúc.

#### Q_LEVEL1_992: What is Buffer?

**Question:**
en: What is `Buffer` in NodeJS?
vi: `Buffer` trong NodeJS là gì?

**Answer:**
en: `Buffer` is a NodeJS object used to handle raw binary data, especially when working with files, streams, sockets, or network protocols.
vi: `Buffer` là object của NodeJS dùng để xử lý dữ liệu nhị phân thô, đặc biệt khi làm việc với file, stream, socket hoặc network protocol.

#### Q_LEVEL1_143: What is process in NodeJS?

**Question:**
en: What is the `process` object in NodeJS?
vi: Object `process` trong NodeJS là gì?

**Answer:**
en: `process` is a global object that provides information and control over the current NodeJS process, including environment variables, arguments, exit codes, and signals.
vi: `process` là global object cung cấp thông tin và quyền điều khiển process NodeJS hiện tại, bao gồm biến môi trường, tham số dòng lệnh, exit code và signal.

#### Q_LEVEL1_257: What is dotenv commonly used for?

**Question:**
en: What is `dotenv` commonly used for in NodeJS projects?
vi: `dotenv` thường được dùng để làm gì trong dự án NodeJS?

**Answer:**
en: `dotenv` loads environment variables from a `.env` file into `process.env`, usually for configuration such as database URLs, API keys, and ports.
vi: `dotenv` load biến môi trường từ file `.env` vào `process.env`, thường dùng cho cấu hình như database URL, API key và port.

---

### Level 2: Understanding

#### Q_LEVEL2_119: Explain why NodeJS is good for I/O-heavy applications.

**Question:**
en: Explain why NodeJS is often a good fit for I/O-heavy applications.
vi: Giải thích vì sao NodeJS thường phù hợp với ứng dụng nặng về I/O.

**Answer:**
en: NodeJS can start I/O operations and continue handling other requests while waiting for the operating system to finish the work. This makes it efficient for APIs, chat systems, streaming, and gateway services.
vi: NodeJS có thể khởi chạy thao tác I/O rồi tiếp tục xử lý request khác trong lúc chờ hệ điều hành hoàn tất công việc. Vì vậy nó phù hợp với API, hệ thống chat, streaming và gateway service.

#### Q_LEVEL2_224: Explain why CPU-heavy work can hurt NodeJS performance.

**Question:**
en: Explain why CPU-heavy work can hurt a NodeJS server.
vi: Giải thích vì sao tác vụ nặng CPU có thể làm giảm hiệu năng server NodeJS.

**Answer:**
en: JavaScript execution normally runs on one main thread. If that thread spends too long computing, it cannot process callbacks, timers, or new requests quickly.
vi: JavaScript thường chạy trên một main thread. Nếu thread này bị chiếm quá lâu bởi tính toán nặng, nó không thể xử lý callback, timer hoặc request mới kịp thời.

#### Q_LEVEL2_338: Compare callback and Promise.

**Question:**
en: Compare callbacks and Promises in NodeJS.
vi: So sánh **callback** và **Promise** trong NodeJS.

**Answer:**
en: Callbacks pass continuation logic as functions, which can become nested and hard to follow. Promises represent async results as values and support chaining, centralized error handling, and `async/await`.
vi: **Callback** truyền logic tiếp theo dưới dạng function, nên dễ bị lồng nhau và khó đọc. **Promise** biểu diễn kết quả async như một giá trị, hỗ trợ chaining, xử lý lỗi tập trung và `async/await`.

#### Q_LEVEL2_441: Explain error-first callbacks.

**Question:**
en: Explain the error-first callback convention in NodeJS.
vi: Giải thích quy ước **error-first callback** trong NodeJS.

**Answer:**
en: In NodeJS, many callbacks receive the error as the first argument and the result as the second argument. If the error is not null, the caller should handle the failure before using the result.
vi: Trong NodeJS, nhiều callback nhận error ở tham số đầu tiên và kết quả ở tham số thứ hai. Nếu error không phải `null`, caller nên xử lý lỗi trước khi dùng kết quả.

#### Q_LEVEL2_492: Explain microtasks and macrotasks.

**Question:**
en: What are microtasks and macrotasks in NodeJS?
vi: **Microtasks** và **macrotasks** trong NodeJS là gì?

**Answer:**
en: Microtasks are small callback jobs that run immediately after the current JavaScript execution finishes, before the event loop moves to the next phase. Common examples include resolved Promise handlers and `queueMicrotask()`. Macrotasks are larger scheduled tasks handled in later event loop phases, such as timers, I/O callbacks, and `setImmediate()`.
vi: **Microtasks** là các callback nhỏ được chạy ngay sau khi đoạn JavaScript hiện tại kết thúc, trước khi event loop chuyển sang pha tiếp theo. Ví dụ phổ biến là callback của **Promise** đã resolve và `queueMicrotask()`. **Macrotasks** là các tác vụ được lên lịch để xử lý ở các pha sau của event loop, như timer, I/O callback và `setImmediate()`.

#### Q_LEVEL2_526: Differences between Node.js and the Browser.

**Question:**
en: What are the main differences between Node.js and the browser?
vi: Những khác biệt chính giữa **Node.js** và trình duyệt là gì?

**Answer:**
en: Node.js runs JavaScript on the server, while the browser runs JavaScript on the client. Node.js provides APIs for files, processes, networking, and the operating system, but it does not provide browser APIs such as `window`, `document`, or the DOM. Browsers focus on rendering UI and user interaction, while Node.js focuses on backend logic, automation, and server-side tasks.
vi: **Node.js** chạy JavaScript ở phía server, còn trình duyệt chạy JavaScript ở phía client. **Node.js** cung cấp API cho file, process, networking và hệ điều hành, nhưng không có các browser API như `window`, `document` hoặc DOM. Trình duyệt tập trung vào render giao diện và tương tác người dùng, còn **Node.js** tập trung vào logic backend, tự động hóa và các tác vụ phía server.

#### Q_LEVEL2_553: Explain require versus import.

**Question:**
en: Explain the practical difference between `require()` and `import`.
vi: Giải thích khác biệt thực tế giữa `require()` và `import`.

**Answer:**
en: `require()` belongs to CommonJS and loads modules synchronously. `import` belongs to ES Modules, is statically analyzable, and better matches modern JavaScript tooling.
vi: `require()` thuộc **CommonJS** và load module theo kiểu đồng bộ. `import` thuộc **ES Modules**, có thể phân tích tĩnh và phù hợp hơn với tooling JavaScript hiện đại.

#### Q_LEVEL2_667: Explain dependency and devDependency.

**Question:**
en: Explain the difference between `dependencies` and `devDependencies`.
vi: Giải thích sự khác nhau giữa `dependencies` và `devDependencies`.

**Answer:**
en: `dependencies` are needed at runtime, while `devDependencies` are mainly needed for development, testing, linting, or building.
vi: `dependencies` cần khi ứng dụng chạy runtime, còn `devDependencies` chủ yếu dùng khi phát triển, test, lint hoặc build.

#### Q_LEVEL2_772: Explain semantic versioning.

**Question:**
en: Explain semantic versioning in npm packages.
vi: Giải thích **semantic versioning** trong npm package.

**Answer:**
en: Semantic versioning uses `MAJOR.MINOR.PATCH`. Major changes can break compatibility, minor changes add compatible features, and patch changes fix compatible bugs.
vi: **Semantic versioning** dùng dạng `MAJOR.MINOR.PATCH`. Major có thể phá vỡ tương thích, minor thêm tính năng tương thích, patch sửa lỗi tương thích.

#### Q_LEVEL2_886: Explain why streams save memory.

**Question:**
en: Explain why streams are memory-efficient.
vi: Giải thích vì sao **stream** tiết kiệm bộ nhớ.

**Answer:**
en: Streams process data in chunks. For large files or network responses, the application does not need to hold the entire payload in memory.
vi: **Stream** xử lý dữ liệu theo từng chunk. Với file lớn hoặc response mạng lớn, ứng dụng không cần giữ toàn bộ payload trong bộ nhớ.

#### Q_LEVEL2_914: Explain backpressure.

**Question:**
en: Explain backpressure in NodeJS streams.
vi: Giải thích **backpressure** trong NodeJS stream.

**Answer:**
en: Backpressure happens when a writable destination cannot consume data as fast as a readable source produces it. NodeJS stream APIs coordinate flow so memory does not grow uncontrollably.
vi: **Backpressure** xảy ra khi nơi ghi không tiêu thụ dữ liệu nhanh bằng nơi đọc tạo dữ liệu. API **stream** của NodeJS điều phối luồng dữ liệu để bộ nhớ không tăng mất kiểm soát.

#### Q_LEVEL2_126: Explain middleware order.

**Question:**
en: Why does middleware order matter in Express-style applications?
vi: Vì sao thứ tự **middleware** quan trọng trong ứng dụng kiểu Express?

**Answer:**
en: Middleware runs in registration order. Authentication, parsing, validation, and error handling can behave incorrectly if they are placed in the wrong sequence.
vi: **Middleware** chạy theo thứ tự được đăng ký. Xác thực, parse dữ liệu, validation và xử lý lỗi có thể sai nếu đặt không đúng thứ tự.

#### Q_LEVEL2_239: Explain environment-based configuration.

**Question:**
en: Why should NodeJS applications use environment-based configuration?
vi: Vì sao ứng dụng NodeJS nên dùng cấu hình theo môi trường?

**Answer:**
en: Environment-based configuration separates code from deployment settings. The same code can run in development, staging, and production with different secrets, ports, or service URLs.
vi: Cấu hình theo môi trường giúp tách code khỏi thiết lập triển khai. Cùng một codebase có thể chạy ở development, staging và production với secret, port hoặc service URL khác nhau.

#### Q_LEVEL2_348: Explain module caching.

**Question:**
en: Explain module caching in NodeJS.
vi: Giải thích **module caching** trong NodeJS.

**Answer:**
en: After a module is loaded, NodeJS caches its exported value. Later imports usually reuse the same instance, which can affect shared state and initialization behavior.
vi: Sau khi một module được load, NodeJS cache giá trị export của module đó. Các lần import sau thường dùng lại cùng một instance, nên có thể ảnh hưởng đến shared state và logic khởi tạo.

#### Q_LEVEL2_455: Explain unhandled Promise rejection.

**Question:**
en: What is an unhandled Promise rejection?
vi: **Unhandled Promise rejection** là gì?

**Answer:**
en: It happens when a Promise rejects but no `.catch()` or surrounding `try/catch` handles the error. In production, this can hide failures or crash the process depending on runtime settings.
vi: Nó xảy ra khi một **Promise** bị reject nhưng không có `.catch()` hoặc `try/catch` xử lý lỗi. Trong production, lỗi này có thể bị che giấu hoặc làm process crash tùy cấu hình runtime.

#### Q_LEVEL2_568: Explain graceful shutdown.

**Question:**
en: Explain graceful shutdown in a NodeJS service.
vi: Giải thích **graceful shutdown** trong service NodeJS.

**Answer:**
en: Graceful shutdown means the service stops accepting new work, finishes in-flight requests, closes resources such as database connections, and exits cleanly after receiving a termination signal.
vi: **Graceful shutdown** nghĩa là service ngừng nhận việc mới, hoàn tất request đang xử lý, đóng tài nguyên như kết nối database và thoát sạch sau khi nhận signal dừng.

#### Q_LEVEL2_679: Explain why logging matters.

**Question:**
en: Why is structured logging important in NodeJS backends?
vi: Vì sao **structured logging** quan trọng trong backend NodeJS?

**Answer:**
en: Structured logs make production behavior searchable and measurable. Fields such as request ID, user ID, route, latency, and error code help debug distributed systems.
vi: **Structured logging** giúp hành vi production dễ tìm kiếm và đo lường. Các trường như request ID, user ID, route, latency và error code giúp debug hệ thống phân tán.

#### Q_LEVEL2_734: Explain memory leaks in NodeJS.

**Question:**
en: What is a memory leak in NodeJS?
vi: **Memory leak** trong NodeJS là gì?

**Answer:**
en: A memory leak happens when the application keeps references to data that is no longer needed, so the garbage collector cannot free it. In NodeJS, common causes include unbounded caches, forgotten event listeners, global state, long-lived closures, and growing queues.
vi: **Memory leak** xảy ra khi ứng dụng vẫn giữ reference tới dữ liệu không còn cần thiết, khiến **garbage collector** không thể giải phóng bộ nhớ đó. Trong NodeJS, nguyên nhân thường gặp gồm cache không giới hạn, event listener không được gỡ, global state, closure sống quá lâu và queue tăng dần.

**DETAILS =>** /backend/nodejs/foundation/Q_LEVEL2_734.md

#### Q_LEVEL2_789: Explain using PM2 with NodeJS applications.

**Question:**
en: Why do teams use PM2 with NodeJS applications?
vi: Vì sao các team dùng **PM2** với ứng dụng NodeJS?

**Answer:**
en: PM2 is a process manager for NodeJS applications. Teams use it to keep apps running, restart crashed processes, manage multiple instances, handle logs, and simplify deployment or startup scripts. It is especially useful for long-running server processes in environments where you want basic process supervision and operational convenience.
vi: **PM2** là một process manager cho ứng dụng NodeJS. Các team dùng nó để giữ app luôn chạy, tự khởi động lại khi process bị crash, quản lý nhiều instance, xử lý log và đơn giản hóa việc deploy hoặc script khởi động. Nó đặc biệt hữu ích cho các server process chạy lâu dài khi cần giám sát process cơ bản và sự tiện lợi trong vận hành.

**DETAILS =>** /backend/nodejs/foundation/Q_LEVEL2_789.md

---

### Level 3: Applying

#### Q_LEVEL3_183: Implement async file reading pattern.

**Question:**
en: Demonstrate a safe asynchronous file-reading pattern similar to NodeJS `fs.promises.readFile`.
vi: Minh họa pattern đọc file bất đồng bộ an toàn tương tự `fs.promises.readFile` trong NodeJS.

**Answer:**
en: Wrap the asynchronous call in `try/catch`, await the result, and handle errors explicitly so failures do not disappear.
vi: **Vấn đề:** Tác vụ đọc file có thể lỗi vì file không tồn tại hoặc thiếu quyền. **Giải pháp:** Dùng `await` với `try/catch` để xử lý lỗi rõ ràng, giống cách làm với `fs.promises.readFile` trong NodeJS.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;

public static class FileReader
{
    public static async Task<string?> ReadConfigAsync(string path)
    {
        try
        {
            // Similar idea to fs.promises.readFile: await non-blocking I/O.
            return await File.ReadAllTextAsync(path);
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Cannot read file: {ex.Message}");
            return null;
        }
    }
}
```

#### Q_LEVEL3_294: Demonstrate middleware chaining.

**Question:**
en: Demonstrate the middleware chaining idea used by Express-style NodeJS applications.
vi: Minh họa ý tưởng chuỗi **middleware** giống ứng dụng NodeJS kiểu Express.

**Answer:**
en: Middleware receives a context and a `next` function. It can do work before and after passing control to the next middleware.
vi: **Vấn đề:** Request cần đi qua nhiều bước như logging, auth và handler chính. **Giải pháp:** Dùng chuỗi **middleware**, mỗi bước nhận context và gọi `next()` để chuyển sang bước kế tiếp.

```csharp
using System;
using System.Threading.Tasks;

public record RequestContext(string Method, string Path);
public delegate Task Middleware(RequestContext ctx, Func<Task> next);

public static class Pipeline
{
    public static Middleware Logger = async (ctx, next) =>
    {
        Console.WriteLine($"{ctx.Method} {ctx.Path}");
        await next();
    };
}
```

#### Q_LEVEL3_376: Apply retry logic for transient failures.

**Question:**
en: Apply a simple retry pattern for transient failures in a NodeJS-style backend service.
vi: Áp dụng pattern retry đơn giản cho lỗi tạm thời trong backend kiểu NodeJS.

**Answer:**
en: Retry only failures that are likely transient, use a small limit, and avoid infinite loops. In real systems, add backoff and observability.
vi: **Vấn đề:** Network hoặc service bên ngoài có thể lỗi tạm thời. **Giải pháp:** Retry có giới hạn, chỉ retry lỗi phù hợp, và trong production nên thêm **backoff** cùng logging/metrics.

```csharp
using System;
using System.Threading.Tasks;

public static class RetryPolicy
{
    public static async Task<T> RetryAsync<T>(Func<Task<T>> action, int maxAttempts = 3)
    {
        for (var attempt = 1; ; attempt++)
        {
            try { return await action(); }
            catch when (attempt < maxAttempts)
            {
                await Task.Delay(100 * attempt); // Simple backoff.
            }
        }
    }
}
```

#### Q_LEVEL3_487: Use stream-like chunk processing.

**Question:**
en: Show how to process large data in chunks instead of loading everything into memory.
vi: Minh họa cách xử lý dữ liệu lớn theo từng chunk thay vì tải toàn bộ vào bộ nhớ.

**Answer:**
en: Chunk processing follows the same memory-saving principle as NodeJS streams: read a portion, process it, then continue.
vi: **Vấn đề:** Tải toàn bộ file lớn vào RAM dễ gây tốn bộ nhớ. **Giải pháp:** Xử lý theo chunk, giống nguyên tắc của **stream** trong NodeJS.

```csharp
using System.IO;
using System.Threading.Tasks;

public static class ChunkProcessor
{
    public static async Task<long> CountBytesAsync(string path)
    {
        var buffer = new byte[8192];
        long total = 0;

        await using var stream = File.OpenRead(path);
        int read;
        while ((read = await stream.ReadAsync(buffer)) > 0)
        {
            total += read; // Process one chunk at a time.
        }

        return total;
    }
}
```

#### Q_LEVEL3_598: Implement graceful shutdown signal handling.

**Question:**
en: Demonstrate the idea of graceful shutdown for a backend service.
vi: Minh họa ý tưởng **graceful shutdown** cho một backend service.

**Answer:**
en: On termination, stop accepting work, wait briefly for active work to finish, close resources, then exit.
vi: **Vấn đề:** Nếu process dừng đột ngột, request đang xử lý hoặc kết nối database có thể bị hỏng. **Giải pháp:** Bắt signal dừng, ngừng nhận việc mới, đóng resource và thoát có kiểm soát.

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;

public static class ServiceHost
{
    public static async Task RunAsync(CancellationToken token)
    {
        try
        {
            while (!token.IsCancellationRequested)
            {
                await Task.Delay(500, token); // Simulate serving requests.
            }
        }
        finally
        {
            Console.WriteLine("Closing database connections and flushing logs...");
        }
    }
}
```
