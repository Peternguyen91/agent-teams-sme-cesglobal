---
name: dong-so-thang
description: Đóng sổ tháng — đối soát QB với cổng thanh toán, đánh dấu khoảng trống, viết tường thuật P&L, xuất gói đóng sổ. Chấp nhận tùy chọn tháng và nơi lưu.
allowed-tools: Read, WebFetch, Bash
---

Chạy quy trình đóng sổ cuối tháng. Đối soát, đánh dấu khoảng trống, tường thuật P&L, và xuất gói đóng sổ cho hồ sơ của chủ doanh nghiệp (và kế toán của họ).

Phân tích đối số:
- `--thang` (mặc định: tháng lịch trước) — định dạng `YYYY-MM`
- `--luu-vao` (mặc định `files`) — `files` (Google Drive / OneDrive), `may-tinh` (local), hoặc `ca-hai`

## Bước 1 — Đối soát (dong-so-cuoi-thang)

Kích hoạt quy trình kỹ năng `dong-so-cuoi-thang`:

1. Lấy tất cả giao dịch QuickBooks cho tháng mục tiêu.
2. Lấy thanh toán từ mỗi cổng thanh toán đã kết nối (PayPal, Stripe, Square) cho cùng tháng.
3. Khớp mục QB với thanh toán từ cổng theo số tiền + ngày (±2 ngày).
4. Nêu bật bốn danh mục khoảng trống:
   - **Giao dịch chưa phân loại** — cần được phân loại trước khi tiếp tục
   - **Chênh lệch thanh toán** — số tiền trong QB không khớp thanh toán từ cổng
   - **Bản sao đáng ngờ** — các khoản phí hoặc tiền gửi trùng lặp tiềm năng
   - **Hóa đơn còn thiếu** — giao dịch chi phí không có tài liệu đính kèm

5. Trình bày tóm tắt khoảng trống. Chờ chủ doanh nghiệp xử lý hoặc bỏ qua rõ ràng từng mục trước khi tiếp tục.

## Bước 2 — Viết tường thuật P&L

Sau khi khoảng trống được xử lý/thừa nhận, viết tường thuật P&L rõ ràng:

```
[Tháng] kết thúc với X triệu đồng doanh thu và Y triệu đồng lợi nhuận ròng.

Doanh thu [tăng/giảm] Z% so [tháng trước] — chủ yếu do [lý do].

Lợi nhuận gộp [giữ/tăng/giảm] ở mức W%. [Ghi chú động lực.]

[Bất kỳ dòng chi phí đáng chú ý nào thay đổi đáng kể.]

Điểm cần theo dõi tháng tới: [1-3 mục.]
```

## Bước 3 — Xuất gói đóng sổ

Tạo:
1. **`goi-dong-so-[YYYY-MM].xlsx`** — P&L + đối soát + việc cần làm
2. **`goi-dong-so-[YYYY-MM]-tom-tat.pdf`** — tường thuật P&L một trang

Lưu vào vị trí `--luu-vao` đã chỉ định. Xác nhận với chủ doanh nghiệp: "Đã lưu vào [vị trí]. Các file này sẵn sàng để chia sẻ với kế toán của bạn."

## Cổng phê duyệt

- **Không bao giờ ghi vào QuickBooks.** Chỉ đọc và báo cáo.
- **Không bao giờ bỏ qua khoảng trống chưa giải quyết** mà không được chủ doanh nghiệp xác nhận.
- **Không bao giờ gửi gói cho kế toán** mà không có phê duyệt rõ ràng — luôn để chủ doanh nghiệp tự gửi.

## Ví dụ câu kích hoạt

- *"Đóng sổ tháng này cho tôi"*
- *"Đóng tháng trước đi"*
- *"Chuẩn bị gói đóng sổ cho kế toán"*
- *"Chạy đối soát tháng này"*
