---
name: to-chuc-mua-quyet-toan
description: >
  Chuẩn bị tài liệu mùa quyết toán thuế cho chủ doanh nghiệp nhỏ — được
  trình bày là tài liệu bàn giao cho kế toán, không phải tư vấn thuế. Hai
  chế độ: (1) tính thuế ước tính hàng quý — lấy thu nhập ròng YTD từ
  QuickBooks và tính nghĩa vụ thuế; (2) chuẩn bị 1099 cuối năm — quét
  QuickBooks, PayPal và Stripe để tìm nhà thầu được thanh toán trên 10 triệu
  đồng, xây dựng danh sách ứng viên 1099-NEC với cờ W-9 còn thiếu. Kích hoạt
  khi người dùng đề cập: thuế quý, thanh toán thuế ước tính, cần dành bao
  nhiêu để nộp thuế, 1099, cuối năm, thanh toán nhà thầu, W-9, hoặc đang
  chuẩn bị cho deadline thuế hay bàn giao tài liệu cho kế toán.
---

# Tổ Chức Mùa Quyết Toán

Chuẩn bị mọi tài liệu mùa quyết toán trong một lần chạy. Kỹ năng này bao gồm cả thuế hàng quý lẫn 1099 cuối năm — chạy một hoặc cả hai dựa theo thời điểm trong năm và nhu cầu của bạn.

> Tất cả tài liệu được đánh nhãn: "Chuẩn bị để kế toán xem xét — không phải tư vấn thuế."

## Bước 1 — Xác định phạm vi

Hỏi chủ doanh nghiệp (hoặc suy ra từ ngày):

- **Quý 1–3** (Tháng 1–Tháng 9): Tập trung vào thuế ước tính hàng quý
- **Quý 4 / Tháng 1** (Tháng 10–Tháng 1): Chạy cả hai — thuế quý Q4 + chuẩn bị 1099

Xác nhận: "Tôi thấy chúng ta đang ở [thời điểm]. Tôi sẽ chuẩn bị [phạm vi]. Đúng không?"

## Bước 2 — Tính thuế ước tính hàng quý

*(Chạy khi trong chế độ `hang-quy` hoặc `ca-hai`)*

1. Lấy P&L QuickBooks YTD: doanh thu, chi phí, thu nhập ròng
2. Áp dụng khung thuế thu nhập doanh nghiệp Việt Nam hiện tại (20% TNDN tiêu chuẩn)
3. Trừ các khoản đã khấu trừ hợp lệ nếu biết
4. Tính nghĩa vụ thuế quý và deadline nộp

**Lưu ý quan trọng**: Tỷ lệ thuế và quy định có thể thay đổi. Kết quả này chỉ là ước tính sơ bộ để kế toán xem xét — không dùng để nộp thuế chính thức.

## Bước 3 — Chuẩn bị danh sách 1099 cuối năm

*(Chạy khi trong chế độ `1099` hoặc `ca-hai`)*

1. Quét tất cả thanh toán cho cá nhân không phải nhân viên trong năm:
   - QuickBooks: mọi khoản chi cho nhà thầu, freelancer
   - PayPal: khoản chuyển khoản đến cá nhân
   - Stripe: thanh toán ngoài giao dịch bán hàng

2. Lọc: chỉ giữ tổng ≥ 10 triệu đồng/người/năm

3. Xây dựng bảng:

| Tên | Tổng thanh toán | Phương thức | Trạng thái W-9 | Cần hành động |
|-----|-----------------|-------------|----------------|---------------|
| ... | ...             | ...         | ✅ / ❌         | ...           |

4. Đánh dấu rõ: người chưa có W-9 cần được thu thập thông tin trước khi kế toán có thể xử lý.

## Bước 4 — Danh sách kiểm tra bàn giao kế toán

Tạo danh sách kiểm tra cụ thể cho cuộc họp với kế toán:

```
✅ Đã chuẩn bị:
□ P&L YTD từ QuickBooks (đính kèm)
□ Ước tính thuế quý (đính kèm)
□ Danh sách ứng viên 1099 (đính kèm)

⚠️ Bạn cần cung cấp cho kế toán:
□ W-9 còn thiếu cho: [danh sách tên]
□ Xác nhận: khoản thanh toán nào là cá nhân vs. công ty
□ Bất kỳ chi phí kinh doanh lớn nào chưa trong QuickBooks

❓ Câu hỏi kế toán có thể hỏi:
□ Có thay đổi về cơ cấu doanh nghiệp trong năm không?
□ Có tài sản mua mới nào cần khấu hao không?
□ Tỷ lệ sử dụng văn phòng tại nhà nếu có?
```

## Bước 5 — Xuất tài liệu

Tạo gói đầy đủ:
- **`ket-qua-thue-[YYYY]-Q[N].pdf`** — ước tính thuế có nhãn "Để kế toán xem xét"
- **`danh-sach-1099-[YYYY].xlsx`** — bảng ứng viên 1099 đầy đủ
- **`danh-sach-kiem-tra-bao-cao-thue.pdf`** — checklist bàn giao

## Cổng phê duyệt

- **Không nộp bất cứ form thuế nào.** Chỉ chuẩn bị tài liệu.
- **Không tư vấn thuế.** Luôn chuyển sang kế toán hoặc tư vấn thuế chuyên nghiệp.
- **Đánh dấu rõ mọi ước tính** là sơ bộ và cần xác minh chuyên nghiệp.

## Ví dụ câu kích hoạt

- *"Chuẩn bị tài liệu quyết toán cuối năm"*
- *"Tổ chức hồ sơ thuế cho kế toán"*
- *"Ai cần nhận 1099? Tôi cần tổng hợp"*
- *"Chuẩn bị mùa quyết toán"*
