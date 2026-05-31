# Common Q&A

[?][source of truth là sao?]

[?][mô hình TCP/IP?]

[?][Giao thức FTP, kết nối TCP ?]

[?][XSS, CSRF]

[?][Tại sao sao phải dùng sticky session? chúng ta có thể dùng Redis hoặc memory cached, các instance khác nhau có thể truy cập cùng 1 Redis mà?]

- trong kiến trúc hệ thống hiện đại, việc sử dụng Redis/Memcached (gọi là Distributed Session) là phương pháp được ưu tiên hơn nhiều so với Sticky Session
- Sticky Session (hay Session Affinity) là cơ chế của Load Balancer đảm bảo rằng tất cả request từ một Client cụ thể sẽ luôn luôn được gửi đến cùng một Server instance duy nhất trong suốt phiên làm việc.
- Sticky Session: Dữ liệu nằm ngay trên RAM của Server đang xử lý. Truy cập dữ liệu phiên mất gần như $0ms$.
- Redis: Dù Redis rất nhanh, nhưng Server vẫn phải tốn một khoảng thời gian (network round-trip) để gửi request qua mạng đến Redis node và đợi phản hồi. Với các ứng dụng yêu cầu độ trễ cực thấp, việc truy cập RAM cục bộ vẫn là "vô đối".
- Nếu dữ liệu session của bạn rất lớn (ví dụ lưu nhiều object phức tạp), việc chuyển toàn bộ dữ liệu đó qua lại giữa App Server và Redis trong mỗi request sẽ làm tăng băng thông nội bộ và gây áp lực lên _I/O mạng_.

[?][khi Redis container restart thì dữ liệu trong RAM trước đó có mất không?]

- Câu trả lời ngắn gọn là: Mặc định là _CÓ (mất sạch)_, nhưng bạn hoàn toàn có thể cấu hình để _KHÔNG_ mất

[?][tại sao Giao thức HTTP và kiến trúc RESTful API là stateless?]

- cần phân biệt stateless ở tầng nào.
- HTTP được thiết kế stateless theo nguyên tắc: "mỗi request là một transaction độc lập, hoàn toàn tự chứa (self-contained)".
- Server không lưu bất kỳ session context nào trong bộ nhớ giữa hai request
- Hệ quả thực tế: Cơ chế "đăng nhập" phổ biến hiện nay như cookie/session hay JWT thực ra là các cơ chế được thêm vào phía trên HTTP để giả lập trạng thái — không phải HTTP tự nó có state.
- Nói ngắn gọn: HTTP stateless vì đó là quyết định thiết kế gốc cho distributed document system. REST stateless vì đó là điều kiện cần thiết để đạt được scalability và reliability trong distributed application architecture.
- _Dưới góc độ HTTP_:HTTP là stateless để tối ưu hóa hiệu suất mạng. Mỗi khi một request kết thúc, kết nối có thể bị đóng lại (trong HTTP/1.0) hoặc giữ lại (Keep-alive trong HTTP/1.1)
- _Dưới góc độ RESTful API:_ Stateless trong REST yêu cầu rằng toàn bộ thông tin cần thiết để phục vụ request phải nằm trong chính request đó. Ví dụ kỹ thuật: `GET /products?page=2` kèm theo Token xác thực trong Header. Server không cần nhớ trước đó bạn đã gọi `page=1`.
- Với kinh nghiệm làm Fullstack, bạn sẽ thấy tính Stateless này giúp việc triển khai các container Docker và điều phối bằng Kubernetes trở nên dễ dàng hơn rất nhiều vì các pod có thể thay thế nhau mà không lo mất context.

[?][Việc 1 kết nối bị đóng lại hoặc giữ lại có ý nghĩa gì? có những ảnh hưởng gì?]

- Đây là khía cạnh thuộc về lớp Transport (TCP) và cách HTTP quản lý nó.
- _Short-lived Connection (Đóng lại ngay - HTTP/1.0):_ Mỗi cặp Request/Response sẽ mở một kết nối TCP riêng và đóng ngay sau khi hoàn tất. **TCP Handshake overhead**: Mỗi lần kết nối lại phải thực hiện bắt tay 3 bước (3-way handshake) và thiết lập TLS (nếu là HTTPS). Việc này cực kỳ tốn thời gian (latency tăng cao). **Tốn tài nguyên Server**: Server phải _liên tục mở/đóng socket, tiêu tốn CPU và RAM_.
- _Persistent Connection (Giữ lại - Keep-Alive / HTTP/1.1+):_ Một kết nối TCP đơn lẻ được giữ mở để phục vụ nhiều Request/Response liên tiếp. **Ảnh hưởng:** _Giảm Latency_: Loại bỏ bước bắt tay cho các request tiếp theo. Tốc độ load trang nhanh hơn đáng kể. _Network Congestion_: Giảm số lượng gói tin điều khiển trên đường truyền. **Nhược điểm:** Nếu Server giữ quá nhiều kết nối "treo" (idle) mà Client không gửi dữ liệu, nó sẽ cạn kiệt tài nguyên (Connection limit). Do đó, luôn có một khoảng timeout để tự động đóng kết nối.

[?][Tại sao giữ connection lâu sẽ cạn kiệt tài nguyên (Connection limit)?]

https://gemini.google.com/share/50ef11d33877

[?][trong giải pháp thứ 2 (Max Keep-Alive Requests), tại sao phải đóng, sau 100 requests thì chứng tỏ connection đang mở này hiệu quả tại sao phải đóng?]

https://gemini.google.com/share/50ef11d33877

[?][Self-descriptive messages khác gì Stateless?]

- Self-descriptive nói về semantic dimension — khả năng một message được hiểu mà không cần tài liệu ngoài hay context ẩn.

```http
POST /users HTTP/1.1
Content-Type: application/json        ← "Hãy parse body theo JSON"
Accept: application/json              ← "Trả về JSON"
Authorization: Bearer <JWT>           ← "Đây là cách xác thực"

{"name": "An", "email": "an@x.com"}
```

- Một intermediary (proxy, API gateway, logging system) chỉ cần đọc message này là biết:

* Đây là tạo resource mới (POST)
* Body format là JSON (Content-Type)
* Cần xác thực Bearer token (Authorization)
* Không cần hỏi thêm bất cứ điều gì bên ngoài

[?][Khi người ta gọi 2 khái niệm session và cookie thành một từ "session cookie", ý người ta là gì?]

### Level 2: Understanding

#### Q_LEVEL2_101: Stateless vs Stateful

**Question 1:**
en: What are stateless and stateful systems? Compare them together.
vi: **Stateless** và **stateful** là gì? Hãy so sánh chúng với nhau.

**Answer:**
en: ...

vi: Là 2 cách tiếp cận khác nhau trong việc quản lý dữ liệu và phiên làm việc (session) giữa client và server:

**Stateless (Không lưu trạng thái):** Server _không lưu giữ bất kì thông tin, dữ liệu (context)_ nào giữa các lần request của client. Mỗi request là _độc lập_ và sẽ mang những thông tin cần thiết khi gửi từ client xuống server
**Stateful (Lưu trạng thái):** Trái ngược với Stateless, server _lưu trữ những thông tin, dữ liệu (context) giữa các lần request của client_ hay còn gọi là _lưu trữ session_ trong bộ nhớ của server (có thể là _RAM hoặc CSDL_). Các lần gọi sau có thể _phụ thuộc vào kết quả hoặc dữ liệu từ lần gọi trước_.

**Cơ chế Stateless:** Client khi gửi request phải kèm theo các thông tin cần thiết (JWT, payload,...) để server có thể hiểu và thực thi.

**Ví dụ điển hình:**HTTP protocal, RESTful API (architectural style).

**Ưu điểm Stateless:**

- _Horizontal Scaling dễ dàng_: điều này giúp khắc phục nhược điểm của Stateful, khi scale theo chiều ngang là scale instance thì requests từ load balancer có thể gửi đến bất kì instance nào mà vẫn có thể xử lý request vì request chứa đầy đủ thông tin cần thiết (load balancer sẽ không cần _sticky session_). Kể cả khi instance crash, request sẽ được chuyển sang instance khác và vẫn có thể xử lý request bình thường.
- Nhờ đặc điểm _độc lập_ của mỗi request, mà Stateless còn có những ưu điểm như _dễ test (reproduce), dễ debug_. Nếu là Stateful thì việc test sẽ khó khăn hơn vì _phải đảm bảo đúng session và dữ liệu của session_ đó.
- _Độ tin cậy cao_: Nếu một instance server bị sập, nó _không kéo theo việc mất dữ liệu phiên_ của người dùng như Stateful.

**Nhược điểm Stateless:**

- Nhược điểm dễ thấy nhất là _payload lớn => băng thông cao_ Client phải _gửi đủ thông tin (context) vào mỗi request_ — token, user info, preferences... làm tăng bandwidth.

```markdown
# Mỗi request đều phải mang theo:

Authorization: Bearer <jwt dài 500+ bytes>
X-User-Preferences: { theme, locale, timezone... }
```

**Cơ chế Stateful:** Khi Client gửi request lần đầu tiên, server sẽ tạo ra 1 session (thường là 1 chuỗi ký tự ngẫu nhiên vd: `session_store["abc123"] = { userId: 1 }`) và lưu trữ nó (session data) trong memory store (có thể là Redis, Memcached) hoặc là database. Sau đó, server sẽ gửi session đó cho client dưới dạng cookie. Các request tiếp theo, client chỉ cần gửi session đó (như Session ID) cho server, server sẽ dựa vào đó để truy xuất bối cảnh (context) hiện tại.

**Ví dụ điển hình:** FTP protocol, TCP connection, hoặc các ứng dụng web truyền thống sử dụng Server-side Session.

**Ưu điểm Stateful:**

- Ưa điểm dễ thấy nhất là _tối ưa băng thông_ bởi vì không cần phải gửi lại toàn bộ thông tin (context) vào mỗi request. Khi gửi request sẽ chỉ kèm theo _session id_ (thường là 1 chuỗi ký tự ngắn) xuống server và server sẽ dùng _session id_ đó để truy xuất _session data_ trong memory store hoặc database để lấy được _bối cảnh (context) hiện tại_.
- Thường được dùng nhiều trong các ứng dụng cần _Realtime Communication_ như _Chat, Game online_ sử dụng _Websocket, gRPC streaming_.
- ...

**Nhược điểm Stateful:**

- Server sẽ phải duy trì bộ nhớ cho hàng triệu session cùng lúc => _tốn tài nguyên_
- _Khó scale_ khi xây dựng hệ thống có load balancer (cần có cơ chế _sticky session_ để đảm bảo 1 client luôn kết nói đúng server đang giữ session của họ) [?][Tại sao sao phải dùng sticky session? chúng ta có thể dùng Redis hoặc memory cached, các instance khác nhau có thể truy cập cùng 1 Redis mà?]

Hệ thống **stateless** không giữ dữ liệu phiên riêng của client giữa các request, nên mỗi request phải mang đủ thông tin để được xử lý. Hệ thống **stateful** giữ lại trạng thái phiên hoặc trạng thái tương tác qua nhiều request, nên request sau có thể phụ thuộc vào request trước. Thiết kế **stateless** thường dễ scale và khôi phục hơn vì server nào cũng có thể xử lý request, trong khi thiết kế **stateful** thuận tiện hơn cho các luồng cần tính liên tục nhưng khó scale, failover và đồng bộ hơn.

**Details:** ./common/Q_LEVEL2_101.md

---

#### Q_LEVEL2_123: Stateless: HTTP Protocol, RESTful API

**Question:**
en: ...
vi: Giao thức HTTP là gì? kiến trúc RESTful API?

**Answer:**
en: ...
vi:

**HTTP (HyperText Transfer Protocol)** là _giao thức (protocol) tầng ứng dụng (application layer - layer 7 trong OSI model)_ hoạt động theo mô hình _client - server_ nghĩa là _mở 1 cổng giao tiếp (connection)_ để client gửi request tới server và server sẽ gửi response về cho client sau đó _đóng cổng giao tiếp_ đó lại. Sử dụng _TCP_ làm giao thức tầng vận chuyển (transport layer - layer 4 trong OSI model). HTTP thường chạy trên nên TCP (port 80) hoặc TLS/SSL (HTTPS port 443).
**Kiến trúc RESTful API:** _REST (Representational State Transfer)_ là một _architectural style_ không phải protocol. RESTful API là _API tuân thủ các nguyên tắc của REST_:

- _Stateless:_ Server không lưu giữ thông tin, dữ liệu,... (context) giữa những request của client
- _Client - Server:_ Tách biệt UI của client và business logic của server
- _Uniform Interface:_ Resouce được định danh qua URI, thao tác thông qua các _method_ (GET, POST, PUT, DELETE, ...)
- _Cacheable:_ Yêu cầu Response từ Server phải tự định nghĩa xem chúng có được phép lưu trữ lại phía Client hoặc qua các bên trung gian (proxy, CDN, Redis...) hay không. Ràng buộc này là về _góc độ tối ưu hóa hiệu năng và tài nguyên và kiến trúc hạ tầng_. Nếu dữ liệu không thay đổi thường xuyên, Client có thể dùng ngay bản cache mà không cần "phiền" đến Server.
- _Layered System:_ Client không biết mình _connect trực tiếp_ với server hay qua các tầng trung gian (proxy, load balancer, CDN...). Ràng buộc này giúp _tăng cường bảo mật và khả năng mở rộng_. REST cho phép _kiến trúc hệ thống nhiều lớp_ (Proxy, Load Balancer, Gateway, Cache Server, ...) đúng giữa Client và Server và Database. Client sẽ không hề biết (cũng không cần biết) mình đang nói chuyện trực tiếp với Server chứa logic hay một máy chủ trung gian. _Security_ lớp trung gian (Firewall/WAF) có thể ngăn chặn các requests độc hại trước khi chạm tới Server chứa logic. _Scalability_ Load Balancer điều hướng request đến các Server rỗi tải. _Shared cached_ một lớp cache chung (redis) phục vụ cho nhiều CLient cùng lúc, giảm tải trực tiếp đến Database.

**4 sub-constraints:**

- _Resource identification in requests_ — URI định danh resource (e.g. /users/42)
- _Resource manipulation through representations_ — Client thao tác resource qua JSON/XML representation
- _Self-descriptive messages_ — Mỗi message chứa đủ thông tin để xử lý (Content-Type, HTTP method...)
- _HATEOAS (Hypermedia As The Engine Of Application State)_ — Response chứa links dẫn đến các action tiếp theo

[?][tại sao Giao thức HTTP và kiến trúc RESTful API là stateless?]
[?][Self-descriptive messages khác gì Stateless?]

**Details:** ./common/Q_LEVEL2_123.md

#### Q_LEVEL2_102: JWT vs Session vs Cookie

**Question:**
en: ...
vi: JWT là gì? Cookie là gì? Session là gì? Ưa điểm? nhược điểm? Lúc nào nên ứng dụng, lúc nào không? Có ảnh hướng hiệu năng, tài nguyên máy tính không? Và ảnh hướng như thế nào nếu có. Nếu không ảnh hưởng tới tài nguyên máy tính thì ảnh hưởng tới gì?. Ví dụ.

**Answer:**
en: ...
vi:

[?][Khi người ta gọi 2 khái niệm session và cookie thành một từ "session cookie", ý người ta là gì?]
[?][Các cách lưu JWT phía Client? Những ảnh hưởng của từng cách? Nên chọn cách nào? Ví dụ.]
[?][LocalStorage với SessionStorage khác gì nhau?]
[?][Các cách để invalidate JWT token? Nên chọn cách nào? Cung cấp code cho kỹ thuật này]

[link][https://claude.ai/share/24e11026-021e-497f-9df3-b576b6a51c28]
[link][https://gemini.google.com/share/fca9febe2e18]

**Details:** ./common/Q_LEVEL2_102.md

#### Q_LEVEL2_333:

**Question:** Single Source of Truth (SSOT) là gì?

**Answer:**

https://gemini.google.com/share/a81aced47502

#### Q_LEVEL2_103: Idempotency
