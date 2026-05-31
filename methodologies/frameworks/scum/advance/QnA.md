# SCRUM Advance Q&A

---

### Level 4: Analyzing

#### Q_LEVEL4_401: Analyze Product Owner bottlenecks

**Question:**
en: Analyze what happens when the Product Owner becomes a bottleneck for every requirement and decision.
vi: Phân tích điều gì xảy ra khi Product Owner trở thành nút thắt cho mọi yêu cầu và quyết định.

**Answer:**
en: Scrum slows down because clarification, prioritization, and stakeholder alignment pile up behind one person. The deeper issue is usually not just workload, but weak product discovery practices, unclear delegation boundaries, or too many parallel initiatives.
vi: Scrum sẽ chậm lại vì mọi việc từ làm rõ yêu cầu, sắp ưu tiên đến đồng bộ stakeholder đều bị dồn vào một người. Gốc rễ vấn đề thường không chỉ là quá tải, mà còn do discovery yếu, ranh giới ủy quyền không rõ hoặc có quá nhiều hướng làm song song.

```csharp
var queuedRequests = new[] { "Clarify story A", "Reprioritize bug B", "Approve copy C", "Stakeholder sync D" };
Console.WriteLine($"PO bottleneck load: {queuedRequests.Length} waiting decisions");
```

#### Q_LEVEL4_404: Analyze Daily Scrum dysfunction

**Question:**
en: Analyze the signs that a Daily Scrum is no longer helping the team.
vi: Phân tích các dấu hiệu cho thấy Daily Scrum không còn giúp ích cho team.

**Answer:**
en: Warning signs include people reporting to a manager instead of coordinating with peers, repeating the same updates without adjustment, and leaving with no changed plan. A useful Daily Scrum should reveal how the team will move closer to the Sprint Goal today.
vi: Dấu hiệu dễ thấy là mọi người đang báo cáo cho manager thay vì phối hợp với nhau, lặp lại cùng một cập nhật mỗi ngày mà không có thay đổi kế hoạch, và kết thúc buổi họp mà không ai biết hôm nay phải điều chỉnh gì. Daily Scrum hiệu quả phải giúp team tiến gần hơn tới Sprint Goal ngay trong ngày đó.

```csharp
var updates = new[] { "Yesterday/Today/Blocker", "Yesterday/Today/Blocker", "Yesterday/Today/Blocker" };
var usefulCoordination = false;
Console.WriteLine(usefulCoordination ? "Daily Scrum is adaptive" : "Daily Scrum is ritualized");
```

#### Q_LEVEL4_407: Analyze incomplete increments

**Question:**
en: Analyze the risk of carrying partially done work across multiple Sprints.
vi: Phân tích rủi ro khi kéo công việc làm dở qua nhiều Sprint.

**Answer:**
en: Repeated carryover hides low quality, weak slicing, and poor planning assumptions. It also distorts transparency because the Sprint appears busy, but little usable value is actually reaching stakeholders.
vi: Việc liên tục kéo việc dở sang Sprint sau thường che giấu chất lượng thấp, khả năng chia nhỏ công việc kém và giả định planning sai. Nó cũng làm transparency méo mó vì Sprint trông rất bận, nhưng giá trị usable thực tế đến tay stakeholder lại rất ít.

```csharp
var sprintItems = new[]
{
    new { Title = "Checkout flow", Done = false },
    new { Title = "Tax rules", Done = false },
    new { Title = "Receipt email", Done = true }
};

var doneRate = sprintItems.Count(x => x.Done) / (double)sprintItems.Length;
Console.WriteLine($"Done rate: {doneRate:P0}");
```

#### Q_LEVEL4_410: Analyze story point inflation

**Question:**
en: Analyze why story point inflation often appears after velocity becomes a management KPI.
vi: Phân tích vì sao hiện tượng bơm story point thường xuất hiện khi velocity bị dùng làm KPI quản lý.

**Answer:**
en: Once velocity is rewarded, teams are pushed to optimize the metric rather than forecasting quality. Estimates drift upward, cross-team comparisons become meaningless, and the organization learns the wrong lesson from the data.
vi: Khi velocity bị đem đi thưởng phạt, team sẽ tối ưu con số thay vì tối ưu chất lượng dự báo. Estimate dần bị đẩy cao lên, so sánh giữa team mất ý nghĩa và tổ chức rút ra kết luận sai từ dữ liệu.

```csharp
var originalEstimate = 5;
var inflatedEstimate = 8;
Console.WriteLine($"Inflation detected: {inflatedEstimate - originalEstimate} extra points");
```

#### Q_LEVEL4_413: Analyze scaling trade-offs

**Question:**
en: Analyze the main trade-offs when Scrum is scaled across multiple dependent teams.
vi: Phân tích các trade-off chính khi scale Scrum qua nhiều team có dependency với nhau.

**Answer:**
en: You gain broader delivery capacity and specialization, but you also pay in alignment cost, dependency risk, and slower decision cycles. The challenge becomes preserving local autonomy while coordinating shared product direction and integration quality.
vi: Bạn có thêm năng lực delivery và chuyên môn hóa, nhưng phải trả giá bằng chi phí đồng bộ, rủi ro dependency và vòng ra quyết định chậm hơn. Bài toán khó là giữ được quyền tự chủ cục bộ trong khi vẫn điều phối đúng hướng sản phẩm và chất lượng tích hợp.

```csharp
var teams = 4;
var dependencies = 7;
Console.WriteLine($"Coordination pressure rises as teams={teams}, dependencies={dependencies}");
```

---

### Level 5: Evaluating

#### Q_LEVEL5_501: Evaluate Scrum for interrupt-driven teams

**Question:**
en: Evaluate whether Scrum is a good fit for a team that is constantly interrupted by urgent production support.
vi: Đánh giá liệu Scrum có phù hợp với team thường xuyên bị gián đoạn bởi công việc hỗ trợ production khẩn cấp hay không.

**Answer:**
en: Scrum can still work, but only if interruptions are limited, visible, and accounted for in planning. If urgent work dominates unpredictably, a flow-based approach like Kanban may fit better because it handles continuous intake more honestly.
vi: Scrum vẫn có thể dùng được nếu lượng gián đoạn được giới hạn, minh bạch và được tính vào planning. Nếu công việc khẩn cấp xuất hiện liên tục và khó đoán, cách tiếp cận flow-based như Kanban thường phù hợp hơn vì phản ánh thực tế incoming work trung thực hơn.

```csharp
var plannedSprintPoints = 24;
var interruptPoints = 11;
var interruptionRatio = interruptPoints / (double)plannedSprintPoints;
Console.WriteLine($"Interruption ratio: {interruptionRatio:P0}");
```

#### Q_LEVEL5_504: Evaluate releasing every Sprint

**Question:**
en: Should a Scrum Team release to production every Sprint if technically possible?
vi: Nếu về kỹ thuật có thể, Scrum Team có nên release production ở mọi Sprint không?

**Answer:**
en: Often yes, because frequent release shortens feedback loops and reduces integration risk. However, the real decision should consider product risk, customer context, regulatory constraints, and whether smaller releases actually improve learning.
vi: Trong nhiều trường hợp là nên, vì release thường xuyên giúp rút ngắn vòng feedback và giảm rủi ro tích hợp. Tuy vậy, quyết định đúng còn phụ thuộc vào mức rủi ro sản phẩm, bối cảnh khách hàng, yêu cầu tuân thủ và việc release nhỏ có thực sự giúp học nhanh hơn hay không.

```csharp
var releaseReady = true;
var complianceApproved = false;
Console.WriteLine(releaseReady && complianceApproved ? "Release now" : "Hold release and resolve constraints");
```

#### Q_LEVEL5_507: Evaluate strong specialization

**Question:**
en: Evaluate whether strict specialist silos fit well inside a Scrum Team.
vi: Đánh giá liệu việc chia silo chuyên môn cứng có phù hợp với Scrum Team hay không.

**Answer:**
en: Strong specialization can help with deep expertise, but rigid silos usually hurt flow and shared ownership. Scrum benefits more when specialists keep their strengths while still collaborating enough to deliver an Increment together.
vi: Chuyên môn sâu có giá trị, nhưng silo cứng thường làm hỏng flow và tinh thần sở hữu chung. Scrum hiệu quả hơn khi specialist vẫn giữ thế mạnh riêng nhưng đủ linh hoạt để cùng nhau giao một Increment hoàn chỉnh.

```csharp
var handoffs = 5;
Console.WriteLine(handoffs > 3 ? "Silo risk is high" : "Collaboration flow is healthier");
```

#### Q_LEVEL5_510: Evaluate skipping estimation

**Question:**
en: Evaluate the claim that Scrum teams should stop estimating completely.
vi: Đánh giá nhận định rằng Scrum team nên bỏ estimation hoàn toàn.

**Answer:**
en: Stopping all estimation can be useful in some mature contexts, but doing it blindly often removes a useful conversation about complexity, risk, and sequencing. The better question is whether the current estimation approach is creating learning or just overhead.
vi: Bỏ estimation hoàn toàn có thể hợp lý trong một số bối cảnh đủ trưởng thành, nhưng làm theo phong trào thường khiến team mất đi một cuộc trao đổi hữu ích về độ phức tạp, rủi ro và thứ tự triển khai. Câu hỏi đúng hơn là cách estimation hiện tại có tạo ra hiểu biết hay chỉ tạo overhead.

```csharp
var estimationMeetingHours = 6;
var planningValueScore = 3;
Console.WriteLine(planningValueScore < 5 ? "Rework estimation approach" : "Current estimation may be justified");
```

#### Q_LEVEL5_513: Evaluate Scrum success

**Question:**
en: How would you evaluate whether Scrum adoption is truly improving product delivery?
vi: Bạn sẽ đánh giá như thế nào để biết việc áp dụng Scrum có thực sự cải thiện delivery của sản phẩm?

**Answer:**
en: Judge Scrum by outcomes such as clearer priorities, more reliable increments, healthier stakeholder feedback loops, better quality, and faster adaptation to learning. Counting ceremonies or certification badges is a weak signal compared with actual product and team behavior.
vi: Hãy đánh giá Scrum bằng kết quả như ưu tiên rõ hơn, Increment đáng tin cậy hơn, vòng feedback với stakeholder khỏe hơn, chất lượng tốt hơn và khả năng thích nghi nhanh hơn trước điều học được. Đếm số ceremony hay chứng chỉ là tín hiệu rất yếu nếu so với hành vi thật của sản phẩm và team.

```csharp
var metrics = new Dictionary<string, bool>
{
    ["Stable delivery"] = true,
    ["Lower escaped defects"] = true,
    ["Faster feedback cycle"] = true,
    ["Ceremonies completed"] = true
};

var strongSignals = metrics.Count(x => x.Key != "Ceremonies completed" && x.Value);
Console.WriteLine($"Strong Scrum outcome signals: {strongSignals}");
```
