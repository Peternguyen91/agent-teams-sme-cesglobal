---
name: bao-cao-quy
description: Tạo tường thuật QBR đầy đủ — xu hướng doanh thu, xu hướng margin, sức khỏe khách hàng, cơ hội và rủi ro hàng đầu — dưới dạng PDF hoặc deck sẵn sàng trình bày. Chấp nhận tùy chọn quý và nơi lưu.
allowed-tools: Read, WebFetch, Bash
---

Chạy đánh giá kinh doanh quý. Lấy dữ liệu tài chính, bán hàng và khách hàng cho quý, tổng hợp thành tường thuật, và tạo tài liệu sẵn sàng trình bày.

Phân tích đối số:
- `--quy` (mặc định: quý lịch trước) — định dạng `YYYY-QN` (ví dụ: `2026-Q1`)
- `--luu-vao` (mặc định: `files`) — `files` (Google Drive / OneDrive), `may-tinh`, hoặc `ca-hai`

## Bước 1 — Hiệu suất tài chính

Dùng kỹ năng `bao-cao-tong-quan` ở chế độ sâu:

1. Lấy P&L QuickBooks cho quý: doanh thu, giá vốn hàng bán (COGS), lợi nhuận gộp, chi phí vận hành, lợi nhuận ròng.
2. So sánh với quý trước và cùng quý năm trước (nếu có).
3. Lấy thanh toán PayPal cùng kỳ để đối chiếu doanh thu QB.
4. Tính: % tăng trưởng doanh thu, thay đổi margin theo điểm, top 3 danh mục doanh thu.

## Bước 2 — Sức khỏe khách hàng

1. Lấy dữ liệu deal HubSpot: khách hàng mới thắng, mất, giá trị deal trung bình, pipeline bước vào quý tiếp theo.
2. Tính chi phí thu hút khách hàng (nếu có dữ liệu) và doanh thu trên mỗi khách hàng.
3. Đánh dấu khách hàng nào chiếm >20% doanh thu (rủi ro tập trung).

## Bước 3 — Cơ hội hàng đầu

Xác định 3 cơ hội cụ thể cho quý tiếp theo dựa trên dữ liệu:
- Tiềm năng doanh thu (danh mục, phân khúc khách hàng, hoặc kênh cần tăng gấp đôi)
- Tiềm năng margin (chi phí để cắt hoặc giá để tăng)
- Tiềm năng khách hàng (phân khúc để nhắm hoặc tỷ lệ rời bỏ để giảm)

## Bước 4 — Rủi ro hàng đầu

Xác định 3 rủi ro cụ thể cho quý tiếp theo:
- Rủi ro doanh thu (tập trung, xu hướng, mùa vụ)
- Rủi ro margin (chi phí tăng, áp lực giá)
- Rủi ro vận hành (khoảng trống pipeline, phụ thuộc nhà cung cấp)

## Bước 5 — Tường thuật QBR

Viết tường thuật 500–800 từ bằng tiếng Việt kinh doanh rõ ràng với cấu trúc này:
1. Tiêu đề quý (một câu)
2. Câu chuyện doanh thu (xu hướng + lý do)
3. Câu chuyện margin (xu hướng + lý do)
4. Câu chuyện khách hàng (sức khỏe + pipeline)
5. Ba cơ hội
6. Ba rủi ro
7. Một đoạn kêu gọi hành động cho quý tiếp theo

## Bước 6 — Xuất

Tạo:
1. **`bao-cao-quy-{YYYY-QN}.pdf`** — tường thuật đã định dạng + biểu đồ chính (dưới dạng bảng ASCII nếu không có công cụ biểu đồ)
2. Lưu vào vị trí `--luu-vao`

## Xử lý khi phần mềm thiếu

Nếu QuickBooks không khả dụng, dừng lại — QBR cần dữ liệu tài chính QB làm nền tảng. Nếu PayPal thiếu, bỏ qua đối chiếu và ghi chú "PayPal chưa kết nối — doanh thu chỉ được đối chiếu từ QB". Nếu HubSpot thiếu, bỏ qua sức khỏe khách hàng (Bước 2) và ghi chú.

## Cổng phê duyệt

- **Không bao giờ tự động phát hành hoặc email QBR.** Luôn hiển thị cho chủ doanh nghiệp xem trước.
- **Đánh dấu nếu nguồn dữ liệu nào trả về dữ liệu không đầy đủ** — ghi chú khoảng trống trong tường thuật.

## Kết quả đầu ra

Trình bày tường thuật nội tuyến, rồi xác nhận xuất. Kết thúc với đoạn tóm tắt "tập trung vào điều gì cho quý tiếp theo".

## Ví dụ câu kích hoạt

- *"Làm báo cáo quý cho tôi"*
- *"Deck QBR Q1 đâu?"*
- *"Đánh giá kết quả 3 tháng vừa rồi"*
- *"Chuẩn bị báo cáo cho ban lãnh đạo"*
