---
name: ke-hoach-tra-luong
description: Dự báo tiền mặt, xếp hạng hóa đơn quá hạn, và chuẩn bị nhắc nhở PayPal để chủ doanh nghiệp tự tin chạy bảng lương. Chấp nhận tùy chọn kỳ hạn và ngày trả lương.
allowed-tools: Read, WebFetch, Bash
---

Chạy pipeline tự tin bảng lương bằng cách kết hợp hai kỹ năng. Chủ doanh nghiệp phê duyệt tại mỗi bước chuyển tiếp — không bao giờ gửi nhắc nhở hay xác nhận dự báo mà không có xác nhận rõ ràng.

Phân tích đối số:
- `--ky-han` (mặc định `30`) — cửa sổ dự báo tính bằng ngày (30, 60, hoặc 90)
- `--ngay-tra-luong` (tùy chọn) — ngày bảng lương chạy; mặc định là thứ Sáu tiếp theo

## Bước 1 — Dự báo tiền mặt (du-bao-dong-tien)

Kích hoạt quy trình kỹ năng `du-bao-dong-tien`:
1. Lấy AR, AP và lịch sử tiền mặt từ QuickBooks, PayPal, Stripe, hoặc Square (bất kể cái nào đã kết nối). Dự phòng bằng upload CSV nếu không có phần mềm nào.
2. Lớp chi phí cố định đã biết (tiền thuê, bảng lương, phí định kỳ từ nhà cung cấp).
3. Tạo dự báo 30/60/90 ngày (dùng `--ky-han` yêu cầu) với dải tin cậy phần trăm biến động.
4. Đặt tên rủi ro cụ thể — ví dụ: "Bảng lương ngày 15/5 đến khi số dư tiền mặt thấp hơn mức chi phí cố định 32 triệu đồng theo dự báo trung bình."
5. Xuất tóm tắt chat + XLSX có thể tải xuống.

**Phân tích cụ thể bảng lương**: Xác định ngày `--ngay-tra-luong`. Kiểm tra xem số dư dự kiến có đủ chi trả bảng lương đầy đủ hay không ở mỗi kịch bản (lạc quan, cơ sở, thận trọng).

Hiển thị dự báo. Hỏi: "Dự báo tiền mặt trông như thế nào với bạn? Bạn có muốn tôi tiến hành với các nhắc nhở hóa đơn không?"

**Chờ xác nhận trước khi tiếp tục.**

## Bước 2 — Xếp hạng hóa đơn quá hạn (nhac-no-khach-hang)

Sau khi xác nhận, kích hoạt quy trình kỹ năng `nhac-no-khach-hang`:
1. Lấy A/R aging từ QuickBooks: tất cả hóa đơn quá hạn.
2. Xếp hạng theo mức độ khẩn cấp: (a) số ngày quá hạn nhất, (b) số tiền lớn nhất, (c) lịch sử thanh toán tốt nhất (khách tốt trả trước).
3. Đánh giá điểm giọng điệu mỗi khách hàng: 🟢 nhẹ nhàng / 🟡 trung tính / 🔴 cứng rắn.
4. Soạn email nhắc nhở phù hợp giọng điệu cho mỗi hóa đơn.
5. Trình bày TẤT CẢ bản nháp cho chủ doanh nghiệp phê duyệt trước khi gửi bất cứ điều gì.

**Kết nối với bảng lương**: Ưu tiên các nhắc nhở sẽ thu hồi đủ tiền trước ngày trả lương. Hiển thị:
> "Thu hồi đầy đủ [top N hóa đơn] có thể đưa số dư dự báo lên [X triệu đồng] — đủ bao gồm bảng lương [ngày]."

## Bước 3 — Xác nhận bảng lương

Sau khi nhắc nhở được phê duyệt (hoặc xếp hàng chờ), đưa ra đánh giá bảng lương cuối cùng:

```
Tóm Tắt Sẵn Sàng Bảng Lương — {ngày}

Bảng lương ngày [ngày]: [X triệu đồng]

Tiền mặt hiện tại:           [A triệu đồng]
Thanh toán đến (dự kiến):    [B triệu đồng]
Nhắc nhở đã gửi:             [C triệu đồng] (nếu thu hồi đầy đủ)
                              ──────────────
Số dư dự kiến ngày bảng lương: [D triệu đồng]

Trạng thái: ✅ ĐỦ / ⚠️ CĂNG / ❌ THIẾU HỤT
```

Nếu thiếu hụt: "Có một khoảng trống dự kiến. Bạn có muốn thảo luận về các lựa chọn như tiếp cận LOC, trì hoãn bảng lương một ngày, hoặc ưu tiên các khoản thu hồi không?"

## Cổng phê duyệt

- **Không bao giờ tự động gửi nhắc nhở hóa đơn.** Luôn phê duyệt qua kỹ năng nhac-no-khach-hang.
- **Không bao giờ xử lý bảng lương trực tiếp.** Cung cấp phân tích; chủ doanh nghiệp chạy bảng lương trong phần mềm bảng lương của họ.
- **Không bao giờ cam kết số liệu không chắc chắn là thực tế.** Dự báo là dự báo; luôn sử dụng kịch bản.

## Ví dụ câu kích hoạt

- *"Tôi có đủ tiền trả lương thứ Sáu không?"*
- *"Chuẩn bị bảng lương cho tôi"*
- *"Lo lắng về việc trả lương tuần tới"*
- *"Ai còn nợ tôi tiền? Tôi cần tiền để trả lương"*
