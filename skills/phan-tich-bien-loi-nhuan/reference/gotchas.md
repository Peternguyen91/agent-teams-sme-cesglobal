# Gotchas — phân tích biên lợi nhuận

Những lỗi phổ biến khi phân tích margin và định giá cho doanh nghiệp nhỏ. Mỗi mục có ví dụ Sai / Đúng.

---

## 1. Nhầm doanh thu với lợi nhuận

**Tại sao quan trọng:** Chủ doanh nghiệp thấy 500 triệu đồng trên PayPal và nghĩ đó là tiền họ kiếm được — thực ra đó chỉ là tiền thu vào, chưa trừ chi phí.

### ✗ Sai

> "Doanh thu PayPal quý vừa rồi của bạn là 500 triệu đồng."

### ✓ Đúng

> "Doanh thu PayPal quý vừa rồi là 500 triệu đồng. Sau khi trừ chi phí trực tiếp 310 triệu đồng, lợi nhuận gộp của bạn là 190 triệu đồng — biên lợi nhuận gộp 38%."

---

## 2. Dùng giá niêm yết thay vì giá thực tế thu được

**Tại sao quan trọng:** Chiết khấu, hoàn tiền và khuyến mãi làm giảm số tiền thực tế thu được mỗi giao dịch. Hóa đơn QuickBooks ghi giá niêm yết, nhưng PayPal phản ánh số thực thu.

### ✗ Sai

> Lấy doanh thu từ hóa đơn QB + chi phí từ PayPal → margin trông tốt hơn thực tế.

### ✓ Đúng

Dùng số tiền giao dịch PayPal/Square làm nguồn doanh thu (số thực thu), dùng QB cho chi phí. Ghi chú bất kỳ chênh lệch nào giữa tổng hóa đơn QB và tổng thanh toán thực tế.

---

## 3. Kết luận độ co giãn giá từ một lần thay đổi duy nhất

**Tại sao quan trọng:** Doanh nghiệp tăng giá một lần, khách hàng giảm một tháng, rồi phục hồi. Kết luận "tăng 5% giá dẫn đến giảm 3% sản lượng" là quá vội vàng.

### ✗ Sai

> "Tháng 3/2024, bạn tăng giá 8% và sản lượng tháng sau giảm 4%. Độ co giãn = −0,5."

### ✓ Đúng

> "Tháng 3/2024, bạn tăng giá 8% và tháng tiếp theo sản lượng giảm 4%. Lưu ý: đây chỉ là một quan sát — mối quan hệ thực giữa giá và cầu có thể thay đổi tùy mùa và yếu tố bên ngoài. Tôi sẽ dùng đây như ước lượng sơ bộ và trình bày một dải kịch bản."

---

## 4. Bỏ qua chi phí phân phối dịch vụ cho doanh nghiệp dịch vụ

**Tại sao quan trọng:** Doanh nghiệp dịch vụ thường tính COGS bằng 0 vì không có nguyên vật liệu hữu hình — nhưng thời gian lao động của chủ doanh nghiệp chính là chi phí lớn nhất bị bỏ sót.

### ✗ Sai

> Một nhà thiết kế tự do ghi COGS = 0đ vì không có vật liệu. Margin gộp hiển thị 100%.

### ✓ Đúng

Hỏi các doanh nghiệp dịch vụ: "Để cung cấp dịch vụ này, bạn tốn bao nhiêu thời gian và chi phí trực tiếp? Kể cả thời gian của bản thân bạn tính theo giờ?" Dùng đó làm COGS cho phân tích.

---

## 5. Dữ liệu COGS trong QuickBooks không phân tách theo sản phẩm/dịch vụ

**Tại sao quan trọng:** Nhiều doanh nghiệp nhỏ ghi COGS vào một dòng tổng hợp, không phân tách theo từng sản phẩm. Không thể tính margin theo sản phẩm nếu COGS bị gộp chung.

### ✗ Sai

> Lấy COGS tổng 220 triệu đồng → chia cho 12 sản phẩm → con số vô nghĩa.

### ✓ Đúng

Nếu QB không có COGS chi tiết theo sản phẩm, hỏi chủ doanh nghiệp: "QuickBooks có tổng chi phí nhưng không có phân tách theo từng sản phẩm. Bạn có thể ước lượng chi phí để sản xuất hoặc cung cấp từng loại không? Số ước lượng cũng được." Tiến hành với số liệu chủ doanh nghiệp cung cấp và ghi chú hạn chế trong output.

---

## 6. PayPal giới hạn tốc độ khi gọi API nhiều lần liên tiếp

**Tại sao quan trọng:** Gọi `list_transactions` nhiều lần liên tiếp có thể kích hoạt rate limit của PayPal, làm phân tích thất bại giữa chừng.

### ✗ Sai

> Lặp qua nhiều khoảng thời gian → lỗi 429 → skill crash không có dữ liệu.

### ✓ Đúng

Gọi `list_transactions` → nếu lỗi 429, dừng 30 giây → thử lại một lần → nếu lần thứ hai vẫn lỗi 429, dừng hoàn toàn và thông báo: "PayPal đang giới hạn tốc độ trong phiên này. Tôi có thể dùng Square thay thế, hoặc bạn có thể tải lên file CSV xuất từ PayPal." Không thử lần thứ ba.

---

## 7. Trình bày kịch bản định giá như dự báo chắc chắn

**Tại sao quan trọng:** Bảng kịch bản định giá là toán học, không phải dự đoán. Chủ doanh nghiệp có thể hiểu nhầm và cảm thấy bị lừa khi kết quả thực tế khác.

### ✗ Sai

> "Nếu bạn tăng giá 10%, bạn sẽ thu được 550 triệu đồng quý tới."

### ✓ Đúng

> "Nếu tăng giá 10% và sản lượng giảm khoảng 5% (dựa trên lịch sử có sẵn), doanh thu ước tính sẽ vào khoảng 530 triệu đồng. Đây là ước lượng sơ bộ — kết quả thực tế sẽ phụ thuộc vào phản ứng của khách hàng và bối cảnh thị trường."
