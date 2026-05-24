---
name: phan-tich-bien-loi-nhuan
description: >
  Phân tích kinh tế đơn vị theo sản phẩm hoặc dịch vụ dùng dữ liệu PayPal và
  QuickBooks, đối chiếu với lạm phát và thay đổi chi phí, và hiển thị dữ liệu
  kịch bản định giá (ví dụ "tăng 5% lịch sử tương quan với giảm ~3% khối lượng").
  Chỉ hiển thị phân tích — không khuyến nghị giá. Dùng khi người dùng hỏi về
  tăng giá, phân tích margin, nên tính bao nhiêu, chi phí có đang ăn vào lợi
  nhuận không, hoặc thay đổi giá sẽ ảnh hưởng thế nào. Kích hoạt ngay cả khi
  người dùng không nói rõ "margin" — các cụm từ như "tôi có kiếm đủ không?",
  "có nên tính cao hơn không?", hay "chi phí của tôi đang tăng" đều gọi kỹ năng này.
---

# Phân Tích Biên Lợi Nhuận

> Chỉ hiển thị phân tích. Không khuyến nghị giá.

## Bắt đầu nhanh

```
Người dùng: "chi phí của tôi đang tăng, tôi có nên tính cao hơn không?"
→ Lấy doanh thu và COGS QuickBooks theo sản phẩm (90 ngày)
→ Đối chiếu PayPal để phát hiện thay đổi khối lượng
→ Tính margin gộp hiện tại theo sản phẩm
→ Xây dựng ba kịch bản: +5%, +10%, +15%
→ Hiển thị dữ liệu: "Với mức tăng +10%, nếu khối lượng giảm ≤15%, doanh thu ròng tăng"
→ Kết thúc: "Dưới đây là dữ liệu — quyết định về giá là của bạn."
```

## Bước 1 — Hiểu sản phẩm/dịch vụ

Nếu người dùng không chỉ định sản phẩm, hỏi: "Bạn muốn phân tích cụ thể sản phẩm hay dịch vụ nào, hay tất cả?"

Lấy từ QuickBooks:
- Danh sách sản phẩm/dịch vụ và doanh thu 90 ngày qua
- COGS hoặc chi phí trực tiếp mỗi mặt hàng (nếu đã phân loại)
- Bất kỳ thay đổi chi phí gần đây nào (nhà cung cấp, nguyên liệu)

## Bước 2 — Tính margin hiện tại

Với mỗi sản phẩm/dịch vụ:

```
Margin gộp = (Doanh thu - COGS) ÷ Doanh thu × 100%
```

Hiển thị bảng:
| Sản phẩm | Doanh thu/đơn | Chi phí/đơn | Margin gộp | Khối lượng 90 ngày |
|----------|---------------|-------------|------------|-------------------|
| A        | X triệu       | Y triệu     | Z%         | N đơn vị          |

Đánh dấu:
- 🔴 Margin < 20% — rủi ro cao
- 🟡 Margin 20-40% — cần theo dõi
- 🟢 Margin > 40% — tốt

## Bước 3 — Ba kịch bản định giá

Với mỗi sản phẩm/dịch vụ đang phân tích, tính ba kịch bản tăng giá:

| Kịch bản | Tăng giá | Khối lượng -5% | Khối lượng -10% | Khối lượng -15% |
|----------|----------|----------------|-----------------|-----------------|
| Nhỏ      | +5%      | Doanh thu ròng | Doanh thu ròng  | Doanh thu ròng  |
| Vừa      | +10%     | Doanh thu ròng | Doanh thu ròng  | Doanh thu ròng  |
| Mạnh     | +15%     | Doanh thu ròng | Doanh thu ròng  | Doanh thu ròng  |

Đánh dấu điểm hòa vốn: tại mức tăng giá X%, khối lượng phải giảm bao nhiêu để doanh thu ròng giảm.

## Bước 4 — Ngữ cảnh thị trường

Ghi chú các yếu tố bên ngoài liên quan (nếu biết):
- Lạm phát tổng quát (CPI Việt Nam gần đây)
- Biến động chi phí nguyên liệu đầu vào phổ biến trong ngành
- Bất kỳ xu hướng giá ngành nào có thể biết

*Lưu ý: Đây là ngữ cảnh chung, không phải dữ liệu ngành cụ thể.*

## Bước 5 — Trình bày phân tích

Kết thúc với:

> "Dưới đây là dữ liệu. Tôi không thể khuyến nghị mức giá đúng — điều đó phụ thuộc vào chiến lược, thị trường và khả năng chấp nhận của khách hàng của bạn. Nhưng dữ liệu cho thấy [X]."

Sau đó hỏi: "Bạn có muốn tôi chạy `/dong-so-cuoi-thang` để xem chi tiết chi phí hơn không?"

## Cổng phê duyệt

- **Không bao giờ khuyến nghị mức giá cụ thể.** Chỉ hiển thị dữ liệu và các kịch bản.
- **Không gửi email hoặc thay đổi giá** trên bất kỳ nền tảng nào.
- **Đánh dấu khi thiếu dữ liệu COGS** — phân tích sẽ không đầy đủ nếu QuickBooks không có phân loại chi phí.

## Ví dụ câu kích hoạt

- *"Chi phí tăng, tôi có nên tăng giá không?"*
- *"Margin của sản phẩm X là bao nhiêu?"*
- *"Tôi có kiếm đủ tiền không?"*
- *"Phân tích lợi nhuận theo sản phẩm"*
