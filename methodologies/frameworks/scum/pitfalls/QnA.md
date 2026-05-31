# SCRUM Pitfalls Q&A

---

### Level 1: Remembering

#### Q_LEVEL1_901: What is the “Scrum means more meetings” mistake?

**Question:**
en: What is the common mistake behind saying Scrum is just more meetings?
vi: Sai lầm phổ biến đằng sau nhận định Scrum chỉ là nhiều cuộc họp hơn là gì?

**Answer:**
en: The mistake is focusing on ceremony count instead of the purpose of inspection and adaptation. Scrum events are meant to improve alignment and learning, not add process theater.
vi: Sai lầm nằm ở chỗ chỉ nhìn số lượng cuộc họp mà bỏ qua mục đích inspect và adapt. Các sự kiện của Scrum được tạo ra để tăng alignment và học hỏi, không phải để dựng thêm “sân khấu quy trình”.

#### Q_LEVEL1_904: What is the fake Scrum Master trap?

**Question:**
en: What is the trap when the Scrum Master acts only as a meeting scheduler?
vi: Cái bẫy nào xảy ra khi Scrum Master chỉ đóng vai người đặt lịch họp?

**Answer:**
en: The team loses coaching, systemic problem solving, and real process improvement. Scrum Master is supposed to enable effective Scrum, not just manage calendars.
vi: Team sẽ mất coaching, mất người nhìn ra vấn đề hệ thống và mất động lực cải tiến quy trình thực chất. Scrum Master phải giúp Scrum vận hành hiệu quả, chứ không chỉ quản lý lịch họp.

#### Q_LEVEL1_907: What is the commitment confusion mistake?

**Question:**
en: What is the mistake of treating Sprint commitment as a rigid contract?
vi: Sai lầm khi xem Sprint commitment như hợp đồng cứng là gì?

**Answer:**
en: It confuses planning intent with guaranteed delivery. Scrum expects commitment to the Sprint Goal, while the detailed scope may adapt as the team learns during the Sprint.
vi: Sai lầm là nhầm giữa ý định planning với cam kết giao hàng tuyệt đối. Scrum nhấn mạnh commitment với Sprint Goal, còn chi tiết scope có thể cần điều chỉnh khi team học thêm trong Sprint.

---

### Level 2: Understanding

#### Q_LEVEL2_911: Why is overcommitting every Sprint dangerous?

**Question:**
en: Why is chronic sprint overcommitment dangerous in Scrum?
vi: Vì sao việc overcommit lặp đi lặp lại ở mỗi Sprint lại nguy hiểm trong Scrum?

**Answer:**
en: It destroys predictability and pushes the team toward quality shortcuts, hidden overtime, or dishonest planning. A pattern of missed commitments is usually a signal that slicing, prioritization, or capacity assumptions are weak.
vi: Nó phá hủy tính dự đoán và đẩy team vào đường tắt chất lượng, overtime ngầm hoặc planning thiếu trung thực. Nếu Sprint nào cũng hụt, đó thường là tín hiệu cho thấy cách chia việc, ưu tiên hoặc giả định về capacity đang có vấn đề.

#### Q_LEVEL2_914: Why is skipping backlog refinement expensive?

**Question:**
en: Why is skipping backlog refinement an expensive Scrum mistake?
vi: Vì sao bỏ backlog refinement là một sai lầm tốn kém trong Scrum?

**Answer:**
en: Without refinement, the team enters Sprint Planning with vague work, weak estimates, and hidden dependencies. The cost shows up later as confusion, rework, and lower confidence in sprint commitments.
vi: Nếu bỏ refinement, team bước vào Sprint Planning với item mơ hồ, estimate yếu và dependency bị che khuất. Cái giá sẽ xuất hiện sau đó dưới dạng hiểu sai yêu cầu, phải làm lại và niềm tin vào sprint commitment giảm đi.

#### Q_LEVEL2_917: Why is velocity as KPI harmful?

**Question:**
en: Why is using velocity as a team performance KPI harmful?
vi: Vì sao dùng velocity như KPI hiệu suất của team lại có hại?

**Answer:**
en: Once velocity becomes a target, the metric gets gamed. Teams inflate estimates, optimize point totals, and lose the forecasting signal velocity was supposed to provide.
vi: Khi velocity trở thành target, chỉ số đó sẽ bị “chơi game”. Team bắt đầu bơm estimate, tối ưu tổng point và làm mất luôn giá trị forecasting vốn có của velocity.

#### Q_LEVEL2_920: Why is a weak Definition of Done risky?

**Question:**
en: Why is a weak or inconsistent Definition of Done risky?
vi: Vì sao Definition of Done yếu hoặc không nhất quán lại rủi ro?

**Answer:**
en: It creates false transparency. Work looks completed on the board, but bugs, missing tests, or integration issues remain hidden until late, when they are more expensive to fix.
vi: Nó tạo ra transparency giả. Trên board thì item trông như đã xong, nhưng bug, thiếu test hoặc lỗi tích hợp vẫn nằm ẩn bên dưới và đến lúc lộ ra thì chi phí sửa đã cao hơn nhiều.

---

### Level 3: Applying

#### Q_LEVEL3_923: Apply a safer capacity rule

**Question:**
en: How would you apply a simple rule to reduce repeated sprint overcommitment?
vi: Bạn sẽ áp dụng quy tắc đơn giản nào để giảm tình trạng overcommit Sprint lặp lại?

**Answer:**
en: Plan below average historical capacity and reserve explicit room for uncertainty, support work, and defects. The goal is not to look maximally busy, but to make the team’s commitments more reliable.
vi: Hãy plan thấp hơn mức capacity lịch sử trung bình và chừa rõ một phần cho bất định, việc hỗ trợ và defect. Mục tiêu không phải là làm cho team trông thật bận, mà là làm cho commitment của team đáng tin hơn.

```csharp
var historicalVelocity = 26;
var uncertaintyBuffer = 0.15;
var plannedPoints = (int)(historicalVelocity * (1 - uncertaintyBuffer));

Console.WriteLine($"Safer sprint plan: {plannedPoints} points");
```

#### Q_LEVEL3_926: Apply a warning check for fake Done

**Question:**
en: How would you detect that a team is claiming items are done before they truly meet the Definition of Done?
vi: Bạn sẽ phát hiện thế nào khi team đánh dấu item là done trước khi nó thực sự đạt Definition of Done?

**Answer:**
en: Compare board status with objective delivery evidence such as tests, integration, review completion, and deployment readiness. If “done” depends on follow-up work after the Sprint, it is usually not truly done.
vi: Hãy đối chiếu trạng thái trên board với bằng chứng delivery khách quan như test, tích hợp, review hoàn tất và khả năng deploy. Nếu một item còn phụ thuộc vào việc làm thêm sau Sprint thì thường nó chưa thật sự done.

```csharp
var evidence = new Dictionary<string, bool>
{
    ["Merged"] = true,
    ["Tests passed"] = false,
    ["Reviewed"] = true,
    ["Deployable"] = false
};

var fakeDone = evidence.Any(x => !x.Value);
Console.WriteLine(fakeDone ? "Warning: item is not truly Done" : "Item meets Done criteria");
```
