---
name: phan-loai-lead
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu HubSpot MCP. Tùy chọn: Gmail MCP để soạn tin nhắn theo dõi; Google Calendar MCP để đề xuất khung giờ gọi điện."
version: "1.1"
description: >
  Chấm điểm lead inbound từ HubSpot theo tín hiệu tương tác, mức độ phù
  hợp với khách hàng lý tưởng, và mức độ khẩn cấp để tạo ra danh sách
  "gọi 5 người này hôm nay" kèm tài liệu trao đổi, soạn tin nhắn theo dõi
  và đề xuất khung giờ trên lịch. Sử dụng khi chủ doanh nghiệp hỏi cần ưu
  tiên lead nào, gọi cho ai trước, hoặc về pipeline bán hàng.
---

# Phân Loại Lead

Lấy lead inbound từ HubSpot, chấm điểm và đưa ra danh sách gọi điện được xếp hạng kèm tài liệu trao đổi. Soạn tin nhắn theo dõi và đề xuất khung giờ — không bao giờ gửi hoặc đặt lịch mà không có phê duyệt từ chủ doanh nghiệp.

```
Ví dụ: "ưu tiên lead cho tôi"
→ Lấy liên hệ: giai đoạn vòng đời Lead hoặc MQL, trạng thái ≠ Không đủ điều kiện
→ Chấm điểm theo tương tác, mức phù hợp, khẩn cấp, gần đây
→ Trả về danh sách được xếp hạng kèm tài liệu trao đổi
→ Đề xuất soạn tin nhắn theo dõi và khung giờ gọi điện
```

---

## Quy trình thực hiện

### Bước 1 — Lấy lead từ HubSpot

Lấy liên hệ có `giai_doan_vong_doi` = `Lead` hoặc `MQL` và `trang_thai_lead` ≠ `Không đủ điều kiện`.

Nếu HubSpot không kết nối được, dừng lại: *"HubSpot chưa được kết nối — hãy kết nối và thử lại."*

---

### Bước 2 — Xác nhận nếu yêu cầu mơ hồ

Nếu người dùng chỉ nói "pipeline" mà không rõ ràng hơn, hỏi: *"Bạn muốn xem tổng quan pipeline (giai đoạn deal + tổng giá trị) hay danh sách gọi điện ưu tiên?"* — rồi xử lý theo câu trả lời.

Không chấm điểm lead khi chỉ nghe từ "pipeline" chung chung.

---

### Bước 3 — Chấm điểm từng lead

Áp dụng mô hình 4 chiều:

- **Tương tác** — email trả lời, mở email, lượt thăm website trong HubSpot (30 ngày gần nhất)
- **Mức phù hợp** — ngành và quy mô công ty so với khách hàng lý tưởng của chủ doanh nghiệp
- **Mức khẩn cấp** — tuổi lead, thời gian ở giai đoạn hiện tại, ghi chú chứa từ khóa "gấp / ASAP / deadline / đã có ngân sách"
- **Phạt gần đây** — trừ điểm nếu hoạt động cuối cùng dưới 24 giờ (đã tiếp cận hôm nay rồi)

---

### Bước 4 — Xây dựng danh sách xếp hạng

Sắp xếp giảm dần theo điểm tổng hợp. Kích thước danh sách tự động điều chỉnh:
- ≤10 lead → hiển thị tất cả
- 11–30 lead → hiển thị top 5
- >30 lead → hiển thị top 8

Với mỗi lead: tên, công ty, điểm, một đoạn tài liệu trao đổi, tóm tắt hoạt động gần nhất.

Nếu tất cả tín hiệu tương tác đều >30 ngày, gắn cờ: *"Tín hiệu tương tác đã cũ — tiếp cận theo hướng cold outreach."*

---

### Bước 5 — Đề xuất soạn tin nhắn theo dõi

Hỏi: *"Bạn muốn tôi soạn tin nhắn theo dõi cho lead nào không?"*

Nếu có, viết một email mỗi lead được chọn, khớp tone với email đã gửi gần nhất trong lịch sử. Hiển thị để xem — không gửi.

---

### Bước 6 — Đề xuất khung giờ gọi điện

Hỏi: *"Bạn muốn tôi đề xuất khung giờ để gọi cho ai không?"*

Nếu có, kiểm tra lịch để tìm khung 30 phút trống trong 2 ngày làm việc tới (tránh ±15 phút xung quanh sự kiện đã có). Đề xuất 2 lựa chọn mỗi lead.

**Không tự tạo sự kiện lịch** — chủ doanh nghiệp tự đặt.

---

## Cổng phê duyệt

- **Không bao giờ gửi email.** Chỉ soạn thảo; chủ doanh nghiệp gửi từ hộp thư của họ.
- **Không bao giờ tự tạo sự kiện lịch.** Chỉ đề xuất khung giờ; chủ doanh nghiệp tự đặt.
- **Không bao giờ thay đổi giai đoạn vòng đời hoặc đánh dấu lead "Không đủ điều kiện"** trừ khi chủ doanh nghiệp yêu cầu rõ ràng.
- **Không bao giờ đưa liên hệ có giai đoạn "Khách hàng" hoặc "Người ủng hộ"** vào danh sách lead.
- **Nếu không có lead nào khớp bộ lọc**, giải thích lý do và đề xuất kiểm tra xem những giai đoạn vòng đời nào đang có — không bịa danh sách.

## Ví dụ câu kích hoạt

- *"Ưu tiên lead cho tôi"*
- *"Gọi cho ai trước hôm nay?"*
- *"Pipeline của tôi thế nào?"*
- *"Lead nào đáng theo đuổi nhất?"*
