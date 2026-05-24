# Gotchas — phân loại lead

Những lỗi phổ biến khi chấm điểm và ưu tiên lead từ HubSpot. Mỗi mục có ví dụ Sai / Đúng.

---

## 1. Từ "pipeline" mơ hồ kích hoạt chấm điểm đầy đủ khi chủ chỉ muốn tổng quan

**Tại sao quan trọng:** "Pipeline của tôi thế nào?" có thể là hỏi tổng số deal theo giai đoạn, không nhất thiết muốn danh sách gọi điện có chấm điểm.

### ✗ Sai

```
Chủ: "pipeline hôm nay thế nào?"
Claude: [chạy chấm điểm đầy đủ, trả về 12 lead được xếp hạng]
```

### ✓ Đúng

```
Chủ: "pipeline hôm nay thế nào?"
Claude: "Bạn muốn tổng quan nhanh (tổng deal theo giai đoạn + giá trị)
         hay danh sách ưu tiên gọi điện hôm nay?"
```

---

## 2. Dữ liệu tương tác cũ làm phình điểm số

**Tại sao quan trọng:** `hs_email_open` là tích lũy — số lần mở từ chiến dịch một năm trước làm lead lạnh trông nóng bỏng.

### ✗ Sai

```
Lead có 20 lần mở (tất cả từ 11 tháng trước). Điểm engagement 25/25.
Đứng #1 trong danh sách. Chủ gọi điện; lead không nhớ thương hiệu.
```

### ✓ Đúng

```
Chỉ tính tín hiệu tương tác trong 30 ngày gần nhất.
Nếu tất cả tín hiệu cũ hơn 30 ngày, điểm engagement = 0
và ghi chú trong tài liệu trao đổi:
"Tín hiệu tương tác đã cũ (gần nhất: [ngày]) — tiếp cận như cold outreach."
```

---

## 3. Khách hàng hiện tại xuất hiện trong danh sách lead

**Tại sao quan trọng:** Gọi điện cho khách hàng hiện tại như thể họ là prospect mới là xấu hổ và làm mất lòng tin.

### ✗ Sai

```
Không áp dụng bộ lọc vòng đời → khách hàng hiện tại xuất hiện là #2 trong danh sách.
```

### ✓ Đúng

```
Lọc chặt: lifecyclestage = Lead hoặc MQL.
Nếu contact có lifecycle stage trống, vẫn đưa vào nhưng gắn cờ cảnh báo:
"⚠ Chưa gán giai đoạn vòng đời — xác nhận đây là lead trước khi gọi."
```

---

## 4. Đề xuất khung giờ gọi điện trùng với lịch có sẵn

**Tại sao quan trọng:** Đề xuất khung giờ chủ doanh nghiệp đã có cuộc họp khác làm mất uy tín ngay lập tức.

### ✗ Sai

```
Claude đề xuất "Thứ Ba 14:00–14:30" mà không kiểm tra lịch.
Chủ đã có cuộc gọi với khách hàng trong khung giờ đó.
```

### ✓ Đúng

```
Lấy Google Calendar cho 2 ngày làm việc tiếp theo trước khi đề xuất bất kỳ khung giờ nào.
Chỉ đề xuất khoảng trống không có sự kiện ±15 phút buffer.
Nếu không có khung trống, nói rõ và hỏi có muốn tìm thêm ngày xa hơn không.
```

---

## 5. Gửi tin nhắn theo dõi mà không chờ phê duyệt

**Tại sao quan trọng:** Tin nhắn gửi đi không thể thu hồi. Nội dung sai, thời điểm sai, hoặc gửi nhầm người gây hệ quả nghiêm trọng với khách hàng tiềm năng.

### ✗ Sai

```
Đã soạn xong 5 email theo dõi → tự động gửi qua Gmail.
```

### ✓ Đúng

```
Hiển thị bản nháp đầy đủ cho từng lead kèm nút "Gửi" và "Chỉnh sửa".
Chờ chủ doanh nghiệp xác nhận rõ ràng từng email trước khi gửi.
Không bao giờ gom nhóm gửi hàng loạt mà không có xác nhận từng cái.
```
