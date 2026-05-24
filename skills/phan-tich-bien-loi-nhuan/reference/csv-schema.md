# Cấu Trúc CSV Upload

Khi chủ doanh nghiệp không có QuickBooks hoặc PayPal được kết nối, họ có thể upload file CSV xuất từ phần mềm của mình. Tài liệu này mô tả các cột cần thiết và cách xử lý các biến thể phổ biến.

---

## CSV Doanh Thu (xuất giao dịch)

Các cột cần thiết (thứ tự không quan trọng; tên cột không phân biệt hoa thường):

| Cột | Bắt buộc | Mô tả |
|---|---|---|
| `date` hoặc `ngay` | Có | Ngày giao dịch (mọi định dạng chuẩn: YYYY-MM-DD, DD/MM/YYYY, v.v.) |
| `item`, `product`, `service`, hoặc `description` | Có | Sản phẩm/dịch vụ đã bán |
| `amount`, `revenue`, hoặc `total` | Có | Số tiền giao dịch (VND) |
| `quantity` hoặc `qty` | Không | Số lượng — nếu thiếu, mặc định là 1 mỗi giao dịch |

**Các nguồn xuất thường khớp định dạng này:**
- PayPal: Hoạt động → Tải xuống (CSV)
- Square: Báo cáo → Giao dịch → Xuất
- Kiot Viet: Báo cáo → Doanh thu → Xuất Excel/CSV
- MISA: Sổ bán hàng → Xuất

Nếu file xuất có thêm cột, bỏ qua. Nếu thiếu cột bắt buộc, hỏi chủ doanh nghiệp cột nào tương ứng.

---

## CSV Chi Phí (xuất chi phí hoặc COGS)

Các cột cần thiết:

| Cột | Bắt buộc | Mô tả |
|---|---|---|
| `date` hoặc `ngay` | Không | Ngày chi phí (hữu ích để phân tích xu hướng) |
| `item`, `product`, `service`, hoặc `category` | Có | Chi phí thuộc về sản phẩm/dịch vụ nào |
| `amount`, `cost`, hoặc `expense` | Có | Số tiền chi phí (VND) |
| `type` | Không | COGS hay chi phí vận hành — nếu thiếu, hỏi chủ doanh nghiệp |

---

## Xử lý CSV lộn xộn

File xuất thực tế thường có vấn đề. Các trường hợp phổ biến:

- **Nhiều dòng tiêu đề thừa:** Bỏ qua các dòng cho đến khi tìm thấy dòng trông như tên cột.
- **Ký hiệu tiền tệ:** Loại bỏ `đ`, `.`, `,` khỏi các trường số trước khi tính toán.
- **Hoàn tiền âm:** Giữ nguyên — chúng làm giảm doanh thu ròng.
- **Nhiều loại tiền tệ:** Gắn cờ và hỏi loại tiền nào dùng; mặc định VND nếu không rõ.
- **Số tiền "gộp" vs "ròng":** Ưu tiên ròng (sau phí) cho doanh thu; hỏi nếu không rõ.

---

## Sau khi tải dữ liệu

Xác nhận hình dạng dữ liệu với chủ doanh nghiệp trước khi tiến hành:

> "Tôi đã tải X giao dịch từ [ngày] đến [ngày] cho Y sản phẩm/dịch vụ. Trông có đúng không?"

Nếu phạm vi ngày hoặc số lượng sản phẩm có vẻ sai, yêu cầu họ kiểm tra lại bộ lọc khi xuất file.
