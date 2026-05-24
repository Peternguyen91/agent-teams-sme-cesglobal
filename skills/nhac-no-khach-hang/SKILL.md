---
name: nhac-no-khach-hang
description: >
  Soạn email nhắc nhở hóa đơn quá hạn từ dữ liệu QuickBooks và PayPal, khớp
  với lịch sử thanh toán và giọng điệu của từng khách hàng (nhẹ nhàng với
  khách hàng tốt, cứng rắn với người trả trễ thường xuyên). Gửi qua PayPal
  với sự phê duyệt của chủ doanh nghiệp; hóa đơn không phải PayPal xếp hàng
  thành bản nháp email. Dùng khi người dùng hỏi "ai còn nợ tôi tiền", đề cập
  hóa đơn quá hạn, hoặc muốn theo dõi hóa đơn chưa thanh toán.
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu QuickBooks MCP. Tùy chọn: PayPal MCP để gửi nhắc nhở trực tiếp; Gmail MCP để tạo bản nháp."
version: "1.1"
---

# Nhắc Nợ Khách Hàng

## Bắt đầu nhanh

Lấy báo cáo tuổi công nợ phải thu, đánh giá từng khách hàng theo lịch sử thanh toán, soạn nhắc nhở phù hợp giọng điệu cho mỗi hóa đơn quá hạn, và trình bày cho chủ doanh nghiệp. Không gửi gì cho đến khi chủ doanh nghiệp đồng ý.

```
Người dùng: "ai còn nợ tôi tiền"
→ Lấy A/R aging từ QuickBooks
→ Lấy lịch sử thanh toán mỗi khách hàng từ QuickBooks + PayPal
→ Đánh giá giọng điệu: nhẹ (trả đúng hạn thường) / vừa / cứng (thường xuyên trễ)
→ Soạn email cho từng hóa đơn
→ Hiển thị bản nháp, chờ phê duyệt
→ Gửi hoặc xếp hàng bản nháp sau khi phê duyệt
```

## Bước 1 — Lấy công nợ phải thu

Lấy từ QuickBooks:
- A/R Aging Report: tất cả hóa đơn chưa thanh toán
- Nhóm theo: khách hàng, số tiền, ngày hóa đơn, ngày đáo hạn, số ngày quá hạn

Lọc: chỉ những cái quá hạn > 0 ngày (đã qua ngày đáo hạn).

Hiển thị tóm tắt:
```
Tổng công nợ phải thu: X triệu đồng
- 0–30 ngày quá hạn:  Y triệu (N khách)
- 31–60 ngày quá hạn: Y triệu (N khách)
- 61+ ngày quá hạn:   Y triệu (N khách) ← ưu tiên ngay
```

## Bước 2 — Đánh giá lịch sử thanh toán

Với mỗi khách hàng có hóa đơn quá hạn, kiểm tra lịch sử QuickBooks + PayPal:

**Đánh giá khách hàng:**
- 🟢 **Thường xuyên đúng hạn**: < 2 lần trễ trong 12 tháng → giọng nhẹ nhàng
- 🟡 **Thỉnh thoảng trễ**: 2–4 lần trễ → giọng trung tính
- 🔴 **Thường xuyên trễ**: > 4 lần trễ hoặc từng tranh chấp → giọng cứng rắn

## Bước 3 — Soạn email theo giọng điệu

Soạn email cho **từng hóa đơn quá hạn** (không gộp nếu cùng khách có nhiều hóa đơn):

**Giọng nhẹ nhàng** (khách hàng tốt):
```
Chủ đề: Nhắc nhẹ — Hóa đơn #{số} đã đến hạn

Kính gửi [Tên],

Hy vọng mọi việc đang tốt đẹp. Tôi muốn nhắc nhẹ rằng hóa đơn #{số}
với giá trị [X triệu đồng] đã đến hạn vào ngày [ngày].

Nếu bạn đã thanh toán, xin bỏ qua email này. Nếu chưa, bạn có thể
thanh toán tại [link] hoặc liên hệ nếu có bất kỳ câu hỏi nào.

Trân trọng,
[Tên chủ doanh nghiệp]
```

**Giọng trung tính** (thỉnh thoảng trễ):
```
Chủ đề: Hóa đơn #{số} — Thanh toán cần thiết

Kính gửi [Tên],

Đây là thông báo thứ hai về hóa đơn #{số} với giá trị [X triệu đồng],
đáo hạn ngày [ngày] và hiện đã quá hạn [N ngày].

Vui lòng thanh toán trong vòng 5 ngày làm việc hoặc liên hệ để thảo
luận về sắp xếp thanh toán.

Trân trọng,
[Tên chủ doanh nghiệp]
```

**Giọng cứng rắn** (thường xuyên trễ / 60+ ngày):
```
Chủ đề: KHẨN: Hóa đơn #{số} — Quá hạn [N ngày]

Kính gửi [Tên],

Hóa đơn #{số} với giá trị [X triệu đồng] hiện đã quá hạn [N ngày].
Bất chấp các thông báo trước đây, chúng tôi chưa nhận được thanh toán.

Vui lòng thanh toán ngay lập tức tại [link] hoặc liên hệ trong vòng
48 giờ để tránh ảnh hưởng đến dịch vụ.

Trân trọng,
[Tên chủ doanh nghiệp]
```

## Bước 4 — Trình bày để phê duyệt

Hiển thị TẤT CẢ bản nháp với:
- Tên khách hàng + số tiền + số ngày quá hạn
- Đánh giá giọng điệu (nhẹ/trung tính/cứng)
- Bản nháp email đầy đủ

Hỏi: "Bạn muốn gửi tất cả, chọn cụ thể, hay sửa bản nào trước?"

## Bước 5 — Gửi sau khi phê duyệt

**Hóa đơn PayPal**: Gửi nhắc nhở qua API PayPal sau khi chủ doanh nghiệp nói "gửi".

**Hóa đơn không phải PayPal**: Tạo bản nháp email (Gmail/Outlook) cho từng hóa đơn. Chủ doanh nghiệp xem lại và gửi từ hộp thư của mình.

**Luôn xác nhận**: "Đã gửi nhắc nhở cho [Tên Khách Hàng] — [X triệu đồng], quá hạn [N ngày]."

## Xử lý lỗi kết nối

**QuickBooks không khả dụng**: Dừng lại — không thể xác định hóa đơn quá hạn mà không có dữ liệu QB. Thông báo: "Không thể kết nối QuickBooks. Vui lòng kiểm tra kết nối và thử lại."

**PayPal không khả dụng**: Tiếp tục soạn và hiển thị bản nháp bình thường. Bỏ qua bước gửi qua PayPal — chuyển sang tạo bản nháp Gmail cho tất cả hóa đơn. Ghi chú: "PayPal không kết nối — tất cả nhắc nhở sẽ được tạo thành bản nháp Gmail."

**Gmail không khả dụng**: Soạn văn bản email và hiển thị trực tiếp trong chat để chủ sao chép thủ công. Ghi chú rõ ràng cho mỗi bản nháp.

## Cổng phê duyệt

- **Không bao giờ gửi email mà không có phê duyệt rõ ràng.** Luôn hiển thị bản nháp trước.
- **Không bao giờ gửi nhiều nhắc nhở cho cùng một hóa đơn** trong cùng phiên — kiểm tra lịch sử nhắc nhở trước.
- **Không bao giờ tự động xóa hoặc điều chỉnh hóa đơn** trong QuickBooks hoặc PayPal.

## Ví dụ câu kích hoạt

- *"Ai còn nợ tôi tiền?"*
- *"Nhắc khách hàng chưa thanh toán hóa đơn"*
- *"Gửi email đòi nợ cho khách"*
- *"Công nợ phải thu của tôi thế nào?"*
