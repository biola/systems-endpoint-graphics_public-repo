# Known gaps

Apps that IT Systems Engineering has specifically requested an icon for, and that no
available source could supply. Listed here so a missing icon is a *known* gap with a
recorded reason rather than something to re-investigate from scratch.

A partial/wrong-product substitute is deliberately **not** shipped for these. A
plausible-but-wrong icon in a Jamf/Baseline install list is worse than no icon, and the
monochrome brand glyphs in `generic/monochrome/` are not a substitute for a `software/`
app icon — they render as solid black on transparent, which disappears on dark UIs.

## 2026-08-04 — Jamf/Baseline 42-app deployment batch (36 of 42 shipped)

Originally 34 of 42. **Pro Tools Studio and Pro Tools Ultimate were resolved on 2026-08-19**
by hand-supplied Avid artwork (see the priority-0 source in
[ATTRIBUTION.md](../ATTRIBUTION.md)); both now ship as aliases of `pro-tools`.

| App | Reason no icon is shipped |
|---|---|
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
| `izotope-rx-standard`, `izotope-rx-advanced` | The **iZotope RX 9 Audio Editor** icon (both editions share it). The requested deployment is RX 12; iZotope's RX artwork is stable enough across versions for identification purposes. |

Resolved 2026-08-19 by hand-supplied art, and no longer approximate: `davinci-resolve-studio`
(was identical to the Free edition, now has its own artwork) and `avid-media-composer` (was
the dark-appearance variant reconstructed from a quantized source).
