---
name: tom-tat-dau-tuan
description: Tạo bản tin sáng thứ Hai một trang — tiền mặt, bán hàng, pipeline, lịch tuần, top 3 việc cần làm. Chấp nhận tùy chọn nơi đăng và nơi lưu.
allowed-tools: Read, WebFetch, Bash
compatibility: "Tùy chọn: QuickBooks, PayPal/Square, HubSpot, Gmail, Google Calendar, Slack/Teams, Google Drive. Giảm dần với các connector đang kết nối."
version: "1.1"
---

Chạy Bản Tin Sáng Thứ Hai. Lấy từ mọi phần mềm đang hoạt động, giảm dần khi thiếu, và tạo bản tin một trang chủ doanh nghiệp đọc được trong dưới 2 phút.

Phân tích đối số:
- `--dang-len` (mặc định `khong`) — đăng tóm tắt lên `slack`, `teams`, hoặc `khong`
- `--luu-vao` (mặc định `files`) — `files` (Google Drive / OneDrive), `may-tinh` (local), hoặc `ca-hai`

## Bước 1 — Chạy báo cáo tổng quan

Kích hoạt quy trình kỹ năng `bao-cao-tong-quan`. Lấy theo thứ tự, mở rộng đến bất cứ phần mềm nào đã kết nối:

1. **Tiền mặt** — số dư QuickBooks + luồng ròng 7 ngày qua
2. **Xu hướng bán hàng** — PayPal/Square 7 ngày qua vs 7 ngày trước, % thay đổi, SKU hàng đầu
3. **Pipeline** — deal HubSpot đã chuyển, deal đình trệ (>14 ngày không hoạt động), lead mới
4. **Cam kết tuần này** — sự kiện lịch có người ngoài, deadline deliverable
5. **Danh sách theo dõi** — Gmail chưa đọc cần trả lời, Slack DM đang chờ
6. **3 việc quan trọng** — ba hành động có đòn bẩy cao nhất hôm nay, xếp theo thứ tự

Nếu thiếu phần mềm, ghi chú trong bản tin ("PayPal chưa kết nối — bỏ qua xu hướng bán hàng") thay vì thất bại.

## Bước 2 — Định dạng bản tin một trang

Bố cục (markdown, hiển thị trên một màn hình):

```
# Bản Tin Thứ Hai — {Thứ Hai, DD/MM/YYYY}

## Tiền Mặt
{X triệu đồng số dư · {+/-}Y triệu ròng 7 ngày · ghi chú thời gian còn lại}

## Bán Hàng (7 ngày so với 7 ngày trước)
{X triệu tổng · {+/-}Z% · sản phẩm hàng đầu: {tên} ({giá trị})}

## Pipeline
{N deal đã chuyển · M đình trệ · K lead mới}

## Tuần tới
- {Thứ 3, 10:00} — {Khách X — cuộc họp khám phá}
- {Thứ 5, hết giờ} — {Gửi đề xuất cho Y}
- ...

## Ba việc cần bạn hôm nay
1. {Hành động có đòn bẩy cao nhất với một dòng lý do}
2. {...}
3. {...}
```

## Bước 3 — Lưu và (tùy chọn) đăng lên

1. Lưu bản tin vào vị trí `--luu-vao` đã chọn:
   - `files` — Google Drive hoặc OneDrive, tên file `ban-tin-thu-hai-YYYY-MM-DD.md`
   - `may-tinh` — `~/Desktop/ban-tin-thu-hai-YYYY-MM-DD.md`
   - `ca-hai` — cả hai vị trí
2. Nếu `--dang-len slack` hoặc `--dang-len teams`, đăng **chỉ phần Ba việc** (không phải bản tin đầy đủ — giữ bài đăng kênh ngắn gọn) và link đến file đã lưu.
3. Hiển thị bản tin đầy đủ trong chat bất kể nơi lưu nào.

## Cổng phê duyệt

- **Lưu file là tự động.** Không cần phê duyệt — đây là drive của chính chủ doanh nghiệp.
- **Đăng lên Slack/Teams cần xác nhận.** Hiển thị bản nháp đăng và chờ "đăng đi" trước khi phát hành.
- **Không bao giờ tự động đăng nếu bản tin có số liệu không thuận** (sụt giảm tiền mặt đáng kể, deal trượt) mà không hỏi rõ ràng chủ doanh nghiệp — kênh có thể có thành viên không phải ban lãnh đạo.

## Lưu ý về nhịp độ

Lệnh này được thiết kế để chạy hàng tuần. Chủ doanh nghiệp có thể lên lịch qua bộ lập lịch Cowork — khi chạy thứ Hai lúc 7:00, kết quả đi thẳng đến drive và (nếu đã cấu hình) kênh DM Slack/Teams.

## Ví dụ câu kích hoạt

- *"Cho tôi xem tóm tắt đầu tuần"*
- *"Tuần này có gì?"*
- *"Bản tin sáng thứ Hai"*
- *"Tôi cần biết gì để bắt đầu tuần này?"*
