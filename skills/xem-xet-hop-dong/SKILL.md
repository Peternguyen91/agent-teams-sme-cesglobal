---
name: xem-xet-hop-dong
allowed-tools: Read, WebFetch, Bash
compatibility: "Không yêu cầu connector — hoạt động hoàn toàn với file cục bộ. Tùy chọn: Gmail MCP để lấy hợp đồng từ email đính kèm; DocuSign MCP để lấy phong bì đang chờ ký."
version: "1.1"
description: >
  Xem xét hợp đồng NDA, MSA và hợp đồng nhà cung cấp cho doanh nghiệp nhỏ
  chưa có bộ phận pháp lý. Đọc hợp đồng từ file cục bộ, tệp đính kèm Gmail,
  hoặc phong bì DocuSign; đánh dấu điều khoản bất thường; giải thích rủi ro
  bằng ngôn ngữ đơn giản; và xuất bản đỏ đánh dấu dưới dạng DOCX riêng. Sử
  dụng khi người dùng nói "xem lại hợp đồng này", "tôi đang ký gì", "có rủi
  ro gì không", "kiểm tra điều khoản thanh toán".
---

# Xem Xét Hợp Đồng

Đính kèm file hợp đồng, chuyển tiếp email có chứa hợp đồng, hoặc dán nội dung trực tiếp.

```
Ví dụ: "Xem lại MSA này và đánh dấu điều gì tôi nên phản đối"
→ Kỹ năng đọc tài liệu, xác định các bên và loại hợp đồng,
  phân tích 8 nhóm rủi ro, trả về tóm tắt theo mức độ nghiêm trọng
  kèm hướng dẫn đàm phán, và xuất DOCX có đánh dấu bản đỏ.
```

> ⚠️ **Đây không phải tư vấn pháp lý.** Luôn xem xét với luật sư của bạn trước khi ký.

---

## Quy trình thực hiện

### Bước 1 — Lấy hợp đồng

Lấy từ một trong ba nguồn theo thứ tự ưu tiên:
- **Gmail**: tìm email gần đây có đính kèm hợp đồng
- **DocuSign**: lấy phong bì theo ID hoặc tìm bản nháp đang chờ ký
- **File cục bộ hoặc dán văn bản**: đọc PDF hoặc DOCX. Nếu người dùng dán văn bản trực tiếp, làm việc với nội dung đó.

Đọc toàn bộ tài liệu trước khi phân tích. Các điều khoản nguy hiểm thường nằm ở phụ lục và phần sau của hợp đồng.

---

### Bước 2 — Xác định loại hợp đồng và các bên

Xác định loại hợp đồng (NDA, MSA, SOW, SaaS, tư vấn, nhà thầu phụ, nhà cung cấp) và bên nào là công ty của người dùng vs. đối tác. Ghi chú nếu đây là mẫu của đối tác — thường một chiều và đối tác mong đợi phản đối.

---

### Bước 3 — Phân tích 8 nhóm rủi ro

**Nhóm 1: Điều khoản thanh toán và dòng tiền**
- Thời hạn thanh toán: Net-30 là tiêu chuẩn; Net-60+ cần đánh dấu; Net-90/120 là điểm đàm phán cứng
- Điều kiện kích hoạt thanh toán, yêu cầu phê duyệt có thể trì hoãn vô thời hạn
- Phạt thanh toán trễ: không có là thiếu sót đáng ghi chú
- Yêu cầu lập hóa đơn: định dạng cứng nhắc có thể trì hoãn thanh toán
- Hoàn trả chi phí: yêu cầu phê duyệt trước và hạn mức
- Điều chỉnh giá: cơ chế tăng hàng năm cho hợp đồng nhiều năm

**Nhóm 2: Trách nhiệm pháp lý và bồi thường**
- Giới hạn trách nhiệm: không có giới hạn luôn là cờ đỏ
- Bồi thường có đi có lại vs. một chiều
- Phạm vi bồi thường quá rộng: đánh dấu nổi bật
- Yêu cầu bảo hiểm: khả năng đạt mức bảo hiểm yêu cầu
- Miễn trừ thiệt hại gián tiếp: thiếu = đánh dấu

**Nhóm 3: Chấm dứt hợp đồng**
- Chấm dứt vì lý do thuận tiện: có đối xứng không? Thông báo 30 ngày là tiêu chuẩn
- Chấm dứt có lý do: thời gian khắc phục; "vi phạm trọng yếu" mơ hồ
- Thanh toán công việc đang thực hiện khi chấm dứt
- Hỗ trợ chuyển giao: có trả phí không, giới hạn thời gian không
- Điều khoản tồn tại vô thời hạn = đánh dấu

**Nhóm 4: Sở hữu trí tuệ**
- Chuyển nhượng IP vs. cấp phép
- Bảo lưu IP nền và công cụ nội bộ — thiếu có nghĩa chuyển nhượng không chủ ý
- Phạm vi định nghĩa sản phẩm: bản nháp, ghi chú, công cụ nội bộ

**Nhóm 5: Phạm vi và quản lý thay đổi**
- Tính rõ ràng của định nghĩa phạm vi
- Quy trình lệnh thay đổi: thiếu = phạm vi creep không có thù lao
- Tiêu chí nghiệm thu: chủ quan ("theo thỏa mãn của khách hàng") vs. được định nghĩa
- Bất đối xứng thời gian: người dùng bị phạt khi chậm trễ nhưng khách hàng không bị phạt

**Nhóm 6: Không cạnh tranh và độc quyền**
- Phạm vi không cạnh tranh, định nghĩa "đối thủ", thời hạn
- Yêu cầu độc quyền từ công ty người dùng
- Không dụ dỗ nhân viên: bình thường; hạn chế toàn ngành là không bình thường

**Nhóm 7: Bảo mật và dữ liệu**
- Phạm vi bảo mật: "mọi thông tin chia sẻ" không có ngoại lệ = quá rộng
- Thời hạn: 2–3 năm là tiêu chuẩn; vĩnh viễn = hung hăng
- Yêu cầu bảo mật dữ liệu so với quy mô công ty
- Yêu cầu trả lại/tiêu hủy sau khi chấm dứt

**Nhóm 8: Vận hành**
- Luật điều chỉnh và giải quyết tranh chấp; trọng tài bắt buộc
- Tự động gia hạn: cửa sổ từ chối và thời gian thông báo (bỏ lỡ cửa sổ 60 ngày là lỗi phổ biến)
- Quyền chuyển nhượng, đặc biệt nếu khách hàng bị mua lại
- Most favored nation: ràng buộc giá với toàn bộ danh sách khách hàng
- Quyền kiểm toán: phạm vi và tần suất

---

### Bước 4 — Tóm tắt theo mức độ

**🔴 Cờ đỏ (phải phản đối trước khi ký)** — Với mỗi mục: trích dẫn điều khoản cụ thể, giải thích vấn đề bằng ngôn ngữ đơn giản, đề xuất ngôn ngữ thay thế cụ thể.

**🟡 Cờ vàng (cần đàm phán, không phải lý do hủy)** — Với mỗi mục: trích dẫn điều khoản, giải thích lo ngại, mô tả điều gì là "tốt hơn".

**🟢 Điều khoản quan trọng cần lưu ý** — Lịch thanh toán, thời hạn thông báo, ngày gia hạn, yêu cầu bảo hiểm.

**📋 Tóm tắt hợp đồng** — Ngôn ngữ đơn giản: ai làm gì, bao nhiêu tiền, trong bao lâu, dưới điều kiện gì.

**💡 Hướng dẫn đàm phán** — Với mỗi cờ đỏ và vàng: yêu cầu gì, cách đặt vấn đề, thỏa hiệp hợp lý.

---

### Bước 5 — Xuất DOCX bản đỏ

Sau khi trình bày tóm tắt, đề xuất xuất DOCX có đánh dấu bản đỏ:
- Giữ nguyên cấu trúc hợp đồng gốc
- Đánh dấu đề xuất xóa bằng gạch ngang, thêm mới bằng gạch chân
- Thêm trang bìa tóm tắt các thay đổi

Hỏi: *"Bạn có muốn tôi xuất DOCX bản đỏ để gửi lại cho đối tác không?"*

---

## Cổng phê duyệt

- **Không bao giờ mô tả kết quả là tư vấn pháp lý.** Luôn khuyến nghị xem xét với luật sư cho cờ đỏ.
- **Trích dẫn ngôn ngữ điều khoản thực tế**, không phải diễn giải. Người dùng cần văn bản cụ thể khi đàm phán.
- **Đánh dấu cả điều gì còn thiếu**, không chỉ điều gì có trong đó.
- **Không đánh dấu boilerplate tiêu chuẩn.** Người dùng muốn tín hiệu, không phải phân tích từng điều khoản.
- **Không bao giờ gửi DOCX bản đỏ cho đối tác** mà không có xác nhận rõ ràng.

## Ví dụ câu kích hoạt

- *"Xem lại hợp đồng này"*
- *"Tôi đang ký gì vậy?"*
- *"Có điểm gì nguy hiểm không?"*
- *"Kiểm tra điều khoản thanh toán"*
- *"Đánh dấu rủi ro trong hợp đồng"*
