---
name: tao-anh-canva
allowed-tools: Read, WebFetch, Bash
compatibility: "Yêu cầu Canva MCP. Tùy chọn: HubSpot MCP để lên lịch đăng bài; Gmail MCP để bàn giao nội dung email."
version: "1.1"
description: >
  Nhận kế hoạch nội dung đã duyệt và thực hiện campaign đầu cuối: xây dựng
  lịch đăng, tạo thiết kế Canva cho bài mạng xã hội, soạn caption và nội
  dung email, lên lịch đăng trong HubSpot. Canva chỉ dùng cho mạng xã hội
  (Instagram, Facebook, X, LinkedIn) — nội dung email được soạn dạng văn
  bản và trình bày để chủ doanh nghiệp tự gửi. Mọi bước đều cần phê duyệt
  rõ ràng. Sử dụng khi người dùng nói "tạo nội dung đi", "tạo bài đăng",
  "tạo ảnh đi", hoặc bàn giao kế hoạch đã duyệt để thực thi.
---

# Tạo Ảnh Canva

Thực thi campaign theo 5 giai đoạn tuần tự, mỗi giai đoạn đều có cổng phê duyệt:

```
kế hoạch → lịch đăng → kiểm kê tài sản → thiết kế Canva → caption/email → lên lịch HubSpot
```

| Đường dẫn | Kênh | Sản phẩm đầu ra |
|-----------|------|-----------------|
| Canva (mạng xã hội) | Instagram, Facebook, X/Twitter, LinkedIn | Thiết kế Canva + caption + bài đặt lịch HubSpot |
| Văn bản thuần | Email (newsletter, marketing) | Tiêu đề + nội dung, trình bày để chủ doanh nghiệp tự gửi |

**Canva không được dùng cho email trong bất kỳ trường hợp nào.**

---

## Kiểm tra trước khi bắt đầu

Trước Giai đoạn 1, xác nhận:

1. **Kế hoạch nội dung.** Người dùng đã tham chiếu hoặc dán vào một kế hoạch đã duyệt. Nếu chưa: *"Tôi cần kế hoạch nội dung trước khi tạo campaign. Bạn có kế hoạch từ kỹ năng `chien-luoc-noi-dung` chưa, hay muốn tự viết?"*

2. **Gói Canva.** Pro/Teams cần chọn template thủ công từ thư viện; Enterprise có thể tự điền từ brand template.

3. **Gói HubSpot.** Lên lịch mạng xã hội cần Marketing Hub Professional. Starter/Free → bỏ qua Giai đoạn 5 và xuất CSV thay thế.

4. **Tài sản thương hiệu.** Xác nhận đường dẫn đến ảnh sản phẩm hoặc brand kit trong Canva.

5. **Ngân sách thiết kế.** Ước tính khối lượng thiết kế Canva và thông báo trước Giai đoạn 1:

```
Ngân sách thiết kế cho campaign này:
  Bài mạng xã hội (Canva): 8
  Ứng viên mỗi bài:        3   (mặc định — nói "1 ứng viên" để giảm)
  Tổng thiết kế:           24
  API calls ước tính:      ~120

Giới hạn Canva: 100 yêu cầu/phút. Sẽ mất khoảng 2–3 phút. Tiếp tục?
```

Nếu tổng thiết kế vượt 30, gợi ý chế độ 1 ứng viên ngay từ đầu.

---

## Giai đoạn 1 — Lịch đăng bài

Lấy từ kế hoạch: chủ đề nội dung, kênh, tần suất, ngày quan trọng.

Xây dựng bảng lịch với cột `Đường dẫn` phân loại từng bài vào Canva hoặc văn bản thuần:

| Ngày | Kênh | Đường dẫn | Chủ đề | Loại tài sản | Góc độ caption/tiêu đề |
|------|------|-----------|--------|--------------|------------------------|
| 2/6  | Instagram | Canva (MXH) | Ra mắt sản phẩm | Bài vuông | "Cuối cùng đã có..." |
| 5/6  | Email | Văn bản thuần | Ra mắt sản phẩm | Nội dung email | "Giải pháp bạn đang chờ" |

Đánh dấu mọi bài email là `Văn bản thuần` trước khi trình bày. Giới hạn 30 ngày trừ khi kế hoạch chỉ định khác.

**Điểm kiểm tra 1.** Trình bày lịch. Hỏi: *"Có khớp với kế hoạch không? Có ngày nào cần dời, kênh nào cần thêm không?"* Lặp lại cho đến khi được duyệt.

---

## Giai đoạn 2 — Kiểm kê tài sản (chỉ bài Canva)

Bài email bỏ qua giai đoạn này. Với từng bài `Canva (MXH)`:

1. **Liệt kê từng ô ảnh theo tên.** Bài vuông Instagram thường có 1–2 ô ảnh; carousel có thể có 5+. Liệt kê từng ô riêng biệt.

2. **Kiểm kê tài sản hiện có.** Văn bản từ kế hoạch (tên sản phẩm, copy khuyến mãi, tagline), ảnh sản phẩm đã upload vào Canva hoặc trên máy tính.

3. **Bảng thiếu sót theo từng ô:**

| Ngày | Tên ô | Loại | Tài sản có sẵn | Trạng thái |
|------|-------|------|----------------|------------|
| 2/6  | Hero_Image | ảnh | san_pham.jpg | upload |
| 2/6  | Headline | văn bản | "Ra mắt hôm nay" | sẵn sàng |
| 9/6  | Product_Image | ảnh | — | **THIẾU** |

4. **Giải quyết thiếu sót với chủ doanh nghiệp** trước khi tạo bất kỳ thiết kế nào:

```
Template "Carousel Sản Phẩm" có 5 ô ảnh. Kế hoạch chỉ cung cấp 1 ảnh.
Xử lý 4 ô còn lại như thế nào?

  1. Dùng lại cùng 1 ảnh cho tất cả 5 ô
  2. Bạn gửi thêm 4 ảnh (đường dẫn file)
  3. Chọn template đơn giản hơn có ít ô hơn
```

Không tạo thiết kế cho đến khi chủ doanh nghiệp chọn.

---

## Giai đoạn 3 — Tạo thiết kế Canva

Tạo thiết kế **từng bài một**, với 3 ứng viên mỗi bài (hoặc số đã chọn ở bước kiểm tra trước). Dừng 30 giây giữa các bài. Không xử lý song song nhiều bài cùng lúc.

**Vòng lặp mỗi bài:**
1. Chọn template (một lần mỗi session)
2. Tạo các ứng viên song song
3. Xác minh trạng thái job — tất cả phải `thành công`
4. Xuất sang PNG cố định (URL không hết hạn)
5. Kiểm tra trực quan — từ chối nếu thấy ảnh placeholder mặc định, ô trống, văn bản template
6. Thử lại ứng viên lỗi (tối đa 1 lần); nếu thất bại lần 2, hỏi chủ doanh nghiệp
7. Trình bày ứng viên và chờ chủ doanh nghiệp chọn
8. Dừng 30 giây, chuyển sang bài tiếp theo

**Xử lý giới hạn tốc độ:**
- Lần đầu bị giới hạn: chờ 60 giây, thử lại 1 lần
- Lần thứ hai bị giới hạn: dừng ngay, không thử tiếp:

```
Canva đang giới hạn tốc độ. Tình trạng hiện tại:
  ✓ Đã tạo: Bài 1–4 (12 thiết kế)
  ⏸ Còn lại: Bài 5–8 (chưa tạo)

Tiếp theo:
  1. Chuyển sang 1 ứng viên mỗi bài còn lại — xong ngay
  2. Tạm dừng — tiếp tục sau 60 phút
  3. Dừng — làm việc với những gì đã có
```

**Điểm kiểm tra 2.** Hoàn thành khi chủ doanh nghiệp đã chọn 1 thiết kế cho mỗi bài.

---

## Giai đoạn 4 — Soạn caption và nội dung email

**Caption mạng xã hội:**
- Độ dài phù hợp kênh (Instagram ≤ 2.200 ký tự; Facebook ≤ 500; X ≤ 280)
- Cấu trúc: hook → lợi ích sản phẩm → CTA → 3–5 hashtag
- Giọng điệu: theo tone markers trong kế hoạch
- Không mở đầu bằng "Tin tuyệt vời!" hay "Chúng tôi vui mừng thông báo!"

**Email (không dùng Canva):**
- Tiêu đề: ≤ 50 ký tự, cụ thể, không clickbait
- Preheader: ≤ 90 ký tự, bổ sung cho tiêu đề
- Nội dung: 100–250 từ, một CTA duy nhất, giọng điệu tự nhiên như người thật

**Điểm kiểm tra 3.** Hỏi: *"Caption hay email nào cần chỉnh? Nói ngày và muốn thay đổi gì."*

---

## Giai đoạn 5 — Lên lịch HubSpot + bàn giao email

Lên lịch bài đăng mạng xã hội trong HubSpot. Nội dung email trình bày inline để chủ doanh nghiệp copy sang công cụ email của họ.

1. Tạo campaign trong HubSpot với tên và ngày từ lịch
2. Lên lịch từng bài mạng xã hội — trạng thái `ĐẶT LỊCH` (không bao giờ `ĐÃ ĐĂNG`)
3. Xác nhận hàng đợi và cung cấp link xem campaign trong HubSpot
4. Trình bày nội dung email inline, phân nhóm theo ngày gửi

**Điểm kiểm tra cuối:**

```
Bài mạng xã hội đã được lên lịch trong HubSpot: [link]
Chúng sẽ được đăng theo lịch — bạn có thể hủy hoặc chỉnh sửa trong HubSpot.

Nội dung email bên dưới — copy vào công cụ email khi bạn sẵn sàng gửi:
  5/6 — "Giải pháp cho mùa hè này"
  15/7 — "Còn vài chỗ cuối"

Có gì cần chỉnh trước khi xong không?
```

---

## Cổng phê duyệt

- **Không gọi Canva cho bài email.** Kiểm tra cột Đường dẫn trước mỗi lệnh API.
- **Không đăng.** Tất cả bài HubSpot đều đặt là `ĐẶT LỊCH`; chủ doanh nghiệp kiểm soát thời điểm live.
- **Luôn thông báo ngân sách thiết kế trước Giai đoạn 1.**
- **Một bài một lần ở Giai đoạn 3.** Ứng viên trong cùng bài tạo song song, nhưng các bài tuần tự.
- **Không bao giờ bỏ qua Điểm kiểm tra 1.** Tạo thiết kế trước khi duyệt lịch là nguồn gốc lãng phí lớn nhất.
- **Không bao giờ bỏ qua kiểm kê tài sản.** Template nhiều ô sẽ hiển thị ảnh placeholder khi thiếu ô.

## Ví dụ câu kích hoạt

- *"Tạo ảnh cho campaign tháng này"*
- *"Tạo bài đăng từ kế hoạch này"*
- *"Tạo ảnh và lên lịch đăng"*
- *"Biến kế hoạch này thành campaign thực tế"*
