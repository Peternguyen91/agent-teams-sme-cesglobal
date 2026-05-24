---
name: tong-ket-cuoi-tuan
description: Tổng kết cuối tuần — doanh thu so tuần trước, sản phẩm bán chạy nhất, thắng lợi và điểm cần theo dõi. Chấp nhận cửa sổ nhìn lại 7 hoặc 14 ngày.
allowed-tools: Read, WebFetch, Bash
---

Chạy tổng kết thắng lợi và điểm theo dõi cuối tuần. Lấy số liệu, nêu bật điều quan trọng, và đưa cho chủ doanh nghiệp bức tranh cuối tuần rõ ràng.

Phân tích đối số:
- `--nhin-lai` (mặc định: `7 ngay`) — `7 ngay` cho một tuần hoặc `14 ngay` cho so sánh hai tuần liên tiếp

## Bước 1 — Đo mạch doanh thu

Dùng quy trình kỹ năng `bao-cao-tong-quan`:

1. Lấy giao dịch PayPal trong kỳ nhìn lại.
2. Lấy deal HubSpot đã đóng trong cùng kỳ.
3. Tính delta doanh thu tuần-qua-tuần.
4. Nêu bật top 3 nguồn doanh thu (sản phẩm / khách hàng / kênh) xếp theo đóng góp.

## Bước 2 — Phân tích bán hàng

1. Liệt kê top 5 sản phẩm/dịch vụ bán chạy theo doanh số và doanh thu.
2. Liệt kê 3 sản phẩm bán chậm nhất (bất cứ thứ gì di chuyển ít hơn kỳ vọng so kỳ trước).
3. Đánh dấu bất kỳ mặt hàng nào tăng hoặc giảm đột biến (>20% thay đổi).

## Bước 3 — Tóm tắt thắng lợi và theo dõi

Định dạng kết quả:

```
Tổng Kết Thứ Sáu — {ngày}

THẮNG LỢI
• {thắng lợi 1}
• {thắng lợi 2}
• {thắng lợi 3}

CẦN THEO DÕI
• {điểm theo dõi 1} — {hành động khuyến nghị}
• {điểm theo dõi 2} — {hành động khuyến nghị}

Doanh thu tuần này: {X triệu đồng} ({+/-}Z% so tuần trước)
```

## Xử lý khi phần mềm thiếu

Chạy với bất cứ phần mềm nào đã kết nối — lệnh này giảm dần khi thiếu. Nếu PayPal thiếu, bỏ qua dữ liệu giao dịch và ghi chú "PayPal chưa kết nối — dữ liệu doanh thu chỉ từ deal HubSpot". Nếu HubSpot thiếu, bỏ qua deal đã đóng và ghi chú. Nếu cả hai đều thiếu, dừng lại và báo cho chủ doanh nghiệp: "Chưa kết nối nguồn doanh thu nào. Kết nối PayPal hoặc HubSpot để chạy tổng kết cuối tuần."

## Cổng phê duyệt

- **Không bao giờ tự động gửi hoặc đăng bản tin này.** Luôn hiển thị cho chủ doanh nghiệp xem trước.
- **Không bao giờ tự động hủy hoặc sửa đổi bất cứ điều gì.** Chỉ hiển thị dữ liệu và khuyến nghị.

## Kết quả đầu ra

Kết thúc với bản tin đã định dạng và hỏi chủ doanh nghiệp: "Bạn có muốn tôi đăng điều này lên Slack, email cho bản thân, hay lưu lại không?"

## Ví dụ câu kích hoạt

- *"Tổng kết tuần này đi"*
- *"Kết quả tuần thế nào?"*
- *"Tóm tắt thứ Sáu"*
- *"Tuần này chúng ta làm được gì?"*
