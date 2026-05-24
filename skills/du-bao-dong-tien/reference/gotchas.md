# Gotchas — dự báo dòng tiền

Những lỗi thường gặp và trường hợp đặc biệt khi dự báo dòng tiền. Mỗi mục có ví dụ Sai / Đúng.

---

## 1. Phải thu trong QuickBooks bao gồm cả hóa đơn đã thu tiền

**Sai:** Đưa cả hóa đơn đã thanh toán vào dự báo thu sẽ thổi phồng dòng tiền vào. QuickBooks đôi khi hiển thị hóa đơn có số dư 0 trong báo cáo tuổi nợ.

**Đúng:** Lọc các dòng phải thu chỉ lấy `so_du_con_lai > 0` trước khi tính dòng tiền vào. Nếu connector không cung cấp số dư còn lại, trừ các khoản quyết toán PayPal/Stripe đã biết khỏi tổng hóa đơn trước khi đưa vào.

---

## 2. Thời gian quyết toán PayPal khác nhau theo loại giao dịch

**Sai:** Giả định tất cả khoản thu PayPal quyết toán sau 1–2 ngày làm việc. PayPal giữ tiền khác nhau cho tranh chấp, người bán mới, và giao dịch giá trị cao — dùng giả định cố định cho ra dự báo thời điểm thiếu chính xác.

**Đúng:** Tính thời gian quyết toán từ các cặp `ngày_giao_dich` → `ngay_hoan_tat` thực tế trong lịch sử PayPal. Dùng trung bình và độ lệch chuẩn theo khách hàng hoặc loại giao dịch.

---

## 3. Tên cột trong file xuất kế toán không nhất quán

**Sai:** Yêu cầu tên cột chính xác như "Ngày", "Số tiền", "Loại". QuickBooks xuất CSV dùng "Ngày giao dịch", "Số tiền", "Loại giao dịch". Phân tích cứng nhắc sẽ thất bại im lặng.

**Đúng:** Khớp mờ tiêu đề cột (ngày → ngày giao dịch → date; số tiền → debit/credit; loại → danh mục). Hiển thị dòng tiêu đề cho người dùng và xác nhận cách khớp trước khi tính — một câu hỏi tốt hơn là một dự báo sai im lặng.

---

## 4. Chi phí cố định ẩn trong các mục AP phát sinh một lần

**Sai:** Chỉ lấy các mục định kỳ được gắn nhãn "recurring" trong QuickBooks. Nhiều doanh nghiệp nhỏ không gắn nhãn nhất quán — tiền thuê có thể xuất hiện là hóa đơn nhà cung cấp một lần mỗi tháng.

**Đúng:** Tìm các mục AP xuất hiện ở 3+ tháng liên tiếp với cùng nhà cung cấp và số tiền tương tự (±10%). Xử lý chúng như chi phí cố định hàng tháng. Trình bày danh sách cho người dùng: "Tôi đang xử lý các khoản này là chi phí cố định hàng tháng — có đúng không?"

---

## 5. Công thức dải tin cậy lỗi khi trung bình thời gian thanh toán bằng 0

**Sai:** Chia độ lệch chuẩn cho trung bình thời gian trễ bằng 0 (ví dụ: khách hàng thanh toán ngay như Square POS) dẫn đến lỗi chia cho 0 hoặc dải vô cực.

**Đúng:** Nếu trung bình thời gian trễ ≤ 1 ngày, đặt band_pct = 5% (biến động thấp, quyết toán gần tức thì). Không thực hiện phép chia này.
