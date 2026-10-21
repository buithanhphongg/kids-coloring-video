---
trigger: always_on
description: Đặc tả kỹ thuật cho video tô màu thiếu nhi (HyperFrames)
---

# Đặc tả video tô màu

## Khung hình

- 1080×1920, 9:16, 30fps, SDR.
- Vùng an toàn: chữ không đặt dưới `y=1700` (UI YouTube che).
- Lề trái/phải 80–90px.

## Bố cục 1 tranh

```
y=96      nhãn "TÔ MÀU CÙNG BÉ" (34px, letter-spacing .28em)
y=176     tên tranh (88px, weight 900)
y=380     vùng hình SVG 900×900 (chiếm 90px lề mỗi bên)
y=1210    dấu "XONG!" (62px, nền #E76F51, chữ #FFFDF7, xoay -7°)
y=1776    thanh tiến trình (3–5 chấm)
y=1836    nhãn chân "BÉ TÔ MÀU"
```

## Nhịp 1 tranh (8.5s)

| Thời điểm | Hành động |
|---|---|
| +0.00 | scene hiện (opacity) |
| +0.10 | tên tranh trượt lên |
| +0.30 | nét vẽ hiện dần, stagger 0.035s |
| +1.45 | tô màu từng mảng, stagger 0.22s, mỗi mảng 0.5s |
| +5.30 | lấp lánh quanh tranh |
| +5.55 | dấu "XONG!" bật (back.out) |
| +6.10 | đẩy nhẹ 1.00 → 1.04 |
| +8.10 | chuyển tranh (fade 0.5s) |

## Màu

| Vai trò | Mã |
|---|---|
| Giấy | `#FFFDF7` |
| Nền | `#FFFBF0 → #F1DDB8` |
| Viền | `#2B2118` |
| Cam chủ đạo | `#E76F51` |
| Vàng | `#F9C74F` |
| Hồng | `#F28DB2` |
| Xanh lá | `#7FB069` |
| Xanh trời | `#A8DADC` |
| Cam nhạt | `#F4A259` |

## Cấu trúc SVG 1 tranh

```html
<section class="scene" id="p1">
  <div class="name">CHÚ MÈO</div>
  <div class="art">
    <svg viewBox="0 0 900 900">
      <!-- mọi hình đều có class art-el; mảng tô màu thêm fillr + data-color -->
      <ellipse class="art-el fillr ink" data-color="#F4A259" cx="450" cy="474" rx="248" ry="222"/>
    </svg>
  </div>
  <div class="stamp">XONG!</div>
</section>
```

Quy tắc vẽ:
- Nét: `stroke-width: 9`, `stroke-linejoin: round`, `vector-effect: non-scaling-stroke`.
- Hình nằm trong hình khác phải vẽ **sau** (z-order) để viền không bị che.
- Mảng tô màu khởi tạo `fill="#FFFDF7"` (do JS set), GSAP đổi `attr.fill` sang `data-color`.
- Không dùng filter/blur/shadow trong SVG (làm chậm render, lệch màu).

## Nội dung an toàn cho trẻ em

- Chủ đề: con vật, cây cối, đồ vật quen, phương tiện, nhà cửa, thức ăn.
- Không: vũ khí, máu, sợ hãi, nhân vật có bản quyền, chữ tiếng Anh khó hiểu.
- Không kêu gọi like/sub trong video.
