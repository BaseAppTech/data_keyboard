# Fonts to upload

Copy all font files and `fonts.json` from this folder to:
`Braly-Danang-2/cute_keyboard_data`, branch `main`, folder `fonts`.

Firebase Remote Config: create/update String key `data_theme_fonts` and paste
`fonts.json` as its value (the JSON object itself, not a URL). The app also bundles
this small JSON as defaults, so existing font_name values keep working without
an activated override. Font binaries are outside every Android source set.

`legacy_resource_id` and `resource_name` preserve existing selection, unlock and
Font Art draft identities. Do not change them for existing fonts. Keep aliases
such as nsimsun/simsun and vni-bandit/bandit. When replacing a font, update its URL,
sha256 and size_bytes. Downloads use the existing GitHub token/CDN asset routing. The app verifies downloads and saves them in private
filesDir for offline use. A failed download keeps the existing selection/theme
and exposes retry through the existing action. UI fonts referenced in XML stay
bundled; all other app fonts, including Customize and Font Art, are remote.

Upload these files before releasing the app: first use requires network access.
No files have been uploaded by this change.
