**Question 1:** Giải về PM2 (https://pm2.keymetrics.io/). Nó giúp gì cho ứng dụng NodeJS

**Answer:** Để hiểu rõ giá trị của PM2, trước tiên chúng ta cần nhìn lại một đặc điểm cốt lõi của hệ sinh thái Node.js: nó chạy trên một **single-thread** (đơn luồng). Điều này có nghĩa là nếu có một lỗi không được xử lý (unhandled exception) xảy ra, tiến trình Node.js sẽ bị crash và toàn bộ server của bạn sẽ "sập" cho đến khi bạn khởi động lại nó bằng tay. Hơn nữa, một tiến trình Node.js mặc định chỉ sử dụng một nhân CPU, gây lãng phí tài nguyên rất lớn trên các hệ thống server đa nhân.

Đây chính là lúc **PM2 (Process Manager 2)** tỏa sáng. PM2 là một trình quản lý tiến trình (process manager) tiêu chuẩn công nghiệp dành cho môi trường production của các ứng dụng Node.js, đi kèm với một bộ cân bằng tải (load balancer) tích hợp sẵn.

Dưới đây là những giải pháp cốt lõi mà PM2 mang lại cho ứng dụng Node.js của bạn:

### 1. Giữ ứng dụng luôn "sống" (Auto-restart / Daemonize)

Thay vì chạy app bằng lệnh `node app.js` (tiến trình sẽ gắn chặt với session terminal của bạn), bạn chạy bằng `pm2 start app.js`. PM2 sẽ đưa ứng dụng chạy ngầm dưới dạng daemon.
Nếu ứng dụng của bạn bị crash do lỗi logic hoặc cạn kiệt bộ nhớ, PM2 sẽ **ngay lập tức tự động khởi động lại** tiến trình đó. Nó cũng có thể được thiết lập để tự động khởi động lại toàn bộ ứng dụng cùng hệ điều hành mỗi khi server bị reboot hoặc crash phần cứng (thông qua lệnh `pm2 startup`).

### 2. Tận dụng sức mạnh đa nhân với Cluster Mode

Để giải quyết bài toán lãng phí CPU, PM2 cho phép bạn khởi chạy ứng dụng ở chế độ Cluster. Nó sẽ tự động sao chép (fork) và tạo ra nhiều phiên bản (instances) của ứng dụng, thường là tương ứng với số lượng nhân CPU có sẵn trên máy chủ.
Đặc biệt, PM2 tích hợp sẵn một bộ Load Balancer để phân bổ đều các request từ client đến các instances này trên cùng một cổng (port) mạng duy nhất. Điều này giúp tăng khả năng chịu tải (throughput) và tối ưu hóa hệ thống hạ tầng mà bạn không cần phải tự viết code can thiệp vào module `cluster` ở tầng thấp của Node.js.
_Lệnh ví dụ:_ `pm2 start app.js -i max` (Chạy tối đa số lượng instances bằng với số core CPU).

### 3. Triển khai không gián đoạn (Zero-Downtime Reload)

Khi bạn có bản cập nhật code và cần deploy lên production, thay vì phải tắt toàn bộ ứng dụng đi (làm rớt các kết nối hiện tại của client) rồi bật lại, PM2 cung cấp tính năng `reload`.
PM2 sẽ lần lượt khởi động lại từng instance một. Hệ thống mạng vẫn sẽ được định tuyến vào các instances đang hoạt động bình thường trong khi chờ các instances mới khởi động xong. Quá trình này đảm bảo luôn có quá trình phục vụ người dùng, mang lại trải nghiệm cập nhật hoàn toàn mượt mà.

### 4. Quản lý cấu hình linh hoạt (Ecosystem File)

Trong các quy trình DevOps thực tế, việc quản lý biến môi trường (Environment Variables) giữa các môi trường (Development, Staging, Production) có thể rất phức tạp. PM2 giải quyết việc này thông qua file `ecosystem.config.js`. Đây là một file khai báo nơi bạn định nghĩa mọi thứ: đường dẫn file chạy, chế độ cluster, số lượng instance, và các tập biến môi trường khác nhau. Bạn chỉ cần gọi file này khi khởi chạy ứng dụng.

### 5. Quản lý Log tập trung và Xoay vòng (Log Management)

Khi chạy ngầm, bạn không còn thấy console terminal nữa. PM2 sẽ tự động hứng toàn bộ luồng `stdout` (log thông tin) và `stderr` (log lỗi) từ tất cả các instances, gom chúng lại và ghi vào các file log tập trung. Bạn có thể xem log realtime qua lệnh `pm2 logs`. Ngoài ra, PM2 hỗ trợ cài đặt các module như `pm2-logrotate` để tự động chia nhỏ và xóa log cũ, ngăn chặn tình trạng file log phình to nuốt trọn dung lượng ổ cứng.

### 6. Giám sát hệ thống trực tiếp (Monitoring)

Bằng lệnh `pm2 monit`, bạn sẽ được cung cấp một bảng điều khiển ngay trên terminal, cho phép theo dõi trực tiếp lượng RAM và % CPU mà mỗi instance đang tiêu thụ theo thời gian thực. Điều này cực kỳ hữu ích để phát hiện các dấu hiệu bất thường như rò rỉ bộ nhớ (memory leak).

**Tóm lại:** Nếu bạn đang lập trình và kiểm thử, sử dụng các công cụ như `nodemon` là sự lựa chọn tốt nhất. Nhưng một khi ứng dụng đã sẵn sàng triển khai lên server thực tế, sử dụng PM2 gần như là một quy chuẩn bắt buộc để đảm bảo hệ thống backend của bạn hoạt động ổn định, bền bỉ và tối đa hóa được hiệu suất phần cứng.
