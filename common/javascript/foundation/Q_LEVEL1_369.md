**Question 1:** Event loop trong JS là gì?

**Answer:** Hiểu một cách đơn giản, **JavaScript Runtime (Môi trường thực thi JavaScript)** chính là "hệ sinh thái" hoặc "ngôi nhà" cung cấp mọi thứ cần thiết để mã (code) JavaScript của bạn có thể chạy được.

Bản thân JavaScript chỉ là một ngôn ngữ (như một kịch bản). Để kịch bản đó biến thành một vở kịch thực tế, nó cần diễn viên, sân khấu, ánh sáng và đạo cụ. JavaScript Runtime chính là toàn bộ nhà hát đó.

Dưới đây là bức tranh toàn cảnh về cách một JavaScript Runtime hoạt động và các thành phần bên trong nó.

---

### Các thành phần chính của một JavaScript Runtime

Dù mã của bạn chạy ở đâu (trên trình duyệt hay trên server), một runtime thường bao gồm 4 thành phần cốt lõi sau:

#### 1. JavaScript Engine (Động cơ JavaScript)

Đây là "trái tim" của runtime. Nó đọc mã JS của bạn, biên dịch và thực thi nó. Engine nổi tiếng nhất là **V8** (được dùng trong Google Chrome và Node.js), ngoài ra còn có SpiderMonkey (Firefox) hay JavaScriptCore (Safari).
Trong Engine có 2 phần chính:

- **Memory Heap:** Nơi cấp phát bộ nhớ (lưu trữ các biến, đối tượng, hàm...).
- **Call Stack (Ngăn xếp lệnh):** Nơi ghi lại xem chương trình đang chạy đến dòng code nào. JS là ngôn ngữ "đơn luồng" (single-threaded), nghĩa là nó chỉ có 1 Call Stack và chỉ làm được 1 việc tại 1 thời điểm.

#### 2. Các APIs (Web APIs hoặc C++ APIs)

Bản thân ngôn ngữ JavaScript không hề có các chức năng như tương tác với giao diện mạng (fetch), đếm thời gian (`setTimeout`), hay thao tác với file. Những tính năng này là do **Runtime cung cấp**.

- **Trong Trình duyệt (Browser Runtime):** Cung cấp các Web APIs như thao tác DOM (`document.getElementById`), `setTimeout`, `fetch`, `localStorage`.
- **Trong Server (Node.js Runtime):** Cung cấp các C++ APIs để đọc/ghi file hệ thống (`fs`), tạo server HTTP, quản lý luồng dữ liệu (streams).

#### 3. Callback Queue (Hàng đợi)

Khi bạn gọi một hàm mất nhiều thời gian (như tải dữ liệu từ máy chủ API bằng `fetch` hoặc đợi `setTimeout`), JS không dừng cả chương trình lại để đợi. Nó giao việc đó cho các APIs xử lý ngầm. Khi APIs làm xong, kết quả (callback) sẽ được đẩy vào **Callback Queue** để xếp hàng chờ được thực thi.

#### 4. Event Loop (Vòng lặp sự kiện)

Đây là "người điều phối giao thông". Nhiệm vụ duy nhất của Event Loop là liên tục quan sát **Call Stack** và **Callback Queue**.

- Nếu Call Stack đang bận, nó sẽ chờ.
- Nếu Call Stack trống, nó sẽ bốc tác vụ đang xếp hàng đầu tiên trong Callback Queue và ném vào Call Stack để chạy. Nhờ cơ chế này, JavaScript dù "đơn luồng" nhưng vẫn có thể xử lý mượt mà hàng ngàn thao tác không đồng bộ (asynchronous) cùng lúc.

---

### Các JavaScript Runtimes phổ biến nhất hiện nay

Tuỳ thuộc vào mục đích sử dụng, bạn sẽ viết code cho các Runtimes khác nhau:

1.  **Trình duyệt Web (Browsers):** Runtimes quen thuộc nhất. Code chạy trực tiếp trên máy của người dùng để tạo giao diện tương tác (Chrome, Firefox, Safari...).
2.  **Node.js:** Runtime mang tính cách mạng đưa JavaScript ra khỏi trình duyệt, cho phép bạn viết backend/server bằng JavaScript. Nó sử dụng V8 engine.
3.  **Deno:** Được tạo ra bởi chính cha đẻ của Node.js (Ryan Dahl) nhằm khắc phục các nhược điểm của Node. Nó bảo mật hơn theo mặc định và hỗ trợ sẵn TypeScript mà không cần cài thêm công cụ chuyển đổi.
4.  **Bun:** Một Runtime mới nổi, cực kỳ nhanh gọn. Nó được thiết kế là công cụ "tất cả trong một" (vừa là runtime, vừa là package manager thay thế npm, vừa là test runner) và đang thu hút rất nhiều sự chú ý của cộng đồng lập trình viên.

===============

**Question 2:** Javascript runtime khác gì browswer runtime and nodejs runtime?

**Answer:** Để làm rõ câu hỏi của bạn, chúng ta cần đính chính một chút về cách gọi: **JavaScript Runtime** là một khái niệm chung (một cái ô lớn), còn **Browser Runtime** và **Node.js Runtime** là hai phiên bản cụ thể nằm dưới cái ô đó.

Nói cách khác, bạn không so sánh 3 thứ ngang hàng với nhau. Bạn đang so sánh 2 môi trường thực thi cụ thể (Browser và Node.js) của cùng một ngôn ngữ (JavaScript).

Cả hai môi trường này đều chia sẻ chung một lõi cốt lõi: **JavaScript Engine** (như V8) để đọc và chạy mã JS. Điểm khác biệt lớn nhất giữa chúng nằm ở **Bộ APIs** mà chúng cung cấp và **Mục đích sử dụng**.

Dưới đây là bảng so sánh trực quan sự khác biệt giữa hai môi trường này:

| Tiêu chí                          | Browser Runtime (Trình duyệt)                                                            | Node.js Runtime (Máy chủ)                                                                |
| :-------------------------------- | :--------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------- |
| **Môi trường chạy**               | Máy tính / Thiết bị của người dùng (Client-side)                                         | Máy chủ (Server-side)                                                                    |
| **Engine phổ biến**               | V8 (Chrome), SpiderMonkey (Firefox), JavaScriptCore (Safari)                             | V8 (Mặc định)                                                                            |
| **Đối tượng Global (Toàn cục)**   | `window`                                                                                 | `global`                                                                                 |
| **Bộ APIs bổ sung**               | **Web APIs:** DOM (`document`), `localStorage`, `fetch`, `Canvas`, `Geolocation`...      | **C++ APIs / Node Modules:** Hệ thống file (`fs`), mạng (`http`), hệ điều hành (`os`)... |
| **Thao tác với HTML/CSS (DOM)**   | Có toàn quyền kiểm soát và thay đổi giao diện.                                           | **Không có**. Node.js không có khái niệm về màn hình, HTML hay CSS.                      |
| **Truy cập File và Hệ điều hành** | **Rất hạn chế** (Sandboxed). Không thể tự ý đọc/ghi file trên máy người dùng để bảo mật. | **Toàn quyền**. Có thể đọc/ghi/xóa file, quản lý bộ nhớ, tiến trình hệ thống.            |
| **Mục đích chính**                | Tạo giao diện tương tác, hiệu ứng động, xử lý thao tác của người dùng trên trang web.    | Xây dựng Backend, RESTful APIs, tương tác với Database, kiến trúc Microservices.         |

---

### Đi sâu vào 3 khác biệt cốt lõi:

#### 1. Bộ công cụ (APIs) được cấp phép

Mã JavaScript nguyên bản không biết cách tạo ra một thẻ `<div>` hay đọc một file `.txt`. Nó phải nhờ Runtime cung cấp công cụ:

- Trong **Browser**, nếu bạn gõ `document.getElementById('app')`, mã chạy trơn tru vì Browser Runtime cung cấp đối tượng `document` (Web API). Nếu bạn mang dòng code này chạy trong Node.js, nó sẽ báo lỗi `ReferenceError: document is not defined` vì Node.js không có Web API này.
- Ngược lại, trong **Node.js**, bạn có thể dùng `const fs = require('fs')` để mở một file trên ổ cứng. Nếu bạn ném đoạn code này lên trình duyệt, nó cũng sẽ báo lỗi vì trình duyệt không cung cấp module `fs`.

#### 2. Tính bảo mật và Giới hạn (Sandboxing)

- **Browser Runtime** được thiết kế như một "nhà tù an toàn" (sandbox). Khi bạn truy cập một trang web, bạn không muốn mã JS của trang web đó có thể lục lọi ổ `C:` hay lấy cắp file cá nhân của bạn. Do đó, Browser Runtime tước đi hoàn toàn quyền can thiệp sâu vào hệ điều hành.
- **Node.js Runtime** chạy trên máy chủ (server) của chính bạn. Bạn là chủ hệ thống, nên Node.js được cấp quyền lực tối đa để tương tác với cơ sở dữ liệu, đọc ghi file hệ thống, và mở các cổng mạng (network ports).

#### 3. Đối tượng Toàn cục (Global Object)

- Trong trình duyệt, cấp cao nhất là đối tượng `window`. Ví dụ, `setTimeout()` thực chất là `window.setTimeout()`.
- Trong Node.js, không có cửa sổ trình duyệt nào cả, nên cấp cao nhất được gọi là `global`. `setTimeout()` ở đây là `global.setTimeout()`. _(Lưu ý: Để giải quyết sự khác biệt này, chuẩn ES2020 đã giới thiệu `globalThis` để bạn gọi đối tượng toàn cục ở bất kỳ runtime nào mà không bị lỗi)._

**Tóm lại:** Khác biệt duy nhất nằm ở "đồ nghề" mà chúng mang theo. Cùng là một người thợ mộc (JavaScript Engine), nhưng nếu cho vào xưởng làm mộc (Node.js), anh ta sẽ có cưa, bào, đục máy (truy cập hệ thống). Nếu đưa anh ta vào phòng triển lãm (Browser), anh ta chỉ được phát cọ vẽ và đèn chiếu sáng (DOM, Web APIs) để trang trí cho sản phẩm.
