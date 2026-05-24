# Ví Dụ Mẫu — Dự Báo Dòng Tiền

**Tình huống:** Doanh nghiệp dịch vụ nhỏ. Kết nối QuickBooks + PayPal. Ba khách hàng đang hoạt động, trả lương hàng tháng, tiền thuê văn phòng.

---

## Dữ liệu đầu vào (lấy từ connector)

**Tuổi nợ phải thu (QuickBooks):**

| Khách hàng        | Hóa đơn | Số tiền      | Ngày đáo hạn | Số ngày quá hạn |
|-------------------|---------|--------------|--------------|-----------------|
| Công ty A         | HD-112  | 8.400.000đ   | 10/4         | 12              |
| Công ty B         | HD-108  | 14.200.000đ  | 22/4         | 0               |
| Công ty C         | HD-115  | 6.000.000đ   | 5/5          | —               |

**Lịch sử thời gian thanh toán (từ quyết toán PayPal):**

| Khách hàng  | Trung bình trễ | Độ lệch chuẩn | Số lần thanh toán |
|-------------|---------------|---------------|-------------------|
| Công ty A   | 18 ngày       | 4 ngày        | 11                |
| Công ty B   | 7 ngày        | 2 ngày        | 8                 |
| Công ty C   | 12 ngày       | 5 ngày        | 6                 |

**Chi phí cố định (AP định kỳ trong QuickBooks):**
- Lương: 22.000.000đ — đến hạn ngày 15/4
- Thuê văn phòng: 3.200.000đ — đến hạn ngày 1/5
- Phần mềm: 480.000đ — đến hạn ngày 1/5

---

## Kết quả Bước 3 — Ngày thu điều chỉnh

| Khách hàng  | Số tiền hóa đơn | Ngày thu dự kiến | Ghi chú                              |
|-------------|----------------|------------------|--------------------------------------|
| Công ty A   | 8.400.000đ     | 28/4             | Đáo hạn 10/4 + trễ trung bình 18 ngày |
| Công ty B   | 14.200.000đ    | 29/4             | Đáo hạn 22/4 + trễ trung bình 7 ngày  |
| Công ty C   | 6.000.000đ     | 17/5             | Đáo hạn 5/5 + trễ trung bình 12 ngày  |

---

## Kết quả Bước 4 — Dự báo 30/60/90 ngày

Tính dải tin cậy:
- Độ lệch chuẩn trọng số: 3,6 ngày
- Trung bình trễ trọng số: 12,7 ngày
- band_pct = 3,6 / 12,7 = **28,3%**

| Kỳ      | Dòng vào dự kiến | Dòng ra dự kiến | Ròng         | Thấp (−28%)  | Cao (+28%)   |
|---------|-----------------|-----------------|--------------|--------------|--------------|
| 0–30n   | 22.600.000đ     | 22.000.000đ     | +600.000đ    | −5.928.000đ  | +7.128.000đ  |
| 31–60n  | 6.000.000đ      | 3.680.000đ      | +2.320.000đ  | +1.670.000đ  | +2.970.000đ  |
| 61–90n  | 0đ              | 0đ              | 0đ           | —            | —            |

---

## Kết quả Bước 5 — Rủi ro cần lưu ý

1. **Rủi ro lương:** Lương (22.000.000đ) đến hạn ngày 15/4. Dòng tiền vào thấp nhất đến ngày 14/4: 0đ (cả hai khoản phải thu đến 28–29/4). Rủi ro thiếu hụt: lên đến 22.000.000đ.
   *Khuyến nghị: Xác nhận thời gian thu tiền với Công ty A và B trước ngày 14/4.*

2. **Rủi ro khách hàng thanh toán trễ:** Công ty A thường thanh toán trễ 18 ngày. Hóa đơn 8.400.000đ (đáo hạn 10/4) sẽ đến tay vào 28/4 — sau ngày trả lương.

---

## Kết quả Bước 6 — Tóm tắt

```
Dự Báo Dòng Tiền — 23/4 → 21/7/2026
Nguồn: QuickBooks, PayPal

              Dự kiến      Thấp          Cao
30 ngày ròng: +600.000đ   −5.928.000đ   +7.128.000đ
60 ngày ròng: +2.320.000đ +1.670.000đ   +2.970.000đ
90 ngày ròng: 0đ          —             —

⚠ 2 rủi ro cần lưu ý:
  • Rủi ro lương: 22 triệu lương đến hạn 15/4; khoản phải thu
    không về đến 28–29/4. Rủi ro thiếu hụt: lên đến 22 triệu.
  • Khách hàng trễ: Công ty A (trung bình trễ 18 ngày) đẩy
    8,4 triệu qua ngày trả lương.

Dải tin cậy: ±28% (dựa trên biến động lịch sử thanh toán của 3 khách hàng).

Dự báo này dựa trên dữ liệu AR/AP từ QuickBooks và lịch sử
quyết toán PayPal. Không thay thế tư vấn kế toán — xác nhận
với kế toán viên trước khi đưa ra quyết định tài chính quan trọng.
```

**File XLSX:** `du-bao-dong-tien-2026-04-23.xlsx` — Sheet Tóm Tắt / Chi Tiết / Rủi Ro.
