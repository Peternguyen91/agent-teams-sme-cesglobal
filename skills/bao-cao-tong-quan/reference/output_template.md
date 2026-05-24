# Template Kết Quả Đầu Ra

Đây là cấu trúc chính xác mà mỗi báo cáo tổng quan phải tuân theo. Không đảo thứ tự phần. Bỏ phần chỉ khi connector không trả về dữ liệu — không bao giờ để header rỗng.

Các biến trong `{{dấu ngoặc kép}}` là placeholder — thay bằng giá trị đã tính. Quy ước mũi tên: ▲ tăng, ▼ giảm, ▬ bằng (<1% thay đổi). Luôn hiện giá trị delta sau mũi tên.

---

```markdown
# Báo Cáo Tổng Quan — {{Thứ, Ngày Tháng Năm}}

**Tổng thể: {{🟢|🟡|🔴}} {{một dòng trạng thái, vd: "Tiền mặt ổn định, một hóa đơn quá hạn cần xử lý."}}}**

## TÓM TẮT NHANH

- {{Thực tế quan trọng nhất có số liệu, vd: "Số dư tiền mặt 420 triệu, giảm 30 triệu so tuần trước — hai khoản chi lớn cho nhà cung cấp đã qua."}}
- {{Thứ hai quan trọng, vd: "17 triệu từ Công ty ABC đã quá hạn 47 ngày — không có phản hồi từ ngày 12/3."}}
- {{Thứ ba, vd: "Pipeline 640 triệu có trọng số; hai deal đã nguội tuần này."}}

---

## 💰 Tiền Mặt & Tài Chính — {{🟢|🟡|🔴}}

- **Số dư tiền mặt**: {{SỐ DƯ}} triệu ({{▲|▼|▬}} {{DELTA}} triệu so tuần trước)
- **Doanh thu tháng này**: {{DTH}} triệu so {{DTH_TRUOC}} triệu tháng trước ({{▲|▼|▬}} {{%}}%)
- **Công nợ phải thu**: {{TONG_AR}} triệu trên {{N}} hóa đơn mở

**Tuổi công nợ phải thu**
- 0–30 ngày: {{AR_0_30}} triệu
- 31–60 ngày: {{AR_31_60}} triệu {{🟡 nếu khác 0}}
- 61+ ngày: {{AR_61}} triệu {{🔴 nếu khác 0}}

**Quá hạn > 30 ngày**
- {{tên khách hàng}} — {{số tiền}} triệu ({{số ngày}} ngày quá hạn)
- {{tên khách hàng}} — {{số tiền}} triệu ({{số ngày}} ngày)

---

## 📈 Doanh Thu & Bán Hàng — {{🟢|🟡|🔴}}

- **Thanh toán 7 ngày**: {{TONG}} triệu ({{▲|▼|▬}} {{%}}% so 7 ngày trước)
- **PayPal**: {{PAYPAL}} triệu | **Square**: {{SQUARE}} triệu {{bỏ nếu không kết nối}}

**Giao dịch bất thường**
- {{số tiền}} — {{đối tác}} — {{trạng thái: thất bại/đang chờ/giá trị lớn}}
- {{hoặc "Không có giao dịch bất thường tuần này."}}

---

## 🔮 Pipeline — {{🟢|🟡|🔴}}

- **Pipeline có trọng số**: {{WEIGHTED}} triệu ({{▲|▼|▬}} {{DELTA}} triệu so tuần trước)
- **Độ phủ so mục tiêu**: {{RATIO}}x mục tiêu tháng {{🟢|🟡|🔴}}
- **Deal đóng tuần này**: {{CLOSED}} triệu trên {{N}} deal
- **Deal mới tạo**: {{N}} deal ({{TONG}} triệu)

**Deal cần chú ý**
- {{tên deal}} — {{giai đoạn}} — {{lý do: đã nguội / bị trễ / đình trệ}}
- {{hoặc "Không có deal nào được đánh dấu tuần này."}}

---

## 📅 Tuần Này

- {{Cuộc họp/deadline — đối tác bên ngoài, lý do quan trọng}}
- {{Cuộc họp/deadline}}
- {{Cuộc họp/deadline}}
{{3–5 mục tối đa. Bỏ qua sự kiện nội bộ thuần túy không cần chủ doanh nghiệp chú ý.}}

---

## ✉️ Danh Sách Theo Dõi

- {{người gửi / nguồn}} — {{tóm tắt một dòng về điều cần chú ý}}
- {{người gửi / nguồn}} — {{tóm tắt}}
{{Hoặc: "Không phát hiện chuỗi email khẩn nào." — bao gồm rõ ràng để chủ biết việc kiểm tra đã chạy.}}

---

## ⚠️ Ưu Tiên #1

{{Một việc cụ thể cần hành động hôm nay. Nêu số tiền, tên người, deadline.
Không phải "xem xét dòng tiền" — hãy nói "Hóa đơn 21 triệu từ Công ty XYZ đã quá hạn 23 ngày. Gọi cho anh Minh số 0912-345-678 hôm nay."}}

---

## Phụ Lục

**Khoảng thời gian**: {{phạm vi ngày}}

**Nguồn đã lấy**: {{danh sách connector đã trả về dữ liệu}}

**Nguồn không khả dụng**: {{danh sách kèm lý do, vd: "Gmail — lỗi xác thực" hoặc "Zendesk — chưa kết nối"}}

**Ngưỡng đang dùng**: {{ghi chú các ngưỡng TODO vẫn là mặc định}}
```

---

## Quy tắc định dạng

1. **Số tiền**: `43 triệu` cho triệu đồng, `1,2 tỷ` cho tỷ đồng. Không thêm số thập phân không cần thiết.
2. **Tỷ lệ phần trăm**: một chữ số thập phân cho xu hướng (vd: "▲ 8,3%"), số nguyên ở những chỗ khác.
3. **Ngày tháng**: đọc được trong văn xuôi ("14 tháng 4"), ISO trong metadata ("2026-04-14").
4. **Khoảng mũi tên**: `▲ 2 triệu` không phải `▲2 triệu`.
5. **Độ dài**: hướng tới một trang. Tối đa hai trang. Nếu một phần phình to, cắt bớt văn xuôi.
