# Gotchas — chạy campaign

Những lỗi phổ biến khi chạy toàn bộ pipeline campaign end-to-end. Mỗi mục có ví dụ Sai / Đúng.

---

## 1. Tiếp tục sang bước tiếp theo mà không chờ phê duyệt

**Tại sao quan trọng:** Pipeline campaign có 3 giai đoạn (phân tích bán hàng → tạo ảnh Canva → lên lịch HubSpot). Tiếp tục tự động từ giai đoạn này sang giai đoạn khác mà không có "đã duyệt" rõ ràng dẫn đến lãng phí công sức lớn nếu chủ muốn thay đổi.

### ✗ Sai

> Kế hoạch nội dung đã được tạo → tự động chuyển sang tạo ảnh Canva.

### ✓ Đúng

Dừng sau mỗi giai đoạn và chờ xác nhận rõ ràng: "Kế hoạch nội dung đã sẵn sàng ở trên. Nếu bạn đã duyệt, gõ 'đã duyệt, tạo ảnh đi' để tiếp tục Giai đoạn 2." Không bao giờ tự động tiến sang bước tiếp theo.

---

## 2. Chạy campaign với khoảng thời gian nhìn lại mặc định mà không kiểm tra phù hợp

**Tại sao quan trọng:** Mặc định 90 ngày nhìn lại dữ liệu bán hàng phù hợp với hầu hết trường hợp, nhưng nếu doanh nghiệp vừa thay đổi sản phẩm hay giá, dữ liệu 90 ngày cũ có thể không phản ánh thực tế hiện tại.

### ✗ Sai

> Luôn dùng --nhin-lai 90d mà không hỏi.

### ✓ Đúng

Nếu người dùng không chỉ định khoảng thời gian, hỏi nhanh: "Bạn muốn tôi phân tích dữ liệu bán hàng 30, 60, hay 90 ngày gần nhất?" Chỉ dùng mặc định 90 ngày nếu chủ xác nhận hoặc không có ý kiến gì.

---

## 3. Trộn lẫn nội dung email và nội dung mạng xã hội trong cùng thiết kế Canva

**Tại sao quan trọng:** Canva tạo ảnh cho mạng xã hội. Email dùng văn bản thuần. Gọi Canva API cho email là lãng phí và tạo ra tài sản sai định dạng.

### ✗ Sai

> Lịch có 4 bài MXH và 2 email → tạo Canva design cho cả 6 bài.

### ✓ Đúng

Phân loại rõ từng bài trong lịch: `Canva (MXH)` hay `Email (văn bản)`. Chỉ gọi Canva API cho các dòng `Canva (MXH)`. Bài email soạn văn bản thuần trong Giai đoạn 3, không bao giờ dùng Canva.

---

## 4. Bỏ qua kênh đã chọn khi phân tích dữ liệu bán hàng

**Tại sao quan trọng:** Nếu chủ chọn `--kenh email`, kế hoạch nội dung chỉ nên gồm email — không thêm bài MXH. Ngược lại sẽ tạo công việc thừa ở các giai đoạn sau.

### ✗ Sai

> `--kenh email` được chỉ định → vẫn tạo kế hoạch 4 bài MXH + 2 email.

### ✓ Đúng

Đọc đối số `--kenh` ngay ở Bước 1 và xây dựng toàn bộ kế hoạch nội dung chỉ theo kênh đó. Khi `--kenh ca-hai`, lịch cần có cả email lẫn MXH với tỷ lệ phù hợp.

---

## 5. Lên lịch HubSpot với trạng thái "đã đăng" thay vì "đặt lịch"

**Tại sao quan trọng:** Bài đăng trực tiếp không thể thu hồi. Chủ doanh nghiệp mất quyền kiểm soát thời điểm nội dung xuất hiện.

### ✗ Sai

> Thiết kế đã xong, lịch đã duyệt → set trạng thái `PUBLISHED` trong HubSpot.

### ✓ Đúng

Tất cả bài trong HubSpot đều set trạng thái `SCHEDULED`. Chủ doanh nghiệp tự quyết định khi nào publish bằng cách xem xét hàng đợi trong HubSpot. Đây là quy tắc tuyệt đối không có ngoại lệ.
