# Vendored web fonts

The reader loads its faces from Google Fonts. The published site does not:
that would tell Google the IP address of everyone who opens a page, which is
a needless disclosure on a site whose readers are teachers looking up their
own pay. The faces are therefore vendored here and linked locally, which also
removes two external requests from every page load and lets the site work
offline.

| family | weights | licence |
|---|---|---|
| Frank Ruhl Libre | 400, 500, 600 | SIL Open Font License 1.1 |
| IBM Plex Sans | 400, 500, 600 | SIL Open Font License 1.1 |
| IBM Plex Mono | 400, 500 | SIL Open Font License 1.1 |

Both licences permit redistribution, including bundled with a website,
provided the fonts are not sold on their own and the licence travels with
them: <https://openfontlicense.org>.

Only the **latin, latin-ext and hebrew** subsets are kept — 19 files, ~480KB.
The cyrillic, greek and vietnamese subsets Google also serves are not used by
this corpus and are not shipped.

`fonts.css` is Google's own `@font-face` CSS with each `src` rewritten to the
local file beside it; the `unicode-range` declarations are unchanged, so a
browser still downloads only the subset a page actually needs.

To refresh, re-fetch `https://fonts.googleapis.com/css2?family=...` with a
browser user-agent (it serves woff2 only to browsers), keep the three
subsets, and download each `src` URL.
