---
name: chay-campaign
description: Chạy toàn bộ quy trình marketing campaign — phân tích bán hàng, kế hoạch nội dung, tạo ảnh Canva, lên lịch HubSpot. Chấp nhận tùy chọn khoảng thời gian nhìn lại và kênh đăng.
allowed-tools: Read, WebFetch, Bash
---

Chạy toàn bộ pipeline campaign bằng cách kết hợp ba kỹ năng theo thứ tự. Chủ doanh nghiệp phê duyệt tại mỗi điểm chuyển giao — không bao giờ tự động tiến sang bước tiếp theo.

Phân tích đối số:
- `--nhin-lai` (mặc định `90d`) — khoảng thời gian nhìn lại dữ liệu doanh thu
- `--kenh` (mặc định `ca-hai`) — `email`, `mang-xa-hoi`, hoặc `ca-hai`

## Bước 1 — Phân tích bán hàng + kế hoạch nội dung (chien-luoc-noi-dung)

Kích hoạt quy trình kỹ năng `chien-luoc-noi-dung`:

1. Lấy dữ liệu bán hàng từ QuickBooks và PayPal cho khoảng thời gian đã chọn.
2. Xác định sản phẩm/dịch vụ nào đang tụt doanh thu — loại nào, giai đoạn nào, mức độ bao nhiêu.
3. Tạo kế hoạch nội dung 30 ngày ưu tiên: cần đẩy gì, chạy ưu đãi gì, tạm giữ gì.
4. Trình bày kế hoạch cho chủ doanh nghiệp. **Chờ xác nhận "đã duyệt, tạo ảnh đi" trước khi tiếp tục.**

Nếu chủ doanh nghiệp chỉnh sửa kế hoạch, cập nhật và trình bày lại.

---

## Bước 2 — Tạo ảnh + lên lịch đăng (tao-anh-canva)

Sau khi Bước 1 được duyệt, kích hoạt quy trình kỹ năng `tao-anh-canva`:

1. Dùng kế hoạch nội dung đã duyệt từ Bước 1 làm đầu vào.
2. Xây dựng lịch đăng bài khớp với các ưu tiên trong kế hoạch.
3. Tạo ảnh Canva theo thương hiệu cho từng bài đăng (hiển thị từng ảnh để chủ doanh nghiệp duyệt trước khi tiếp tục).
4. Soạn caption/nội dung cho từng bài.
5. Lên lịch trong HubSpot (KHÔNG đăng — chỉ lên lịch).
6. Trình bày campaign đã lên lịch cho chủ doanh nghiệp. **Chờ xác nhận "đã duyệt, gửi cho phân khúc X" trước khi sang Bước 3.**

---

## Bước 3 — Phân loại khách hàng mục tiêu (phan-loai-lead)

Sau khi Bước 2 được duyệt, kích hoạt quy trình kỹ năng `phan-loai-lead`:

1. Lấy danh sách liên hệ HubSpot khớp với phân khúc mục tiêu của campaign (từ kế hoạch đã duyệt).
2. Chấm điểm theo mức độ tương tác, mức độ phù hợp, mức độ khẩn cấp.
3. Tạo hai danh sách:
   - **Danh sách gửi hàng loạt** — phân khúc nhận campaign từ Bước 2
   - **Danh sách gọi điện ưu tiên** — top 5 lead nên gọi trực tiếp với tài liệu trao đổi
4. Chặn thời gian trên lịch cho các cuộc gọi.
5. Trình bày cả hai danh sách. **Chờ lệnh "gửi đi" rõ ràng trước khi đẩy campaign HubSpot live.**

---

## Cổng phê duyệt (bắt buộc giữ)

- **Không bao giờ tự động chuyển giữa các bước.** Mỗi điểm chuyển giao cần phê duyệt rõ ràng.
- **Không bao giờ gửi campaign HubSpot** nếu chưa có lệnh "gửi đi" từ chủ doanh nghiệp ở Bước 3.
- **Nếu có connector không kết nối được** (QuickBooks, PayPal, Canva, HubSpot), dừng lại, báo connector nào lỗi, và hỏi có muốn thử lại hay hủy không.

---

## Kết quả đầu ra

Kết thúc bằng một đoạn tóm tắt: sản phẩm cần đẩy đã xác định, số bài đăng đã tạo, quy mô phân khúc, số cuộc gọi đã lên lịch. Kèm link đến campaign trong HubSpot sau khi đã gửi.

## Ví dụ câu kích hoạt

- *"Chạy campaign tháng này"*
- *"Lên campaign marketing cho tôi"*
- *"Tạo campaign đầy đủ từ phân tích đến đăng bài"*
- *"Chạy hết pipeline marketing"*
