# Gotchas — tạo ảnh Canva

Những lỗi phổ biến khi tạo campaign nội dung với Canva MCP. Mỗi mục có ví dụ Sai / Đúng.

---

## 1. Tạo thiết kế trước khi duyệt lịch đăng

**Tại sao quan trọng:** Nếu lịch thay đổi sau khi thiết kế đã tạo (đổi ngày, đổi kênh, bỏ bài nào đó), toàn bộ công tạo ảnh bị lãng phí — đây là nguồn lãng phí lớn nhất trong quy trình.

### ✗ Sai

> Kế hoạch nội dung đã có, bắt đầu tạo thiết kế Canva ngay để tiết kiệm thời gian.

### ✓ Đúng

Luôn trình bày lịch đăng đầy đủ (Điểm kiểm tra 1) và chờ chủ doanh nghiệp phê duyệt trước khi gọi bất kỳ lệnh API Canva nào. Lịch được duyệt = cam kết không thay đổi kênh và ngày đăng.

---

## 2. Gọi Canva API cho bài email

**Tại sao quan trọng:** Canva tạo ảnh, không tạo email HTML. Gọi Canva cho bài email là lỗi luồng — lãng phí API call và tạo ra tài sản sai định dạng.

### ✗ Sai

> Lịch có 6 bài mạng xã hội và 2 email — tạo thiết kế Canva cho cả 8 bài.

### ✓ Đúng

Kiểm tra cột "Đường dẫn" trước mỗi lệnh API. Chỉ gọi Canva cho các dòng có `Canva (MXH)`. Bài email soạn dạng văn bản thuần trong Giai đoạn 4, không bao giờ dùng Canva.

---

## 3. Không kiểm kê tài sản trước khi tạo template nhiều ô ảnh

**Tại sao quan trọng:** Template carousel 5 ô với chỉ 1 ảnh sẽ hiển thị 4 ô placeholder mặc định — kết quả trông thiếu chuyên nghiệp và phải làm lại từ đầu.

### ✗ Sai

> Kế hoạch chỉ cung cấp 1 ảnh sản phẩm — tạo template carousel 5 ảnh và để Canva tự điền.

### ✓ Đúng

Thực hiện Giai đoạn 2 (Kiểm kê tài sản) đầy đủ trước khi tạo thiết kế. Với mỗi ô ảnh trong template, xác nhận tài sản có sẵn hoặc giải quyết thiếu sót với chủ doanh nghiệp. Không bỏ qua bước này kể cả khi "chỉ có 1–2 bài đơn giản".

---

## 4. Tạo song song nhiều bài cùng lúc ở Giai đoạn 3

**Tại sao quan trọng:** Canva API có giới hạn 100 request/phút. Gửi nhiều bài song song có thể kích hoạt rate limit, khiến một số bài thành công và một số thất bại — tạo ra trạng thái không nhất quán khó debug.

### ✗ Sai

> Có 6 bài cần tạo — gửi tất cả 6 lệnh tạo thiết kế song song để nhanh hơn.

### ✓ Đúng

Tạo từng bài một theo vòng lặp, dừng 30 giây giữa các bài. Ứng viên trong cùng một bài có thể tạo song song, nhưng các bài phải tuần tự. Nếu bị rate limit, thông báo rõ tình trạng và hỏi chủ doanh nghiệp muốn xử lý thế nào.

---

## 5. Đăng trực tiếp lên mạng xã hội thay vì đặt lịch

**Tại sao quan trọng:** Bài đăng trực tiếp không thể thu hồi nếu có lỗi về nội dung, thời điểm, hoặc hình ảnh. Chủ doanh nghiệp mất quyền kiểm soát thời điểm nội dung xuất hiện.

### ✗ Sai

> Lịch đăng đã duyệt, thiết kế đã xong — đăng trực tiếp lên Facebook và Instagram ngay bây giờ.

### ✓ Đúng

Tất cả bài đăng trong HubSpot đều đặt trạng thái `ĐẶT LỊCH` (scheduled), không bao giờ `ĐÃ ĐĂNG` (published). Chủ doanh nghiệp quyết định thời điểm live bằng cách xem xét hàng đợi trong HubSpot. Đây là quy tắc tuyệt đối không có ngoại lệ.
