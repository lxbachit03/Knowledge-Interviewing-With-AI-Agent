# Javascript Pitfalls Q&A

---

### Level 1: Remembering

#### Q_LEVEL1_601: What mistake happens when developers confuse `==` with `===`?

**Question:**
en: What common mistake happens when developers confuse `==` with `===`?
vi: Lỗi phổ biến nào xảy ra khi lập trình viên nhầm giữa `==` và `===`?

**Answer:**
en: The mistake is relying on implicit type coercion and getting unexpected matches. Warning signs include conditions that pass for values like `"0"` and `0`; the safer alternative is to use `===` unless coercion is explicitly required.
vi: Sai lầm nằm ở chỗ dựa vào ép kiểu ngầm rồi nhận kết quả so sánh ngoài mong đợi. Dấu hiệu cảnh báo là điều kiện pass với các giá trị như `"0"` và `0` dù về mặt nghiệp vụ không nên xem là giống nhau; cách an toàn hơn là mặc định dùng `===` nếu không có lý do rất rõ để ép kiểu.

#### Q_LEVEL1_602: What mistake happens when using `var` in loops?

**Question:**
en: What common mistake happens when using `var` in loops with callbacks?
vi: Lỗi phổ biến nào xảy ra khi dùng `var` trong vòng lặp có callback?

**Answer:**
en: Developers often expect each callback to capture a different loop value, but `var` is function-scoped so callbacks may all see the same final value. The safer fix is to use `let` or create a new scope intentionally.
vi: Vấn đề là nhiều người nghĩ mỗi callback sẽ giữ một giá trị riêng của biến lặp, nhưng `var` lại dùng function scope nên tất cả callback có thể cùng nhìn thấy giá trị cuối cùng. Cách phòng tránh an toàn là dùng `let` hoặc chủ động tạo scope mới cho từng lần lặp.

#### Q_LEVEL1_603: What mistake happens when `this` is assumed to be stable?

**Question:**
en: What common mistake happens when developers assume `this` is always stable?
vi: Lỗi phổ biến nào xảy ra khi lập trình viên cho rằng `this` luôn ổn định?

**Answer:**
en: The mistake is assuming `this` depends on where a function is written rather than how it is called. Warning signs include methods losing context when passed as callbacks; safer alternatives include `bind`, arrow functions, or explicit wrapper functions.
vi: Sai lầm ở đây là tưởng rằng `this` phụ thuộc vào nơi khai báo hàm, trong khi thực tế nó thường phụ thuộc vào cách hàm được gọi. Dấu hiệu dễ thấy là method bị mất context khi truyền làm callback; giải pháp an toàn là dùng `bind`, arrow function, hoặc viết wrapper rõ ràng.

---

### Level 2: Understanding

#### Q_LEVEL2_604: Explain why mutating shared objects causes production bugs.

**Question:**
en: Explain why mutating shared objects directly often causes production bugs.
vi: Giải thích vì sao việc mutate trực tiếp object dùng chung thường gây bug production.

**Answer:**
en: Direct mutation changes data in place, so any part of the app holding that reference sees the update immediately, even if it did not expect it. This leads to hidden coupling, inconsistent UI, and debugging sessions where the original source of change is hard to locate; safer practice is to copy before updating.
vi: Vấn đề là khi mutate trực tiếp một object dùng chung, mọi nơi đang giữ cùng tham chiếu sẽ bị ảnh hưởng ngay lập tức dù không hề chuẩn bị cho thay đổi đó. Hậu quả là coupling ngầm, UI hiển thị không nhất quán, và lúc debug thì rất khó tìm nơi đầu tiên đã sửa dữ liệu; giải pháp an toàn là tạo bản sao trước khi cập nhật.

#### Q_LEVEL2_605: Explain why unhandled Promise rejections are dangerous.

**Question:**
en: Explain why unhandled Promise rejections are dangerous.
vi: Giải thích vì sao unhandled Promise rejection là vấn đề nguy hiểm.

**Answer:**
en: Unhandled rejections can hide real failures until they surface as unstable behavior, missing data, or process warnings in production. A warning sign is async code that awaits success paths but ignores error paths; the safer alternative is to use `try/catch` or explicit `.catch()` handling consistently.
vi: Unhandled rejection nguy hiểm vì lỗi thật sự có thể bị bỏ sót cho tới khi hệ thống biểu hiện ra dữ liệu thiếu, hành vi chập chờn, hoặc cảnh báo khó hiểu trong production. Dấu hiệu phổ biến là code chỉ viết luồng thành công mà không có luồng lỗi; cách an toàn hơn là chuẩn hóa `try/catch` hoặc `.catch()` ở mọi điểm bất đồng bộ quan trọng.

#### Q_LEVEL2_606: Explain why mixing callback and async-await styles is risky.

**Question:**
en: Explain why mixing callback-based code and `async`-`await` style can be risky.
vi: Giải thích vì sao việc trộn callback với phong cách `async`-`await` có thể rủi ro.

**Answer:**
en: Mixing styles makes control flow harder to follow because error handling, timing, and cancellation logic become inconsistent. The code may technically work, but the warning sign is when developers need to mentally jump across multiple async patterns to understand one feature; safer teams standardize on one dominant style per layer.
vi: Khi trộn nhiều kiểu bất đồng bộ, luồng xử lý trở nên khó theo dõi vì cách bắt lỗi, thứ tự chạy, và cơ chế timeout hoặc hủy bỏ không còn nhất quán. Dấu hiệu cảnh báo là chỉ để hiểu một chức năng mà reviewer phải đọc qua nhiều kiểu async khác nhau; cách an toàn hơn là chuẩn hóa một phong cách chủ đạo cho từng tầng code.

---

### Level 3: Applying

#### Q_LEVEL3_607: Show how to avoid shared-state mutation.

**Question:**
en: Show how to avoid a bug caused by updating shared state in place.
vi: Hãy minh họa cách tránh bug do cập nhật shared state ngay trên object gốc.

**Answer:**
en: The safer approach is to create a new value and keep the original object unchanged. This prevents hidden side effects and makes state transitions easier to audit.
vi: Vấn đề của mutate tại chỗ là các phần khác trong hệ thống có thể bị ảnh hưởng mà không ai nhận ra. Giải pháp an toàn là tạo dữ liệu mới từ dữ liệu cũ rồi thay thế có chủ đích, như vậy việc theo dõi thay đổi state sẽ rõ ràng hơn.

```csharp
using System;

public record Settings(bool IsEnabled, string Theme);

public class MutationPitfallDemo
{
    public static void Main()
    {
        var original = new Settings(false, "Light");

        // Safer than mutating shared data in place
        var updated = original with { IsEnabled = true };

        Console.WriteLine(original); // unchanged
        Console.WriteLine(updated);  // new value with the intended update
    }
}
```

#### Q_LEVEL3_608: Show how to protect async code with error handling.

**Question:**
en: Show how to protect asynchronous code from silent failures.
vi: Hãy minh họa cách bảo vệ code bất đồng bộ khỏi lỗi bị nuốt mất.

**Answer:**
en: A safer pattern wraps awaited work in explicit error handling and logs or propagates failure intentionally. This avoids hidden rejection paths that only appear later as corrupted behavior.
vi: Sai lầm phổ biến là chờ kết quả bất đồng bộ nhưng không bảo vệ luồng lỗi, khiến hệ thống hỏng âm thầm rồi bộc lộ ở chỗ khác. Giải pháp là bao tác vụ bằng xử lý lỗi rõ ràng để có log, có ngữ cảnh, và quyết định dừng hay phục hồi một cách chủ động.

```csharp
using System;
using System.Threading.Tasks;

public class AsyncPitfallDemo
{
    public static async Task Main()
    {
        try
        {
            string result = await LoadDataAsync();
            Console.WriteLine(result);
        }
        catch (Exception ex)
        {
            // Equivalent to handling a rejected Promise intentionally
            Console.WriteLine($"Handled error: {ex.Message}");
        }
    }

    private static async Task<string> LoadDataAsync()
    {
        await Task.Delay(100);
        throw new InvalidOperationException("Service timeout");
    }
}
```

#### Q_LEVEL3_609: Show how to avoid loop-capture mistakes.

**Question:**
en: Show how to avoid loop variable capture mistakes similar to JavaScript `var` issues.
vi: Hãy minh họa cách tránh lỗi capture biến lặp, tương tự vấn đề hay gặp với `var` trong JavaScript.

**Answer:**
en: The safe pattern is to create a fresh variable for each iteration so each callback captures the intended value. This makes delayed execution predictable instead of depending on one shared changing variable.
vi: Vấn đề cốt lõi là nhiều callback cùng tham chiếu vào một biến thay đổi liên tục, nên khi chạy muộn thì giá trị không còn như kỳ vọng. Giải pháp là tạo giá trị riêng cho từng vòng lặp để mỗi callback giữ đúng dữ liệu cần dùng.

```csharp
using System;
using System.Collections.Generic;

public class LoopCapturePitfallDemo
{
    public static void Main()
    {
        var actions = new List<Action>();

        for (int i = 0; i < 3; i++)
        {
            int captured = i; // Fresh value per iteration
            actions.Add(() => Console.WriteLine(captured));
        }

        foreach (var action in actions)
        {
            action();
        }
    }
}
```
