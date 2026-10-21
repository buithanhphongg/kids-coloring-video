# Kênh thiếu nhi — video tô màu (HyperFrames)

Repo này dạy agent (Antigravity, Claude, Codex…) cách sản xuất **video tô màu cho trẻ em**,
dọc 9:16, 20–30 giây, bằng HyperFrames — không cần quay, không cần API trả tiền.

## Sản phẩm đầu ra

| Thông số | Giá trị |
|---|---|
| Kích thước | 1080×1920 (9:16), 30fps |
| Độ dài | 20–30s (3 tranh × 8.5s, hoặc 5 tranh × 5.5s) |
| Nội dung | Tranh viền đen → tô màu từng mảng → "XONG!" → chuyển tranh |
| Âm thanh | Không bắt buộc; nếu có chỉ dùng nhạc/tiếng có license |
| Đối tượng | Trẻ 3–7 tuổi + phụ huynh |

## Cài đặt

```bash
npm i -g hyperframes     # hoặc dùng npx hyperframes@latest
```

Mỗi video là 1 project HyperFrames riêng:

```bash
npx hyperframes init <ten-video> --example blank --resolution portrait --non-interactive
cp templates/index.html <ten-video>/index.html
```

## Quy trình 6 bước

1. **Chốt đề** — 3–5 tranh, mỗi tranh 1 chủ đề trẻ con (con vật, đồ vật, thiên nhiên).
2. **Vẽ SVG** — mỗi tranh 1 `<section class="scene">`, mỗi mảng màu là 1 shape
   `class="art-el fillr ink"` với `data-color`.
3. **Dựng nhịp** — dùng hàm `page(id, t0, len)` trong template, không sửa cấu trúc.
4. **Kiểm** — `npx hyperframes check` phải **0 error** (lint, layout, contrast).
5. **Soi khung** — `npx hyperframes snapshot --at <các mốc giây>`, xem `contact-sheet.jpg`.
6. **Render** — `npx hyperframes render --quality delivery --output renders/<ten>.mp4`.

## Cấu trúc repo

```
AGENTS.md                     luật bắt buộc cho agent
.agents/rules/video-spec.md   đặc tả kỹ thuật (pixel, thời lượng, màu, chữ)
.agents/workflows/tao-video-to-mau.md   workflow /tao-video-to-mau
templates/index.html          template 3 tranh đã pass check + render
docs/phat-hanh.md             checklist đăng YouTube (Made for kids, bản quyền)
```

## Mẫu tham chiếu

`templates/index.html` là video **25.5s – 3 tranh (mèo, hoa, nhà)** đã render thành công.
Mọi video mới chỉ cần: copy template → thay hình SVG → đổi nhãn → render.

## Giấy phép

Code: MIT. Tranh SVG trong template: tự vẽ, dùng thoải mái.
