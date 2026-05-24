---
name: review-hop-dong
description: >
  Xem xét hợp đồng bằng ngôn ngữ dễ hiểu, phát hiện điểm rủi ro có phân loại
  mức độ và xuất bản đỏ đánh dấu dưới dạng DOCX/PDF để chủ doanh nghiệp dùng
  trong đàm phán. Chấp nhận đường dẫn file cục bộ hoặc ID phong bì DocuSign.
  Kích hoạt khi: "xem lại hợp đồng này", "kiểm tra điều khoản", "có điểm gì
  nguy hiểm không", "đánh dấu rủi ro hợp đồng".
allowed-tools: Read, WebFetch, Bash
---

# Xem Xét Hợp Đồng

Chạy quy trình xem xét hợp đồng ngay. Đọc tài liệu, giải thích nội dung, đánh dấu rủi ro, và xuất bản đỏ để chủ doanh nghiệp dùng khi đàm phán.

```
Ví dụ: "Xem lại hợp đồng dịch vụ này cho tôi"
→ Đọc file hợp đồng
→ Tóm tắt 3 đoạn bằng ngôn ngữ đơn giản
→ Liệt kê rủi ro với mức độ 🔴🟡🟢
→ Xuất danh sách bản đỏ cụ thể
→ Hỏi có muốn xuất file DOCX đánh dấu không
```

> ⚠️ **Đây không phải tư vấn pháp lý.** Luôn xem xét với luật sư trước khi ký bất kỳ hợp đồng nào.

Phân tích đối số:
- `DUONG_DAN_FILE_HOAC_ID_PHONG_BI` — đường dẫn file PDF/DOCX cục bộ, hoặc ID phong bì DocuSign; nếu bỏ trống, kiểm tra phong bì mới nhất đang chờ ký trong DocuSign

---

## Bước 1 — Tải hợp đồng

1. Nếu có đường dẫn file: đọc tài liệu từ Files hoặc Desktop.
2. Nếu có ID phong bì DocuSign: lấy tài liệu từ DocuSign.
3. Nếu không có gì: kiểm tra DocuSign xem có phong bì mới nhất với trạng thái `chờ ký` không, xác nhận với chủ doanh nghiệp trước khi tiếp tục.

**Nếu DocuSign không kết nối và không có đường dẫn file:** yêu cầu chủ doanh nghiệp tải lên hợp đồng dạng PDF hoặc DOCX. Kỹ năng này hoạt động hoàn toàn offline với file cục bộ — connector là tùy chọn.

---

## Bước 2 — Tóm tắt bằng ngôn ngữ đơn giản

Viết tóm tắt 3 đoạn:

1. **Hợp đồng này làm gì** — mô tả giao dịch bằng ngôn ngữ đơn giản (ai, làm gì, bao nhiêu tiền, trong bao lâu)
2. **Nghĩa vụ chính** — chủ doanh nghiệp phải làm gì và khi nào
3. **Quyền lợi chính** — chủ doanh nghiệp được gì và các điều kiện chấm dứt hoặc thoát hợp đồng

---

## Bước 3 — Danh sách rủi ro

Với mỗi rủi ro, đánh giá mức độ: 🔴 Cao / 🟡 Trung bình / 🟢 Thấp

Phải kiểm tra tối thiểu:
- Điều khoản tự động gia hạn với cửa sổ hủy ngắn
- Quyền thay đổi giá một chiều
- Chuyển nhượng quyền sở hữu trí tuệ diện rộng
- Trách nhiệm pháp lý không giới hạn hoặc thiếu điều khoản giới hạn trách nhiệm
- Điều khoản độc quyền
- Điều khoản không cạnh tranh hoặc không dụ dỗ nhân viên
- Điều khoản thanh toán hoặc phạm vi dịch vụ mơ hồ

Định dạng mỗi rủi ro:
```
{Mức độ} {Tên điều khoản} — {nội dung bằng ngôn ngữ đơn giản} — Đề xuất sửa: {cách sửa cụ thể}
```

---

## Bước 4 — Danh sách bản đỏ cụ thể

Tạo danh sách đề xuất sửa đổi cụ thể theo định dạng:
```
§{điều khoản}: XÓA "[ngôn ngữ gốc]" / THÊM "[ngôn ngữ đề xuất thay thế]"
Lý do: {một câu giải thích}
```

Đề xuất xuất danh sách này dưới dạng DOCX hoặc PDF có đánh dấu lưu vào Files hoặc Desktop.

---

## Xử lý lỗi connector

- Nếu DocuSign kết nối được nhưng ID phong bì không hợp lệ: báo lỗi và yêu cầu chủ doanh nghiệp kiểm tra lại ID.
- Nếu không có connector nào và không có file: yêu cầu tải lên file PDF hoặc DOCX.
- Kỹ năng này hoạt động hoàn toàn với file cục bộ — không cần connector.

---

## Cổng phê duyệt

- **Không bao giờ ký, gửi, hoặc chỉnh sửa phong bì DocuSign thực tế.** Chỉ trình bày kết quả xem xét và chờ chủ doanh nghiệp quyết định.
- **Luôn cảnh báo:** "Đây không phải tư vấn pháp lý. Xem xét với luật sư trước khi ký."
- **Không bao giờ xóa hoặc ghi đè tài liệu gốc.**

---

## Kết quả đầu ra

Trình bày tóm tắt bằng ngôn ngữ đơn giản, danh sách rủi ro phân mức độ, và các đề xuất bản đỏ. Hỏi chủ doanh nghiệp có muốn xuất file DOCX đánh dấu và lưu ở đâu không.

## Ví dụ câu kích hoạt

- *"Xem lại hợp đồng này cho tôi"*
- *"Tôi đang ký gì vậy?"*
- *"Có điểm gì nguy hiểm không?"*
- *"Kiểm tra điều khoản thanh toán trong hợp đồng"*
- *"Đánh dấu rủi ro và xuất bản đỏ"*
