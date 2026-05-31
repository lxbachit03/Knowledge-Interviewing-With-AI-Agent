# Javascript Advance Q&A

---

### Level 4: Analyzing

#### Q_LEVEL4_401: Analyze when prototypal inheritance becomes a maintenance problem.

**Question:**
en: Analyze when JavaScript's prototypal inheritance model becomes a maintenance problem.
vi: Phân tích khi nào mô hình prototypal inheritance của JavaScript trở thành vấn đề về bảo trì.

**Answer:**
en: It becomes problematic when teams rely on implicit prototype chains without clear ownership or abstraction boundaries. Debugging gets harder because behavior may come from distant ancestors, and accidental mutation of shared prototypes can affect many objects unexpectedly.
vi: Vấn đề xuất hiện khi team lạm dụng prototype chain nhưng không có ranh giới thiết kế rõ ràng. Lúc đó hành vi của object có thể đến từ nhiều tầng cha khác nhau, khiến việc debug rất mệt; tệ hơn nữa, nếu ai đó sửa shared prototype sai cách thì nhiều object trong hệ thống có thể hỏng cùng lúc.

#### Q_LEVEL4_402: Analyze the trade-offs of dynamic typing.

**Question:**
en: Analyze the trade-offs of JavaScript's dynamic typing in large applications.
vi: Phân tích sự đánh đổi của dynamic typing trong các ứng dụng JavaScript lớn.

**Answer:**
en: Dynamic typing speeds up prototyping and lowers ceremony, but it increases the risk of runtime bugs when data contracts are unclear. In large systems, teams usually compensate with conventions, tests, linting, or TypeScript to regain safety.
vi: Dynamic typing giúp viết nhanh và rất linh hoạt trong giai đoạn đầu, nhưng đổi lại là rủi ro lỗi runtime tăng mạnh nếu hợp đồng dữ liệu không được kiểm soát tốt. Trong hệ thống lớn, team thường phải bù lại bằng test, lint rule, review nghiêm ngặt hoặc chuyển sang TypeScript để lấy lại độ an toàn.

#### Q_LEVEL4_403: Compare microtasks and macrotasks in debugging scenarios.

**Question:**
en: Compare microtasks and macrotasks and explain why the difference matters during debugging.
vi: So sánh microtasks và macrotasks, đồng thời giải thích vì sao sự khác nhau này quan trọng khi debug.

**Answer:**
en: Microtasks, such as Promise callbacks, run before the next macrotask like `setTimeout`. This matters because execution order can look counterintuitive; a callback scheduled later in code may still run earlier, causing state transitions that confuse debugging if the queue model is not understood.
vi: Microtask như callback của `Promise` sẽ được ưu tiên xử lý trước khi event loop chuyển sang macrotask như `setTimeout`. Điều này rất quan trọng khi debug vì thứ tự chạy thực tế có thể khác với trực giác đọc code, dẫn tới việc state thay đổi sớm hơn dự kiến và làm lập trình viên chẩn đoán sai nguyên nhân.

#### Q_LEVEL4_404: Analyze the risks of shared mutable state.

**Question:**
en: Analyze the risks of shared mutable state in JavaScript frontend applications.
vi: Phân tích rủi ro của shared mutable state trong ứng dụng frontend JavaScript.

**Answer:**
en: Shared mutable state creates hidden coupling between components or modules because any consumer can change the same object. The result is flaky UI updates, hard-to-reproduce bugs, and debugging sessions where the source of mutation is difficult to trace.
vi: Shared mutable state tạo ra coupling ngầm giữa các component hoặc module vì nhiều nơi có thể cùng sửa một object. Hậu quả là UI cập nhật không ổn định, bug khó tái hiện, và khi truy vết thì rất khó xác định chính xác nơi nào đã mutate dữ liệu trước đó.

#### Q_LEVEL4_405: Analyze when asynchronous code harms readability.

**Question:**
en: Analyze when asynchronous JavaScript code starts harming readability and maintainability.
vi: Phân tích khi nào code bất đồng bộ trong JavaScript bắt đầu làm giảm khả năng đọc và bảo trì.

**Answer:**
en: Readability drops when async flows mix callbacks, nested Promise chains, retries, and error handling without a clear structure. The code may still work, but the cognitive load rises sharply because developers must mentally reconstruct timing, dependencies, and failure paths.
vi: Code bất đồng bộ bắt đầu trở nên nguy hiểm khi nó trộn callback, Promise chain, retry, timeout, và xử lý lỗi theo kiểu vá chỗ nào hay chỗ đó. Vấn đề không chỉ là syntax xấu mà là tư duy luồng xử lý bị vỡ, khiến người bảo trì phải tự dựng lại toàn bộ thứ tự thời gian và nhánh lỗi trong đầu.

---

### Level 5: Evaluating

#### Q_LEVEL5_501: Evaluate whether TypeScript should be mandatory.

**Question:**
en: Evaluate whether TypeScript should be mandatory for a large JavaScript codebase.
vi: Đánh giá liệu TypeScript có nên là bắt buộc với một codebase JavaScript lớn hay không.

**Answer:**
en: For most large teams, the answer is yes because the static checks improve refactoring safety, tooling, and onboarding. The trade-off is extra setup and type maintenance, but that cost is usually lower than the ongoing cost of runtime type mistakes in a growing system.
vi: Với đa số codebase lớn, câu trả lời nghiêng mạnh về có vì TypeScript giúp refactor an toàn hơn, tooling tốt hơn và onboarding nhanh hơn. Đánh đổi là phải đầu tư thêm vào type và cấu hình, nhưng chi phí đó thường vẫn rẻ hơn rất nhiều so với việc gánh bug runtime kéo dài trong hệ thống đang tăng trưởng.

#### Q_LEVEL5_502: Judge when `var` is unacceptable in modern code.

**Question:**
en: Judge when using `var` is unacceptable in modern JavaScript code.
vi: Hãy đánh giá khi nào việc dùng `var` là không chấp nhận được trong JavaScript hiện đại.

**Answer:**
en: In most new production code, `var` is unacceptable because function scope and hoisting make reasoning about state harder than necessary. Exceptions are rare and usually limited to legacy compatibility work where rewriting would introduce more risk than value.
vi: Trong phần lớn code production mới, `var` gần như không nên xuất hiện vì function scope và hoisting của nó làm tăng độ mơ hồ mà không đem lại lợi ích thực tế. Trường hợp ngoại lệ chủ yếu nằm ở code legacy cần giữ ổn định tạm thời, nơi việc thay đổi hàng loạt có thể tạo thêm rủi ro.

#### Q_LEVEL5_503: Evaluate Promise chains versus async-await.

**Question:**
en: Evaluate Promise chains versus `async` and `await` for team productivity.
vi: Đánh giá Promise chain so với `async` và `await` dưới góc nhìn năng suất của team.

**Answer:**
en: `async` and `await` usually improve productivity because they express linear workflows more clearly and reduce nesting. Promise chains still have value for composition-heavy cases, but for day-to-day business logic, `async` and `await` are easier for most teams to read and maintain.
vi: Xét trên năng suất chung, `async/await` thường thắng vì biểu diễn luồng tuần tự rõ hơn và giảm độ rối của code. Promise chain vẫn phù hợp ở các tình huống composition đặc thù, nhưng với business logic hằng ngày thì `async/await` giúp đa số team đọc nhanh, review nhanh và sửa lỗi dễ hơn.

#### Q_LEVEL5_504: Critique excessive abstraction in JavaScript utilities.

**Question:**
en: Critique the practice of creating too many generic utility helpers in JavaScript projects.
vi: Hãy phê bình việc tạo quá nhiều utility helper tổng quát trong dự án JavaScript.

**Answer:**
en: Excessive abstraction often produces utilities that are technically reusable but semantically unclear. Teams spend more time learning internal helper conventions than solving product problems, and bugs become harder to trace because logic is fragmented across generic layers.
vi: Việc trừu tượng hóa quá đà thường tạo ra các helper có vẻ tái sử dụng được nhưng lại không nói rõ mục đích nghiệp vụ. Hậu quả là team mất thời gian học “framework nội bộ”, còn bug thì khó truy vết hơn vì logic bị xé nhỏ và giấu sau nhiều lớp generic.

#### Q_LEVEL5_505: Justify when direct DOM manipulation is acceptable.

**Question:**
en: Justify when direct DOM manipulation is acceptable in a modern JavaScript application.
vi: Hãy biện minh khi nào thao tác DOM trực tiếp là chấp nhận được trong ứng dụng JavaScript hiện đại.

**Answer:**
en: Direct DOM manipulation is acceptable when it is small, localized, performance-sensitive, and clearly isolated from a framework's rendering model. It becomes a poor choice when it bypasses state management conventions and creates two competing sources of truth.
vi: Thao tác DOM trực tiếp là chấp nhận được khi phạm vi rất nhỏ, được cô lập rõ ràng, và có lý do cụ thể như tối ưu hiệu năng hoặc tích hợp thư viện ngoài. Nó trở thành lựa chọn tệ khi phá vỡ cơ chế quản lý state chung và tạo ra hai nguồn chân lý khác nhau giữa dữ liệu ứng dụng và giao diện thực tế.
