**Question 1:** Middleware, Filter, Pipeline trong ASP.NET là gì? (Nói theo ngôn ngữ kỹ thuật)

**Answer:** Trong ASP.NET Core, ba khái niệm này cùng giải quyết bài toán xử lý Request và Response, nhưng chúng vận hành ở các tầng khác nhau và có mục đích chuyên biệt.

Dưới đây là phân tích chi tiết theo góc nhìn kiến trúc hệ thống:

---

## 1. Middleware

**Middleware** là các thành phần (component) phần mềm được lắp ráp vào một **Pipeline** để xử lý các HTTP Request và Response. Mỗi Middleware có quyền quyết định xem có chuyển Request sang thành phần tiếp theo hay không (Short-circuiting).

- **Cơ chế:** Hoạt động theo mô hình **Chain of Responsibility**.
- **Phạm vi:** Toàn cục (Global) cho mọi Request đi vào ứng dụng.
- **Thứ tự:** Rất quan trọng. Thứ tự đăng ký trong `Program.cs` chính là thứ tự thực thi khi Request đi vào và ngược lại khi Response đi ra.
- **Ứng dụng:** Logging, Authentication, Static Files, Exception Handling, CORS.

---

## 2. Filter

**Filter** là một phần của **ASP.NET Core MVC Action Invocation Pipeline** (thường được gọi là Filter Pipeline). Nó cho phép bạn chạy code trước hoặc sau các giai đoạn cụ thể trong chu kỳ thực thi của một Action Method.

- **Phạm vi:** Hẹp hơn Middleware. Filter chỉ thực thi khi Request đã được Middleware **Routing** khớp với một Controller Action.
- **Phân loại (Filter Pipeline):**
  1.  **Authorization Filters:** Chạy đầu tiên để xác định quyền.
  2.  **Resource Filters:** Chạy sau Authorization, hữu ích cho Caching.
  3.  **Action Filters:** Chạy ngay trước và sau khi Action Method được thực thi.
  4.  **Exception Filters:** Xử lý ngoại lệ xảy ra trong Controller.
  5.  **Result Filters:** Chạy trước và sau khi Action Result được thực thi.
- **Ứng dụng:** Validation, Logging riêng cho Action, nén dữ liệu đầu ra cho một số API cụ thể.

---

## 3. Pipeline (The Big Picture)

**Pipeline** không phải là một đối tượng cụ thể mà là thuật ngữ chỉ toàn bộ quy trình luân chuyển của Request thông qua Middleware và Filter.

Có hai cấp độ Pipeline cần phân biệt:

1.  **Request Pipeline (Middleware Pipeline):** Bao quát toàn bộ ứng dụng. Bắt đầu từ khi Server (Kestrel) nhận Request cho đến khi trả về Response.
2.  **MVC Filter Pipeline:** Là một "nhánh con" nằm bên trong Middleware `EndpointRouting`.

---

## Bảng so sánh kỹ thuật

| Tiêu chí          | Middleware                                    | Filter                                                            |
| :---------------- | :-------------------------------------------- | :---------------------------------------------------------------- |
| **Vị trí**        | Nằm ngoài MVC framework, thuộc tầng ứng dụng. | Nằm trong phạm vi của MVC/Web API.                                |
| **Context**       | Chỉ truy cập được `HttpContext`.              | Truy cập được `ActionContext` (Model state, Controller instance). |
| **Độ chi tiết**   | Thấp (xử lý thô các Request).                 | Cao (xử lý logic liên quan đến Business/Action).                  |
| **Khả năng ngắt** | Có thể ngắt bằng cách không gọi `next()`.     | Có thể ngắt bằng cách thiết lập `context.Result`.                 |

### Tóm tắt luồng thực thi:

1.  **Request** đi qua các **Middleware** (từ ngoài vào trong).
2.  Đến Middleware **Routing**, nếu khớp với Controller, nó sẽ chuyển tiếp vào **Filter Pipeline**.
3.  Các **Filter** thực thi -> **Action Method** thực thi.
4.  **Response** đi ngược lại qua các Filter -> Quay lại các **Middleware** (từ trong ra ngoài) -> Trả về Client.

Bạn đang thiết kế một hệ thống yêu cầu xử lý logic ở tầng nào trong hai tầng này?

=============

**Question 2:** Action Method là gì?

**Answer:** Trong kiến trúc ASP.NET Core MVC hoặc Web API, **Action Method** là một phương thức (method) công khai (public) nằm trong một **Controller**, đóng vai trò là điểm cuối (endpoint) để tiếp nhận và xử lý các HTTP Request từ phía Client.

Dưới đây là các đặc điểm kỹ thuật cốt lõi của Action Method:

### 1. Vai trò trong Request Life Cycle

Khi một Request đi qua Middleware Routing, hệ thống sẽ ánh xạ (map) URL thành một Controller và một Action cụ thể. Action Method chịu trách nhiệm:

- Tiếp nhận dữ liệu đầu vào (thông qua Model Binding).
- Thực thi logic nghiệp vụ (Business Logic) hoặc gọi đến các Service.
- Trả về một kết quả (Action Result) để phản hồi cho Client.

---

### 2. Các quy tắc định nghĩa Action Method

Để một phương thức được coi là một Action Method hợp lệ, nó phải tuân thủ các điều kiện:

- **Access Modifier:** Phải là `public`. Các phương thức `private`, `protected` hoặc `internal` sẽ không thể được gọi thông qua HTTP.
- **Không phải Static:** Phương thức không được phép có từ khóa `static`.
- **Attribute:** Thường đi kèm với các **Http Verbs** (như `[HttpGet]`, `[HttpPost]`, `[HttpPut]`, `[HttpDelete]`) để xác định loại request mà nó xử lý.
- **NonAction:** Nếu bạn có một phương thức public trong Controller nhưng không muốn nó làm Action, bạn phải đánh dấu nó với thuộc tính `[NonAction]`.

---

### 3. Kiểu dữ liệu trả về (Return Types)

Các Action Method hiện đại thường trả về một đối tượng thực thi Interface `IActionResult` hoặc `ActionResult<T>`. Các kiểu trả về phổ biến bao gồm:

- **ViewResult:** Trả về một giao diện HTML (thường dùng trong MVC).
- **JsonResult:** Trả về dữ liệu định dạng JSON (thường dùng trong Web API).
- **OkObjectResult (200 OK):** Trả về trạng thái thành công kèm dữ liệu.
- **NotFoundResult (404 Not Found):** Trả về khi không tìm thấy tài nguyên.
- **RedirectResult:** Điều hướng người dùng sang một URL khác.

---

### 4. Ví dụ minh họa

Dưới đây là cấu trúc của một Action Method tiêu chuẩn trong Web API:

```csharp
[ApiController]
[Route("api/[controller]")]
public class ProductsController : ControllerBase
{
    // Đây là một Action Method
    [HttpGet("{id}")]
    public IActionResult GetProduct(int id)
    {
        var product = _service.GetById(id);

        if (product == null)
        {
            return NotFound(); // Trả về 404
        }

        return Ok(product); // Trả về 200 kèm data
    }
}
```

---

### 5. Mối liên hệ với Filter Pipeline

Như đã thảo luận ở phần trước, Action Method là "trái tim" của Filter Pipeline. Trước khi code bên trong Action Method thực thi, các **Action Filters** sẽ chạy để kiểm tra logic (như Validation), và sau khi Action Method hoàn tất, nó lại đi qua các Filter lần nữa để xử lý kết quả trả về trước khi gửi tới Middleware.

Bạn có muốn tìm hiểu sâu hơn về cách **Model Binding** truyền dữ liệu từ URL/Body vào tham số của Action Method không?

=================

**Question 3:** chu kỳ thực thi của một Action Method là gì?

**Answer:** Chu kỳ thực thi của một **Action Method** (thường được gọi là **Action Invocation Pipeline**) là một tập hợp các bước tuần tự nằm trong lòng của MVC Middleware. Khi một Request đã vượt qua được các Middleware tầng thấp và được Routing xác định là khớp với một Action cụ thể, chu trình này sẽ bắt đầu.

Dưới đây là các giai đoạn kỹ thuật chi tiết theo đúng thứ tự thực thi:

---

### 1. Authorization Filters

Đây là chốt chặn đầu tiên. Hệ thống kiểm tra xem người dùng có quyền truy cập vào Action này hay không (ví dụ: qua attribute `[Authorize]`). Nếu thất bại, Pipeline sẽ bị ngắt ngay lập tức và trả về `401 Unauthorized` hoặc `403 Forbidden`.

### 2. Resource Filters

Giai đoạn này chạy ngay sau Authorization. Đây là nơi tốt nhất để triển khai **Caching**.

- **OnResourceExecuting:** Chạy trước khi bất kỳ logic nào khác được thực thi. Nếu có dữ liệu trong Cache, nó có thể trả về kết quả luôn (Short-circuit).
- **OnResourceExecuted:** Chạy sau khi toàn bộ phần còn lại của Pipeline đã hoàn tất.

### 3. Model Binding (Quá trình cực kỳ quan trọng)

Trước khi vào Action Method, ASP.NET Core thực hiện ánh xạ dữ liệu từ HTTP Request (Query string, Route data, Form body) vào các tham số của phương thức.

- Quá trình này bao gồm cả **Model Validation**. Kết quả của việc kiểm tra tính đúng đắn dữ liệu sẽ được lưu vào `ModelState`.

### 4. Action Filters

Đây là giai đoạn bao quanh việc thực thi Action Method:

- **OnActionExecuting:** Chạy **ngay trước** khi Action Method được gọi. Tại đây bạn có thể kiểm tra `ModelState.IsValid` và ngắt request nếu dữ liệu không hợp lệ.
- **Action Execution:** Bản thân code bên trong Action Method của bạn sẽ thực thi ở đây.
- **OnActionExecuted:** Chạy **ngay sau** khi Action Method trả về một kết quả, nhưng trước khi kết quả đó được xử lý.

### 5. Exception Filters

Nếu có bất kỳ lỗi (Exception) nào xảy ra trong quá trình Model Binding, Action Filter hoặc bản thân Action Method, các **Exception Filters** sẽ bắt được chúng để xử lý (ví dụ: log lỗi hoặc trả về định dạng lỗi chuẩn).

### 6. Action Result Execution

Sau khi Action Method thực hiện xong, nó trả về một đối tượng (ví dụ: `ViewResult`, `OkObjectResult`).

- **Result Filters:** Chạy trước (`OnResultExecuting`) và sau (`OnResultExecuted`) khi kết quả được thực thi (ví dụ: trước khi render ra HTML hoặc chuyển đổi object thành JSON).

---

### Tóm tắt luồng di chuyển (Flow)

$$Request \rightarrow Auth \rightarrow Resource \rightarrow Model Binding \rightarrow Action Filter \rightarrow \mathbf{Action Method} \rightarrow Action Filter \rightarrow Exception \rightarrow Result Filter \rightarrow Response$$

### Tại sao cần hiểu chu kỳ này?

- **Tối ưu hiệu năng:** Biết đặt logic Caching ở Resource Filter thay vì Action Filter.
- **Xử lý lỗi tập trung:** Sử dụng Exception Filter để tránh việc dùng `try-catch` quá nhiều trong Controller.
- **Validation:** Tận dụng Action Filter để kiểm tra `ModelState` tự động cho mọi API.

Bạn có muốn đi sâu vào cách tùy chỉnh một **Custom Filter** để can thiệp vào chu kỳ này không?
