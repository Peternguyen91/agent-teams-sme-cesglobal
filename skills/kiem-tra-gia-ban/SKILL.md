---
name: kiem-tra-gia-ban
description: Tạo bảng margin theo sản phẩm và ba kịch bản định giá để chủ doanh nghiệp thấy bức tranh tài chính đầy đủ trước khi ra quyết định giá. Chấp nhận tùy chọn tên sản phẩm.
allowed-tools: Read, WebFetch, Bash
---

Chạy phân tích giá. Lấy dữ liệu chi phí và doanh thu, xây dựng bảng margin, và mô hình ba kịch bản giá — để chủ doanh nghiệp thấy rõ con số trước khi quyết định giá.

Phân tích đối số:
- `TEN_SAN_PHAM` (tùy chọn) — sản phẩm hoặc dịch vụ cụ thể để phân tích; nếu bỏ qua, phân tích tất cả sản phẩm đang hoạt động

## Bước 1 — Margin hiện tại (phan-tich-bien-loi-nhuan)

Dùng quy trình kỹ năng `phan-tich-bien-loi-nhuan`:

1. Lấy doanh thu QuickBooks theo sản phẩm/dịch vụ trong 90 ngày qua.
2. Lấy COGS hoặc chi phí trực tiếp mỗi sản phẩm từ QuickBooks (nếu đã phân loại).
3. Lấy tổng doanh thu PayPal cho cùng sản phẩm để đối chiếu.
4. Tính margin gộp hiện tại mỗi sản phẩm: (doanh thu − COGS) ÷ doanh thu.

Xuất bảng margin — một hàng mỗi sản phẩm, bao gồm: giá hiện tại, chi phí ước tính, margin gộp %, doanh thu 90 ngày, đơn vị đã bán.

Nếu COGS không có trong QuickBooks, hỏi người dùng ước tính chi phí trực tiếp mỗi sản phẩm.

## Bước 2 — Ba kịch bản định giá

Với mỗi sản phẩm trong phân tích, tính ba kịch bản tăng giá. Cho mỗi kịch bản, mô hình hóa ba mức giảm khối lượng (−5%, −10%, −15%):

```
[TÊN SẢN PHẨM] — Giá hiện tại: X.000đ | Margin hiện tại: Y%

         Tăng +5%    Tăng +10%    Tăng +15%
Vol −0%:  Doanh thu  Doanh thu   Doanh thu
Vol −5%:  Doanh thu  Doanh thu   Doanh thu
Vol −10%: Doanh thu  Doanh thu   Doanh thu
Vol −15%: Doanh thu  Doanh thu   Doanh thu

↑ Điểm hòa vốn (nơi doanh thu ròng không thay đổi):
  +5% → khối lượng có thể giảm tối đa X% trước khi bị tổn thất
  +10% → khối lượng có thể giảm tối đa X% trước khi bị tổn thất
  +15% → khối lượng có thể giảm tối đa X% trước khi bị tổn thất
```

## Bước 3 — Trình bày kết quả

Hiển thị:
1. Bảng margin tóm tắt (tất cả sản phẩm)
2. Bảng kịch bản chi tiết (mỗi sản phẩm đang phân tích)
3. Điểm hòa vốn rõ ràng cho mỗi mức tăng giá

Kết thúc bằng:
> "Dưới đây là dữ liệu. Quyết định về giá là của bạn — những con số này cho thấy bạn có bao nhiêu không gian để di chuyển ở các mức khối lượng khác nhau."

## Cổng phê duyệt

- **Không khuyến nghị mức giá cụ thể.** Chỉ hiển thị dữ liệu và kịch bản.
- **Không thay đổi giá** trên bất kỳ nền tảng nào.
- **Đánh dấu khi dữ liệu COGS bị ước tính** thay vì đến trực tiếp từ QuickBooks.

## Ví dụ câu kích hoạt

- *"Kiểm tra giá cho tôi"*
- *"Margin theo sản phẩm đang thế nào?"*
- *"Tôi có nên tăng giá không?"*
- *"Phân tích giá bán của chúng tôi"*
