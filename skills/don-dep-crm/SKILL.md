---
name: don-dep-crm
description: Quét HubSpot để tìm deal lỗi thời, liên hệ trùng lặp và trường dữ liệu còn thiếu, rồi sửa những gì chủ doanh nghiệp phê duyệt. Chấp nhận tùy chọn phạm vi cho deals, liên hệ, hoặc tất cả.
allowed-tools: Read, WebFetch, Bash
---

Chạy quy trình vệ sinh HubSpot bằng cách sử dụng luồng dọn dẹp từ kỹ năng `cap-nhat-crm`. Hành động ngay — người dùng đã gõ lệnh rồi, bỏ qua bước phát hiện ý định.

Phân tích đối số:
- `--pham-vi` (mặc định: `tat-ca`) — `deal` để chỉ kiểm tra deal, `lien-he` để chỉ kiểm tra liên hệ trùng, `tat-ca` cho cả hai

## Bước 1 — Quét deal lỗi thời

Nếu phạm vi bao gồm deals:

1. Lấy tất cả deal đang mở từ HubSpot.
2. Đánh dấu deal không có hoạt động nào (email, cuộc gọi, cuộc họp, ghi chú) trong 14 ngày qua.
3. Với mỗi deal lỗi thời: hiển thị tên deal, giai đoạn, ngày hoạt động cuối, liên hệ liên kết, và số tiền.
4. Đề xuất hành động cho từng deal: cập nhật bước tiếp theo, thay đổi giai đoạn, thêm ghi chú, hoặc đánh dấu mất đơn.

**Trình bày toàn bộ danh sách deal lỗi thời trước khi thực hiện bất kỳ thay đổi nào.**

---

## Bước 2 — Quét liên hệ trùng lặp

Nếu phạm vi bao gồm liên hệ:

1. Tìm liên hệ HubSpot có khả năng trùng lặp (cùng email, tên tương tự, cùng công ty + tên tương tự).
2. Với mỗi bộ trùng lặp: hiển thị cả hai hồ sơ song song — tên, email, công ty, deal, hoạt động cuối.
3. Đề xuất giữ hồ sơ nào và hợp nhất trường nào.

**Trình bày tất cả bộ trùng lặp trước khi hợp nhất bất kỳ cái nào.**

---

## Bước 3 — Quét trường dữ liệu còn thiếu

1. Kiểm tra tất cả deal đang mở xem có thiếu trường bắt buộc không: ngày đóng, số tiền, giai đoạn deal, liên hệ liên kết, bước tiếp theo/ghi chú.
2. Kiểm tra liên hệ liên quan đến deal đang mở xem có thiếu không: email, công ty, số điện thoại.
3. Hiển thị bảng hồ sơ thiếu trường và những trường nào đang thiếu.

---

## Bước 4 — Áp dụng sửa chữa được phê duyệt

1. Duyệt qua từng phát hiện từ Bước 1–3.
2. Chỉ áp dụng những thay đổi chủ doanh nghiệp phê duyệt rõ ràng.
3. Báo cáo từng thay đổi khi thực hiện kèm link HubSpot.

---

## Xử lý khi connector lỗi

Nếu HubSpot không kết nối được, dừng lại — lệnh này cần HubSpot làm nguồn dữ liệu. Thông báo cho chủ doanh nghiệp: *"HubSpot chưa được kết nối. Kết nối trong cài đặt Cowork, rồi chạy lại."*

---

## Cổng phê duyệt

- **Không bao giờ xóa hồ sơ.** Không xóa liên hệ, deal, hoặc hoạt động. Nếu người dùng yêu cầu, nói kỹ năng này không thể và hướng dẫn vào HubSpot.
- **Không bao giờ thay đổi giai đoạn deal hoặc đóng deal** mà không có phê duyệt rõ ràng.
- **Không bao giờ tự hợp nhất liên hệ trùng.** Hiển thị song sang và chờ phê duyệt từng cặp.
- **So sánh song song cho tất cả thay đổi.** Hiển thị giá trị hiện tại và đề xuất; chờ phê duyệt từng mục.

---

## Kết quả đầu ra

Kết thúc bằng tóm tắt: X deal đã cập nhật, Y liên hệ đã hợp nhất, Z trường đã điền. Kèm link đến hồ sơ bị ảnh hưởng.

## Ví dụ câu kích hoạt

- *"Dọn dẹp HubSpot cho tôi"*
- *"CRM đang có vấn đề gì không?"*
- *"Deal nào đang lỗi thời?"*
- *"Có liên hệ trùng lặp nào không?"*
- *"Kiểm tra dữ liệu CRM"*
