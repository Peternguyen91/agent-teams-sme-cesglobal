---
name: dong-so-thang
description: Đóng sổ tháng — đối soát QB với cổng thanh toán, đánh dấu mục đáng ngờ, viết tường thuật P&L, xuất gói đóng sổ. Chấp nhận tùy chọn --thang và --luu-vao.
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu QuickBooks MCP. Tùy chọn: PayPal, Stripe, Square (ít nhất một cổng thanh toán để đối soát đầy đủ)."
version: "1.1"
---

Chạy quy trình đóng sổ cuối tháng. Đối soát, đánh dấu khoảng trống và mục đáng ngờ, tường thuật P&L, và xuất gói đóng sổ cho hồ sơ của chủ doanh nghiệp (và kế toán của họ).

Phân tích đối số:
- `--thang` (mặc định: tháng lịch trước) — định dạng `YYYY-MM`
- `--luu-vao` (mặc định `files`) — `files` (Google Drive / OneDrive), `may-tinh` (local), hoặc `ca-hai`

---

## Bước 1 — Đối soát

Kích hoạt quy trình kỹ năng `dong-so-cuoi-thang`:

1. Lấy tất cả giao dịch QuickBooks cho tháng mục tiêu.
2. Lấy thanh toán từ mỗi cổng thanh toán đã kết nối (PayPal, Stripe, Square) cho cùng tháng.
3. Khớp mục QB với thanh toán từ cổng theo số tiền + ngày (±2 ngày).
4. Nêu bật ba danh mục khoảng trống:
   - **Thanh toán từ cổng chưa khớp** — tiền vào qua PayPal/Stripe/Square nhưng chưa được ghi vào QB
   - **Khoản tiền gửi QB chưa khớp** — QB ghi nhận thu nhập nhưng không có hồ sơ từ cổng (tiền mặt? chuyển khoản? phân loại sai?)
   - **Dòng chênh lệch** — đã khớp nhưng số tiền khác nhau (phí, hoàn tiền tách biệt)

---

## Bước 2 — Đánh dấu mục đáng ngờ

Hiển thị trong cùng báo cáo:
- **Giao dịch chưa phân loại** — mục QB không có danh mục
- **Bản sao đáng ngờ** — cùng số tiền, cùng nhà cung cấp, trong vòng 3 ngày
- **Hóa đơn còn thiếu** — mục chi phí QB trên 2.000.000đ không có đính kèm

Với mỗi mục, đề xuất hành động: phân loại là X, xóa bản sao, đính kèm hóa đơn từ hộp thư.

Chờ chủ doanh nghiệp xử lý các mục được đánh dấu trước khi tạo tường thuật. **Không tự động phân loại hoặc tự động xóa.**

---

## Bước 3 — Tường thuật P&L

Sau khi khoảng trống được xử lý/thừa nhận, viết tường thuật P&L rõ ràng:

```
[Tháng YYYY] kết thúc với X triệu đồng doanh thu ([+/-]Y% so tháng trước).
Động lực chính: [danh mục/khách hàng]. Thay đổi lớn nhất: [danh mục] [hướng] Z triệu
vì [lý do suy ra từ giao dịch].

Margin: X% ([+/-]Y điểm so trước). [Nhận xét về chi phí].

Ba điểm đáng chú ý:
1. ...
2. ...
3. ...
```

Số liệu lấy từ QB; phần *lý do* đến từ việc đối chiếu các giao dịch lớn nhất, tên nhà cung cấp, và chênh lệch tháng trước.

---

## Bước 4 — Xuất gói đóng sổ

Tạo hai file:

1. **`goi-dong-so-[YYYY-MM].xlsx`** — bảng tính nhiều tab:
   - `Đối soát` — bảng khớp QB ↔ cổng thanh toán với các dòng khoảng trống được tô màu
   - `Đánh dấu` — giao dịch chưa phân loại / bản sao / thiếu hóa đơn
   - `P&L` — báo cáo thu nhập có định dạng với cột chênh lệch tháng trước
   - `Cân đối thử` — tài khoản + số dư cuối kỳ

2. **`goi-dong-so-[YYYY-MM].pdf`** — tóm tắt một trang: tường thuật P&L + số liệu tổng quan + số lượng khoảng trống

Lưu vào vị trí `--luu-vao` đã chỉ định. Định dạng tên file: `goi-dong-so-2026-04.xlsx`.

---

## Xử lý lỗi kết nối

Nếu QuickBooks không khả dụng, dừng lại — đối soát yêu cầu QB làm nguồn sự thật. Nếu một cổng thanh toán (PayPal, Stripe, Square) không khả dụng, chạy đối soát với các cổng có sẵn và ghi chú "PayPal chưa kết nối — bỏ qua thanh toán PayPal khỏi đối soát". Nếu tất cả cổng đều thiếu, chạy phân tích chỉ QB và đánh dấu rõ điều đó.

---

## Cổng phê duyệt

- **Không bao giờ tự sửa mục được đánh dấu.** Luôn hiển thị khoảng trống, đề xuất hành động, chờ chủ doanh nghiệp.
- **Không bao giờ xóa bản sao mà không có xác nhận rõ ràng.** Hiển thị cả hai bản ghi cạnh nhau.
- **Không bao giờ ghi vào QuickBooks.** Chỉ đọc và báo cáo.
- **Không bao giờ gửi gói cho kế toán** — luôn để chủ doanh nghiệp tự gửi.

---

## Kết quả đầu ra

Kết thúc bằng một đoạn tóm tắt: doanh thu, margin, số khoảng trống còn lại (nếu có), đường dẫn file đến gói đã lưu. Nếu các khoảng trống chưa được giải quyết hết, liệt kê để chủ doanh nghiệp xem xét lại.

---

## Ví dụ câu kích hoạt

- *"Đóng sổ tháng này cho tôi"*
- *"Đóng tháng trước đi"*
- *"Chuẩn bị gói đóng sổ cho kế toán"*
- *"Chạy đối soát tháng này"*
- *"Đóng sổ --thang 2026-04 --luu-vao ca-hai"*
