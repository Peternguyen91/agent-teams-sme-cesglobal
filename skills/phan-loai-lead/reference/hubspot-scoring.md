# Chấm Điểm HubSpot — phân-loai-lead

Tên trường, trọng số điểm, và cấu hình ICP mặc định.

---

## Các trường cần lấy

| Trường HubSpot | Dùng cho |
|---|---|
| `firstname`, `lastname` | Hiển thị |
| `company` | Hiển thị + đối chiếu ICP |
| `email` | Người nhận bản nháp theo dõi |
| `lifecyclestage` | Lọc (giữ Lead, MQL) |
| `hs_lead_status` | Lọc (loại bỏ Unqualified) |
| `industry` | Mức độ phù hợp công ty |
| `numemployees` | Mức độ phù hợp — quy mô. Thường null; nếu null, xử lý là không rõ và chấm điểm tương ứng. |
| `createdate` | Độ khẩn — tuổi lead |
| `hs_last_activity_date` | Phạt gần đây |
| `notes_last_updated` | Độ khẩn — ghi chú mới |
| `hs_sales_email_last_replied` | Tương tác — tín hiệu trả lời |
| `hs_email_open` | Tương tác — số lần mở (chỉ dùng nếu trong 30 ngày) |
| `hs_analytics_last_visit_timestamp` | Tương tác — lượt truy cập website |
| `num_contacted_notes` | Tương tác — số lần liên hệ |

---

## Mô hình chấm điểm (tổng 0–100)

Bốn chiều, mỗi chiều 0–25. Cộng để ra điểm tổng hợp.

### Tương tác (0–25)
Chỉ tính tín hiệu từ 30 ngày gần nhất. Tín hiệu cũ hơn = 0 điểm.

| Tín hiệu | Điểm |
|---|---|
| Trả lời email trong 14 ngày qua | +15 |
| Mở email trong 7 ngày qua (không có trả lời) | +8 |
| Truy cập website trong 7 ngày qua | +5 |
| Đã liên hệ >3 lần, không phản hồi | −5 |

### Mức độ phù hợp công ty (0–25)
ICP mặc định nếu chủ chưa chỉ định: mọi ngành, 1–50 nhân viên.

| Mức độ | Điểm |
|---|---|
| Ngành + quy mô đều khớp ICP | 25 |
| Quy mô khớp, ngành không rõ | 15 |
| Ngành khớp, quy mô không rõ | 12 |
| Không khớp hoặc cả hai không rõ | 5 |

### Độ khẩn (0–25)

| Tín hiệu | Điểm |
|---|---|
| Ghi chú chứa "gấp", "khẩn", "deadline", "đã duyệt ngân sách" | +15 |
| Tuổi lead 7–21 ngày (cửa sổ follow-up tốt nhất) | +10 |
| Tuổi lead < 7 ngày | +5 |
| Tuổi lead > 60 ngày | −5 |

### Phạt hoạt động gần đây (trừ khỏi tổng)

| Hoạt động gần nhất | Trừ điểm |
|---|---|
| < 24 giờ trước | −25 |
| 1–3 ngày trước | −10 |
| 4–7 ngày trước | −5 |
| > 7 ngày trước | 0 |

---

## Tùy chỉnh ICP (ghi đè lúc chạy)

Nếu chủ doanh nghiệp nêu ICP trong lúc chat ("tập trung vào công ty sản xuất, 10–100 nhân viên"), áp dụng cho phiên đó. Không lưu lại vĩnh viễn — ghi đè chỉ áp dụng cho lần chạy hiện tại.
