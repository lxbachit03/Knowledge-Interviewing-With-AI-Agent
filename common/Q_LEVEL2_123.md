## Giao thức HTTP

**HTTP (HyperText Transfer Protocol)** là giao thức tầng ứng dụng (Application Layer - Layer 7 trong OSI model) hoạt động theo mô hình **client-server**, sử dụng **TCP** làm transport layer (mặc định port 80, HTTPS port 443).

### Cấu trúc HTTP Message

**Request:**

```
METHOD /path HTTP/version
Headers: value

Body (optional)
```

**Response:**

```
HTTP/version STATUS_CODE Reason
Headers: value

Body
```

**HTTP Methods (Verbs):** `GET`, `POST`, `PUT`, `PATCH`, `DELETE`, `HEAD`, `OPTIONS`, `CONNECT`, `TRACE`

**Status Codes:** 1xx (Informational), 2xx (Success), 3xx (Redirection), 4xx (Client Error), 5xx (Server Error)

---

## Kiến trúc RESTful API

**REST (Representational State Transfer)** là một **architectural style** (không phải protocol) được Roy Fielding định nghĩa năm 2000 trong luận văn tiến sĩ. RESTful API là API tuân thủ các ràng buộc (constraints) của REST.

### 6 Constraints của REST:

| Constraint                      | Mô tả                                                                     |
| ------------------------------- | ------------------------------------------------------------------------- |
| **Stateless**                   | Server không lưu client context giữa các request                          |
| **Client-Server**               | Tách biệt UI layer và data storage layer                                  |
| **Cacheable**                   | Response phải định nghĩa rõ có cache được không                           |
| **Uniform Interface**           | Resource được định danh qua URI, thao tác qua representations             |
| **Layered System**              | Client không biết mình đang connect trực tiếp hay qua proxy/load balancer |
| **Code on Demand** _(optional)_ | Server có thể gửi executable code (e.g. JavaScript) về client             |

### Uniform Interface - 4 sub-constraints:

1. **Resource identification in requests** — URI định danh resource (e.g. `/users/42`)
2. **Resource manipulation through representations** — Client thao tác resource qua JSON/XML representation
3. **Self-descriptive messages** — Mỗi message chứa đủ thông tin để xử lý (Content-Type, HTTP method...)
4. **HATEOAS** _(Hypermedia As The Engine Of Application State)_ — Response chứa links dẫn đến các action tiếp theo

---

## Tại sao HTTP và RESTful API là Stateless?

Đây là câu hỏi quan trọng — cần phân biệt **stateless ở tầng nào**.

### HTTP Stateless — by design

HTTP được thiết kế stateless theo nguyên tắc: **"mỗi request là một transaction độc lập, hoàn toàn tự chứa (self-contained)"**.

```
Request 1: GET /products  →  Server xử lý → Response → forget
Request 2: GET /users/1   →  Server xử lý → Response → forget
                                ↑
                        Không có memory về Request 1
```

Server **không lưu bất kỳ session context nào** trong bộ nhớ giữa hai request. Đây là quyết định thiết kế của Tim Berners-Lee nhằm tối ưu cho việc phân phối hypertext document trên một mạng lưới phân tán (distributed network).

**Hệ quả thực tế:** Cơ chế "đăng nhập" phổ biến hiện nay như **cookie/session** hay **JWT** thực ra là các cơ chế được **thêm vào phía trên** HTTP để _giả lập_ trạng thái — không phải HTTP tự nó có state.

### RESTful Stateless — inherited + enforced

REST **kế thừa** tính stateless từ HTTP và **nâng thành constraint bắt buộc** với lý do kiến trúc rõ ràng hơn:

```
❌ Stateful (vi phạm REST):
  POST /login          → server lưu session_id=abc123
  GET  /cart           → server tra session_id=abc123 để biết user là ai

✅ Stateless (đúng REST):
  GET  /cart           → Authorization: Bearer <JWT chứa user_id>
                         → Server decode token, không cần tra cứu session
```

**3 lý do kỹ thuật REST enforce stateless:**

**1. Scalability (Khả năng mở rộng ngang - Horizontal Scaling)**

> Nếu server lưu state, mọi request của một client phải đến đúng server đó (**sticky session**). Với stateless, bất kỳ node nào trong cluster cũng xử lý được request → Load balancer hoạt động tự do.

**2. Reliability & Fault Tolerance**

> Server crash không mất session của client. Client chỉ cần retry request với đầy đủ thông tin — không cần "reconnect" hay "restore session".

**3. Visibility & Debuggability**

> Monitoring system, proxy, hay API gateway có thể hiểu hoàn toàn một request chỉ bằng cách đọc nó, không cần tra cứu state bên ngoài.

### Tóm tắt cơ chế:

```
Client                          Server
  │                               │
  │  GET /orders/99               │
  │  Authorization: Bearer <JWT>  │
  │  ─────────────────────────── ▶│
  │                               │ ← Tất cả context cần thiết
  │                               │   nằm trong chính request này
  │                               │ ← Server không cần nhớ gì từ
  │  ◀─────────────────────────── │   các request trước
  │  200 OK { order data }        │
  │                               │
  │  (5 giây sau)                 │
  │                               │
  │  DELETE /orders/99            │
  │  Authorization: Bearer <JWT>  │
  │  ─────────────────────────── ▶│  ← Request hoàn toàn độc lập
```

Nói ngắn gọn: **HTTP stateless vì đó là quyết định thiết kế gốc cho distributed document system. REST stateless vì đó là điều kiện cần thiết để đạt được scalability và reliability trong distributed application architecture.**
