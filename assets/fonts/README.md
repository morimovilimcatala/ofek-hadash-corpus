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

Only the **latin, latin-ext and hebrew** subsets are kept — 9 files, ~220KB.
The cyrillic, greek and vietnamese subsets Google also serves are not used by
this corpus and are not shipped.

**ONE FILE PER FAMILY PER SUBSET.** Frank Ruhl Libre and IBM Plex Sans are
VARIABLE fonts: one file spans the whole weight axis, so Google serves the
same bytes whichever weight is asked for, and the fetch saved them three times
under three names — ten of the nineteen files here were byte-identical copies
of another five, and they are gone (2026-09-19, MMS-72). IBM Plex Mono is not
variable: its 400 and 500 are different files and both are kept.

`fonts.css` is Google's own `@font-face` CSS with each `src` rewritten to the
local file beside it and each variable family declared ONCE per subset with a
weight RANGE (`font-weight: 400 600`) rather than three times with a single
value. The `unicode-range` declarations are unchanged, so a browser still
downloads only the subset a page actually needs.

The axis stops at 600, so a page asking for 700 is clamped to it — the
reader's sheet therefore asks for 600, and `tests/test_vendored_fonts.py`
keeps the two in step.

To refresh, re-fetch `https://fonts.googleapis.com/css2?family=...` with a
browser user-agent (it serves woff2 only to browsers), keep the three
subsets, and download each `src` URL.
