---
name: tom-tat-ban-hang
description: Tổng hợp sản phẩm bán chạy và bán chậm, xác định xu hướng theo mùa, và tạo kế hoạch nội dung 2 tuần để đẩy mạnh hàng thắng và xử lý hàng chậm. Chấp nhận tùy chọn khoảng thời gian nhìn lại 30, 60 hoặc 90 ngày.
allowed-tools: Read, WebFetch, Bash
---

Chạy phân tích bán hàng và tạo kế hoạch nội dung. Lấy dữ liệu cái gì đang bán (và cái gì không), giải thích nguyên nhân, và tạo kế hoạch nội dung sẵn sàng dùng ngay dựa trên dữ liệu thực tế.

Phân tích đối số:
- `--nhin-lai` (mặc định: `30d`) — khoảng thời gian nhìn lại: `30d`, `60d`, hoặc `90d`

## Bước 1 — Phân tích doanh số

Sử dụng quy trình kỹ năng `chien-luoc-noi-dung` để phân tích bán hàng:

1. Lấy giao dịch PayPal trong kỳ nhìn lại, phân nhóm theo mặt hàng/dịch vụ/SKU.
2. Lấy doanh thu theo danh mục sản phẩm/dịch vụ từ QuickBooks.
3. Xếp hạng sản phẩm theo: tổng doanh thu, số lượng bán, và biên lợi nhuận (nếu có trong QB).
4. Tính tỷ trọng doanh thu mỗi sản phẩm so với kỳ tương đương trước.

Sản phẩm bán chạy: sản phẩm tăng tỷ trọng hoặc giữ top 3.
Sản phẩm chậm: sản phẩm giảm số lượng hoặc dưới 5% tổng doanh thu.

---

## Bước 2 — Kiểm tra xu hướng theo mùa

1. So sánh kỳ hiện tại với cùng kỳ năm trước (nếu QuickBooks có lịch sử).
2. Đánh dấu mặt hàng có xu hướng theo mùa (ví dụ: tăng đột biến Q4, chậm vào mùa hè).
3. Ghi chú sản phẩm mới chưa đủ dữ liệu để phát hiện xu hướng.

---

## Bước 3 — Phân tích nguyên nhân

Với mỗi sản phẩm bán chạy và bán chậm, giải thích nguyên nhân có thể:
- Thay đổi giá, khuyến mãi, kênh mới, nhu cầu theo mùa, đối thủ thay đổi
- Đối chiếu với hoạt động campaign HubSpot trong kỳ
- Ghi chú rõ khi nào là suy luận và khi nào có bằng chứng

---

## Bước 4 — Kế hoạch nội dung 2 tuần

Tạo kế hoạch nội dung sẵn sàng sử dụng ngay:

```
Kế Hoạch Nội Dung 2 Tuần — {khoảng ngày}

ĐẨY MẠNH (sản phẩm thắng)
• {sản phẩm}: {góc độ gợi ý} — {kênh: email|mạng xã hội|cả hai}
• {sản phẩm}: {góc độ gợi ý} — {kênh}

XỬ LÝ HÀNG CHẬM (slow movers)
• {sản phẩm}: {góc khuyến mãi hoặc gợi ý đóng gói combo} — {kênh}

LỊCH NỘI DUNG
Tuần 1:
  Thứ Hai: {concept bài đăng/email}
  Thứ Tư:  {concept bài đăng/email}
  Thứ Sáu: {concept bài đăng/email}
Tuần 2:
  Thứ Hai: {concept bài đăng/email}
  Thứ Tư:  {concept bài đăng/email}
  Thứ Sáu: {concept bài đăng/email}
```

---

## Xử lý khi connector lỗi

Nếu cả QuickBooks và PayPal đều không kết nối được, dừng lại — phân tích bán hàng cần ít nhất một nguồn doanh thu. Nếu chỉ một trong hai kết nối được, chạy từ nguồn đó và ghi chú. Nếu HubSpot không có, bỏ qua phần đối chiếu campaign và ghi chú.

---

## Cổng phê duyệt

- **Không bao giờ tự lên lịch hay đăng nội dung.** Kế hoạch chỉ để chủ doanh nghiệp xem xét.
- **Không tự tạo ảnh Canva** — đề xuất tạo ảnh sau khi chủ doanh nghiệp duyệt kế hoạch.

---

## Kết quả đầu ra

Trình bày phân tích bán hàng, rồi đến kế hoạch nội dung. Hỏi chủ doanh nghiệp có muốn tạo ảnh Canva cho các bài đã lên kế hoạch không.

## Ví dụ câu kích hoạt

- *"Tóm tắt bán hàng tháng này"*
- *"Sản phẩm nào đang bán chạy?"*
- *"Kế hoạch nội dung 2 tuần"*
- *"Hàng nào đang chậm, xử lý thế nào?"*
