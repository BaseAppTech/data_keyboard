# cute_keyboard_data_new — Bộ data mới cho app CuteKeyboard

Dựng 100% từ 4 file zip (không tái sử dụng file nào của `cute_keyboard_data` cũ):

| Zip | Nội dung |
|---|---|
| `data_keyboard_combo_160.zip` | 160 theme hoàn chỉnh (ID 310–469), mỗi theme: Background, Keycap, Popup, Sound, Effect, ThemePreview, PreviewFullKeyboard + `catalog_combo_160.json` — **đã bỏ video preview** (xóa 160 mp4, lược field `preview_video_url` khỏi catalog; app tự fallback ảnh webp tĩnh) |
| `sticker_100packs_thumbsv2.zip` | 100 pack sticker (ID 1001–1100) trong `Template_V2/Sticker/` (static) và `Template_V2/Sticker Animation/` (gif) + `categories.json` |
| `effects_100.zip` | 115 hiệu ứng trong `Effect/` + `effects.json` |
| `fonts_100.zip` | 112 font trong `fonts/{Display,Handwriting,Sans,Serif,Mono,Cute}/` + `fonts/fonts.json` |

Tổng: ~6.000 file, ~520 MB.

## Manifest cho app

App đọc manifest JSON qua Firebase Remote Config (fallback asset trong APK) và tải
file nhị phân theo **đường dẫn tương đối** ghép với base URL repo data. Các manifest
đã sinh sẵn ở root thư mục này:

| File | Dùng cho Remote Config key | Ghi chú |
|---|---|---|
| `catalog_combo_160.json` | `data_themes_cute_keyboard` | Đúng format `KeyboardModel`, dùng nguyên bản từ zip |
| `data_effect_cute_keyboard.json` | `data_effect_cute_keyboard` | Chuyển từ `effects.json` sang format `EffectModel` (id, name, image_url, is_free, effect_type=1). 15 entry cuối của zip không có `id`/`name` — đã gán từ số `n` và tên file |
| `data_stickers.json` | `data_stickers` | Chuyển từ `categories.json` sang format `StickerCategoryModel` (id, name, img_thumb, stickers[], price, is_free). `img_thumb` = `Thumb.webp` của pack. **Tự phân cấp theo độ phổ biến (downloads)**: 75 pack free / 15 pack 100 cà rốt / 10 pack hot nhất 200 cà rốt — model sticker không có `premium_only` nên chỉ 2 tầng free/carrot (VIP sub mở hết) |
| `fonts/fonts.json` | `data_theme_fonts` | Nguyên bản từ zip, đã rewrite URL trỏ về repo mới |

## Category — đủ 4 nhóm, mỗi nhóm có icon riêng (40 icon tự vẽ trong `Category/`)

Icon tự sinh bằng `_tools/build_categories.py` (nền pastel bo góc + emoji, webp 128px):

| Nhóm | File JSON | Số category | Icon |
|---|---|---|---|
| Theme | `data_categories_cute_keyboard.json` (format `CategoryItem`, set key `data_categories_cute_keyboard`) | 14 (cute 44, trending 15, sport 14, kawaii 14, zodiac 13, new 13, kpop 11, cartoon/aesthetic/minimal/gaming 6, holiday 5, cat 4, pixel 3) | `Category/cate_<type>.webp` |
| Effect | `data_effect_categories.json` + field `category` trong `data_effect_cute_keyboard.json` | 10 (Sparkles 33, Cute 15, Leaves 14, Smoke & Clouds 14, Bubbles 12, Stars 10, Splats 8, Flames 5, Snowflakes 3, Hearts 1) | `Category/effects/effc_*.webp` |
| Sticker | `data_sticker_categories.json` + field `category`/`type` trong `data_stickers.json` | 10 (Cats 15, Animals/Anime/Cute 12, Couple/Meme 10, Chibi/Food/Seasonal 8, Game 4) | `Category/stickers/stc_*.webp` |
| Font | `data_font_categories.json` + field `category` sẵn trong `fonts/fonts.json` | 6 (Sans 34, Display 28, Handwriting 24, Cute 12, Serif 8, Mono 6) | `Category/fonts/fontc_*.webp` |

App hiện tại: tab theme đọc category thật (`CategoryItem`); effect/sticker/font app chưa
có UI nhóm theo category — field đã đặt sẵn, Gson bỏ qua cho tới khi có UI. Mọi
`icon_url` là đường dẫn tương đối, app tự ghép base URL repo mới.

## Bước deploy

1. **Tạo GitHub repo data mới** (ví dụ `BaseAppTech/data_keyboard`) và
   push toàn bộ thư mục này (trừ `_tools/`).
2. **Sửa `NEW_BASE_URL`** trong `_tools/build_manifests.py` cho khớp repo thật rồi
   chạy lại `python _tools/build_manifests.py` để rewrite lại URL trong
   `fonts/fonts.json` và validate toàn bộ path/hash. `fonts/fonts.json` hiện đang
   trỏ tới `https://raw.githubusercontent.com/BaseAppTech/data_keyboard/main/`.
3. **Cấp GitHub token** (key `access_key_remote_data`) quyền đọc repo đó — app gửi
   token trong header Authorization khi tải asset.
4. **Set Firebase Remote Config**: 4 key ở bảng trên (dán nguyên nội dung JSON).
   Các key cũ (`data_theme_premium`, `data_discovery`…) giữ nguyên vẫn dùng data cũ.

## Không trùng data cũ

- Theme ID 310–469 vs cũ 1–144; sticker pack ID 1001–1100; 0 pack sticker trùng tên với cũ.
- 160 thư mục theme `<name>_theme/` không đụng tên thư mục nào của repo cũ.
- 112 font mới là font hoàn toàn khác 78 font cũ (chỉ trùng tên file
  `patrickhand.ttf`/`sniglet.ttf` ở thư mục con khác — nội dung là file mới).
- Font của theme cũng chỉ dùng font mới (đã gán lại — xem mục dưới).

## Font đã gán cho theme (dùng font mới 100%)

`catalog_combo_160.json` ban đầu tham chiếu 22 font không có trong fonts_100.zip —
đã gán lại toàn bộ bằng font mới theo vibe (`_tools/assign_fonts.py`, chạy sẵn):

| Font cũ (thiếu) | Font mới | Số theme |
|---|---|---|
| comicneue | sniglet (Cute) | 50 |
| fredoka | mplusrounded1c (Cute rounded) | 18 |
| baloo | baloo2 (cùng họ Baloo) | 13 |
| rowdies | blackopsone (bold display) | 10 |
| sancreek, rye | barriecito (decorative) | 6 |
| sairastencilone | goldman (techy) | 5 |
| dynapuff | itim (Cute) | 4 |
| bebas_neue | bigshoulders (condensed) | 3 |
| praise | alexbrush (script) | 3 |
| pixelifysans | majormonodisplay (Mono game) | 2 |
| summershow | cherrybombone | 2 |
| cupcake | coiny (Cute) | 2 |
| 10 font dùng 1 theme | super_mario→bungee, skranji→proteststrike, pixeloperator→jetbrainsmono, nsimsun→**lxgwwenkaitc** (CJK), pecita→mali, mental_mania→foldit, shojumaru→chokokutai (Japanese), tagesschrift→museomoderno, vni-bandit→bungeetint | 10 |

33 theme còn lại dùng `urbanist`/`urbanist_regular`/`urbanist_bold` — app bundle
sẵn trong APK nên không cần font ngoài. Sau khi gán: **mọi theme đều có font
trong bộ data mới, không phụ thuộc repo cũ, không font nào thiếu.**
