# Những Lỗi Thường Gặp

Các lỗi đã biết của kỹ năng bao-cao-tong-quan. Mỗi lỗi có cặp Sai / Đúng.

---

## Lỗi: QuickBooks trả về trạng thái bất ngờ

**Tại sao quan trọng:** QuickBooks có thể trả về kết quả rỗng, trạng thái đang đồng bộ, hoặc lỗi xác thực mà không ném ra exception cứng. Coi im lặng là "không có dữ liệu" làm báo cáo bỏ qua phần Tiền mặt hoàn toàn mà không báo chủ doanh nghiệp — họ nghĩ doanh nghiệp không có dữ liệu QuickBooks.

### ✗ Sai

```
Claude: [QuickBooks trả về phản hồi rỗng]
        → bỏ qua phần Tiền mặt im lặng
        → báo cáo không có dữ liệu tiền mặt; chủ nghĩ QB không kết nối
```

Chủ doanh nghiệp mất 10 phút reconnect QuickBooks trước khi nhận ra QB luôn kết nối — chỉ đang ở trạng thái tạm thời.

### ✓ Đúng

```
Claude: [QuickBooks trả về phản hồi rỗng hoặc lỗi]
        → Header phần Tiền mặt hiện: "không có — QuickBooks không khả dụng (lỗi đồng bộ hoặc cần xác thực)"
        → "Nguồn không khả dụng: QuickBooks — trả về phản hồi rỗng" ở phụ lục
```

Chủ doanh nghiệp thấy khoảng trống rõ ràng và có thể quyết định có reconnect không hoặc tiếp tục với báo cáo một phần.

---

## Lỗi: Gmail lỗi xác thực giữa chừng

**Tại sao quan trọng:** Xác thực Gmail không ổn định. Hiển thị lỗi xác thực thô giữa báo cáo làm trông như công cụ bị hỏng và phá vỡ niềm tin của chủ vào kỹ năng.

### ✗ Sai

```
Claude: [Lỗi xác thực Gmail giữa chừng khi soạn]
        → "Lỗi: Xác thực Gmail thất bại. Vui lòng xác thực lại."
        → Kết quả báo cáo dừng lại hoặc hiện lỗi thô trong phần Danh sách theo dõi
```

Chủ doanh nghiệp thấy công cụ bị hỏng, không phải bản tóm tắt hữu ích.

### ✓ Đúng

```
Claude: [Lỗi xác thực Gmail]
        → Tiếp tục báo cáo mà không có phần Danh sách theo dõi
        → Phụ lục: "Gmail — lỗi xác thực; Danh sách theo dõi không khả dụng lần này"
        → Tất cả phần khác không bị ảnh hưởng
```

Báo cáo vẫn có giá trị. Chủ doanh nghiệp được thông báo, không bị giật mình.

---

## Lỗi: Hỏi xin phép trước khi lấy dữ liệu

**Tại sao quan trọng:** Giá trị cốt lõi của kỹ năng là tự làm việc mà không cần nhắc. Chủ doanh nghiệp đã kích hoạt báo cáo là đã ngầm chấp thuận việc lấy dữ liệu. Hỏi "có nên kiểm tra QuickBooks không?" làm mất đi mục đích và giảm niềm tin vào kỹ năng như một trợ lý tự chủ.

### ✗ Sai

```
Chủ: "tình hình kinh doanh thế nào?"
Claude: "Tôi có nên kiểm tra QuickBooks để xem số dư tiền mặt không? Và có ổn không nếu tôi xem pipeline HubSpot của bạn?"
```

Ba lượt trao đổi nữa trước khi có gì hữu ích được cung cấp.

### ✓ Đúng

```
Chủ: "tình hình kinh doanh thế nào?"
Claude: [ngay lập tức gọi tất cả công cụ song song]
        → trình bày báo cáo trong một phản hồi
```

---

## Lỗi: Ghi vào Slack mà không có xác nhận rõ ràng

**Tại sao quan trọng:** Ghi vào Slack không được kiểm tra trong luồng xác thực tiêu chuẩn và đăng vào các kênh mà người khác có thể thấy. Tự động đăng mà không có xác nhận có thể làm chủ doanh nghiệp bối rối hoặc spam cho nhóm.

### ✗ Sai

```
Claude: [ở cuối báo cáo]
        "Tôi đã đăng báo cáo này lên kênh #chung."
```

Chủ chưa bao giờ yêu cầu đăng Slack; bây giờ cả nhóm có dữ liệu tài chính.

### ✓ Đúng

```
Claude: [ở cuối báo cáo]
        "Bạn có muốn tôi đăng báo cáo này lên Slack không? Nếu có, kênh nào?"
```

Ghi Slack chỉ xảy ra khi có "có + tên kênh" cụ thể từ chủ. Không bao giờ tự giả định.

---

## Lỗi: Dùng tính từ thay vì số liệu

**Tại sao quan trọng:** "Doanh thu tốt" không giúp chủ doanh nghiệp ra quyết định. Số liệu cụ thể thì có.

### ✗ Sai

```
Claude: "Doanh thu tháng này khá tốt, pipeline trông ổn, và tiền mặt nhìn chung ổn."
```

Không thể hành động được — không có con số để phán đoán.

### ✓ Đúng

```
Claude: "Doanh thu tháng này 43 triệu, ▲ 8% so tháng trước. Pipeline có trọng số 320 triệu — 1,8x mục tiêu tháng (🟡). Số dư tiền mặt 280 triệu, ▼ 15 triệu so tuần trước do hai khoản chi nhà cung cấp."
```
