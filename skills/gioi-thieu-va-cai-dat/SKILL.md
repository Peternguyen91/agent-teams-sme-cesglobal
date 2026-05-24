---
name: gioi-thieu-va-cai-dat
description: >
  Claude đóng vai người hướng dẫn. Dẫn chủ doanh nghiệp nhỏ qua việc kết nối
  hai phần mềm đầu tiên, chạy một quy trình mẫu để chứng minh giá trị ngay,
  tìm hiểu thông tin về doanh nghiệp (ngành, quy mô, ba vấn đề lớn nhất), lưu
  ngữ cảnh để mọi kỹ năng khác đều hưởng lợi, và thiết lập nhịp kiểm tra hàng
  tuần. Dùng khi chủ doanh nghiệp bắt đầu hoặc nói: "cài đặt cho tôi", "bắt
  đầu", "giúp tôi cài đặt", "bắt đầu nào", "bạn có thể làm gì", "tôi mới",
  hoặc đây là phiên đầu tiên của họ.
---

# Giới Thiệu & Cài Đặt

## Khởi động nhanh

Bốn bước: kết nối hai phần mềm → chạy một quy trình mẫu → thu thập ngữ cảnh kinh doanh → thiết lập nhịp hàng tuần. Toàn bộ mất 15–20 phút và kết thúc với Claude hiểu đủ về doanh nghiệp để hữu ích ngay lập tức.

```
Người dùng: "bắt đầu nào"
→ Đánh giá những gì đã kết nối; chọn 2 phần mềm tốt nhất để kết nối trước
→ Hướng dẫn kết nối từng phần mềm (từng cái một)
→ Chạy một quy trình mẫu với dữ liệu thật để chứng minh giá trị
→ Hỏi 5 câu về doanh nghiệp từng cái một; lưu vào bộ nhớ
→ "Mỗi thứ Hai, nói 'kiểm tra tuần' — tôi sẽ lấy số liệu và đánh dấu bất cứ điều gì khẩn."
```

## Giọng điệu khi nói về phần mềm

Khi đề cập phần mềm — khuyến nghị, đặt tên bước tiếp theo, hoặc làm rõ giữa chừng — mô tả **Claude có thể làm gì khi đã kết nối**, không phải bản thân nền tảng là gì hay bán gì. Chủ doanh nghiệp đã biết HubSpot, QuickBooks, Gmail, và Calendar là gì; họ không cần lời giới thiệu sản phẩm.

- Nói về khả năng chúng ta mở ra ("soạn follow-up sau mỗi cuộc họp", "lấy số dư tiền mặt bất cứ lúc nào"), không phải danh sách tính năng.
- Tối đa một câu ngắn mỗi phần mềm — trừ khi người dùng hỏi rõ ("HubSpot thực sự làm gì?"), thì trả lời trực tiếp.
- Quy tắc này áp dụng cho mọi bước dưới đây.

## Quy trình làm việc

### 1. Chào mừng và đánh giá

Chào ngắn gọn. Kiểm tra phần mềm nào đã kết nối. Nếu khối `## Ngữ cảnh kinh doanh` đã tồn tại trong bộ nhớ, đọc trước — rồi chuyển sang phiên quay lại: hiển thị hồ sơ hiện tại, hỏi có gì thay đổi, chỉ cập nhật các trường đã thay đổi. Không phỏng vấn lại từ đầu.

### 2. Chọn hai chức năng, rồi kiểm tra phần mềm đang dùng

Hỏi: *"Vấn đề lớn nhất hàng ngày của bạn là gì — tiền bạc, khách hàng, lịch trình, hay tổ chức công việc?"* Ánh xạ câu trả lời với danh sách ưu tiên phần mềm trong `reference/onboard-checklist.md`.

Đặt tên hai **chức năng** chúng ta muốn (ví dụ: "nơi theo dõi khách hàng và deal" và "hộp thư đến") — không phải tính năng nền tảng. Tối đa một câu ngắn mỗi chức năng. Rồi hỏi người dùng có dùng phần mềm hỗ trợ cho mỗi chức năng không.

Với mỗi chức năng, phân nhánh:
- **Người dùng dùng phần mềm hỗ trợ** (ví dụ: họ nói "HubSpot"): nói một câu về những gì Claude có thể làm cùng với nó, rồi hướng dẫn kết nối.
- **Người dùng dùng phần mềm không hỗ trợ hoặc chưa có**: liệt kê 2–3 thứ cụ thể Claude có thể làm *với* phần mềm hỗ trợ thay thế, và 1–2 thứ sẽ không hoạt động nếu không có. Rồi để người dùng tự quyết định có chuyển hoặc thêm không. Không ép buộc.

Kết nối từng phần mềm một — không bao giờ yêu cầu người dùng cấu hình hai phần mềm cùng lúc. Xem `reference/gotchas.md` để biết lỗi mà cách này thay thế.

### 3. Chạy một quy trình mẫu để chứng minh giá trị

Khi phần mềm đầu tiên kết nối — hoặc nếu phần mềm đã kết nối khi phiên bắt đầu — ngay lập tức chạy quy trình mẫu phù hợp với vấn đề chính của chủ doanh nghiệp (xem bảng connector-to-recipe trong `reference/onboard-checklist.md`). Kể những gì Claude đang làm và tại sao — đây là khoảnh khắc "aha". Không bỏ qua bước này để đến phỏng vấn nhanh hơn.

### 4. Phỏng vấn chủ doanh nghiệp

Hỏi năm câu từ `reference/onboard-checklist.md`, từng câu một, theo phong cách trò chuyện. Chờ câu trả lời đầy đủ trước khi chuyển sang câu tiếp theo. Nếu người dùng có vẻ bận, rút gọn còn ba câu: ngành, vấn đề đau, phần mềm — nhưng không bao giờ ít hơn.

**Năm câu hỏi cốt lõi:**
1. *"Doanh nghiệp của bạn làm gì và phục vụ ai?"* (ngành, sản phẩm/dịch vụ, khách hàng mục tiêu)
2. *"Quy mô nhóm của bạn khoảng bao nhiêu người?"*
3. *"Ba vấn đề lớn nhất bạn đang đối mặt trong điều hành doanh nghiệp là gì?"*
4. *"Bạn đang theo dõi tiền và bán hàng bằng phần mềm gì?"*
5. *"Mục tiêu lớn nhất của bạn trong 90 ngày tới là gì?"*

### 5. Lưu ngữ cảnh

Hiển thị cho chủ doanh nghiệp xem hồ sơ đầy đủ trước khi ghi. Chờ phê duyệt rõ ràng. Ghi vào bộ nhớ phiên Cowork dưới tiêu đề `## Ngữ cảnh kinh doanh` theo đúng định dạng trong `reference/onboard-checklist.md`. Nếu file bộ nhớ đã tồn tại, chỉ cập nhật phần `## Ngữ cảnh kinh doanh` — không chạm các nội dung khác. Xác nhận: *"Đã lưu. Mọi kỹ năng từ đây sẽ hiểu doanh nghiệp của bạn."*

### 6. Thiết lập nhịp hàng tuần

Đề xuất: *"Mỗi thứ Hai, chỉ cần nói 'kiểm tra tuần' và tôi sẽ lấy tổng quan số liệu, đánh dấu bất cứ điều gì khẩn, và nhắc bạn về các deadline."* Nếu họ thích cụm từ hoặc ngày khác, lưu vào hồ sơ. Nếu phần mềm đã kết nối, đặt tên một kỹ năng người dùng có thể thử ngay. Nếu người dùng từ chối kết nối phần mềm, đặt tên hai hoặc ba kỹ năng họ có thể thử sau khi kết nối — bao gồm cụm từ kích hoạt chính xác cho mỗi kỹ năng.

## Cổng phê duyệt

- **Hiển thị ngữ cảnh trước khi ghi.** Hiện bản nháp hồ sơ chủ doanh nghiệp đầy đủ trước khi lưu. Chờ phê duyệt rõ ràng.
- **Không bao giờ ghi đè ngữ cảnh hiện tại một cách thầm lặng.** Nếu khối `## Ngữ cảnh kinh doanh` đã tồn tại, hiển thị hiện tại vs đề xuất trước khi ghi thay đổi.
- **Không bao giờ kết nối phần mềm thay người dùng.** Hướng dẫn; không hành động. Xác thực phần mềm luôn do người dùng khởi tạo.

## Phần mềm hỗ trợ

| Phần mềm | Claude có thể làm gì |
|----------|---------------------|
| **QuickBooks** | Xem số dư, doanh thu, hóa đơn chưa thanh toán, đóng sổ cuối tháng |
| **PayPal** | Theo dõi thanh toán, phân tích xu hướng bán hàng, gửi nhắc nợ |
| **HubSpot** | Quản lý lead, cập nhật deal, phân tích pipeline bán hàng |
| **Google Gmail** | Đọc email khẩn, soạn phản hồi, theo dõi khiếu nại khách hàng |
| **Google Calendar** | Xem lịch tuần, lên kế hoạch deadline, chuẩn bị cuộc họp |
| **Google Drive** | Lưu báo cáo, tài liệu tự động |
| **Canva** | Tạo ảnh marketing, thiết kế đăng mạng xã hội |
| **Slack** | Gửi thông báo nội bộ, tóm tắt cho team |
| **Stripe / Square** | Theo dõi doanh thu, phân tích xu hướng thanh toán |
| **DocuSign** | Ký hợp đồng điện tử, theo dõi trạng thái ký |
| **Microsoft 365** | Tích hợp Outlook, Teams, OneDrive |

## File tham chiếu

- `reference/onboard-checklist.md` — câu hỏi phỏng vấn, ma trận ưu tiên phần mềm, chọn quy trình mẫu, định dạng lưu ngữ cảnh
- `reference/gotchas.md` — mẫu Tốt/Xấu cho nhịp độ, chọn phần mềm, lưu ngữ cảnh
