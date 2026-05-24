---
name: dong-so-cuoi-thang
description: >
  Dẫn chủ doanh nghiệp nhỏ qua quy trình đóng sổ cuối tháng: đối soát QuickBooks
  với thanh toán PayPal (và Square/Stripe), đánh dấu giao dịch chưa phân loại,
  bản sao đáng ngờ và hóa đơn thiếu, sau đó viết tường thuật P&L rõ ràng và
  xuất gói đóng sổ (xlsx + PDF một trang). Dùng khi người dùng nói "đóng sổ
  tháng", "cuối tháng", "đối soát", "còn thiếu gì", "P&L", hoặc hỏi tại sao
  doanh thu hoặc margin thay đổi tháng này.
---

# Đóng Sổ Cuối Tháng

## Bắt đầu nhanh

Kết nối QuickBooks và ít nhất một cổng thanh toán (PayPal, Square, hoặc Stripe), rồi nói "đóng sổ tháng này đi." Claude đi qua từng bước của checklist, dừng lại để bạn xác nhận trước khi tiếp tục.

Nếu thiếu phần mềm, Claude dùng phương án xuất CSV — không bao giờ bỏ qua bước một cách thầm lặng.

## Quy trình làm việc

Thực hiện theo thứ tự. Mỗi bước có trạng thái hoàn thành; không chuyển sang bước tiếp theo cho đến khi bước hiện tại xong.

### Bước 1 — Xác nhận tháng cần đóng sổ

Hỏi người dùng tháng nào cần đóng sổ. Mặc định là tháng lịch trước nếu không chỉ định. Xác nhận trước khi lấy bất kỳ dữ liệu nào.

### Bước 2 — Lấy P&L và sổ giao dịch QuickBooks

Lấy:
- Báo cáo Lợi nhuận & Lỗ cho tháng mục tiêu (doanh thu, giá vốn, lợi nhuận gộp, chi phí vận hành, lợi nhuận ròng)
- Sổ giao dịch: mọi dòng thu và chi

Đánh dấu ngay lập tức:
- **Giao dịch chưa phân loại** — bất kỳ dòng nào có danh mục "Chưa phân loại" hoặc để trống
- **Cần xem xét** — cờ của QB

Trình bày số lượng ("14 giao dịch cần phân loại") và liệt kê để người dùng phân loại trước khi tiếp tục. Không chuyển sang bước tiếp với giao dịch chưa phân loại trừ khi người dùng nói rõ "bỏ qua tạm".

### Bước 3 — Lấy thanh toán từ cổng thanh toán

Lấy báo cáo thanh toán từ PayPal, Square, hoặc Stripe — bất kể cái nào đã kết nối — cho cùng tháng lịch.

Khớp mỗi khoản thanh toán với dòng tiền gửi ngân hàng QuickBooks:
- **Khớp** — số tiền và ngày đồng ý trong 2 ngày → đánh dấu đã đối soát
- **Chênh lệch < 5.000đ** — làm tròn/phí; ghi chú nhưng không đánh dấu
- **Chênh lệch ≥ 5.000đ** — đánh dấu với số tiền chênh lệch
- **Thanh toán tồn tại, không có tiền gửi QB** — đánh dấu là "thiếu trong QuickBooks"
- **Tiền gửi QB tồn tại, không có trong thanh toán** — đánh dấu là "tiền gửi không có trong dữ liệu cổng thanh toán"

### Bước 4 — Phát hiện bản sao đáng ngờ

Quét sổ giao dịch để tìm các khoản phí hoặc tiền gửi trùng lặp. Đánh dấu giao dịch là bản sao đáng ngờ khi **cả ba** điều này khớp:
- Cùng số tiền (trong 1.000đ)
- Cùng tên nhà cung cấp hoặc khách hàng
- Đăng trong vòng 5 ngày lịch của nhau

Trình bày các cặp đã đánh dấu cho người dùng. Họ quyết định từng cái có hợp lệ không (ví dụ: đăng ký hàng tuần định kỳ) hay là bản sao thật cần hủy.

### Bước 5 — Kiểm tra hóa đơn

Nếu connector Desktop khả dụng, quét thư mục hóa đơn cho tháng mục tiêu.

Với mỗi giao dịch chi phí QuickBooks trên 500.000đ không có tài liệu đính kèm:
- Kiểm tra file hóa đơn phù hợp (khớp theo số tiền ± 50.000đ và ngày trong 3 ngày)
- **Khớp** → ghi chú "có hóa đơn"
- **Không khớp** → đánh dấu "thiếu hóa đơn"

Liệt kê hóa đơn còn thiếu. Người dùng có thể cung cấp file hoặc đánh dấu "không cần hóa đơn".

### Bước 6 — Cổng ký duyệt của chủ doanh nghiệp

Trình bày tóm tắt trước khi tiếp tục:

```
Giao dịch chưa phân loại:  X trong X đã xử lý
Chênh lệch thanh toán:     X đã đánh dấu, X đã xử lý
Bản sao đáng ngờ:          X đã đánh dấu, X đã xóa
Hóa đơn còn thiếu:         X tồn đọng
```

Hỏi: "Sẵn sàng viết tóm tắt P&L và xuất gói đóng sổ chưa?"

**Không tiếp tục Bước 7–8 mà không có xác nhận rõ ràng.**

### Bước 7 — Viết tường thuật P&L

Viết tóm tắt rõ ràng về tháng — loại mà chủ doanh nghiệp sẽ chia sẻ với kế toán. Mục tiêu 150–250 từ.

Cấu trúc:
1. **Tiêu đề** — một câu: "Tháng 3 đạt X triệu lợi nhuận ròng, tăng/giảm Y% so tháng 2."
2. **Doanh thu** — điều gì thúc đẩy con số; đặt tên sản phẩm, dịch vụ hoặc khách hàng nếu dữ liệu cho thấy sự tập trung.
3. **Lợi nhuận gộp** — có giữ nguyên, tăng hay giảm không, và lý do chính.
4. **Chi phí chính** — bất kỳ dòng nào thay đổi hơn 10% so tháng trước hoặc nằm ngoài phạm vi bình thường; mỗi dòng một câu.
5. **Kết quả cuối** — lợi nhuận ròng so tháng trước; hỏi nếu họ có mục tiêu để so sánh.
6. **Danh sách theo dõi** — 1–3 điều cần theo dõi tháng tới.

Tránh thuật ngữ kỹ thuật; giải thích bất cứ điều gì không phải tiếng Việt bình thường.

### Bước 8 — Xuất gói đóng sổ

Tạo hai file:

**`goi-dong-so-[YYYY-MM].xlsx`** — ba sheet:
- `P&L` — dữ liệu P&L QuickBooks, đã định dạng
- `Đối soát` — giao dịch đã khớp và đã đánh dấu cạnh nhau
- `Việc cần làm` — bất kỳ cờ còn tồn đọng nào

**`goi-dong-so-[YYYY-MM]-tom-tat.pdf`** — một trang:
- Tháng và tên doanh nghiệp ở đầu
- Các con số chính (doanh thu, % lợi nhuận gộp, lợi nhuận ròng)
- Tường thuật P&L từ Bước 7
- Số mục hành động còn mở, nếu có

Lưu cả hai vào Desktop (hoặc đường dẫn người dùng chỉ định). Xác nhận vị trí file.

## Cổng phê duyệt

- **Không bao giờ chạy đối soát cho tháng đã nộp báo cáo.** Xác nhận sổ sách vẫn đang mở trước khi lấy dữ liệu.
- **Không bao giờ trực tiếp hủy hoặc sửa giao dịch QuickBooks.** Hiển thị cờ; chủ doanh nghiệp thực hiện thay đổi trong QuickBooks.
- **Luôn dừng lại ở Bước 6** trước khi tạo kết quả. Các cờ chưa giải quyết phải được thừa nhận hoặc bỏ qua một cách rõ ràng.

## Phương án dự phòng khi thiếu phần mềm

| Thiếu phần mềm | Phương án dự phòng |
|---|---|
| QuickBooks | Yêu cầu xuất CSV từ QB (P&L + chi tiết giao dịch) |
| Cổng thanh toán | Yêu cầu CSV thanh toán từ trang web cổng |
| Desktop (hóa đơn) | Hỏi người dùng xác nhận trạng thái hóa đơn cho từng chi phí đã đánh dấu |

## Ví dụ câu kích hoạt

- *"Đóng sổ tháng này đi"*
- *"Cuối tháng rồi, cho tôi xem P&L"*
- *"Đối soát QuickBooks với PayPal"*
- *"Còn thiếu giao dịch gì không?"*
