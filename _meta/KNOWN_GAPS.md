# Known gaps

Apps that IT Systems Engineering has specifically requested an icon for, and that no
available source could supply. Listed here so a missing icon is a *known* gap with a
recorded reason rather than something to re-investigate from scratch.

A partial/wrong-product substitute is deliberately **not** shipped for these. A
plausible-but-wrong icon in a Jamf/Baseline install list is worse than no icon, and the
monochrome brand glyphs in `generic/monochrome/` are not a substitute for a `software/`
app icon — they render as solid black on transparent, which disappears on dark UIs.

## 2026-08-04 — Jamf/Baseline 42-app deployment batch (34 of 42 shipped)

| App | Reason no icon is shipped |
|---|---|
| Pro Tools Studio | Correct art exists on macosicons.com but the stored object returns `403`; that source is now retired. Not present in any other source. |
| Pro Tools Ultimate | Same as Pro Tools Studio. |
| Avid Link | Correct art exists on macosicons.com but all four candidate objects return `504`; that source is now retired. Not present in any other source. |
| AvidApplicationManager | Not present in any available source. |
| Line Budgeter | Not present in any available source. |
| SEH UTN Manager | Not present in any available source. |
| TortoiseSVN | Windows-only application; absent from all the macOS-oriented sources this repo draws from. |
| VIVEPORT | Not present in any available source. |

If you have a legitimately-licensed icon for any of the above, hand it to IT Systems
Engineering rather than uploading it directly — icons enter this repo through the
scripted pipeline so that source and license stay recorded in `manifest.json`.

## Approximate matches (shipped, but not the exact app's art)

These slugs ship a usable icon that is the right product family and vendor but not a
render of that exact application. They're recorded here so nobody assumes they're
pixel-accurate, and so they're easy to upgrade if better art turns up.

| Slug | What's actually shipped |
|---|---|
| `blackmagic-raw` | The **Blackmagic RAW Speed Test** app icon (a speedometer). Correct vendor and RAW branding, but that's Blackmagic's benchmarking utility, not a RAW player/codec icon. |
| `davinci-resolve-studio` | Currently **identical to `davinci-resolve-free`**. A Studio-specific submission exists upstream but its object was unreachable. The separate slug is intentional so Studio can be given its own art later without touching the Free URL. |
| `izotope-rx-standard`, `izotope-rx-advanced` | The **iZotope RX 9 Audio Editor** icon (both editions share it). The requested deployment is RX 12; iZotope's RX artwork is stable enough across versions for identification purposes. |
| `avid-media-composer` | The dark-appearance variant of the Media Composer icon — the light/default variant's object was unreachable. |
