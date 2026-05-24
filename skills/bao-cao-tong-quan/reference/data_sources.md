# Nguồn Dữ Liệu

Mapping chính xác từ mỗi phần báo cáo đến công cụ MCP tương ứng. **Gọi tất cả đồng thời trong một batch song song** — không gọi tuần tự; gọi tuần tự làm chậm hơn 30 giây.

---

## Tiền mặt & Tài chính (QuickBooks)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Số dư tiền mặt / ngân hàng | `cash-flow-quickbooks-account` | Số dư hiện tại; hiện delta so tuần trước nếu có |
| Doanh thu tháng hiện tại | `profit-loss-quickbooks-account` | Tháng này so tháng trước |
| Công nợ phải thu | Danh sách hóa đơn QuickBooks | Lọc hóa đơn mở/chưa thanh toán |
| Tuổi công nợ phải thu | Danh sách hóa đơn QuickBooks | Nhóm theo ngày quá hạn: 0–30, 31–60, 61+ ngày |
| Hóa đơn quá hạn | Danh sách hóa đơn QuickBooks | Lọc ngày đến hạn > 30 ngày qua; nêu tên khách + số tiền + số ngày quá hạn |

**Xử lý trạng thái QB**: nếu `cash-flow-quickbooks-account` trả về lỗi, phản hồi rỗng, hoặc trạng thái "chưa kết nối", đánh dấu toàn bộ phần Tiền mặt là "không có — QuickBooks không khả dụng" và tiếp tục. Không thử lại.

---

## Doanh thu & Bán hàng (PayPal / Square / Stripe)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Tổng thanh toán 7 ngày | Giao dịch PayPal | Tổng hợp thanh toán đã hoàn tất trong khoảng thời gian |
| Xu hướng bán hàng | Giao dịch PayPal | 7 ngày này so 7 ngày trước; tính delta |
| Giao dịch thất bại / đang chờ | Giao dịch PayPal | Đánh dấu bất kỳ giao dịch nào > 2.000.000đ |
| Thanh toán Square | Square (nếu kết nối) | Giống PayPal — tổng hợp + xu hướng |
| Doanh thu Stripe | Stripe `list_invoices` (nếu kết nối) | Hóa đơn đã thanh toán trong khoảng thời gian |

Dùng bất kỳ connector thanh toán nào đang khả dụng. Nếu cả PayPal và Square đều kết nối, báo cáo tổng hợp và từng nguồn riêng.

---

## Pipeline (HubSpot)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Pipeline theo giai đoạn | `get_crm_objects` type=deals | Nhóm theo giai đoạn deal; tổng giá trị |
| Deal đóng tuần này | `search_crm_objects` | Lọc ngày đóng trong khoảng, giai đoạn = closed-won |
| Deal đình trệ | `search_crm_objects` | Lọc ngày hoạt động cuối > 7 ngày, giai đoạn đang mở |
| Lead mới tuần này | `search_crm_objects` | Lọc ngày tạo trong khoảng |
| Deal bị trễ | `search_crm_objects` | Deal đang mở có ngày đóng đã qua mà vẫn chưa đóng |

---

## Cam kết (Google Calendar)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Sự kiện quan trọng tuần này | `list_events` | Lọc tuần hiện tại; nêu bật cuộc họp với khách hàng, deadline, giữ chỗ quan trọng |
| 7 ngày tới | `list_events` | Xem trước; đánh dấu bất cứ thứ gì có bên ngoài |

---

## Danh sách theo dõi (Gmail)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Chuỗi email khẩn | `search_threads` | Truy vấn: `is:important OR is:starred` trong 7 ngày qua |
| Leo thang từ khách hàng | `search_threads` | Truy vấn: từ khóa như "khẩn cấp", "khiếu nại", "hủy", "hoàn tiền" trong 7 ngày |
| Yêu cầu nhạy cảm thời gian | `search_threads` | Truy vấn: `is:unread` + từ khóa như "deadline", "ASAP", "hôm nay", "ngay bây giờ" |

**Dự phòng Gmail**: nếu cuộc gọi Gmail bị lỗi (xác thực không ổn định — đây là vấn đề đã biết), bỏ qua Danh sách theo dõi một cách im lặng và thêm "Gmail không khả dụng" vào phụ lục. Không hiển thị lỗi trong thân báo cáo.

---

## Tín hiệu nội bộ (Slack / Teams)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Chuỗi khẩn | Tìm kiếm Slack (nếu kết nối) | Chuỗi có @mention hoặc tín hiệu khẩn trong kênh liên quan đến chủ |
| Việc cần làm | Tìm kiếm Slack | Tin nhắn gửi đến chủ hoặc được tag để theo dõi |

---

## Hỗ trợ khách hàng (Intercom / Zendesk)

| Chỉ số | Công cụ | Ghi chú |
|---|---|---|
| Ticket đang mở | Intercom `search_conversations` / Zendesk | Đếm đang mở; đánh dấu bất kỳ ticket nào > 48 giờ chưa giải quyết |
| Leo thang | Intercom `search_conversations` | Lọc theo mức ưu tiên hoặc được tag là leo thang |

Chỉ bao gồm nếu connector khả dụng; bỏ phần này hoàn toàn nếu không có.

---

## Quét rủi ro

Chạy song song với các lần lấy chỉ số — không chờ chỉ số hoàn thành trước.

| Rủi ro | Nguồn | Điều kiện kích hoạt |
|---|---|---|
| Công nợ quá hạn | Hóa đơn QuickBooks | Ngày đến hạn > 30 ngày qua, chưa thanh toán |
| Deal đình trệ | HubSpot | Deal đang mở, không có hoạt động 7+ ngày |
| Deal bị trễ | HubSpot | Deal đang mở, ngày đóng đã qua |
| Email Gmail khẩn | Gmail | `is:important` hoặc từ khóa leo thang |
| Thanh toán thất bại | PayPal / Square | Thất bại hoặc đang chờ > 2.000.000đ |

---

## Phân tán song song

Tất cả nội dung trên nên được gọi trong một batch công cụ duy nhất. Một báo cáo đầy đủ thường có 8–15 cuộc gọi song song. Nếu một cuộc gọi bị lỗi, những cuộc còn lại tiếp tục bình thường và nguồn bị lỗi xuất hiện trong phần "Nguồn không khả dụng" ở cuối báo cáo.
