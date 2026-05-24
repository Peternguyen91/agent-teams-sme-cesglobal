# Hướng Dẫn Đẩy Repo Lên GitHub

Thực hiện các bước sau trong **Terminal** (macOS).

---

## Bước 1 — Mở Terminal và vào thư mục dự án

```bash
cd "/Users/macbookpro/Desktop/1 person/agent-teams-doanh-nghiep-nho-cesglobal"
```

---

## Bước 2 — Khởi tạo Git repo

```bash
git init
git branch -m main
git config user.email "peternguyen9192@gmail.com"
git config user.name "CESGLOBAL"
```

---

## Bước 3 — Thêm tất cả file và tạo commit đầu tiên

```bash
git add .
git commit -m "feat: Khởi tạo Agent Teams CESGLOBAL - 31 kỹ năng tiếng Việt

Plugin Claude Cowork 100% tiếng Việt, chuyển thể từ small-business plugin.
Dành cho chủ doanh nghiệp nhỏ Việt Nam.

31 kỹ năng chia 4 nhóm:
- Tier 1 (6): Tổng quan & điều phối hàng ngày
- Tier 2 (10): Tài chính & dòng tiền
- Tier 3 (8): Marketing & bán hàng
- Tier 4 (7): Vận hành & khách hàng"
```

---

## Bước 4 — Tạo repo trên GitHub

1. Truy cập [github.com/new](https://github.com/new)
2. Điền thông tin:
   - **Repository name:** `agent-teams-doanh-nghiep-nho-cesglobal`
   - **Description:** Plugin Claude Cowork 100% tiếng Việt cho doanh nghiệp nhỏ - CESGLOBAL
   - **Visibility:** Public (để học viên có thể cài đặt dễ dàng)
   - ❌ **KHÔNG** tick "Add a README file" (đã có sẵn)
3. Nhấn **Create repository**

---

## Bước 5 — Kết nối và đẩy lên GitHub

Thay `TEN_GITHUB_CUA_BAN` bằng username GitHub thực tế (ví dụ: `cesglobal`):

```bash
git remote add origin https://github.com/TEN_GITHUB_CUA_BAN/agent-teams-doanh-nghiep-nho-cesglobal.git
git push -u origin main
```

**Nếu GitHub yêu cầu xác thực:** Dùng Personal Access Token (PAT) thay vì mật khẩu.
- Tạo PAT tại: Settings → Developer settings → Personal access tokens → Generate new token
- Tích vào quyền `repo` → Generate → copy token
- Dán token vào ô Password khi Terminal hỏi

---

## Bước 6 — Kiểm tra kết quả

Mở trình duyệt và vào:
```
https://github.com/TEN_GITHUB_CUA_BAN/agent-teams-doanh-nghiep-nho-cesglobal
```

Bạn sẽ thấy toàn bộ 35 file (README + 31 SKILL.md + cấu hình) hiển thị đầy đủ.

---

## Cấu Trúc Repo Hoàn Chỉnh

```
agent-teams-doanh-nghiep-nho-cesglobal/
├── .claude-plugin/
│   └── plugin.json              # Manifest plugin
├── .mcp.json                    # 12 MCP connectors
├── .gitignore
├── README.md                    # Giới thiệu và bảng 31 kỹ năng
├── HUONG_DAN_PUSH_GITHUB.md     # File này
│
└── skills/                      # 31 kỹ năng tiếng Việt
    ├── bao-cao-tong-quan/       # Tier 1: Core daily (6 kỹ năng)
    ├── dieu-phoi-thong-minh/
    ├── gioi-thieu-va-cai-dat/
    ├── tom-tat-dau-tuan/
    ├── tong-ket-cuoi-tuan/
    ├── bao-cao-quy/
    │
    ├── dong-so-cuoi-thang/      # Tier 2: Tài chính (10 kỹ năng)
    ├── du-bao-dong-tien/
    ├── phan-tich-bien-loi-nhuan/
    ├── nhac-no-khach-hang/
    ├── ke-hoach-tra-luong/
    ├── kiem-tra-gia-ban/
    ├── dong-so-thang/
    ├── canh-bao-cuoi-thang/
    ├── chuan-bi-quyet-toan-thue/
    ├── to-chuc-mua-quyet-toan/
    │
    ├── chien-luoc-noi-dung/     # Tier 3: Marketing & Sales (8 kỹ năng)
    ├── chay-campaign/
    ├── phan-loai-lead/
    ├── tao-anh-canva/
    ├── tom-tat-ban-hang/
    ├── danh-sach-goi-dien/
    ├── cap-nhat-crm/
    ├── don-dep-crm/
    │
    ├── tuyen-dung/              # Tier 4: Vận hành & Khách hàng (7 kỹ năng)
    ├── xem-xet-hop-dong/
    ├── review-hop-dong/
    ├── xu-ly-khieu-nai/
    ├── giai-quyet-phan-nan/
    ├── do-nhiet-do-khach-hang/
    └── kiem-tra-mach-dap-khach-hang/
```

---

## Cập Nhật Sau Này

Khi chỉnh sửa hoặc thêm kỹ năng mới:

```bash
cd "/Users/macbookpro/Desktop/1 person/agent-teams-doanh-nghiep-nho-cesglobal"
git add .
git commit -m "cập nhật: [mô tả thay đổi]"
git push
```

---

## Cài Đặt Plugin Từ GitHub (cho học viên)

Sau khi repo đã lên GitHub, học viên cài đặt trong Claude Cowork bằng URL:

```
https://github.com/TEN_GITHUB_CUA_BAN/agent-teams-doanh-nghiep-nho-cesglobal
```

Hoặc clone về máy và cài đặt theo hướng dẫn trong `README.md`.
