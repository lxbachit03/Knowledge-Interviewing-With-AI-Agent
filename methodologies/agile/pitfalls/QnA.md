# Agile Methodology Pitfalls Q&A

### Level 1: Remembering

#### Q_LEVEL1_901: What is the “Agile means no documentation” mistake?

**Question:**
en: What is a common mistake when people say Agile means no documentation?
vi: Lỗi phổ biến khi mọi người nói Agile nghĩa là không cần documentation là gì?

**Answer:**
en: The mistake is confusing "less unnecessary documentation" with "no documentation at all." Teams still need enough documentation to support clarity, onboarding, maintenance, and safe delivery.
vi: Lỗi nằm ở việc nhầm giữa "ít documentation không cần thiết hơn" với "không cần documentation". Team vẫn cần đủ tài liệu để hỗ trợ sự rõ ràng, onboarding, bảo trì và delivery an toàn.

#### Q_LEVEL1_914: What is the stand-up status-report trap?

**Question:**
en: What is the common mistake of turning stand-ups into status reports for a manager?
vi: Lỗi phổ biến khi biến stand-up thành buổi báo cáo trạng thái cho manager là gì?

**Answer:**
en: The mistake is shifting the meeting away from team coordination toward performance theater. Stand-ups are meant to help the team synchronize and surface blockers, not perform upward reporting.
vi: Lỗi là biến buổi họp từ công cụ phối hợp của team thành một màn trình diễn báo cáo hiệu suất. Stand-up được tạo ra để team đồng bộ và làm lộ blocker, không phải để báo cáo lên trên.

#### Q_LEVEL1_927: What is the “Agile equals Scrum” misconception?

**Question:**
en: What is the misconception in assuming Agile and Scrum are the same thing?
vi: Hiểu lầm gì xảy ra khi cho rằng Agile và Scrum là một?

**Answer:**
en: Scrum is only one Agile framework. Treating Agile as identical to Scrum ignores other valid approaches such as Kanban and ignores the underlying values behind the practices.
vi: Scrum chỉ là một framework trong Agile. Xem Agile đồng nhất với Scrum sẽ bỏ qua các cách tiếp cận hợp lệ khác như Kanban và bỏ qua các giá trị nền phía sau practice.

---

### Level 2: Understanding

#### Q_LEVEL2_938: Why is fake agility dangerous?

**Question:**
en: Why is adopting Agile vocabulary without changing behavior dangerous?
vi: Vì sao dùng từ ngữ Agile nhưng không thay đổi hành vi lại nguy hiểm?

**Answer:**
en: It creates a false sense of progress. Teams may rename meetings and roles while keeping the same slow approvals, siloed decisions, and low trust. That produces cynicism because the label changes but the pain remains.
vi: Nó tạo ra cảm giác tiến bộ giả. Team có thể đổi tên cuộc họp và vai trò nhưng vẫn giữ quy trình phê duyệt chậm, quyết định theo silo và niềm tin thấp. Kết quả là sự hoài nghi tăng lên vì cái tên thay đổi nhưng nỗi đau thì không.

#### Q_LEVEL2_951: Why is overcommitting each sprint harmful?

**Question:**
en: Why is overcommitting every sprint a serious Agile anti-pattern?
vi: Vì sao overcommit ở mọi sprint là một Agile anti-pattern nghiêm trọng?

**Answer:**
en: Chronic overcommitment destroys predictability and encourages cutting quality to "make the sprint." Over time it trains the team to promise optimistically and hide risk instead of planning honestly.
vi: Việc overcommit kéo dài phá hủy tính dự đoán và khuyến khích cắt giảm chất lượng để "kịp sprint". Theo thời gian, nó huấn luyện team hứa hẹn lạc quan và che giấu rủi ro thay vì planning trung thực.

#### Q_LEVEL2_964: Why is skipping retrospectives expensive?

**Question:**
en: Why is skipping retrospectives an expensive mistake even when the team is busy?
vi: Vì sao bỏ retrospective là một sai lầm đắt giá ngay cả khi team đang rất bận?

**Answer:**
en: Teams that never pause to improve usually repeat the same friction and defects. Skipping reflection saves one meeting today but often costs much more time later.
vi: Những team không bao giờ dừng lại để cải thiện thường lặp lại cùng một ma sát và defect. Bỏ một buổi nhìn lại có thể tiết kiệm một cuộc họp hôm nay nhưng thường làm mất nhiều thời gian hơn về sau.

#### Q_LEVEL2_977: Why is focusing only on feature output risky?

**Question:**
en: Why is focusing only on feature output risky in Agile product development?
vi: Vì sao chỉ tập trung vào feature output lại rủi ro trong Agile product development?

**Answer:**
en: Agile is supposed to optimize learning and value, not just shipping more tickets. If the team only counts output, it may deliver many things that nobody needs.
vi: Agile được kỳ vọng tối ưu việc học và giá trị, chứ không chỉ đẩy thật nhiều ticket ra ngoài. Nếu team chỉ đếm output, họ có thể giao rất nhiều thứ mà chẳng ai thực sự cần.

---

### Level 3: Applying

#### Q_LEVEL3_988: Apply a safer sprint commitment policy

**Question:**
en: How would you design a simple rule to avoid chronic sprint overcommitment?
vi: Bạn sẽ thiết kế một quy tắc đơn giản như thế nào để tránh overcommit sprint kéo dài?

**Answer:**
en: Reserve some capacity for uncertainty instead of filling every sprint to 100 percent. A practical approach is to plan below historical capacity and review carryover honestly.
vi: Hãy chừa một phần capacity cho sự bất định thay vì nhồi kín sprint đến 100 phần trăm. Một cách thực tế là plan thấp hơn năng lực lịch sử và review phần carryover một cách trung thực.

```csharp
var historicalVelocity = 30;
var safetyBuffer = 0.2;
var plannedCommitment = (int)(historicalVelocity * (1 - safetyBuffer));

Console.WriteLine($"Planned sprint commitment: {plannedCommitment} points");
```

#### Q_LEVEL3_996: Apply a retrospective follow-through check

**Question:**
en: How would you prevent retrospective action items from being forgotten?
vi: Bạn sẽ ngăn action item của retrospective bị lãng quên như thế nào?

**Answer:**
en: Track retro actions explicitly, assign an owner, and review open items in the next retrospective or stand-up. Improvement without follow-through is just discussion.
vi: Hãy theo dõi action retro một cách rõ ràng, gán owner và review các item còn mở trong retrospective hoặc stand-up tiếp theo. Cải tiến mà không theo đến cùng thì chỉ là thảo luận suông.

```csharp
var retroActions = new[]
{
    new { Title = "Reduce PR review delay", Owner = "Lan", Done = false },
    new { Title = "Clarify acceptance criteria template", Owner = "Minh", Done = true }
};

var missingFollowThrough = retroActions.Count(x => !x.Done);
Console.WriteLine($"Open improvement actions: {missingFollowThrough}");
```
