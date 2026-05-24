---
name: chuan-bi-quyet-toan-thue
description: Chuẩn bị tài liệu thuế — tính thuế ước tính hàng quý hoặc chuẩn bị danh sách nhà thầu 1099 cuối năm — và tạo gói bàn giao cho kế toán. Chấp nhận tùy chọn chế độ và năm.
allowed-tools: Read, WebFetch, Bash
---

Chạy quy trình chuẩn bị thuế. Hành động ngay — không qua giai đoạn khám phá.

Phân tích đối số:
- `--che-do` (mặc định: suy ra từ ngày — Q1-Q3 mặc định `hang-quy`, Q4/Tháng 1 mặc định `ca-hai`) — `hang-quy` cho thanh toán thuế ước tính, `1099` cho chuẩn bị 1099-NEC cuối năm, `ca-hai` cho kết hợp
- `--nam` (mặc định: năm hiện tại)

> **Khung:** Mở mọi tài liệu với "Được chuẩn bị để kế toán xem xét — không phải tư vấn thuế."

## Bước 1 — Xác định chế độ

Nếu `--che-do` chưa được cung cấp:
1. Kiểm tra ngày hiện tại. Nếu Tháng 10–Tháng 1, mặc định `ca-hai`. Nếu không, mặc định `hang-quy`.
2. Xác nhận với chủ doanh nghiệp: "Dựa theo thời điểm trong năm, tôi sẽ chuẩn bị [chế độ]. Bạn có muốn làm gì khác không?"

## Bước 2a — Chế độ Thuế Hàng Quý

**Mục tiêu:** Tính thuế thu nhập ước tính và tự doanh nghiệp phải nộp cho quý này.

1. **Lấy thu nhập ròng YTD** từ QuickBooks P&L (đầu năm đến tháng hiện tại).
2. **Ước tính thuế thu nhập doanh nghiệp** dựa trên thu nhập ròng YTD và khung thuế áp dụng.
3. **Trừ các khoản đã nộp** trong các quý trước (nếu biết từ dữ liệu QuickBooks).
4. **Tính khoản nợ quý này**: (Nợ năm dự kiến × %) − Đã nộp
5. **Đặt tên deadline nộp**: ngày đến hạn quý thuế tiếp theo.

Hiển thị:
```
Tóm Tắt Thuế Quý — Chuẩn Bị Cho Kế Toán
(Không phải tư vấn thuế — vui lòng xác minh với kế toán của bạn)

Thu nhập ròng YTD:          {X triệu đồng}
Nợ thuế ước tính năm:       {Y triệu đồng}
Đã nộp các quý trước:       {Z triệu đồng}
Khoản nợ quý này ước tính:  {W triệu đồng}
Deadline nộp:               {ngày}
```

## Bước 2b — Chế độ 1099

**Mục tiêu:** Xác định nhà thầu cần nhận 1099-NEC (thanh toán ≥ 10 triệu đồng trong năm).

1. Quét QuickBooks, PayPal và Stripe để tìm **người không phải nhân viên được thanh toán ≥ 10 triệu đồng** trong năm lịch.
2. Tạo danh sách ứng viên 1099-NEC bao gồm: tên, tổng thanh toán, phương thức thanh toán, trạng thái W-9.
3. Đánh dấu thiếu sót: **Thiếu W-9** (yêu cầu thông tin thuế trước khi nộp), **Mã số thuế chưa xác minh**.
4. Loại trừ: thanh toán cho các công ty (LLC/Corp — kiểm tra W-9 nếu có), giao dịch hàng hóa.

Hiển thị:
```
Danh Sách Ứng Viên 1099-NEC — [Năm]
(Được chuẩn bị để kế toán xem xét — không phải tư vấn thuế)

[Tên]           [Tổng thanh toán]    [Trạng thái W-9]    [Nguồn]
A. Nguyễn       X triệu đồng         ✅ Có                QB
B. Trần         Y triệu đồng         ❌ Thiếu — YÊU CẦU  PayPal
...

Tổng người cần 1099: N
Thiếu W-9: M → cần thu thập trước khi nộp
```

## Bước 3 — Gói bàn giao kế toán

Xuất:
- **`ket-qua-thue-[YYYY]-Q[N].pdf`** (Chế độ hàng quý) hoặc **`danh-sach-1099-[YYYY].xlsx`** (Chế độ 1099)
- Tóm tắt PDF một trang với số liệu chính và danh sách thiếu sót
- Bao gồm chú thích: "Được chuẩn bị bởi [Tên doanh nghiệp] dùng Claude AI — vui lòng xem xét và xác minh trước khi nộp."

## Cổng phê duyệt

- **Không bao giờ nộp thuế** hoặc điền form thay mặt chủ doanh nghiệp.
- **Không tư vấn thuế** — luôn chuyển đến kế toán để xem xét.
- **Không gửi cho kế toán tự động** — hiển thị để chủ doanh nghiệp tự gửi.

## Ví dụ câu kích hoạt

- *"Chuẩn bị tài liệu thuế cho tôi"*
- *"Thuế quý này bao nhiêu?"*
- *"Ai cần nhận 1099 năm nay?"*
- *"Chuẩn bị hồ sơ cho kế toán"*
