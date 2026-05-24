---
name: canh-bao-cuoi-thang
description: Chạy vào ngày 25 hàng tháng — hiển thị triển vọng dòng tiền 30 ngày tới và đánh dấu bất cứ điều gì cần chú ý trước cuối tháng. Chấp nhận cửa sổ dự báo 30 hoặc 60 ngày.
allowed-tools: Read, WebFetch, Bash
---

Chạy cảnh báo cuối tháng. Lấy dữ liệu tiền mặt hướng về phía trước và cho chủ doanh nghiệp bức tranh rõ ràng "30 ngày tới như thế nào" với những điều cụ thể cần theo dõi.

Phân tích đối số:
- `--ky-han` (mặc định: `30`) — cửa sổ dự báo tính bằng ngày (`30` hoặc `60`)

## Bước 1 — Vị trí tiền mặt hiện tại

Dùng quy trình kỹ năng `du-bao-dong-tien`:

1. Lấy số dư tiền mặt và khoản phải thu hiện tại từ QuickBooks.
2. Lấy số dư đã thanh toán PayPal và các khoản thanh toán chờ.
3. Kết hợp để có tổng tiền mặt và khoản sắp đến.

## Bước 2 — Nghĩa vụ sắp đến

Lấy và lên lịch cho kỳ dự báo:

- **Hóa đơn nhà cung cấp sắp đến** (A/P aging, ngày đáo hạn trong 30–60 ngày)
- **Bảng lương sắp đến** (ngày, số tiền)
- **Tiền thuê / thế chấp** (ngày đến hạn, số tiền)
- **Đăng ký và phí định kỳ** (bất kỳ điều nào định kỳ)
- **Hóa đơn thuế đến hạn** (nếu trong kỳ)
- **Khoản vay hoặc thanh toán LOC** (ngày đến hạn tiếp theo)

Tính tổng nghĩa vụ đã biết: **X triệu đồng** phải ra trong 30 ngày.

## Bước 3 — Dự báo doanh thu

Ước tính doanh thu dự kiến cho 30 ngày tới:

- **A/R aging**: khoản phải thu nào dự kiến vào trong 30 ngày?
- **Doanh thu định kỳ**: khách hàng thuê bao, hợp đồng định kỳ
- **Xu hướng lịch sử**: so sánh tháng này với cùng tháng năm trước (nếu có)

Tạo ba trường hợp:
- **Lạc quan**: 90% A/R thu đúng hạn, doanh thu bằng tháng tốt nhất gần đây
- **Cơ sở**: 70% A/R, doanh thu trung bình 3 tháng
- **Thận trọng**: 50% A/R, doanh thu -15% trung bình

## Bước 4 — Đánh dấu điểm cần theo dõi

So sánh dự báo doanh thu với nghĩa vụ đã biết. Đánh dấu cụ thể:

```
⚠️ KỊCH BẢN THẬN TRỌNG: Khoảng trống dự kiến của -X triệu vào ngày [ngày]
   Lý do: Bảng lương (Y triệu) + Tiền thuê (Z triệu) đến trước hóa đơn lớn của khách A (W triệu) được thanh toán

⚠️ TẬP TRUNG RỦI RO: Khách hàng B chiếm 35% A/R dự kiến — nếu trễ, ảnh hưởng tất cả kịch bản
```

## Bước 5 — Hành động khuyến nghị

Với mỗi rủi ro được đánh dấu, đề xuất hành động cụ thể (nhưng không tự thực hiện):

- "Cân nhắc gửi nhắc nhở hóa đơn sớm cho [Khách hàng B] — chạy `/nhac-no-khach-hang` để soạn"
- "Theo dõi ngày thanh toán A/R từ [Khách hàng C] — khoản của họ sắp đến hạn"
- "Có thể cần xem lại timeline bảng lương nếu kịch bản thận trọng trở thành sự thật"

## Bước 6 — Xuất tóm tắt

```
Cảnh Báo Cuối Tháng — {ngày}
(Dự báo cho {N} ngày tới)

💰 TIỀN MẶT HIỆN TẠI: {X triệu đồng}
📥 DỰ KIẾN VÀO:      {Y triệu đồng} (kịch bản cơ sở)
📤 ĐÃ LÊN LỊCH RA:   {Z triệu đồng}
                      ──────────────
📊 SỐ DƯ DỰ KIẾN:    {W triệu đồng}

Trạng thái: ✅ TỐT / ⚠️ THEO DÕI / ❌ CẦN HÀNH ĐỘNG

ĐIỂM CẦN CHÚ Ý:
[Danh sách đánh dấu cụ thể với hành động khuyến nghị]
```

## Cổng phê duyệt

- **Không gửi email, thanh toán, hay thay đổi bất cứ điều gì** dựa trên phân tích này.
- **Trình bày dưới dạng thông tin**, không phải hành động. Chủ doanh nghiệp quyết định phải làm gì tiếp theo.

## Ví dụ câu kích hoạt

- *"Tháng tới tiền mặt thế nào?"*
- *"Có gì cần lo trước cuối tháng không?"*
- *"Cảnh báo tháng tới"*
- *"Xem trước dòng tiền 30 ngày"*
