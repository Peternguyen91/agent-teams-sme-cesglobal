---
name: giai-quyet-phan-nan
description: >
  Xử lý phàn nàn của khách hàng từ đầu đến cuối — tải ngữ cảnh, soạn phản
  hồi phù hợp, và đề xuất cải thiện quy trình nếu phát hiện vấn đề lặp lại.
  Kết hợp kỹ năng xu-ly-khieu-nai và do-nhiet-do-khach-hang. Chấp nhận ID
  email hoặc ID ticket tùy chọn. Kích hoạt khi: "xử lý phàn nàn này",
  "giải quyết khiếu nại", "khách hàng không hài lòng".
allowed-tools: Read, WebFetch, Bash
---

# Giải Quyết Phàn Nàn

Xử lý phàn nàn của khách hàng bằng cách kết hợp hai kỹ năng. Đọc nội dung phàn nàn, thu thập ngữ cảnh, soạn phản hồi phù hợp, và đề xuất cải thiện để tránh lặp lại.

```
Ví dụ: "Giải quyết phàn nàn này" [ID hoặc văn bản phàn nàn]
→ Tải nội dung phàn nàn
→ Xem lịch sử khách: giá trị vòng đời, lần phàn nàn trước, giao dịch
→ Soạn phản hồi phù hợp lịch sử và mức độ nghiêm trọng
→ Kiểm tra xem đây có phải vấn đề lặp lại không
→ Trình bày ngữ cảnh + bản thảo + đề xuất cải thiện quy trình
```

Phân tích đối số:
- `EMAIL_HOAC_ID_TICKET` (tùy chọn) — ID chuỗi Gmail, ID ticket HubSpot, hoặc "moi-nhat" để lấy phàn nàn chưa giải quyết gần nhất. Nếu bỏ trống, yêu cầu chủ doanh nghiệp dán nội dung phàn nàn.

---

## Bước 1 — Tải nội dung phàn nàn (kỹ năng xu-ly-khieu-nai)

Sử dụng quy trình kỹ năng `xu-ly-khieu-nai`:

1. Nếu có ID: lấy toàn bộ chuỗi từ Gmail hoặc HubSpot.
2. Nếu là "moi-nhat": lấy ticket HubSpot hoặc chuỗi Gmail chưa giải quyết gần nhất được gắn thẻ phàn nàn/hỗ trợ.
3. Nếu không có gì: yêu cầu chủ doanh nghiệp dán nội dung phàn nàn trực tiếp.
4. Xác định: tên khách hàng, thông tin đơn hàng/tài khoản, lý do không hài lòng, yêu cầu cụ thể của họ.

**Nếu Gmail và HubSpot đều không kết nối được:** yêu cầu chủ doanh nghiệp dán nội dung phàn nàn — kỹ năng này hoạt động với input thủ công. Nếu PayPal không kết nối: bỏ qua tra cứu giao dịch và ghi chú "PayPal chưa kết nối — không có dữ liệu đơn hàng, làm việc từ nội dung phàn nàn."

---

## Bước 2 — Thu thập ngữ cảnh

1. Tìm kiếm lịch sử khách trong HubSpot: lần mua trước, phàn nàn trước đó, giai đoạn vòng đời, giá trị vòng đời.
2. Tìm giao dịch liên quan trong PayPal: trạng thái đơn hàng, lịch sử hoàn tiền, trạng thái tranh chấp.
3. Tóm tắt: "Đây là khách {mới/cũ}, {tổng giá trị mua hàng} triệu đồng, {0/N} lần phàn nàn trước. Vấn đề hiện tại: {một câu}."

---

## Bước 3 — Soạn phản hồi (kỹ năng xu-ly-khieu-nai)

Sử dụng quy trình kỹ năng `xu-ly-khieu-nai` để soạn phản hồi phù hợp tông và lịch sử:

1. Soạn phản hồi phù hợp mức độ và lịch sử của khách:
   - **Lần phàn nàn đầu, giá trị cao** → đồng cảm, hào phóng, định hướng giải pháp
   - **Phàn nàn lặp lại** → chuyên nghiệp, kiên định, tập trung giải pháp
   - **Tông hung hăng hoặc thô lỗ** → chuyên nghiệp, ngắn gọn, giữ ranh giới
2. Bao gồm: ghi nhận vấn đề, giải thích (nếu biết), đề xuất giải quyết, bước tiếp theo rõ ràng.
3. **Trình bày bản thảo cho chủ doanh nghiệp. KHÔNG gửi.**

---

## Bước 4 — Đề xuất cải thiện quy trình (kỹ năng do-nhiet-do-khach-hang)

1. Kiểm tra xem phàn nàn này có khớp với vấn đề đã biết không (từ các lần chạy `/kiem-tra-mach-dap-khach-hang` trước hoặc các phàn nàn tương tự trong HubSpot).
2. Nếu là vấn đề lặp lại: "Đây là lần thứ {N} phàn nàn về {vấn đề} trong tháng này. Cân nhắc: {thay đổi quy trình cụ thể}."
3. Nếu là sự cố đơn lẻ: "Đây có vẻ là sự cố riêng lẻ. Chưa phát hiện vấn đề có hệ thống."

---

## Cổng phê duyệt

- **Không bao giờ gửi phản hồi mà không có phê duyệt rõ ràng từ chủ doanh nghiệp.** Chỉ soạn thảo.
- **Không bao giờ tự hoàn tiền hoặc cấp tín dụng.** Trình bày tùy chọn; chủ doanh nghiệp quyết định.
- **Không bao giờ đóng ticket hoặc giải quyết tranh chấp mà không có xác nhận của chủ.**

---

## Kết quả đầu ra

Trình bày tóm tắt ngữ cảnh khách hàng, bản thảo phản hồi đã soạn, và đề xuất cải thiện quy trình (nếu phát hiện vấn đề lặp lại). Hỏi: "Bạn muốn gửi phản hồi này, chỉnh sửa thêm, hay xử lý theo cách khác?"

## Ví dụ câu kích hoạt

- *"Xử lý phàn nàn này cho tôi"*
- *"Giải quyết khiếu nại mới nhất"*
- *"Khách hàng không hài lòng, cần phản hồi"*
- *"Xem ticket hỗ trợ ID #123 và soạn trả lời"*
- *"Handle complaint từ email này"*
