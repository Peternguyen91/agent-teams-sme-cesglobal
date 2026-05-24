# Những Lỗi Thường Gặp — Giới Thiệu & Cài Đặt

Mẫu Sai / Đúng cho các lỗi đã biết trong quy trình giới thiệu.

---

## Lỗi: Bỏ qua bước chứng minh giá trị sau khi kết nối

**Tại sao quan trọng:** Nếu chủ doanh nghiệp kết nối phần mềm nhưng Claude chuyển thẳng sang phỏng vấn, khoảnh khắc "aha" không bao giờ đến. Bước chứng minh giá trị là điều khiến chủ tin rằng việc cài đặt đáng giá — và phân biệt kỹ năng này với một bài điền form nhàm chán.

### ✗ Sai

> "Tuyệt, QuickBooks đã kết nối! Bây giờ hãy để tôi hỏi bạn vài câu về doanh nghiệp."

Bỏ qua quy trình mẫu hoàn toàn. Chủ rời đi mà không biết họ vừa mở khóa điều gì.

### ✓ Đúng

> "QuickBooks đã kết nối. Để tôi lấy dòng tiền 30 ngày gần nhất — khoảng 10 giây."
> *[chạy ke-hoach-tra-luong, hiển thị kết quả]*
> "Đây là những gì chúng ta có thể làm bất cứ lúc nào bạn muốn kiểm tra số. Bây giờ, vài câu về doanh nghiệp của bạn…"

Bản demo chạy trước phỏng vấn, mọi lần, không ngoại lệ.

---

## Lỗi: Đổ tất cả năm câu hỏi phỏng vấn cùng một lúc

**Tại sao quan trọng:** Năm câu hỏi trình bày cùng nhau trông như một biểu mẫu, không phải cuộc trò chuyện. Chủ doanh nghiệp sẽ trả lời qua loa hoặc bỏ ngang. Nhịp độ trò chuyện tạo ra câu trả lời sâu sắc hơn và tỷ lệ hoàn thành cao hơn.

### ✗ Sai

> "Để thiết lập cho bạn, tôi cần: (1) Doanh nghiệp của bạn làm gì? (2) Có bao nhiêu nhân viên? (3) Ba vấn đề lớn nhất là gì? (4) Bạn dùng phần mềm gì? (5) Muốn check-in mỗi bao lâu?"

### ✓ Đúng

Hỏi từng câu, nhận câu trả lời đầy đủ, rồi hỏi câu tiếp. Rút gọn còn ba câu (ngành, vấn đề đau, phần mềm) nếu chủ ra hiệu bận — không bao giờ hỏi ít hơn ba câu đó.

---

## Lỗi: Lưu ngữ cảnh mà không hiển thị hồ sơ trước

**Tại sao quan trọng:** Ghi âm thầm có vẻ xâm phạm và tước đi cơ hội sửa câu trả lời bị hiểu sai. Hiển thị hồ sơ nháp cũng là xác nhận tự nhiên Claude đã hiểu đúng — thường bộc lộ sửa chữa mà chủ không chủ động chia sẻ.

### ✗ Sai

> "Được rồi, tôi đã lưu hồ sơ doanh nghiệp của bạn!"

Không xem trước, không phê duyệt — chủ không biết gì được ghi.

### ✓ Đúng

> "Đây là những gì tôi sắp lưu làm hồ sơ doanh nghiệp của bạn — cho tôi biết nếu có gì cần sửa:"
>
> ```
> Doanh nghiệp: Cửa hàng phần cứng ABC — bán lẻ vật liệu xây dựng
> Quy mô: 4 người (bao gồm chủ)
> Vấn đề đau: thiếu hụt dòng tiền · khách trả chậm · sắp xếp ca làm việc
> Phần mềm đã kết nối: QuickBooks, Gmail
> Nhịp hàng tuần: kiểm tra mỗi thứ Hai
> Ngày bắt đầu: 2026-05-24
> ```
>
> "Đúng chưa? Tôi sẽ lưu sau khi bạn xác nhận."

Hiển thị khối, chờ phê duyệt, rồi mới ghi.

---

## Lỗi: Quảng cáo nền tảng thay vì nói về khả năng

**Tại sao quan trọng:** Chủ doanh nghiệp đã biết HubSpot, QuickBooks, Gmail, và Calendar là gì. Khi khuyến nghị nghe như trang sản phẩm, nó đến như quảng cáo, không phải lời khuyên. Chủ mất tập trung đúng lúc cần sự chú ý nhất.

### ✗ Sai

> "1. HubSpot (CRM) — Một nơi cho mọi lead, khách hàng, deal và hội thoại. Khi đã kết nối, tôi có thể ưu tiên ai cần gọi hôm nay, soạn follow-up, ghi chú từ hộp thư..."

Nghe như marketing cho HubSpot. Chủ đang bị bán hàng.

### ✓ Đúng

> "Để theo dõi khách hàng, tôi cần hai thứ: nơi quản lý deal và hộp thư đến của bạn.
>
> Bạn đang dùng phần mềm CRM gì — HubSpot, hay cái khác?"
>
> *(Chủ: "Tôi không dùng gì cả.")*
>
> "Nếu kết nối HubSpot, tôi có thể: lập danh sách 5 lead cần gọi mỗi sáng, soạn follow-up sau mỗi cuộc họp, cảnh báo deal đang nguội. Tất cả đều miễn phí. Muốn thử không?"

Nêu chức năng, kiểm tra chủ đang dùng gì, đưa ra lợi/hại rõ ràng bằng ngôn ngữ đơn giản, để quyết định cho chủ.

---

## Lỗi: Yêu cầu kết nối hai phần mềm cùng một lúc

**Tại sao quan trọng:** Xác thực OAuth đòi hỏi sự chú ý và chuyển tab. Yêu cầu hai lần cùng lúc gây nhầm lẫn — chủ không biết cái nào đang xử lý, dễ nhấp sai bước.

### ✗ Sai

> "Hãy kết nối cả QuickBooks và HubSpot ngay bây giờ. Đây là link cả hai."

### ✓ Đúng

> "Hãy bắt đầu với QuickBooks — tôi sẽ hướng dẫn từng bước."
> *[Đợi xác nhận kết nối QB]*
> "QuickBooks hoàn tất. Để xem số thật, tôi sẽ lấy dòng tiền của bạn ngay..."
> *[Chạy bản demo]*
> "Giờ, nếu muốn, chúng ta có thể kết nối HubSpot — cần thêm 2 phút."

Từng bước một, với bản demo ở giữa để giữ động lực.
