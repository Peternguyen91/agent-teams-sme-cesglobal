---
name: do-nhiet-do-khach-hang
description: >
  Tổng hợp tranh chấp PayPal, phản hồi và ticket HubSpot, luồng email tiêu
  cực (và đánh giá Google/Yelp nếu được dán vào) thành báo cáo theo chủ đề
  với trích dẫn nguyên văn và danh sách "làm 3 việc này tuần này". Kích hoạt
  khi: "khách hàng đang nghĩ gì", "phân tích đánh giá", "khách hàng đang
  phàn nàn về gì", "có tranh chấp nào không".
---

# Đo Nhiệt Độ Khách Hàng

## Khởi động nhanh

Hỏi: *"Khách hàng đang cảm thấy thế nào tháng này?"*

Claude tổng hợp tranh chấp, ticket, luồng email và hội thoại trong 30 ngày qua, nhóm thành 3–5 chủ đề với bằng chứng nguyên văn, và đưa ra danh sách "làm 3 việc này tuần này".

Để bao gồm đánh giá Google/Yelp, dán chúng vào sau khi kích hoạt — hoặc nói "Tôi có thêm một số đánh giá".

---

## Quy trình thực hiện

### Bước 1 — Xác định cửa sổ thời gian

Mặc định: 30 ngày qua. Nếu người dùng chỉ định phạm vi cụ thể, sử dụng phạm vi đó.

---

### Bước 2 — Lấy tranh chấp PayPal

Lấy tranh chấp được mở trong cửa sổ thời gian. Nếu PayPal trả về lỗi giới hạn tốc độ: bỏ qua và thêm `PayPal: bị giới hạn tốc độ — không được bao gồm` vào phần Nguồn. Không thử lại; không báo lỗi. Tiếp tục với các nguồn còn lại.

---

### Bước 3 — Lấy ticket và phản hồi HubSpot

Lấy ticket đang mở và đã đóng gần đây. Nếu có 0 ticket: ghi lại `HubSpot ticket: 0` và tiếp tục — không hiển thị cảnh báo.

---

### Bước 4 — Lấy luồng Gmail

Tìm kiếm luồng email trong cửa sổ thời gian chứa các từ khóa: `hoàn tiền hủy không hài lòng vấn đề sự cố thất vọng bực bội hỏng trễ chậm sai thiếu`. Trích xuất dòng tiêu đề và 1–2 câu tóm tắt mỗi luồng.

---

### Bước 5 — Lấy hội thoại Intercom (nếu kết nối)

Gọi `search_conversations` để lấy hội thoại đang mở và đã đóng gần đây. Sau đó gọi `get_conversation` cho từng ID hội thoại để truy cập đầy đủ `conversation_parts`. Chỉ trích xuất phần có `author.type === 'user'` — đây là tin nhắn của khách hàng. Loại bỏ phần có `author.type` là `admin` hoặc `bot`.

---

### Bước 6 — Nhận đánh giá được dán (tùy chọn)

Nếu người dùng dán văn bản đánh giá Google hoặc Yelp, bao gồm vào nhóm nguồn được gắn thẻ `[Đánh giá]`. Không cần connector.

---

### Bước 7 — Trích xuất chủ đề

Nhóm tất cả bằng chứng thành 3–5 chủ đề lặp lại. Mỗi chủ đề phải bao gồm:
- Một câu nhãn (ví dụ: "Giao hàng chậm gây phàn nàn lặp lại")
- 2–3 trích dẫn **nguyên văn** với thẻ nguồn: `[PayPal]`, `[HubSpot]`, `[Gmail]`, `[Intercom]`, hoặc `[Đánh giá]`
- Số lượng tín hiệu (bao nhiêu mục liên quan đến chủ đề này)

**Trích dẫn nguyên văn là bắt buộc** — không bao giờ diễn giải lại lời khách hàng. Từ ngữ chính xác là bằng chứng quan trọng nhất.

---

### Bước 8 — Tạo danh sách "làm 3 việc này"

Xếp hạng chủ đề theo số lượng tín hiệu. Chọn top 3 và viết một bước hành động cụ thể cho chủ doanh nghiệp mỗi chủ đề. Định dạng danh sách đánh số.

---

### Bước 9 — Trình bày báo cáo

Cấu trúc đầu ra theo thứ tự:

**Tiêu đề** — H2 với "Nhiệt Độ Khách Hàng" và phạm vi ngày.

**Nguồn đã thu thập** — Danh sách gạch đầu dòng với số lượng tín hiệu mỗi nguồn (tranh chấp PayPal, ticket HubSpot, luồng Gmail, hội thoại Intercom, đánh giá được dán). Ghi chú nguồn nào bị giới hạn tốc độ và bị bỏ qua.

**Chủ đề** — Với mỗi chủ đề: nhãn in đậm kèm số tín hiệu, theo sau là hai trích dẫn nguyên văn dạng blockquote, mỗi trích dẫn ghi rõ nguồn.

**Làm 3 việc này tuần này** — Danh sách đánh số gồm 3 bước cụ thể, mỗi bước gắn với một chủ đề hàng đầu.

---

## Cổng phê duyệt

Kỹ năng này **chỉ đọc** — không đăng, gửi, trả lời, hoặc chỉnh sửa bất kỳ bản ghi nào. Không cần cổng phê duyệt.

---

## Ví dụ câu kích hoạt

- *"Khách hàng đang cảm thấy thế nào?"*
- *"Phân tích đánh giá của khách cho tôi"*
- *"Có bao nhiêu tranh chấp tháng này?"*
- *"Khách hàng đang phàn nàn về điều gì?"*
- *"Kiểm tra mạch đập khách hàng tháng này"*
- *"Tổng hợp phản hồi khách 30 ngày qua"*
