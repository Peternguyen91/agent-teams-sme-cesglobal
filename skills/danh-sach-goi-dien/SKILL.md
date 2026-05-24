---
name: danh-sach-goi-dien
description: Xếp hạng top lead đáng gọi nhất hôm nay, cung cấp tài liệu trao đổi từ lịch sử email, chặn thời gian trên lịch và soạn tin nhắn theo dõi. Chấp nhận tùy chọn số lượng và ngày cụ thể.
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu HubSpot MCP. Tùy chọn: Gmail MCP để lấy ngữ cảnh email; Google Calendar MCP để đề xuất chặn lịch."
version: "1.1"
---

Chạy phân loại lead ưu tiên. Quét pipeline, xếp hạng theo độ khẩn cấp và cơ hội, lấy thông tin email liên quan, và chuẩn bị để chủ doanh nghiệp thực hiện các cuộc gọi.

Phân tích đối số:
- `--so-luong` (mặc định: `5`) — số lượng lead cần hiển thị (1–10)
- `--ngay` (mặc định: hôm nay) — ngày xây dựng danh sách gọi điện (`YYYY-MM-DD`)

## Bước 1 — Quét pipeline

Sử dụng quy trình kỹ năng `phan-loai-lead`:

1. Lấy deal và liên hệ đang mở trong HubSpot có hoạt động trong 30 ngày qua.
2. Lấy chuỗi email từ hộp thư cho mỗi lead (3 email gần nhất mỗi liên hệ).
3. Chấm điểm mỗi lead theo:
   - **Gần đây**: số ngày kể từ lần chủ doanh nghiệp liên hệ cuối (ít hơn = tốt hơn)
   - **Giai đoạn**: càng gần chốt đơn càng ưu tiên cao
   - **Tín hiệu**: có hoạt động inbound gần đây không (mở email, trả lời, giữ lịch, thăm website)
   - **Giá trị**: quy mô deal từ HubSpot

---

## Bước 2 — Xếp hạng và chọn top N

Xếp hạng tất cả lead được chấm điểm và chọn top `--so-luong`. Nếu hòa, ưu tiên lead có tín hiệu inbound chưa được phản hồi.

Với mỗi lead được chọn, tạo thẻ gọi điện:

```
{Thứ hạng}. {Tên liên hệ} — {Công ty}
Deal: {số tiền} triệu | Giai đoạn: {giai đoạn} | Liên hệ cuối: {X ngày trước}
Tín hiệu: {hoạt động gần nhất}

TÀI LIỆU TRAO ĐỔI
• {điểm từ ngữ cảnh email/deal}
• {điểm từ ngữ cảnh email/deal}
• {câu hỏi mở cần hỏi}

MỤC TIÊU CUỘC GỌI NÀY: {một câu — tiến sang giai đoạn tiếp / tái kết nối / chốt đơn}
```

---

## Bước 3 — Chặn lịch

Với mỗi lead trong danh sách, đề xuất chặn 20 phút trên lịch của chủ doanh nghiệp cho ngày mục tiêu.

Hiển thị các mục lịch được đề xuất:
```
{khung giờ} — Gọi: {Tên liên hệ} ({Công ty})
```

Chờ chủ doanh nghiệp xác nhận cuộc gọi nào cần chặn trước khi tạo sự kiện lịch.

---

## Bước 4 — Soạn tin nhắn theo dõi

Với bất kỳ lead nào có email chưa được trả lời quá 3 ngày, soạn tin nhắn theo dõi ngắn gọn:

```
Tiêu đề: Re: {tiêu đề chuỗi email}

Chào {tên},

{Một câu nhắc lại cuộc trò chuyện trước}. {Một câu với bước tiếp theo rõ ràng hoặc câu hỏi cụ thể}.

{Lời kết}
```

---

## Xử lý khi connector lỗi

Nếu HubSpot không kết nối được, dừng lại và thông báo cho chủ doanh nghiệp — chấm điểm lead cần dữ liệu CRM. Nếu hộp thư không kết nối được, bỏ qua Bước 3–4 (ngữ cảnh email và soạn tin theo dõi) và ghi chú. Nếu Google Calendar không kết nối được, bỏ qua chặn lịch và ghi chú.

---

## Cổng phê duyệt

- **Không bao giờ tự gửi email.** Chỉ trình bày bản thảo để chủ doanh nghiệp phê duyệt.
- **Không bao giờ tự tạo lịch** mà không có xác nhận — hiển thị danh sách đề xuất trước.
- **Không bao giờ cập nhật giai đoạn deal trong HubSpot tự động.**

---

## Kết quả đầu ra

Trình bày danh sách gọi điện được xếp hạng kèm tài liệu trao đổi. Rồi hiển thị đề xuất chặn lịch và hỏi xác nhận. Rồi hiển thị bản thảo tin theo dõi và hỏi cái nào cần gửi.

## Ví dụ câu kích hoạt

- *"Danh sách gọi điện hôm nay"*
- *"Gọi cho ai hôm nay?"*
- *"Top lead cần liên hệ ngay"*
- *"Chuẩn bị danh sách gọi điện"*
