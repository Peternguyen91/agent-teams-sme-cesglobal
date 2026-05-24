---
name: kiem-tra-mach-dap-khach-hang
description: >
  Tổng hợp chủ đề từ tranh chấp PayPal, ticket HubSpot và file xuất đánh giá
  thành danh sách top-3 vấn đề có thể khắc phục kèm mẫu phản hồi đã soạn sẵn
  để chủ doanh nghiệp xem xét. Chấp nhận đối số --tu-ngay. Kích hoạt khi:
  "kiểm tra mạch đập khách hàng", "vấn đề nào đang lặp lại", "top vấn đề
  khách hàng", "phản hồi nào cần gửi tuần này".
allowed-tools: Read, WebFetch, Bash
---

# Kiểm Tra Mạch Đập Khách Hàng

Chạy tổng hợp phản hồi khách hàng. Lấy tín hiệu từ tất cả nguồn đã kết nối, xác định 3 vấn đề thực sự có thể khắc phục, và tạo mẫu phản hồi đã soạn sẵn để chủ doanh nghiệp xem xét.

```
Ví dụ: "Top vấn đề khách hàng tháng này là gì?"
→ Thu thập: tranh chấp PayPal + ticket HubSpot + đánh giá
→ Phân cụm thành chủ đề với đánh giá tác động
→ Chọn top 3 vấn đề có thể khắc phục
→ Tạo mẫu phản hồi cho từng vấn đề
→ Trình bày bảng tóm tắt + mẫu để chủ phê duyệt
```

Phân tích đối số:
- `--tu-ngay` (mặc định: 30 ngày qua) — ngày bắt đầu `YYYY-MM-DD` cho cửa sổ nhìn lại

---

## Bước 1 — Thu thập tín hiệu phản hồi (kỹ năng do-nhiet-do-khach-hang)

Sử dụng quy trình kỹ năng `do-nhiet-do-khach-hang`:

1. Lấy tranh chấp và chargeback PayPal trong kỳ: mã lý do, số tiền, trạng thái giải quyết.
2. Lấy ticket hỗ trợ và ghi chú hội thoại HubSpot trong kỳ.
3. Nếu có file xuất đánh giá (CSV từ Google Reviews, xuất Yelp, v.v.) trong Files: đọc và phân tích.
4. Đếm tổng số tín hiệu mỗi nguồn.

**Nếu connector bị thiếu:** chạy với bất kỳ nguồn nào đã kết nối — kỹ năng này giảm cấp nhẹ nhàng. Ghi chú nguồn nào bị bỏ qua. Nếu không có nguồn nào kết nối: dừng lại và thông báo: "Chưa có nguồn phản hồi nào kết nối. Kết nối ít nhất một trong số PayPal, HubSpot, hoặc tải lên file CSV đánh giá."

---

## Bước 2 — Trích xuất chủ đề

Phân cụm tất cả tín hiệu thành các chủ đề lặp lại. Với mỗi chủ đề:
- Đếm số tín hiệu đề cập đến chủ đề đó
- Phân loại: Chất lượng sản phẩm / Giao hàng / Thanh toán / Giao tiếp / Sai lệch kỳ vọng / Khác
- Đánh giá tác động: 🔴 Cao (rủi ro doanh thu, mất khách) / 🟡 Trung bình / 🟢 Thấp

---

## Bước 3 — Top-3 vấn đề có thể khắc phục (kỹ năng xu-ly-khieu-nai)

Chọn top 3 chủ đề theo: tần suất × mức tác động. Với mỗi vấn đề:
1. Nêu vấn đề trong một câu
2. Giải thích nguyên nhân gốc rễ (nếu rõ ràng)
3. Đề xuất cải thiện quy trình cụ thể
4. Soạn mẫu phản hồi khách hàng

**Định dạng mẫu phản hồi:**
```
Tiêu đề: Re: {chủ đề vấn đề}

Chào {tên},

Cảm ơn bạn đã liên hệ với chúng tôi. {Ghi nhận trải nghiệm của họ trong 1-2 câu}.

{Chúng tôi đang làm gì / điều gì đã xảy ra / giải pháp đề xuất}.

{Bước tiếp theo hoặc đề xuất}.

{Lời kết}
```

**Lưu ý bảo mật:** Chỉ dùng tên + chữ cái đầu họ (ví dụ: "Anh Minh N.") trong mẫu — không bao gồm địa chỉ email đầy đủ, số điện thoại, hoặc thông tin đặt hàng cụ thể trong báo cáo tóm tắt.

---

## Bước 4 — Bảng tóm tắt

Định dạng đầu ra:

```
Mạch Đập Khách Hàng — {phạm vi ngày}
Tổng tín hiệu: {n} (Tranh chấp PayPal: {n} | Ticket HubSpot: {n} | Đánh giá: {n})

TOP 3 VẤN ĐỀ CÓ THỂ KHẮC PHỤC
1. {Vấn đề} ({tần suất}) — {tác động} — Khắc phục: {một dòng giải pháp}
2. {Vấn đề} ({tần suất}) — {tác động} — Khắc phục: {một dòng giải pháp}
3. {Vấn đề} ({tần suất}) — {tác động} — Khắc phục: {một dòng giải pháp}
```

---

## Cổng phê duyệt

- **Không bao giờ tự gửi email phản hồi.** Chỉ trình bày mẫu để chủ xem xét.
- **Không bao giờ đóng ticket HubSpot hoặc giải quyết tranh chấp PayPal mà không có xác nhận rõ ràng từ chủ doanh nghiệp.**
- **Không bao giờ đưa thông tin cá nhân của khách hàng vào bảng tóm tắt** — chỉ dùng tên + chữ cái đầu họ.

---

## Kết quả đầu ra

Trình bày bảng tóm tắt, sau đó từng mẫu phản hồi. Hỏi chủ doanh nghiệp muốn gửi mẫu nào, rồi chờ phê duyệt rõ ràng trước khi soạn thảo lệnh gửi.

## Ví dụ câu kích hoạt

- *"Kiểm tra mạch đập khách hàng tháng này"*
- *"Vấn đề nào đang lặp lại với khách hàng?"*
- *"Top 3 khiếu nại cần giải quyết tuần này"*
- *"Có bao nhiêu tranh chấp và về vấn đề gì?"*
- *"Soạn mẫu phản hồi cho các vấn đề phổ biến nhất"*
