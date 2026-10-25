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
├── catalog_combo_160.json             # manifest theme   → RC key data_themes_cute_keyboard
├── data_categories_cute_keyboard.json # category theme   → RC key data_categories_cute_keyboard
├── data_effect_cute_keyboard.json     # manifest effect  → RC key data_effect_cute_keyboard
├── data_effect_categories.json        # category effect
├── data_stickers.json                 # manifest sticker → RC key data_stickers
├── data_sticker_categories.json       # category sticker
├── data_font_categories.json          # category font
├── categories.json                    # sticker gốc từ zip (tham khảo)
├── effects.json                       # effect gốc từ zip (tham khảo)
│
├── <name>_theme/                      # 160 theme (ID 310–469), ~118 MB
│   ├── Background/          bg_<name>_1.webp
│   ├── Keycap/              keycap_<name>_{normal,space,special}_1.webp
│   ├── Popup/               keycap_<name>_1_popup.webp
│   ├── Effect/              img_effect_<name>_1.webp
│   ├── Sound/               sound_<name>_theme_1.mp3
│   ├── ThemePreview/        preview_<name>_theme_1.webp
│   └── PreviewFullKeyboard/ preview_<name>_1.webp
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
└── Category/                          # 40 icon category (webp 128px)
    ├── cate_<type>.webp               # 14 nhóm theme
    ├── effects/effc_*.webp            # 10 nhóm effect
    ├── stickers/stc_*.webp            # 10 nhóm sticker
    └── fonts/fontc_*.webp             # 6 nhóm font
```

## Số liệu

| Thư mục | Số file | Dung lượng |
|---|---|---|
| `*_theme/` (160 thư mục) | ~1.120 | ~118 MB |
| `Template_V2/` | 3.582 | ~350 MB |
| `Effect/` | 115 | ~5.6 MB |
| `fonts/` | 113 | ~7.6 MB |
| `Category/` | 40 | ~176 KB |

Không đưa lên repo: `_tools/` (script build/audit) và `_audit/` (ảnh gallery kiểm tra),
giữ ở bản local `cute_keyboard_data_new`.
