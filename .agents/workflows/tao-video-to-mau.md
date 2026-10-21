---
description: Dựng 1 video tô màu thiếu nhi 20-30s bằng HyperFrames
---

# Workflow: tạo video tô màu

Chạy workflow này khi người dùng nói "làm video tô màu", "video cho bé", "tô màu con mèo"…

## Bước 0 — Hỏi (tối đa 3 câu, gộp 1 lần)

1. Mấy tranh? (mặc định 3 → 25s)
2. Chủ đề từng tranh? (mặc định: con mèo, bông hoa, ngôi nhà)
3. Tên kênh / nhãn chân? (mặc định "BÉ TÔ MÀU")

Nếu người dùng đã nói rõ thì bỏ qua, làm luôn.

## Bước 1 — Tạo project

```bash
npx hyperframes init <slug> --example blank --resolution portrait --non-interactive
cp templates/index.html <slug>/index.html
```

Đổi `data-duration` theo số tranh: `n = số tranh`, mỗi tranh 8.5s, cộng 0.5s đuôi.

## Bước 2 — Vẽ tranh

Với mỗi tranh, thay `<section id="pN">`:

- Đổi tên tranh trong `.name`.
- Vẽ SVG mới trong `<svg viewBox="0 0 900 900">`, theo đặc tả `.agents/rules/video-spec.md`.
- Mỗi mảng cần tô: `class="art-el fillr ink" data-color="#..."`.
- Mỗi chi tiết chỉ viền: `class="art-el ink"` + `fill="none"` (nếu là path).
- Giữ thứ tự vẽ: nền → chi tiết lớn → chi tiết nhỏ → mắt/miệng.

Kiểm tra bằng mắt: hình phải kín, không hở nét, không chồng viền lên màu đã tô.

## Bước 3 — Dựng nhịp

Cuối file, sửa danh sách gọi:

```js
page("p1", 0.0, 8.4);
page("p2", 8.5, 8.4);
page("p3", 17.0, 8.5);
```

Thêm/bớt theo số tranh. Giữ nguyên tham số nhịp trong hàm `page()`.

## Bước 4 — Kiểm

```bash
npx hyperframes check
```

Phải **0 error**. Lỗi thường gặp:

| Lỗi | Cách sửa |
|---|---|
| `content_overlap` | hai khối chữ đè nhau → hạ khối dưới xuống |
| `gsap_css_transform_conflict` | bỏ `transform` khỏi CSS, để GSAP lo |
| `font_family_without_font_face` | dùng `sans-serif`, đừng đặt tên font lạ |
| contrast < 3:1 | làm chữ đậm hơn (`#2B2118`) hoặc nền sáng hơn |

## Bước 5 — Soi khung

```bash
npx hyperframes snapshot --at 2,6,10,14,19,23
```

Mở `contact-sheet.jpg` trong thư mục snapshot. Kiểm:
- Tranh có bị "dính" mảng (thiếu đường viền phân cách) không.
- Có mảng nào còn trắng dù đáng ra phải tô không.
- Chữ "XONG!" có che mất chi tiết quan trọng không.

## Bước 6 — Render + bàn giao

```bash
npx hyperframes render --quality delivery --output renders/<slug>.mp4
```

Báo lại: đường dẫn file, thời lượng, kích thước. Nhắc người dùng:
- Tick **"Made for kids"** khi đăng.
- Tiêu đề gợi ý: `Tô màu <chủ đề> 🎨 | Bé tô màu cùng bố mẹ`.
- Không dùng nhạc trending.

## Sai thì làm gì

1. Đọc lỗi `check` → sửa đúng file, không sửa lung tung.
2. Render hỏng: xoá `.hyperframes/` rồi chạy lại.
3. Không chắc bố cục: chạy `npx hyperframes preview` để xem trực tiếp.
