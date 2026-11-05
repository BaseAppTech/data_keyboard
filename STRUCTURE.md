# Cấu trúc data CuteKeyboard (bản new)

Repo: `https://github.com/BaseAppTech/data_keyboard` — base URL raw:
`https://raw.githubusercontent.com/BaseAppTech/data_keyboard/main/`

Mọi đường dẫn trong manifest JSON là **tương đối** so với base URL trên
(riêng `fonts/fonts.json` chứa URL đầy đủ).

```
data_keyboard/
├── README.md                          # nguồn gốc data, cách deploy, ghi chú font
├── STRUCTURE.md                       # file này
│
├── catalog_combo_all.json             # manifest theme   → RC key data_themes_cute_keyboard (398 theme)
├── catalog_combo_160.json             # 160 theme combo nguyên bản từ zip (tham khảo)
├── data_categories_cute_keyboard.json # category theme   → RC key data_categories_cute_keyboard (16 nhóm)
├── data_effect_cute_keyboard.json     # manifest effect  → RC key data_effect_cute_keyboard
├── data_effect_categories.json        # category effect
├── data_stickers.json                 # manifest sticker → RC key data_stickers
├── data_sticker_categories.json       # category sticker
├── data_font_categories.json          # category font
├── categories.json                    # sticker gốc từ zip (tham khảo)
├── effects.json                       # effect gốc từ zip (tham khảo)
│
├── <name>_theme/                      # 398 theme: 160 combo (ID 310–469, ~113 MB)
│   │                                  #          + 238 mới (ID 470–747, ~87 MB, từ 05/11/2026)
│   ├── Background/          bg_<name>_1.webp (+ bg_<name>_night_1.webp nếu ngày/đêm)
│   ├── Keycap/              keycap_<name>_normal_<n>.webp | _c<n>.webp (nhiều màu) | _<n>.gif (premium, động)
│   │                        keycap_<name>_special_1.webp, keycap_<name>_special_1_row3.webp,
│   │                        keycap_<name>_space_1.webp
│   ├── Popup/               keycap_<name>_1_popup.webp
│   ├── Effect/              img_effect_<name>_1.webp
│   ├── Sound/               sound_<name>_theme_1.mp3
│   ├── ThemePreview/        preview_<name>_theme_1.webp (+ preview_<name>_theme_1.mp4: theme mới)
│   └── PreviewFullKeyboard/ preview_<name>_1.webp (+ preview_<name>_night_1.webp nếu ngày/đêm)
│
├── Template_V2/                       # 100 pack sticker (ID 1001–1100), ~350 MB
│   ├── Sticker/<Category>/<Pack>/          <Pack> N.webp, Thumb.webp   (tĩnh)
│   └── Sticker Animation/<Category>/<Pack>/ *.gif                       (động)
│
├── Effect/<Category>/                 # 115 hiệu ứng, img_effect_new_*.webp (~5.6 MB)
│                                      # Bubbles, Cute, Flames, Hearts, Leaves,
│                                      # Smoke & Clouds, Snowflakes, Sparkles, Splats, Stars
│
├── fonts/                             # 112 font (~7.6 MB)
│   ├── fonts.json                     # manifest font → RC key data_theme_fonts
│   └── {Cute,Display,Handwriting,Mono,Sans,Serif}/*.ttf
│
└── Category/                          # 42 icon category (webp 128px)
    ├── cate_<type>.webp               # 16 nhóm theme (thêm cate_glass, cate_coquette)
    ├── effects/effc_*.webp            # 10 nhóm effect
    ├── stickers/stc_*.webp            # 10 nhóm sticker
    └── fonts/fontc_*.webp             # 6 nhóm font
```

## Số liệu

| Thư mục | Số file | Dung lượng |
|---|---|---|
| `*_theme/` (398 thư mục: 160 combo + 238 mới) | 4.920 (2.031 + 2.889) | ~200 MB (113 + 87) |
| `Template_V2/` | 3.582 | ~350 MB |
| `Effect/` | 115 | ~5.6 MB |
| `fonts/` | 113 | ~7.6 MB |
| `Category/` | 42 | ~115 KB |

Không đưa lên repo: `_tools/` (script build/audit) và `_audit/` (ảnh gallery kiểm tra),
giữ ở bản local `cute_keyboard_data_new`.
