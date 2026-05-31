**Question 1:** Giải thích về về mói quan hệ giữa process và thread và cách chia sẻ tài nguyên

**Answer:** Chào bạn. Mối quan hệ giữa Process và Thread, đặc biệt là cách chúng quản lý bộ nhớ như **Stack** và **Heap**, là nền tảng cốt lõi khi xây dựng các hệ thống backend hiệu năng cao hoặc khi tối ưu hóa mã nguồn ở mức độ thấp.

Để dễ hình dung, bạn có thể coi **Process (Tiến trình)** như một "nhà máy", còn **Thread (Luồng)** là những "công nhân" làm việc bên trong nhà máy đó.

### 1. Phân biệt Process và Thread

- **Process:** Là một chương trình đang được hệ điều hành thực thi. Khi một process được tạo ra, hệ điều hành cấp phát cho nó một không gian bộ nhớ hoàn toàn độc lập và tách biệt với các process khác. Nếu một process bị crash (lỗi), nó thường không làm ảnh hưởng đến các process khác.
- **Thread:** Là đơn vị thực thi nhỏ nhất bên trong một Process. Một nhà máy (Process) phải có ít nhất một công nhân (Main Thread) để hoạt động, và có thể thuê thêm nhiều công nhân khác (Multi-threading) để làm nhiều việc cùng lúc. Vì các Thread nằm trong cùng một Process, nếu một Thread gặp lỗi nghiêm trọng (ví dụ: tràn bộ nhớ), nó có thể kéo theo sự sụp đổ của toàn bộ Process đó.

### 2. Cách chia sẻ tài nguyên (Resource Sharing)

Sự khác biệt lớn nhất giữa Process và Thread nằm ở cách chúng sử dụng bộ nhớ. Các "công nhân" trong cùng một nhà máy sẽ có những công cụ dùng chung, nhưng cũng có những đồ đạc cá nhân không ai được đụng vào.

**Tài nguyên DÙNG CHUNG (Shared Resources):**
Tất cả các Thread trong cùng một Process đều có thể nhìn thấy và truy cập các vùng nhớ sau:

- **Heap (Vùng nhớ động):** Bất kỳ dữ liệu nào được cấp phát động (ví dụ như khi bạn dùng từ khóa `new` để tạo một object mới) đều nằm trên Heap. Mọi Thread đều có thể dùng con trỏ để truy cập vào vùng nhớ này. Sự chia sẻ này giúp các Thread giao tiếp với nhau cực kỳ nhanh chóng, nhưng cũng sinh ra bài toán đau đầu về xung đột dữ liệu (Race Condition) nếu hai Thread cùng sửa một dữ liệu trên Heap cùng lúc.
- **Data Segment & Code Segment:** Các biến toàn cục (global variables) và bản thân mã nguồn của chương trình.
- **Tài nguyên hệ thống:** Các file đang mở (File descriptors), kết nối mạng (Network sockets).

**Tài nguyên DÙNG RIÊNG (Private Resources):**
Để các Thread có thể thực thi các hàm khác nhau mà không dẫm chân lên nhau, mỗi Thread bắt buộc phải có không gian riêng:

- **Stack (Vùng nhớ ngăn xếp):** Rất quan trọng. Mỗi Thread được cấp một Stack độc lập để lưu trữ các biến cục bộ (local variables), tham số truyền vào hàm và địa chỉ trả về khi hàm kết thúc. Do đó, một biến cục bộ khai báo bên trong một hàm do Thread A chạy sẽ hoàn toàn vô hình với Thread B.
- **Registers & Program Counter (PC):** Lưu trữ trạng thái hiện tại của CPU (thanh ghi) để biết chính xác Thread này đang chạy đến dòng lệnh nào. Khi hệ điều hành tạm dừng Thread A để chuyển sang Thread B, trạng thái thanh ghi của Thread A được cất đi và nạp lại khi nó được chạy tiếp.
