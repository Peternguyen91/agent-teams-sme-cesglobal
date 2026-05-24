---
name: bao-cao-tong-quan
description: >
  Tạo bản tóm tắt tình hình kinh doanh một trang cho chủ doanh nghiệp nhỏ —
  tiền mặt (QuickBooks), xu hướng doanh thu (PayPal/Square), pipeline
  (HubSpot), lịch tuần (Google Calendar), mục cần theo dõi khẩn (Gmail/Slack),
  và việc quan trọng nhất cần làm hôm nay. Tự động thử kết nối mọi phần mềm
  khả dụng và xuất kết quả theo phạm vi thực tế — 1 phần mềm cho bức tranh
  một phần; đầy đủ phần mềm cho bức tranh toàn diện. Kích hoạt khi chủ doanh
  nghiệp hỏi tình hình kinh doanh, muốn xem tổng quan, tóm tắt tuần, hoặc nói
  bất cứ điều gì như "tôi đang bỏ lỡ điều gì" hay "cập nhật tình hình doanh nghiệp".
---

# Báo Cáo Tổng Quan Doanh Nghiệp

Một câu hỏi, một trang kết quả. Lấy dữ liệu trực tiếp từ mọi phần mềm đã kết nối, tổng hợp thành bản báo cáo súc tích, và nêu bật MỘT việc quan trọng nhất cần xử lý hôm nay. Tự làm việc — không hỏi người dùng giúp tìm dữ liệu.

## Bước 1 — Lấy dữ liệu song song

**Gọi tất cả phần mềm cùng lúc trong một batch** — xem `reference/data_sources.md` để biết tool nào lấy metric nào. Không gọi tuần tự; chờ từng cái làm chậm hơn 30 giây.

Các phần mềm cần gọi đồng thời:

- **QuickBooks** — số dư tiền mặt, doanh thu tháng hiện tại, công nợ phải thu, hóa đơn quá hạn
- **PayPal / Square** — thanh toán 7 ngày qua, xu hướng bán hàng, giao dịch thất bại/đang chờ
- **HubSpot** — pipeline theo giai đoạn, deal mới/đóng/nguội, lead mới
- **Google Calendar** — cuộc họp quan trọng, deadline, sự kiện tuần này và 7 ngày tới
- **Gmail** — email đánh dấu khẩn, khiếu nại khách hàng, yêu cầu thời hạn
- **Slack / Teams** — tín hiệu nội bộ khẩn, thread cần chủ doanh nghiệp trả lời
- **Intercom / Zendesk** — ticket đang mở, leo thang (nếu kết nối)
- **Shopify / Square** — vấn đề giao hàng (nếu kết nối)

Nếu một phần mềm lỗi hoặc không có dữ liệu, ghi nhận nội bộ và tiếp tục. Không chặn báo cáo vì một phần mềm kém.

**Phương án dự phòng QuickBooks**: Nếu QuickBooks trả về trạng thái bất ngờ, đánh dấu phần Tiền mặt "không có — QuickBooks không khả dụng" và tiếp tục. Không thử lại hay hỏi người dùng kết nối lại.

**Phương án dự phòng Gmail**: Gmail xác thực không ổn định. Nếu lỗi, bỏ qua phần Theo dõi và ghi chú "Gmail không khả dụng" ở phụ lục — không hiện lỗi giữa chừng.

## Bước 2 — Tính các chỉ số

Đọc `reference/thresholds.md` để biết ngưỡng đỏ/vàng/xanh. Tính:

- **Tuổi công nợ phải thu** — hóa đơn chưa thanh toán QuickBooks theo số ngày quá hạn (0–30, 31–60, 61+)
- **Độ phủ pipeline** — pipeline có trọng số HubSpot ÷ mục tiêu doanh thu tháng
- **Xu hướng doanh thu** — doanh thu QBO tháng này vs tháng trước (hoặc 7 ngày PayPal/Square vs 7 ngày trước)

Gán trạng thái 🟢/🟡/🔴 cho từng phần. Nếu nguồn không có dữ liệu, đánh dấu "không có" và ghi chú ở phụ lục.

## Bước 3 — Cảnh báo rủi ro chủ động

Quét các mục cần hành động. Mỗi cảnh báo phải nêu tên cụ thể và bước tiếp theo — "một số hóa đơn quá hạn" là vô dụng; "3.400$ từ Công ty A, 47 ngày quá hạn, không phản hồi từ ngày 12/3" mới có giá trị.

- Hóa đơn QuickBooks quá hạn > 30 ngày — tên khách, số tiền, số ngày quá hạn
- Deal HubSpot không có hoạt động > 7 ngày, hoặc ngày đóng đã qua mà vẫn mở
- Gmail có chủ đề "khẩn cấp", "leo thang", "khiếu nại", "hủy", "hoàn tiền"
- Giao dịch PayPal/Square thất bại hoặc đang chờ > 500$

## Bước 4 — Soạn kết quả đầu ra

Dùng đúng template trong `reference/output_template.md`. Chỉ hiển thị phần nào có dữ liệu thực — bỏ header của phần mềm không khả dụng. Điều chỉnh độ sâu theo ngữ cảnh: "tình hình thế nào" nhận báo cáo đầy đủ hơn; "tóm tắt nhanh trước cuộc họp" nhận báo cáo ngắn hơn.

Tổng hợp liên phần mềm là giá trị cốt lõi. Nếu tin nhắn Slack liên quan đến deal HubSpot đang đình trệ, nêu mối liên hệ đó ở phần Ưu tiên #1. Tổng hợp giúp báo cáo hữu ích hơn là kiểm tra từng phần mềm riêng lẻ.

Quy tắc viết:
- Con số đi trước, lời giải thích đi sau. Không viết "doanh thu tốt" — viết "43 triệu tháng này, ▲ 8% so tháng trước" và để chủ doanh nghiệp tự đánh giá.
- Mỗi con số đều có delta so kỳ trước khi có thể. Ảnh chụp tuyệt đối (số dư tiền) vẫn hiện delta so tuần trước.
- Tên và tiền, không phải tính từ. "4.200$ từ Công ty X, 23 ngày quá hạn" tốt hơn "một số công nợ đáng lo".
- Không lấp đầy bằng nội dung vô nghĩa. Nếu phần nào không có gì đáng báo cáo, viết "Không có thay đổi đáng kể" và tiếp tục.

## Bước 5 — Xuất và chia sẻ (một lần)

Sau khi trình bày báo cáo, hỏi một lần:
- "Bạn có muốn lưu thành file không?" (dùng connector Files nếu có)
- "Có nên đăng lên Slack của bạn không?" (chỉ nếu Slack đã kết nối và người dùng xác nhận — ghi Slack cần phê duyệt rõ ràng)

Nếu đồng ý, thực hiện. Nếu không, tiếp tục — không hỏi lại.

## Các biến thể phạm vi

Chủ doanh nghiệp có thể yêu cầu xem hẹp hơn:

- **"Chỉ tiền mặt" / "kiểm tra tài chính"** → chỉ phần Tiền mặt & Tài chính + rủi ro công nợ
- **"Chỉ pipeline" / "kiểm tra deal"** → chỉ phần Pipeline + rủi ro deal đình trệ
- **"Danh sách theo dõi" / "có gì khẩn không"** → chỉ Danh sách theo dõi + tất cả rủi ro, không có phần chỉ số
- **"Tóm tắt nhanh trước cuộc họp"** → chỉ TL;DR + Ưu tiên #1, không có phần đầy đủ

## Những điều KHÔNG làm

- **Không hỏi xin phép trước khi lấy dữ liệu.** Kỹ năng đã được kích hoạt thì chạy luôn. Hỏi "có nên kiểm tra QuickBooks không?" vô nghĩa.
- **Không bịa hay ước lượng số liệu.** Nếu nguồn không có gì, nói "không có" rõ ràng. Không bịa để lấp chỗ trống.
- **Không bỏ qua delta.** Một con số không có so sánh là cơ hội bị bỏ lỡ. Nếu không có kỳ trước để so sánh, ghi "(không có dữ liệu kỳ trước)" thay vì bỏ trường đó.
- **Không hiện lỗi phần mềm giữa báo cáo.** Ghi vào phụ lục. Báo cáo dẫn đầu bằng những gì đã lấy được.

## File tham chiếu

- `reference/data_sources.md` — mapping tool → metric với phương án dự phòng
- `reference/thresholds.md` — ngưỡng 🟢/🟡/🔴, có thể điều chỉnh theo chủ doanh nghiệp
- `reference/output_template.md` — cấu trúc markdown chính xác; không thay đổi
- `reference/gotchas.md` — các lỗi đã biết (trạng thái QB, xác thực Gmail, ghi Slack)
