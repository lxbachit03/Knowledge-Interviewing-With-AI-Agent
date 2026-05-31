**Question 1:** Event Emitter trong NodeJS là gì

**Answer:** **Event Emitter** là một trong những khái niệm quan trọng và cốt lõi nhất trong Node.js. Nó là cơ chế giúp các đối tượng (objects) trong Node.js có thể giao tiếp với nhau thông qua việc **phát ra (emit)** và **lắng nghe (listen)** các sự kiện.

Về bản chất, Event Emitter triển khai một mẫu thiết kế phần mềm gọi là **Observer Pattern** (hoặc Publish-Subscribe).

### 1. Cách hoạt động (Ví dụ thực tế)

Hãy tưởng tượng Event Emitter giống như việc bạn đăng ký (Subscribe) một kênh YouTube:

- **Kênh YouTube (Emitter):** Khi có video mới, kênh này sẽ "phát ra" một thông báo.
- **Bạn (Listener):** Bạn "lắng nghe" thông báo đó. Khi thông báo đến, bạn sẽ thực hiện một hành động (ví dụ: mở điện thoại lên xem video).

Trong Node.js, rất nhiều module tích hợp sẵn (như HTTP, File System, Streams) đều được xây dựng dựa trên Event Emitter. Ví dụ, khi một máy chủ HTTP nhận được một yêu cầu, nó sẽ phát ra sự kiện `'request'`.

### 2. Cách sử dụng cơ bản

Để sử dụng, bạn cần gọi module `events` có sẵn trong Node.js.

```javascript
// 1. Nạp module events
const EventEmitter = require("events");

// 2. Tạo một instance (đối tượng) từ class EventEmitter
const myEmitter = new EventEmitter();

// 3. Tạo một Listener (Người lắng nghe sự kiện)
// Khi sự kiện 'userLogin' xảy ra, hàm callback sẽ được chạy
myEmitter.on("userLogin", (username) => {
  console.log(`Xin chào, ${username}! Bạn đã đăng nhập thành công.`);
});

// 4. Emit (Phát ra) sự kiện
// Khi dòng code này chạy, nó sẽ "đánh thức" Listener ở trên
myEmitter.emit("userLogin", "NguyenVanA");

// Kết quả in ra terminal: Xin chào, NguyenVanA! Bạn đã đăng nhập thành công.
```

### 3. Các phương thức phổ biến của Event Emitter

- **`.on(eventName, listener)`**: Đăng ký một hàm lắng nghe (listener) cho một sự kiện. Mỗi khi sự kiện được phát ra, hàm này sẽ chạy. (Giống hàm `.addListener`).
- **`.emit(eventName, [args])`**: Phát ra sự kiện, có thể truyền kèm theo các dữ liệu (`args`) để gửi đến hàm lắng nghe.
- **`.once(eventName, listener)`**: Đăng ký một hàm lắng nghe, nhưng nó **chỉ chạy đúng một lần duy nhất**. Sau khi chạy xong, nó tự động bị gỡ bỏ.
  ```javascript
  myEmitter.once("firstLogin", () => {
    console.log("Tặng 100 điểm thưởng cho lần đăng nhập đầu tiên!");
  });
  ```
- **`.removeListener(eventName, listener)`** hoặc **`.off(eventName, listener)`**: Gỡ bỏ một hàm lắng nghe cụ thể khỏi một sự kiện.
- **`.removeAllListeners([eventName])`**: Gỡ bỏ toàn bộ các hàm lắng nghe của một sự kiện (hoặc của tất cả sự kiện nếu không truyền tham số).

### 4. Tại sao Event Emitter lại quan trọng?

Node.js hoạt động theo cơ chế **Bất đồng bộ (Asynchronous)** và **Hướng sự kiện (Event-driven)**. Thay vì bắt hệ thống phải chờ đợi một tác vụ (như đọc file, gọi API) hoàn thành xong mới chạy code tiếp theo, Node.js sẽ cứ chạy tiếp. Khi nào tác vụ kia xong, nó sẽ dùng **Event Emitter** để thông báo: _"Tôi làm xong rồi, xử lý dữ liệu đi!"_.

Điều này giúp Node.js có thể xử lý hàng ngàn kết nối cùng lúc mà không bị treo máy chủ.
