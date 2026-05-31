# Kanban Methodology Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_811: What is the board-only mistake?

**Question:**
en: What is the common mistake of treating Kanban as only a board?
vi: Lỗi phổ biến khi xem Kanban chỉ là một cái board là gì?

**Answer:**
en: The mistake is thinking that visualizing tasks alone is enough. Without WIP limits, explicit policies, and flow management, the board does not create real Kanban behavior.
vi: Lỗi là nghĩ rằng chỉ cần trực quan hóa task là đủ. Nếu không có WIP limit, explicit policy và quản lý flow thì board đó chưa tạo ra hành vi Kanban thật sự.

#### Q_LEVEL1_824: What is the “everyone is urgent” mistake?

**Question:**
en: What is the mistake of treating too many items as urgent in Kanban?
vi: Lỗi gì xảy ra khi xem quá nhiều item là khẩn cấp trong Kanban?

**Answer:**
en: When too many items are marked urgent, the system loses prioritization discipline and expedite flow becomes meaningless.
vi: Khi quá nhiều item bị gắn nhãn khẩn cấp, hệ thống sẽ mất kỷ luật ưu tiên và luồng expedite trở nên vô nghĩa.

#### Q_LEVEL1_836: What is the hidden blocked-work mistake?

**Question:**
en: What is the common mistake of hiding blocked work in Kanban?
vi: Lỗi phổ biến khi che giấu blocked work trong Kanban là gì?

**Answer:**
en: The mistake is leaving blocked items looking like normal progress. That hides delivery risk and prevents the team from escalating the real problem.
vi: Lỗi là để blocked item trông giống như tiến độ bình thường. Điều đó che giấu rủi ro delivery và ngăn team escalate đúng vấn đề thực sự.

---

### Level 2: Understanding

#### Q_LEVEL2_848: Why is ignoring WIP limit dangerous?

**Question:**
en: Why is ignoring WIP limits a serious Kanban anti-pattern?
vi: Vì sao bỏ qua WIP limit là một Kanban anti-pattern nghiêm trọng?

**Answer:**
en: Ignoring WIP limits reintroduces multitasking and queue growth, which are exactly the system problems Kanban is supposed to expose and reduce.
vi: Bỏ qua WIP limit sẽ đưa multitasking và queue dài quay trở lại, trong khi đó chính là những vấn đề hệ thống mà Kanban được tạo ra để làm lộ và giảm bớt.

#### Q_LEVEL2_861: Why is measuring activity instead of flow harmful?

**Question:**
en: Why is measuring individual activity instead of system flow harmful in Kanban?
vi: Vì sao đo hoạt động cá nhân thay vì flow của hệ thống lại có hại trong Kanban?

**Answer:**
en: Measuring activity rewards busyness instead of delivery. The team may look active while customers still wait too long for value.
vi: Đo hoạt động cá nhân sẽ thưởng cho sự bận rộn thay vì delivery. Team có thể trông rất tích cực trong khi khách hàng vẫn phải chờ quá lâu mới nhận được giá trị.

#### Q_LEVEL2_874: Why is oversized work a flow trap?

**Question:**
en: Why are oversized work items a common flow trap in Kanban?
vi: Vì sao work item quá lớn là bẫy flow thường gặp trong Kanban?

**Answer:**
en: Large items stay in progress longer, hide uncertainty, and block capacity for other work. They make the system less predictable and less responsive.
vi: Item lớn nằm trong trạng thái in progress lâu hơn, che giấu bất định và chiếm capacity của công việc khác. Điều đó làm hệ thống kém dự đoán và phản ứng chậm hơn.

#### Q_LEVEL2_887: Why is stale policy dangerous?

**Question:**
en: Why are unclear or outdated workflow policies dangerous in Kanban?
vi: Vì sao workflow policy mơ hồ hoặc lỗi thời lại nguy hiểm trong Kanban?

**Answer:**
en: If policies are unclear, people move work inconsistently and argue about priorities or done criteria. That weakens flow discipline and trust in the system.
vi: Nếu policy không rõ, mọi người sẽ di chuyển công việc thiếu nhất quán và tranh cãi về ưu tiên hoặc tiêu chí done. Điều đó làm yếu kỷ luật flow và niềm tin vào hệ thống.

---

### Level 3: Applying

#### Q_LEVEL3_899: Apply a blocked-item signal

**Question:**
en: How would you create a simple rule in C# to flag blocked Kanban items?
vi: Bạn sẽ tạo một quy tắc đơn giản trong C# như thế nào để đánh dấu blocked item trong Kanban?

**Answer:**
en: Add an explicit blocked indicator and treat any non-empty block reason as a signal that the item needs attention.
vi: Hãy thêm chỉ báo blocked rõ ràng và xem mọi block reason không rỗng là tín hiệu cho thấy item cần được chú ý.

```csharp
public sealed record KanbanItem(string Title, string? BlockReason);

var item = new KanbanItem("Upgrade logging pipeline", "Waiting for security approval");
var isBlocked = !string.IsNullOrWhiteSpace(item.BlockReason);

Console.WriteLine($"Blocked: {isBlocked}");
```

#### Q_LEVEL3_912: Apply an aging-work alert

**Question:**
en: How would you detect aging work that may be stuck in a Kanban flow?
vi: Bạn sẽ phát hiện aging work có thể đang bị kẹt trong flow Kanban như thế nào?

**Answer:**
en: Compare how long an item has been in progress against a threshold based on typical cycle time, then alert when it stays too long.
vi: Hãy so sánh thời gian item ở trạng thái in progress với một ngưỡng dựa trên cycle time điển hình, rồi cảnh báo khi nó nằm quá lâu.

```csharp
var startedAt = new DateTime(2026, 4, 1, 9, 0, 0, DateTimeKind.Utc);
var typicalCycleDays = 3;
var ageInDays = (DateTime.UtcNow - startedAt).TotalDays;
var agingAlert = ageInDays > typicalCycleDays;

Console.WriteLine($"Aging work alert: {agingAlert}");
```
