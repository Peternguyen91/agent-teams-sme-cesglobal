# Gotchas — đóng sổ cuối tháng

Những lỗi phổ biến và trường hợp ngoại lệ khi đóng sổ cuối tháng. Mỗi mục nêu rõ vấn đề, tại sao quan trọng, và ví dụ Sai / Đúng.

---

## Gotcha: Đánh dấu giao dịch split là trùng lặp

**Tại sao quan trọng:** Một lần mua hàng được chia nhỏ sang nhiều danh mục GL sẽ xuất hiện nhiều dòng trong QuickBooks — cùng nhà cung cấp, cùng ngày, khác số tiền. Đánh dấu là trùng lặp sẽ khiến chủ doanh nghiệp mất công điều tra vô ích.

### ✗ Sai

> Đánh dấu trùng: VP Văn Phòng Phẩm 475.000đ ngày 12/3 và VP Văn Phòng Phẩm 625.000đ ngày 12/3 — cùng nhà cung cấp, cùng ngày.

Hai dòng này cùng `TxnID` — đây là split của giao dịch 1.100.000đ chia sang "Văn phòng phẩm" và "Thiết bị".

### ✓ Đúng

Trước khi đánh dấu trùng lặp, nhóm các dòng theo `TxnID`. Chỉ so sánh các giao dịch có ID khác nhau. Các dòng split trong cùng một giao dịch không bao giờ là trùng lặp.

---

## Gotcha: Nhầm hoàn tiền là giao dịch thiếu

**Tại sao quan trọng:** Hoàn tiền qua PayPal xuất hiện dưới dạng giao dịch âm trong báo cáo quyết toán. Nếu xử lý như luồng tiền ra chưa khớp, sẽ đánh dấu một khoản hoàn tiền hợp lệ là vấn đề.

### ✗ Sai

> Cảnh báo: Luồng ra PayPal –890.000đ ngày 18/3 không có khoản nào khớp trong QB. Có thể thiếu giao dịch.

Khoản –890.000đ là hoàn tiền cho khách. Nó phải khớp với ghi chú tín dụng trong QB, không phải với khoản nạp tiền.

### ✓ Đúng

Tách luồng vào (dương) với luồng ra (âm) trước khi đối chiếu. Khớp số âm từ bộ xử lý thanh toán với ghi chú tín dụng hoặc giao dịch hoàn tiền trong QB. Chỉ cảnh báo khoản âm chưa khớp khi không có ghi chú tín dụng tương ứng trong QB.

---

## Gotcha: So sánh số tiền gộp PayPal với số tiền ròng QB

**Tại sao quan trọng:** QuickBooks thường ghi nhận số tiền nạp vào ngân hàng ròng (sau phí PayPal), nhưng báo cáo giao dịch PayPal hiển thị số tiền gộp. So sánh gộp với ròng luôn cho ra chênh lệch bằng đúng số phí.

### ✗ Sai

> Chênh lệch: Quyết toán PayPal 5.000.000đ, khoản nạp QB 4.848.000đ — delta 152.000đ. Đánh dấu lỗi đối chiếu.

152.000đ là phí xử lý PayPal khoảng 3,04%. Đây là kết quả đúng và bình thường.

### ✓ Đúng

Dùng trường **số tiền ròng** từ báo cáo quyết toán PayPal (số tiền giao dịch trừ phí) khi so sánh với khoản nạp ngân hàng trong QB. Nếu delta < 5.000đ sau khi đã trừ phí, đánh dấu là ĐÃ ĐỐI CHIẾU.

---

## Gotcha: Xuất gói đóng sổ khi vẫn còn cờ đỏ chưa xử lý

**Tại sao quan trọng:** Gói đóng sổ là tài liệu cuối cùng chủ doanh nghiệp lưu trữ hoặc gửi cho kế toán. Xuất khi còn cờ đỏ là ghi nhận lỗi vào hồ sơ vĩnh viễn.

### ✗ Sai

> Chủ doanh nghiệp chưa phản hồi về 3 giao dịch chưa phân loại. Xuất gói đóng sổ trước để họ có cái nhìn vào.

### ✓ Đúng

Dừng ở cổng phê duyệt cho đến khi chủ doanh nghiệp xác nhận từng cờ đỏ — hoặc xử lý ("phân loại vào văn phòng phẩm") hoặc hoãn rõ ràng ("đánh dấu để xem lại sau"). Chỉ khi đó mới xuất. Các mục chủ doanh nghiệp hoãn phải xuất hiện trong sheet Hạng Mục Cần Xử Lý, không bị bỏ qua im lặng.
