# Waterfall Methodology Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_811: What is the “requirements are final” mistake?

**Question:**
en: What is the common mistake of treating early requirements as unquestionably final in Waterfall?
vi: Sai lầm phổ biến khi xem requirements ban đầu là hoàn toàn cuối cùng trong Waterfall là gì?

**Answer:**
en: The mistake is assuming approved documents remove uncertainty. Approval creates a baseline for control, but it does not guarantee the requirements are complete or correct.
vi: Sai lầm nằm ở chỗ cho rằng tài liệu đã được phê duyệt thì đồng nghĩa với việc mọi bất định đã biến mất. Approval chỉ tạo baseline để kiểm soát, chứ không đảm bảo requirement đã đầy đủ hoặc hoàn toàn đúng.

#### Q_LEVEL1_822: What is the documentation theater trap?

**Question:**
en: What is the documentation theater trap in Waterfall projects?
vi: Bẫy documentation theater trong dự án Waterfall là gì?

**Answer:**
en: It is the habit of producing documents mainly to pass reviews rather than to improve shared understanding and execution quality.
vi: Đó là thói quen tạo tài liệu chủ yếu để qua vòng review thay vì để cải thiện hiểu biết chung và chất lượng thực thi.

#### Q_LEVEL1_833: What is the late-testing trap?

**Question:**
en: What is the late-testing trap in Waterfall?
vi: Bẫy late-testing trong Waterfall là gì?

**Answer:**
en: It is the situation where meaningful validation happens so late that defects, integration issues, or requirement misunderstandings become expensive to fix.
vi: Đó là tình huống việc validation có ý nghĩa diễn ra quá muộn, khiến defect, lỗi integration hoặc hiểu sai requirement trở nên rất đắt để sửa.

---

### Level 2: Understanding

#### Q_LEVEL2_844: Why is silent scope creep dangerous in Waterfall?

**Question:**
en: Why is silent scope creep especially dangerous in Waterfall delivery?
vi: Vì sao silent scope creep lại đặc biệt nguy hiểm trong Waterfall delivery?

**Answer:**
en: Because Waterfall plans depend on approved baselines, undocumented change corrupts estimates, testing assumptions, responsibilities, and stakeholder expectations. Warning signs include informal promises, undocumented exceptions, and “small” additions that never go through change control.
vi: Vì kế hoạch Waterfall phụ thuộc vào baseline đã duyệt, nên thay đổi không được ghi nhận sẽ làm hỏng estimate, giả định kiểm thử, phân công trách nhiệm và kỳ vọng của stakeholder. Dấu hiệu cảnh báo gồm các lời hứa miệng, ngoại lệ không được ghi nhận và các bổ sung “nhỏ” nhưng không đi qua change control.

#### Q_LEVEL2_855: Why do phase handoffs fail in practice?

**Question:**
en: Why do formal phase handoffs still fail in practice?
vi: Vì sao các phase handoff chính thức vẫn thất bại trong thực tế?

**Answer:**
en: They fail when teams mistake document transfer for real understanding. A safer approach is to combine documentation with walkthroughs, review sessions, and explicit acceptance criteria between teams.
vi: Chúng thất bại khi team nhầm việc chuyển tài liệu với việc hiểu nhau thật sự. Cách an toàn hơn là kết hợp documentation với walkthrough, review session và acceptance criteria rõ ràng giữa các team.

#### Q_LEVEL2_866: Why is “on time” a misleading success signal?

**Question:**
en: Why can “we are on time” be a misleading signal in a Waterfall project?
vi: Vì sao tín hiệu “chúng ta vẫn đúng tiến độ” có thể gây hiểu lầm trong dự án Waterfall?

**Answer:**
en: A project can be on time in documents and milestone reporting while still hiding severe product risk. If progress is measured only by closed phases, teams may miss whether the actual system works as intended.
vi: Một dự án có thể đúng tiến độ trên tài liệu và milestone report nhưng vẫn che giấu rủi ro sản phẩm nghiêm trọng. Nếu tiến độ chỉ được đo bằng việc đóng phase, team có thể bỏ lỡ câu hỏi quan trọng là hệ thống thật sự có hoạt động đúng như kỳ vọng hay không.

#### Q_LEVEL2_877: Why is weak requirement review a root cause?

**Question:**
en: Why is a weak requirement review process a root cause of later Waterfall failure?
vi: Vì sao quy trình review requirement yếu lại là root cause của nhiều thất bại Waterfall về sau?

**Answer:**
en: Because Waterfall amplifies early misunderstandings. If unclear assumptions survive the requirement phase, they become more expensive and politically harder to challenge later.
vi: Vì Waterfall khuếch đại các hiểu nhầm từ giai đoạn sớm. Nếu các giả định mơ hồ sống sót qua phase requirement, chúng sẽ đắt hơn và khó bị thách thức hơn nhiều ở các phase phía sau.

---

### Level 3: Applying

#### Q_LEVEL3_888: Apply a safer response to unstable requirements

**Question:**
en: What should a team do if they realize requirements are still volatile after the project has already started in Waterfall?
vi: Team nên làm gì nếu nhận ra requirements vẫn còn biến động mạnh sau khi dự án Waterfall đã bắt đầu?

**Answer:**
en: They should surface the volatility explicitly, stop pretending the baseline is still reliable, and use formal replanning or controlled change requests. A safer alternative is to introduce discovery checkpoints or a hybrid phase before more downstream commitments accumulate.
vi: Team nên làm lộ rõ mức biến động đó, dừng việc giả định rằng baseline vẫn đáng tin cậy và dùng replanning chính thức hoặc change request có kiểm soát. Giải pháp an toàn hơn là thêm discovery checkpoint hoặc một phase hybrid trước khi các cam kết ở giai đoạn sau chồng chất thêm.

#### Q_LEVEL3_899: Apply an early warning pattern for late defects

**Question:**
en: How would you create an early warning pattern to reduce the late-defect risk in Waterfall?
vi: Bạn sẽ tạo một cơ chế cảnh báo sớm như thế nào để giảm rủi ro defect muộn trong Waterfall?

**Answer:**
en: Introduce intermediate reviews tied to executable evidence, interface validation, test case preparation from requirements, and milestone-based risk reviews. The safer alternative is to seek proof earlier instead of trusting document completeness alone.
vi: Hãy thêm các buổi review trung gian gắn với bằng chứng có thể kiểm tra được, validation cho interface, chuẩn bị test case từ requirement và các buổi risk review theo milestone. Cách an toàn hơn là tìm bằng chứng sớm hơn thay vì chỉ tin vào việc tài liệu đã đầy đủ.
