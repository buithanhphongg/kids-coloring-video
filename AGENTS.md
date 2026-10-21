# AGENTS.md — kênh thiếu nhi "Bé tô màu"

Bạn là người dựng video cho kênh YouTube Shorts thiếu nhi. Mục tiêu: video tô màu
9:16, 20–30 giây, sạch, an toàn cho trẻ em, render được bằng HyperFrames.

## Lệnh chuẩn

```bash
npx hyperframes init <ten> --example blank --resolution portrait --non-interactive
npx hyperframes check                     # phải 0 error
npx hyperframes snapshot --at 2,6,10,15,20
npx hyperframes render --quality delivery --output renders/<ten>.mp4
```

## Luật bắt buộc

- **Kích thước:** 1080×1920, `data-width="1080"` `data-height="1920"`, 30fps.
- **Thời lượng:** 20–30s. Mỗi tranh 5–9s. Không vượt 30s.
- **Một timeline duy nhất:** `gsap.timeline({ paused: true })` gắn vào
  `window.__timelines["main"]`, key trùng `data-composition-id`.
- **Không tween `visibility` / `autoAlpha` trên phần tử `.clip`.** Không dùng
  `.clip` trừ khi thật cần; template hiện tại không dùng.
- **Không đặt `transform` trong CSS rồi tween cùng thuộc tính đó bằng GSAP**
  (`gsap_css_transform_conflict`). Căn giữa bằng `left/right + margin:auto`,
  không dùng `translate(-50%,-50%)`.
- **Mọi màu phải tương phản ≥ 3:1** với nền nếu là chữ. Chữ luôn nằm trên nền sáng.
- **Không nhạc/tiếng có bản quyền.** Không dùng nhạc trending, không dùng bài hát
  thiếu nhi nổi tiếng (Baby Shark, Let It Go…). Nếu thêm tiếng, chỉ dùng file có
  license rõ ràng hoặc tiếng tự tạo.
- **Không nhân vật có bản quyền** (Peppa, Mickey, Pokémon…). Chỉ hình tự vẽ.

## Phong cách

- Nền giấy kem `#FFFBF0 → #F7E3BE`, viền đen `#2B2118` dày 9px, nét bo tròn.
- Màu tô tươi, tối đa 6 màu/tranh: `#F4A259 #F28DB2 #F9C74F #7FB069 #A8DADC #E76F51`.
- Chữ tiêu đề không dấu hoa mỹ, in đậm, tiếng Việt có dấu đầy đủ.
- Kết tranh bằng dấu "XONG!" màu `#E76F51`, xoay -7°.

## Quy trình làm 1 video

Theo đúng workflow `/tao-video-to-mau` trong `.agents/workflows/`. Không tự đổi
cấu trúc template nếu chưa hỏi người dùng.

## Trước khi bàn giao

- [ ] `check` 0 error
- [ ] `snapshot` đã xem contact sheet, không có chữ đè chữ, không có mảng màu trắng sót
- [ ] MP4 đúng 1080×1920, đúng 20–30s
- [ ] Nhắc người dùng tick **"Made for kids"** khi đăng
