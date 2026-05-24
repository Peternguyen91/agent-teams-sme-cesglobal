---
name: chien-luoc-noi-dung
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu ít nhất một trong: PayPal, Square, hoặc QuickBooks MCP để phân tích doanh thu."
version: "1.1"
description: >
  Phân tích dữ liệu bán hàng từ PayPal và QuickBooks để tìm sản phẩm bán
  chạy và sản phẩm chậm, kết hợp xu hướng theo mùa, và tạo ra bản kế hoạch
  nội dung 30 ngày ưu tiên: cần đẩy gì, chạy khuyến mãi gì, tạm giữ gì.
  Chỉ là kết quả chiến lược — không tạo lịch hay tài sản sáng tạo. Sử dụng
  khi chủ doanh nghiệp hỏi cần đăng gì, muốn kế hoạch nội dung, hỏi cái
  gì đang bán chạy, hoặc nên quảng bá gì tháng này.
---

# Chiến Lược Nội Dung

Phân tích dữ liệu bán hàng thực tế để tạo kế hoạch nội dung 30 ngày có căn cứ — biết sản phẩm nào đang chạy tốt, cái nào đang chậm, và nên làm gì với từng loại.

> **Đầu ra:** Kế hoạch chiến lược thuần túy — không lên lịch, không tạo ảnh/video.

---

## Bước 1 — Kiểm tra cấu hình ban đầu (chỉ với QuickBooks)

Nếu dùng QuickBooks, kiểm tra thông tin doanh nghiệp:

1. Kiểm tra xem `Ngành nghề` đã được điền trong hồ sơ QuickBooks chưa.
2. Nếu chưa có hoặc để trống:
   - Hỏi: *"Tôi cần biết ngành nghề của bạn để so sánh xu hướng theo mùa chính xác hơn. Bạn đang kinh doanh trong lĩnh vực gì? (ví dụ: bán lẻ, dịch vụ, thực phẩm, ...)"*
   - Cập nhật thông tin và xác nhận: *"Đã cập nhật. Đang tiến hành phân tích dữ liệu bán hàng."*
3. Nếu đã có thông tin, chuyển sang Bước 2.

**Lưu ý:** PayPal và Square không yêu cầu bước này.

---

## Bước 2 — Xác định tiêu chí đánh giá

Trước khi phân tích, hỏi chủ doanh nghiệp:

- **"Bạn muốn tôi đánh giá 'sản phẩm bán chạy' theo tiêu chí nào?"**
  - Tổng doanh thu?
  - Lợi nhuận biên?
  - Tốc độ bán (bán nhanh đến mức nào)?
  - Kết hợp các yếu tố trên?

- **"Bạn có biết xu hướng theo mùa trong ngành mình không?"**
  - Nếu có: *"Hãy chia sẻ để tôi tính vào phân tích"*
  - Nếu không: *"Tôi sẽ dùng benchmark ngành để ước tính"*

---

## Bước 3 — Lấy và phân tích dữ liệu bán hàng

Lấy dữ liệu từ nguồn được kết nối (QuickBooks, PayPal, hoặc Square):

- **Khoảng thời gian:** 90 ngày gần nhất (hoặc toàn bộ lịch sử nếu dưới 90 ngày)
- **Dữ liệu cần:** Tên sản phẩm/dịch vụ, ngày bán, doanh thu, số lượng

**Lưu ý theo nguồn:**
- **QuickBooks:** Lấy chi tiết hóa đơn theo dòng sản phẩm/dịch vụ
- **PayPal:** Lấy lịch sử giao dịch. *Nếu bị giới hạn tốc độ: chờ 30 giây và thử lại. Nếu vẫn thất bại, hỏi có muốn chuyển sang QuickBooks không.*
- **Square:** Cần location ID trước. Lấy danh sách địa điểm rồi tổng hợp đơn hàng.

**Dự phòng:** Nếu dữ liệu dưới 3 tháng, dùng benchmark theo mùa của ngành.

Xác định:
- **Top 3–5 bán chạy** (theo tiêu chí chủ doanh nghiệp chọn)
- **Bottom 3–5 bán chậm** (cân nhắc giữ hay định vị lại)
- **Đang tăng** (tạo đà trong 30 ngày qua)
- **Đang giảm** (mất đà)

---

## Bước 4 — Phân tích xu hướng theo mùa

- **Do chủ doanh nghiệp cung cấp:** Nếu họ chia sẻ xu hướng, tính vào khuyến nghị.
- **Benchmark ngành:** Với những ngành không có dữ liệu rõ ràng (ví dụ: *"Q1 thường mạnh cho dịch vụ kế toán"*).
- **Thời điểm:** Đánh dấu sản phẩm nào cần đẩy/giảm trong 30 ngày tới theo mùa.

---

## Bước 5 — Xây dựng kế hoạch nội dung 30 ngày

Cấu trúc bản kế hoạch:

- **Tóm tắt ngắn gọn** (1–2 câu: *"Sản phẩm bán chạy nhất là X và Y. Đang bắt đầu vào mùa của Z."*)
- **Đẩy mạnh** — Top 2–3 sản phẩm + góc độ nội dung gợi ý (ví dụ: *"Case study về kết quả thực tế"*, *"Video hướng dẫn sử dụng"*)
- **Duy trì** — Sản phẩm trung bình; giữ độ hiện diện nhưng không cần đầu tư nặng
- **Định vị lại hoặc tạm dừng** — Sản phẩm chậm; cân nhắc giảm giá, đóng gói combo, hoặc tạm ngừng
- **Cơ hội theo mùa** — Cái gì sắp vào mùa, cần chuẩn bị content từ bây giờ
- **Khuyến nghị ưu đãi** — Chiến lược combo, giảm giá, hoặc dùng thử dựa trên dữ liệu

Độ dài kế hoạch: **200–400 từ** — ngắn gọn, có thể hành động ngay, không dài dòng.

---

## Bước 6 — Xin phê duyệt và điều chỉnh

Trình bày kế hoạch cho chủ doanh nghiệp. Hỏi:
- *"Có khớp với cảm nhận thực tế của bạn không?"*
- *"Có điểm nào cần điều chỉnh?"*
- *"Bạn có muốn tôi tạo ảnh/bài đăng từ kế hoạch này không?"*

Điều chỉnh nếu cần; khi đã được duyệt, kế hoạch sẵn sàng để đưa vào `tao-anh-canva` hoặc `chay-campaign`.

---

## Cổng phê duyệt

- **Không tự lên lịch hay đăng nội dung.** Kế hoạch chỉ để chủ doanh nghiệp xem xét.
- **Không tự tạo ảnh/video.** Chờ chủ doanh nghiệp phê duyệt kế hoạch trước.
- **Đánh dấu rõ khi dữ liệu ít hơn 90 ngày** và đang dùng benchmark ngành.

## Ví dụ câu kích hoạt

- *"Tháng này tôi nên đăng gì?"*
- *"Kế hoạch nội dung tháng tới"*
- *"Cái gì đang bán chạy nhất?"*
- *"Nên quảng bá sản phẩm nào?"*
