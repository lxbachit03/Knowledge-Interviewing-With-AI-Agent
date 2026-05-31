# NodeJS Advance Q&A

### Level 4: Analyzing

#### Q_LEVEL4_164: Analyze Event Loop starvation.

**Question:**
en: Analyze how Event Loop starvation can happen in a NodeJS service.
vi: Phân tích cách **Event Loop starvation** có thể xảy ra trong service NodeJS.

**Answer:**
en: Event Loop starvation happens when callbacks, microtasks, or CPU-heavy work keep the main thread busy for too long. Symptoms include high latency, delayed timers, slow health checks, and request timeouts even when CPU or memory metrics may not immediately explain the issue.
vi: **Vấn đề:** Main thread bị chiếm liên tục bởi callback, microtask hoặc tính toán nặng, khiến **Event Loop** không có cơ hội xử lý việc khác. **Giải pháp:** Đo event loop delay, chia nhỏ công việc, tránh vòng lặp đồng bộ dài và chuyển CPU-heavy task sang **Worker Threads**, process riêng hoặc service khác.

#### Q_LEVEL4_275: Compare Worker Threads and child processes.

**Question:**
en: Compare Worker Threads and child processes for CPU-heavy work in NodeJS.
vi: So sánh **Worker Threads** và **child processes** cho tác vụ nặng CPU trong NodeJS.

**Answer:**
en: Worker Threads share the same process and are useful for CPU work that benefits from lower communication overhead. Child processes provide stronger isolation and can run separate NodeJS instances, but inter-process communication is heavier. For pure CPU tasks, Worker Threads are often simpler; for fault isolation, child processes may be safer.
vi: **Worker Threads** chạy trong cùng process nên giao tiếp nhẹ hơn và phù hợp với tác vụ CPU cần chia việc. **Child processes** cách ly tốt hơn vì là process riêng, nhưng IPC nặng hơn. Nếu ưu tiên hiệu năng trong cùng ứng dụng, chọn **Worker Threads**; nếu ưu tiên cô lập lỗi, chọn **child processes**.

```csharp
using System.Threading.Tasks;

public static class CpuOffload
{
    public static Task<int> RunOnBackgroundThreadAsync(int input)
    {
        // Similar decision idea to NodeJS Worker Threads:
        // keep CPU-heavy work away from the request-handling path.
        return Task.Run(() => input * input);
    }
}
```

#### Q_LEVEL4_331: Compare single thread, child process, Worker Threads, and cluster.

**Question:**
en: Compare the main NodeJS thread, child processes, Worker Threads, and cluster.
vi: So sánh main thread của NodeJS, **child processes**, **Worker Threads** và **cluster**.

**Answer:**
en: The main NodeJS thread is best for normal request handling and asynchronous I/O, but it should not be blocked by long CPU-heavy work. Worker Threads are best for CPU-bound tasks that need parallel execution with lower communication cost inside one process. Child processes are better when you need stronger isolation, separate runtimes, or to run external commands. Cluster runs multiple NodeJS worker processes to use multiple CPU cores for handling incoming traffic, but it does not make a single request faster; it mainly improves throughput and process-level resilience.
vi: Main thread của NodeJS phù hợp nhất cho xử lý request thông thường và async I/O, nhưng không nên bị chặn bởi tác vụ nặng CPU kéo dài. **Worker Threads** phù hợp cho công việc **CPU-bound** cần chạy song song với chi phí giao tiếp thấp hơn trong cùng một process. **Child processes** phù hợp hơn khi cần cách ly mạnh hơn, runtime riêng hoặc chạy lệnh/chương trình bên ngoài. **Cluster** chạy nhiều process NodeJS worker để tận dụng nhiều lõi CPU khi xử lý traffic vào, nhưng nó không làm một request đơn lẻ nhanh hơn; nó chủ yếu tăng throughput và khả năng chịu lỗi ở mức process.

**DETAILS =>** backend/nodejs/advance/Q_LEVEL4_331.md

#### Q_LEVEL4_386: Analyze memory leak investigation.

**Question:**
en: Analyze how you would investigate a memory leak in a NodeJS production service.
vi: Phân tích cách điều tra **memory leak** trong service NodeJS production.

**Answer:**
en: Start by confirming growth patterns with heap usage, RSS, GC activity, and request volume. Then capture heap snapshots, compare object retainers, inspect caches, event listeners, global arrays, closures, and unbounded queues. The goal is to identify what retains memory after the request or job should have completed.
vi: **Vấn đề:** Memory tăng dần có thể do cache không giới hạn, listener không được gỡ, closure giữ object hoặc queue tồn đọng. **Giải pháp:** Theo dõi heap/RSS/GC, chụp heap snapshot, so sánh object còn bị giữ lại và kiểm tra nơi nào giữ reference lâu hơn vòng đời hợp lý.

#### Q_LEVEL4_497: Analyze backpressure failure.

**Question:**
en: Analyze what happens when a NodeJS streaming pipeline ignores backpressure.
vi: Phân tích điều gì xảy ra khi pipeline **stream** NodeJS bỏ qua **backpressure**.

**Answer:**
en: If a readable source produces data faster than the writable destination can consume it, buffers grow, memory increases, latency rises, and the process may crash. Proper stream piping, awaiting drain signals, or using built-in pipeline helpers prevents uncontrolled buffering.
vi: **Vấn đề:** Nguồn đọc đẩy dữ liệu nhanh hơn nơi ghi xử lý, buffer sẽ phình to, RAM tăng và process có thể crash. **Giải pháp:** Dùng API **stream pipeline**, tôn trọng tín hiệu `drain`, hoặc giới hạn tốc độ xử lý để tránh buffer không kiểm soát.

#### Q_LEVEL4_508: Analyze dependency supply chain risk.

**Question:**
en: Analyze dependency supply chain risks in a NodeJS project.
vi: Phân tích rủi ro **dependency supply chain** trong dự án NodeJS.

**Answer:**
en: NodeJS projects often depend on many direct and transitive packages. Risks include malicious packages, abandoned dependencies, vulnerable versions, typo-squatting, and postinstall scripts. Mitigation includes lockfiles, audit tools, package review, minimal dependencies, pinned versions for critical services, and CI security checks.
vi: **Vấn đề:** Dự án NodeJS thường kéo theo nhiều dependency trực tiếp và gián tiếp. Rủi ro gồm package độc hại, package bỏ bảo trì, phiên bản có lỗ hổng, typo-squatting và script chạy lúc install. **Giải pháp:** Dùng lockfile, audit CI, review package quan trọng, giảm dependency không cần thiết và kiểm soát version.

---

### Level 5: Evaluating

#### Q_LEVEL5_619: Evaluate NodeJS for CPU-heavy services.

**Question:**
en: Evaluate whether NodeJS is a good choice for a CPU-heavy backend service.
vi: Đánh giá NodeJS có phù hợp cho backend service nặng CPU hay không.

**Answer:**
en: NodeJS is usually not the first choice for sustained CPU-heavy work because the main JavaScript thread can become a bottleneck. It can still work if CPU tasks are isolated with Worker Threads, queues, native modules, or separate services. The decision depends on team expertise, latency targets, operational complexity, and whether most workload is CPU-bound or I/O-bound.
vi: NodeJS thường không phải lựa chọn đầu tiên cho workload CPU-heavy kéo dài vì main thread JavaScript dễ thành nút cổ chai. Tuy vậy vẫn có thể dùng nếu cô lập tác vụ bằng **Worker Threads**, queue, native module hoặc service riêng. Quyết định nên dựa vào năng lực team, mục tiêu latency, độ phức tạp vận hành và tỷ lệ workload CPU-bound so với I/O-bound.

**DETAILS =>** backend/nodejs/advance/Q_LEVEL5_619.md

#### Q_LEVEL5_724: Evaluate TypeScript adoption.

**Question:**
en: Evaluate the trade-offs of using TypeScript in a large NodeJS backend.
vi: Đánh giá sự đánh đổi khi dùng **TypeScript** trong backend NodeJS lớn.

**Answer:**
en: TypeScript improves refactoring confidence, API contracts, editor support, and team collaboration. The cost is build complexity, type maintenance, and occasional friction with dynamic libraries. For large teams and long-lived services, the maintainability benefits usually outweigh the overhead.
vi: **TypeScript** giúp refactor tự tin hơn, rõ contract API, hỗ trợ IDE tốt hơn và giảm hiểu nhầm giữa các thành viên. Chi phí là build phức tạp hơn, phải bảo trì type và đôi khi khó chịu với thư viện quá dynamic. Với service lớn và team đông, lợi ích bảo trì thường đáng hơn chi phí ban đầu.

#### Q_LEVEL5_835: Defend a framework choice.

**Question:**
en: Defend choosing a minimal framework like Express versus a structured framework like NestJS.
vi: Bảo vệ lựa chọn framework tối giản như **Express** so với framework có cấu trúc như **NestJS**.

**Answer:**
en: Express is strong when the service is small, the team wants maximum flexibility, or the architecture is already well defined. NestJS is stronger when the team needs consistent structure, dependency injection, modules, testing patterns, and onboarding discipline. A mature choice considers team size, service lifespan, standards, and maintenance cost rather than popularity alone.
vi: **Express** phù hợp khi service nhỏ, team cần linh hoạt cao hoặc kiến trúc đã được định nghĩa rõ. **NestJS** phù hợp hơn khi cần cấu trúc nhất quán, **dependency injection**, module, pattern test và dễ onboarding. Lựa chọn trưởng thành nên dựa trên quy mô team, tuổi thọ service, tiêu chuẩn nội bộ và chi phí bảo trì.

#### Q_LEVEL5_946: Evaluate serverless NodeJS.

**Question:**
en: Evaluate when serverless NodeJS functions are a good production choice.
vi: Đánh giá khi nào **serverless NodeJS functions** là lựa chọn production tốt.

**Answer:**
en: Serverless is effective for event-driven workloads, irregular traffic, simple APIs, scheduled jobs, and integrations where scaling to zero matters. It is less ideal for consistently low latency, long-running connections, heavy cold-start sensitivity, or complex local debugging. The best fit is workload-dependent.
vi: **Serverless** hiệu quả cho workload theo event, traffic không đều, API đơn giản, scheduled job và integration cần scale về 0. Nó kém phù hợp nếu cần latency rất ổn định, kết nối dài, nhạy với **cold start** hoặc debug local phức tạp. Lựa chọn đúng phụ thuộc vào workload cụ thể.

#### Q_LEVEL5_157: Critique the statement that NodeJS is single-threaded.

**Question:**
en: Critique the statement: "NodeJS is single-threaded, so it cannot scale."
vi: Phê bình nhận định: "NodeJS đơn luồng nên không thể scale."

**Answer:**
en: The statement is incomplete. NodeJS runs JavaScript on a main thread, but it uses asynchronous I/O, a libuv thread pool, clustering, Worker Threads, and horizontal scaling to handle large workloads. The real limitation appears when the main thread is blocked by CPU-heavy code or poor design.
vi: Nhận định này thiếu chính xác. NodeJS chạy JavaScript trên main thread, nhưng dùng async I/O, **libuv thread pool**, clustering, **Worker Threads** và horizontal scaling để xử lý workload lớn. Giới hạn thật sự xuất hiện khi main thread bị chặn bởi CPU-heavy code hoặc thiết kế kém.
