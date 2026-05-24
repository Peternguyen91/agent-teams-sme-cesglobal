---
name: kiem-tra-gia-ban
description: Tạo bảng margin theo sản phẩm, ba kịch bản định giá, và bản tóm tắt thông điệp cho khách hàng để chủ doanh nghiệp thấy bức tranh tài chính đầy đủ trước khi ra quyết định giá. Chấp nhận tùy chọn tên sản phẩm.
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu QuickBooks MCP. Tùy chọn: PayPal MCP để đối chiếu doanh thu."
version: "1.1"
---

Chạy phân tích giá. Lấy dữ liệu chi phí và doanh thu, xây dựng bảng margin, mô hình ba kịch bản giá, và soạn thông điệp truyền thông cho khách hàng — để chủ doanh nghiệp thấy rõ toàn bộ bức tranh trước khi quyết định.

Phân tích đối số:
- `TEN_SAN_PHAM` (tùy chọn) — sản phẩm hoặc dịch vụ cụ thể để phân tích; nếu bỏ qua, phân tích tất cả sản phẩm đang hoạt động

---

## Bước 1 — Margin hiện tại

Dùng quy trình kỹ năng `phan-tich-bien-loi-nhuan`:

1. Lấy doanh thu QuickBooks theo sản phẩm/dịch vụ trong 90 ngày qua.
2. Lấy COGS hoặc chi phí trực tiếp mỗi sản phẩm từ QuickBooks (nếu đã phân loại).
3. Lấy tổng doanh thu PayPal cho cùng sản phẩm để đối chiếu.
4. Tính margin gộp hiện tại mỗi sản phẩm: (doanh thu − COGS) ÷ doanh thu.

Xuất bảng margin:

```
Sản phẩm         | Doanh thu  | Chi phí  | Lợi nhuận gộp | Margin %
[sản phẩm]       | X triệu   | X triệu  | X triệu       | X%
```

Đánh dấu bất kỳ sản phẩm nào có margin dưới 20% là rủi ro.

Nếu COGS không có trong QuickBooks, hỏi người dùng ước tính chi phí trực tiếp mỗi sản phẩm trước khi tiếp tục.

---

## Bước 2 — Ba kịch bản định giá

Với mỗi sản phẩm trong phân tích, **không khuyến nghị giá** — chỉ trình bày dữ liệu.

**Kịch bản A — Giữ nguyên giá hiện tại**
- Dự báo doanh thu theo giá × khối lượng hiện tại
- Dự báo margin theo COGS hiện tại

**Kịch bản B — Tăng giá (+10% đến +20%, chủ doanh nghiệp chỉ định)**
- Dự báo doanh thu khi khối lượng giảm 0%, 5%, 10%
- Hiển thị điểm hòa vốn — khối lượng cần để duy trì lợi nhuận hiện tại

**Kịch bản C — Giảm giá (−10%, để thúc đẩy khối lượng)**
- Dự báo doanh thu khi khối lượng tăng 10%, 20%, 30%
- Hiển thị khối lượng cần để khớp lợi nhuận hiện tại

```
[TÊN SẢN PHẨM] — Giá hiện tại: X.000đ | Margin hiện tại: Y%

              Giữ nguyên   Tăng +10%    Tăng +20%   Giảm −10%
Khối lượng ±0%: Doanh thu  Doanh thu   Doanh thu   Doanh thu
Thay đổi −5%:   Doanh thu  Doanh thu   Doanh thu   —
Thay đổi +10%:  —          —           —           Doanh thu

↑ Điểm hòa vốn:
  Tăng +10% → khối lượng có thể giảm tối đa X% trước khi lợi nhuận giảm
  Tăng +20% → khối lượng có thể giảm tối đa X% trước khi lợi nhuận giảm
```

---

## Bước 3 — Bản tóm tắt thông điệp khách hàng

Nếu đang cân nhắc kịch bản tăng giá, soạn bản tóm tắt thông điệp cho khách hàng:

**Một đoạn giải thích thay đổi** — ngắn gọn, tập trung vào lý do (chi phí vận hành, đầu tư chất lượng, v.v.)

**Ba lựa chọn thông điệp:**
- *Trực tiếp:* "Từ [ngày], giá [sản phẩm] sẽ điều chỉnh lên [giá mới]. Chúng tôi trân trọng sự đồng hành của bạn và cam kết tiếp tục..."
- *Tập trung vào giá trị:* "Chúng tôi đã đầu tư [cải thiện cụ thể]. Để duy trì chất lượng này, giá sẽ được điều chỉnh..."
- *Đồng cảm:* "Chúng tôi hiểu mọi sự thay đổi đều cần thích nghi. Vì vậy chúng tôi thông báo trước [X tuần]..."

**Thời điểm và kênh đề xuất:** email thông báo trước 2–4 tuần; ghi chú trên hóa đơn; thông báo trực tiếp với khách hàng lớn.

---

## Xử lý lỗi kết nối

Nếu QuickBooks không khả dụng, dừng lại — phân tích margin yêu cầu dữ liệu doanh thu và chi phí QB. Nếu PayPal không có, chạy từ QB và ghi chú "PayPal chưa kết nối — bỏ qua đối chiếu doanh thu PayPal."

---

## Cổng phê duyệt

- **Không bao giờ khuyến nghị mức giá cụ thể.** Chỉ cung cấp dữ liệu và kịch bản — quyết định thuộc về chủ doanh nghiệp.
- **Không bao giờ cập nhật giá** trên bất kỳ nền tảng nào (QB, PayPal, v.v.).
- **Đánh dấu rõ khi dữ liệu COGS bị ước tính** thay vì đến trực tiếp từ QuickBooks.

---

## Kết quả đầu ra

Trình bày bảng margin, sau đó ba bảng kịch bản. Nếu kịch bản tăng giá đang được xem xét, thêm bản tóm tắt thông điệp khách hàng. Kết thúc bằng: "Kịch bản nào bạn muốn khám phá thêm?"

---

## Ví dụ câu kích hoạt

- *"Kiểm tra giá cho tôi"*
- *"Margin theo sản phẩm đang thế nào?"*
- *"Tôi có nên tăng giá không?"*
- *"Phân tích giá bán sản phẩm X"*
- *"Chi phí đang tăng, tôi cần xem lại giá"*
