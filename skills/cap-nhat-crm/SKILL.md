---
name: cap-nhat-crm
description: >
  Giữ HubSpot luôn cập nhật mà không cần chủ doanh nghiệp phải mở ứng dụng:
  tạo và cập nhật liên hệ/deal từ ngữ cảnh email và lịch, ghi chú cuộc gọi
  và cuộc họp, đánh dấu hồ sơ lỗi thời. Kỹ năng "không cần nhập dữ liệu
  thủ công". Sử dụng khi người dùng muốn cập nhật CRM, ghi nhật ký cuộc
  gọi, dọn dẹp HubSpot, hoặc thêm ngữ cảnh vào một deal.
---

# Cập Nhật CRM

Lấy ngữ cảnh từ email hoặc sự kiện lịch được đề cập, tìm đúng liên hệ và deal trong HubSpot, ghi lại hoạt động, và báo cáo những gì đã thay đổi.

```
Ví dụ: "ghi cuộc gọi này vào deal Công ty A"
→ Đọc sự kiện lịch hoàn thành gần nhất
→ Xác nhận người tham dự khớp với liên hệ của deal Công ty A
→ Ghi hoạt động cuộc gọi vào deal Công ty A
→ Báo cáo: "Đã ghi cuộc gọi vào Deal Mở Rộng Q2 của Công ty A."
```

---

## Quy trình thực hiện

### Bước 1 — Xác định ý định

Xác định đường dẫn nào phù hợp từ tin nhắn và ngữ cảnh của người dùng:

- **Đường dẫn Email** — "cập nhật CRM của tôi", "thêm vào deal", hoặc bất kỳ đề cập nào đến chuỗi email
- **Đường dẫn Cuộc gọi** — "ghi cuộc gọi này", "ghi cuộc họp", hoặc đề cập đến sự kiện lịch
- **Đường dẫn Dọn dẹp** — "dọn dẹp HubSpot", "deal này có cập nhật không", hoặc yêu cầu kiểm tra một deal cụ thể

Nếu ý định mơ hồ (ví dụ: "cập nhật HubSpot" mà không đề cập email/cuộc họp/deal cụ thể), hỏi đường dẫn nào trước khi tiến hành.

---

### Bước 2 — Thu thập ngữ cảnh

- **Đường dẫn Email:** đọc chuỗi (tiêu đề, người tham gia, 1–3 tin nhắn gần nhất). Xác định liên hệ bên ngoài chính.
- **Đường dẫn Cuộc gọi:** đọc sự kiện lịch (tiêu đề, người tham dự, thời gian, mô tả). Nếu không có sự kiện cụ thể, dùng cuộc họp hoàn thành gần nhất trong 24 giờ qua và xác nhận với người dùng trước khi tiến hành.
- **Đường dẫn Dọn dẹp:** lấy deal (giai đoạn, số tiền, ngày đóng, bước tiếp theo, liên hệ liên kết, hoạt động trong 60 ngày qua), cộng với 14 ngày chuỗi email và sự kiện lịch liên quan đến liên hệ của deal.

---

### Bước 3 — Tìm liên hệ và deal HubSpot

Với đường dẫn Email/Cuộc gọi:

- Tìm liên hệ HubSpot theo địa chỉ email. Nếu thiếu, tạo từ chữ ký email hoặc dữ liệu lời mời lịch — **thông báo trong chat trước khi ghi**.
- Tìm deal theo thứ tự: (a) khớp rõ ràng nếu người dùng đặt tên, (b) deal mở duy nhất của liên hệ, (c) khớp mờ theo chuỗi email/tiêu đề cuộc họp — xác nhận trước khi ghi, (d) hỏi người dùng nếu không khớp.
- **Không bao giờ tự tạo deal mới.**

---

### Bước 4 — Thực hiện hành động

- **Đường dẫn Email:** ghi hoạt động email với tiêu đề chuỗi là tên và tóm tắt ngắn gọn (không phải toàn bộ chuỗi) làm nội dung. Timestamp theo tin nhắn mới nhất.
- **Đường dẫn Cuộc gọi:** ghi hoạt động cuộc gọi với tiêu đề sự kiện, thời lượng và ghi chú nếu có. Timestamp theo thời gian bắt đầu sự kiện.
- **Đường dẫn Dọn dẹp:** kiểm tra từng trường và lập danh sách thay đổi được đề xuất. Hiển thị hiện tại → đề xuất song song. Chỉ ghi những gì người dùng phê duyệt.

---

### Bước 5 — Cổng phê duyệt

- Với tạo liên hệ và ghi hoạt động: thông báo trước khi ghi và hiển thị kết quả sau.
- Với chỉnh sửa dọn dẹp: không ghi bất cứ điều gì cho đến khi người dùng phê duyệt từng thay đổi cụ thể.

---

### Bước 6 — Báo cáo kết quả

Thông báo những gì đã ghi và những gì còn chờ. Kèm link HubSpot đến deal bị ảnh hưởng khi có thể. Giữ ngắn gọn.

---

## Cổng phê duyệt

- **Không bao giờ xóa hồ sơ.** Không xóa liên hệ, deal, hoặc hoạt động. Nếu người dùng yêu cầu, nói kỹ năng này không thể và hướng dẫn họ vào HubSpot.
- **Không bao giờ thay đổi giai đoạn deal hoặc đóng deal** mà không có phê duyệt rõ ràng. Đánh dấu và để chủ doanh nghiệp quyết định.
- **Không bao giờ tự tạo deal mới.** Hỏi nếu không tìm được deal phù hợp.
- **Thông báo trước khi tạo liên hệ mới.** Một dòng — để chủ doanh nghiệp kiểm tra lỗi hoặc trùng lặp.
- **So sánh song song khi dọn dẹp.** Hiển thị giá trị hiện tại và giá trị đề xuất; chờ phê duyệt từng mục.

## Ví dụ câu kích hoạt

- *"Cập nhật CRM từ email này"*
- *"Ghi cuộc họp hôm nay vào HubSpot"*
- *"Thêm ngữ cảnh vào deal Công ty B"*
- *"Deal này có cập nhật gì không?"*
- *"Đừng để tôi phải nhập dữ liệu thủ công nữa"*
