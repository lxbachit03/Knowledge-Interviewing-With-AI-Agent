**Question 1:** CORS là gì?

**Answer:** **CORS** (Cross-Origin Resource Sharing) hay **Chia sẻ tài nguyên đa nguồn gốc** là một cơ chế bảo mật dựa trên HTTP. Nó cho phép trình duyệt kiểm soát việc các trang web truy cập vào tài nguyên (như API, font chữ, dữ liệu) từ một **nguồn (origin)** khác với nguồn của trang web hiện tại.

---

## 1. Hiểu về "Origin" (Nguồn)

Để biết tại sao cần CORS, bạn cần biết một "nguồn" được xác định bởi bộ ba: **Giao thức (Protocol)**, **Tên miền (Domain)**, và **Cổng (Port)**.

Nếu bất kỳ yếu tố nào trong ba cái này khác nhau, đó được coi là **Cross-Origin**.

- **Cùng nguồn:** `https://example.com/page1` và `https://example.com/page2`
- **Khác nguồn:** `https://example.com` và `http://example.com` (khác giao thức)
- **Khác nguồn:** `https://example.com` và `https://api.example.com` (khác subdomain)
- **Khác nguồn:** `https://example.com:8080` và `https://example.com:3000` (khác cổng)

---

## 2. Tại sao CORS lại tồn tại?

CORS được sinh ra để nới lỏng **Chính sách đồng nguồn (Same-Origin Policy - SOP)**.

Mặc định, SOP ngăn chặn các kịch bản độc hại (như một trang web giả mạo cố gắng đọc dữ liệu từ tài khoản ngân hàng của bạn khi bạn đang đăng nhập). Tuy nhiên, trong kỷ nguyên ứng dụng hiện đại, việc ứng dụng Frontend (ví dụ: `localhost:3000`) gọi API từ một Backend Server (ví dụ: `api.myapp.com`) là rất phổ biến. CORS cho phép Server "mở cửa" cho những nguồn tin cậy này.

---

## 3. Cách thức hoạt động của CORS

Khi trình duyệt thực hiện một yêu cầu đa nguồn, quá trình thường diễn ra như sau:

### Yêu cầu đơn giản (Simple Request)

Với các yêu cầu như `GET` hoặc `POST` thông thường, trình duyệt gửi yêu cầu trực tiếp kèm theo Header `Origin`. Server sẽ phản hồi và kèm theo Header `Access-Control-Allow-Origin`. Nếu giá trị này khớp với nguồn của bạn (hoặc là `*`), trình duyệt sẽ cho phép dữ liệu đi qua.

### Yêu cầu cần kiểm tra trước (Preflight Request)

Với các yêu cầu phức tạp hơn (như có chứa Header tùy chỉnh hoặc dùng phương thức `PUT`, `DELETE`), trình duyệt sẽ gửi một yêu cầu "nháp" bằng phương thức **OPTIONS** trước khi gửi yêu cầu thực tế.

1.  **Browser:** "Này Server, tôi sắp gửi một lệnh `DELETE` từ `myapp.com`, ông có cho phép không?"
2.  **Server:** "Được, tôi chấp nhận `DELETE` từ nguồn đó." (Trả về status 200)
3.  **Browser:** Gửi yêu cầu `DELETE` thật sự.

---

## 4. Các Header CORS quan trọng

Dưới đây là các Header mà Server cần trả về để cấu hình CORS:

| Header                             | Ý nghĩa                                                                                      |
| :--------------------------------- | :------------------------------------------------------------------------------------------- |
| **`Access-Control-Allow-Origin`**  | Xác định nguồn nào được phép truy cập (Ví dụ: `https://myfrontend.com` hoặc `*` cho tất cả). |
| **`Access-Control-Allow-Methods`** | Các phương thức HTTP được phép (GET, POST, PUT, DELETE, ...).                                |
| **`Access-Control-Allow-Headers`** | Các Header tùy chỉnh được phép gửi lên (Content-Type, Authorization, ...).                   |
| **`Access-Control-Max-Age`**       | Thời gian (giây) trình duyệt có thể lưu kết quả Preflight mà không cần hỏi lại.              |

---

## 5. Lỗi "CORS error" thường gặp

Nếu bạn thấy dòng chữ đỏ _“Access to XMLHttpRequest at... has been blocked by CORS policy”_ trong Console, điều đó có nghĩa là:

- Server chưa cấu hình CORS.
- Server chỉ cho phép một số Domain nhất định và Domain của bạn không nằm trong số đó.
- Bạn đang gửi một Header hoặc phương thức mà Server không khai báo cho phép.

> **Lưu ý quan trọng:** CORS là một cấu hình ở phía **Server**. Bạn không thể sửa lỗi CORS hoàn toàn chỉ bằng cách thay đổi code ở Frontend (trừ khi bạn dùng Proxy để đánh lừa trình duyệt).

Bạn đang gặp lỗi CORS khi phát triển ứng dụng hay chỉ đang tìm hiểu lý thuyết về bảo mật web?
