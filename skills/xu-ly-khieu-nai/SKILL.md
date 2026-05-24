---
name: xu-ly-khieu-nai
description: >
  Đọc email hoặc tin nhắn khiếu nại từ khách hàng, tra cứu trạng thái đơn
  hàng từ PayPal và lịch sử tài khoản từ HubSpot, soạn thảo phản hồi phù hợp
  giọng văn của chủ doanh nghiệp, và có thể hoàn tiền qua PayPal khi được
  phê duyệt rõ ràng. Kích hoạt khi: "soạn phản hồi khách hàng", "trả lời
  khách này", "đơn hàng ở đâu", "khách muốn hoàn tiền".
compatibility: "Cần PayPal, HubSpot, Gmail. Tùy chọn: Intercom, Square."
---

# Xử Lý Khiếu Nại

## Khởi động nhanh

Chuyển tiếp hoặc dán email khách hàng — Claude tra cứu trạng thái đơn hàng từ PayPal, xem lịch sử khách trong HubSpot, và soạn phản hồi theo giọng văn của chủ doanh nghiệp. Nếu cần hoàn tiền, Claude trình bày chi tiết và chờ phê duyệt rõ ràng trước khi thực hiện bất cứ điều gì.

```
Ví dụ: "Trả lời khách hàng này" [chuyển tiếp email]
→ Trích xuất email + vấn đề từ chuỗi thư
→ Tra cứu trạng thái giao dịch PayPal
→ Xem lịch sử khách trong HubSpot
→ Soạn phản hồi theo giọng văn chủ doanh nghiệp
→ Chủ phê duyệt → gửi hoặc lưu bản nháp
→ Nếu cần hoàn tiền: hiển thị xác nhận → chủ xác nhận → thực hiện
```

---

## Quy trình thực hiện

### Bước 1 — Đọc tin nhắn khách hàng

Nhận chuỗi Gmail được chuyển tiếp hoặc văn bản dán trực tiếp. Trích xuất: địa chỉ email khách, tên khách, mã đơn hàng hoặc giao dịch (nếu có), và vấn đề cốt lõi — yêu cầu hoàn tiền, hỏi trạng thái đơn hàng, hoặc khiếu nại chung. Nếu có nhiều vấn đề, xử lý theo thứ tự xuất hiện.

---

### Bước 2 — Tra cứu trạng thái đơn hàng từ PayPal

Tìm giao dịch PayPal theo email hoặc mã giao dịch khách cung cấp. Ghi lại: số tiền, ngày, trạng thái, và xem đã hoàn tiền chưa. Nếu PayPal chưa kết nối, ghi chú vào bản thảo và tiếp tục.

**Giới hạn tốc độ PayPal:**
- Nếu khách cung cấp mã giao dịch cụ thể: dùng mã đó — tra cứu từng bản ghi tránh bị throttle
- Nếu tìm theo email: dùng cửa sổ 7 ngày (không phải 30 ngày) — endpoint danh sách giao dịch của PayPal bị throttle nặng với phạm vi ngày rộng
- Nếu nhiều giao dịch khớp: hiển thị tất cả và để chủ doanh nghiệp chọn trước khi soạn thảo

**Nguồn bổ sung:**
- Nếu Intercom kết nối: kiểm tra ticket hỗ trợ đang mở của khách này
- Nếu Square kết nối: kiểm tra lịch sử giao dịch Square làm nguồn phụ

Nếu không tìm được giao dịch nào khớp: đánh dấu trong bản thảo — **không đoán mò**.

---

### Bước 3 — Tra cứu lịch sử khách từ HubSpot

Tìm liên hệ theo địa chỉ email. Lấy: giai đoạn vòng đời, ghi chú, deal đang mở, và hoạt động gần đây. Nếu không tìm được liên hệ, ghi chú và đề xuất tạo mới **sau** khi gửi phản hồi — không tạo trong luồng xử lý khiếu nại này.

---

### Bước 4 — Soạn phản hồi

Viết theo giọng văn của chủ doanh nghiệp. Điều chỉnh tông phù hợp với loại vấn đề:
- **Yêu cầu hoàn tiền** → đồng cảm, rõ ràng, định hướng hành động
- **Hỏi trạng thái đơn hàng** → thực tế, trấn an
- **Khiếu nại chung** → ghi nhận, giải thích, đề xuất giải pháp

Nếu có khoảng trống dữ liệu, đánh dấu trực tiếp trong bản thảo bằng ghi chú trong ngoặc vuông (ví dụ: *[Lưu ý: Không tìm thấy giao dịch PayPal — xác minh mã đơn hàng trước khi gửi]*) để chủ doanh nghiệp thấy trước khi gửi.

**Không bao giờ bịa đặt thông tin đơn hàng.** Nếu PayPal không có dữ liệu, nói rõ trong bản thảo.

---

### Bước 5 — Cổng phê duyệt: chủ doanh nghiệp xem xét bản thảo

Trình bày toàn bộ bản thảo. **Không gửi hoặc lưu nháp cho đến khi chủ doanh nghiệp phê duyệt.** Chủ doanh nghiệp có thể chỉnh sửa tự do trước khi phê duyệt.

---

### Bước 6 — Cổng phê duyệt: hoàn tiền (nếu cần)

Nếu cần hoàn tiền, hiển thị lời xác nhận riêng sau khi chủ phê duyệt bản thảo:

> *"Hoàn tiền [số tiền] cho [tên khách] ([email]) giao dịch [ID]? Trả lời Đồng ý để tiến hành."*

Chờ xác nhận rõ ràng. Nếu câu trả lời của chủ không phải là đồng ý rõ ràng, dừng lại và hỏi họ muốn làm gì.

---

### Bước 7 — Gửi hoặc lưu bản thảo

Sau khi phê duyệt bản thảo, hỏi chủ doanh nghiệp: gửi qua Gmail ngay, hay lưu làm bản nháp? Thực hiện theo lựa chọn. Sau đó ghi nhật ký tương tác vào dòng thời gian liên hệ HubSpot.

---

### Bước 8 — Báo cáo

Một đoạn ngắn: đã gửi hay lưu nháp phản hồi, đã hoàn tiền hay chưa, đã ghi ghi chú HubSpot.

---

## Cổng phê duyệt

- **Không bao giờ hoàn tiền PayPal mà không có xác nhận rõ ràng từ chủ doanh nghiệp** — luôn hiển thị số tiền, tên khách, email và ID giao dịch trước khi thực hiện.
- **Không bao giờ gửi phản hồi mà không có chủ doanh nghiệp xem xét.** Luôn trình bày bản thảo đầy đủ trước.
- **Không bao giờ tạo liên hệ HubSpot trong luồng xử lý.** Đề xuất sau khi hoàn thành phản hồi.
- **Không bao giờ tự chọn giao dịch PayPal.** Nếu nhiều giao dịch khớp, hiển thị tất cả và để chủ doanh nghiệp chọn.
- **Không bao giờ bịa đặt thông tin đơn hàng.** Nếu PayPal không có dữ liệu, nói thẳng trong bản thảo.

---

## Ví dụ câu kích hoạt

- *"Trả lời khách hàng này cho tôi"*
- *"Soạn phản hồi cho email khiếu nại này"*
- *"Đơn hàng của khách ở đâu rồi?"*
- *"Khách muốn hoàn tiền, xử lý giúp tôi"*
- *"Khách hàng không hài lòng, tôi cần phản hồi"*
