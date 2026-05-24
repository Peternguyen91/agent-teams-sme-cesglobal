---
name: du-bao-dong-tien
description: >
  Đọc công nợ phải thu/phải trả, lịch sử thời gian tiền mặt, và chi phí cố
  định đã biết từ QuickBooks, PayPal, Stripe, hoặc Square — hoặc upload CSV —
  và tạo dự báo dòng tiền 30/60/90 ngày với dải tin cậy phần trăm biến động
  và cờ rủi ro được đặt tên. Xuất tóm tắt chat và XLSX có thể tải xuống. Dùng
  khi người dùng hỏi "dự báo dòng tiền của tôi", "tôi có đủ tiền trả lương
  không", đề cập "runway", hoặc nói "căng thẳng tiền mặt". Dự phòng bằng
  upload CSV khi không có phần mềm nào kết nối.
---

# Dự Báo Dòng Tiền

Tạo dự báo dòng tiền 30/60/90 ngày với dải tin cậy phần trăm biến động và cờ rủi ro được đặt tên. Xuất hai phần: tóm tắt chat súc tích và workbook XLSX có thể tải xuống.

## Bắt đầu nhanh

Nếu QuickBooks đã kết nối → lấy AR, AP và lịch sử ngay lập tức.
Nếu chưa kết nối phần mềm nào → hỏi upload CSV (xem Bước 0).
Nếu người dùng chỉ muốn nói về lo lắng tiền mặt → thu thập số thủ công (xem Bước 0b).

```
Người dùng: "tôi có đủ tiền trả lương không"
→ Lấy số dư tiền mặt và AR từ QuickBooks
→ Lấy thanh toán chờ từ PayPal
→ Lớp chi phí cố định (bảng lương, tiền thuê, định kỳ)
→ Dự báo 30 ngày với ba kịch bản
→ Đặt tên rủi ro cụ thể: "Bảng lương ngày 15/5 đến khi số dư thấp hơn mức cố định $X triệu tại dự báo trung bình"
→ Xuất XLSX + tóm tắt chat
```

## Bước 0 — Thu thập dữ liệu đầu vào (khi không có phần mềm)

**Nếu không có phần mềm nào kết nối:**

Hỏi upload CSV. Chấp nhận ba định dạng:
- **Xuất QuickBooks** — báo cáo A/R Aging + A/P Aging
- **Xuất ngân hàng** — sổ tài khoản séc/tiết kiệm 90 ngày
- **Template đơn giản** — cung cấp template 3 cột (ngày, mô tả, số tiền)

Nếu người dùng không có file nào: hỏi 5 câu để xây dựng mô hình tối thiểu:
1. "Số dư tiền mặt hiện tại của bạn là bao nhiêu?"
2. "Ai nợ bạn tiền và khoảng bao nhiêu?"
3. "Hóa đơn hay thanh toán nào bạn phải trả trong 30 ngày tới?"
4. "Chi phí cố định hàng tháng của bạn (bảng lương, tiền thuê, đăng ký) là bao nhiêu?"
5. "Doanh thu tháng điển hình của bạn là bao nhiêu?"

## Bước 1 — Lấy số dư và các khoản phải thu

Lấy từ các phần mềm đã kết nối:
- **QuickBooks**: số dư tiền mặt hiện tại, A/R aging (0-30, 31-60, 61+ ngày), A/P aging
- **PayPal**: số dư đã thanh toán, các khoản thanh toán chờ xử lý
- **Stripe**: tổng ngân quỹ có sẵn, thanh toán chờ
- **Square**: số dư ngân hàng liên kết, nhận được hôm nay

Kết hợp: **tổng tiền mặt và khoản sắp đến** = số dư QB + số dư đã thanh toán PayPal/Stripe/Square.

## Bước 2 — Lớp chi phí cố định và đã biết

Đặt câu hỏi nếu không rõ từ dữ liệu QB:
- Ngày trả lương và số tiền bảng lương
- Tiền thuê/thế chấp và ngày đáo hạn
- Đăng ký và dịch vụ định kỳ (phần mềm, bảo hiểm, v.v.)
- Khoản vay hoặc thanh toán LOC với ngày đáo hạn

## Bước 3 — Xây dựng ba kịch bản

Dự báo mỗi kịch bản qua 30, 60 và 90 ngày:

| Kịch bản | Giả định thu | Giả định chi |
|----------|-------------|--------------|
| **Lạc quan** | 90% A/R thu đúng hạn, +10% trên doanh thu điển hình | Chi phí cố định chỉ |
| **Cơ sở** | 70% A/R thu đúng hạn, doanh thu bằng trung bình 3 tháng | Tất cả chi phí đã biết |
| **Thận trọng** | 50% A/R thu đúng hạn, -15% dưới trung bình | Chi phí đầy đủ + 10% đệm phát sinh |

Tính số dư tiền mặt cuối ngày cho mỗi ngày trong kỳ dự báo theo từng kịch bản.

## Bước 4 — Đặt tên rủi ro

Quét mỗi kịch bản để tìm ngày có số dư tiền mặt dự kiến xuống dưới:
- **0** → cờ khủng hoảng tiền mặt
- **Chi phí cố định tháng** → cờ cảnh báo
- **Chi phí bảng lương tiếp theo** → cờ rủi ro bảng lương

Mỗi cờ phải đặt tên ngày cụ thể và số tiền cụ thể:
> "⚠️ Kịch bản thận trọng: Bảng lương ngày 15/5 (50 triệu đồng) đến khi số dư tiền mặt chỉ còn 32 triệu theo dự báo."

## Bước 5 — Xuất

**Tóm tắt chat** (in trong chat):
```
Dự Báo Dòng Tiền — {ngày}
Số dư hiện tại: {X triệu đồng}

              Lạc quan    Cơ sở      Thận trọng
30 ngày:      +X triệu   +Y triệu   -Z triệu
60 ngày:      +X triệu   +Y triệu   -Z triệu
90 ngày:      +X triệu   +Y triệu   -Z triệu

⚠️ RỦI RO: [tên rủi ro cụ thể theo kịch bản thận trọng]
```

**XLSX** (cung cấp link tải xuống):
- Sheet 1: Dự báo dòng tiền hàng ngày (ba kịch bản, 90 ngày)
- Sheet 2: Giả định đã dùng
- Sheet 3: Chi tiết cờ rủi ro

## Cổng phê duyệt

- **Không cố vấn về quyết định tài chính.** Hiển thị các con số; chủ doanh nghiệp quyết định.
- **Không gửi email, chuyển tiền, hoặc thực hiện bất cứ điều gì** dựa trên dự báo — chỉ phân tích.
- **Đánh dấu rõ ràng** khi dựa vào dữ liệu thủ công thay vì dữ liệu trực tiếp từ phần mềm.

## Ví dụ câu kích hoạt

- *"Tôi có đủ tiền trả lương không?"*
- *"Dự báo dòng tiền 3 tháng tới"*
- *"Tiền mặt tháng tới như thế nào?"*
- *"Còn bao lâu nữa là hết tiền?"*
