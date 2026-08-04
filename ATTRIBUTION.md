# Attribution

This repository aggregates icons from multiple upstream sources, deduplicated and re-rendered to a consistent format. Each shipped icon's exact source is recorded per-slug in [`_meta/manifest.json`](_meta/manifest.json); this file documents the sources themselves.

## `software/` sources (priority order — higher priority wins when the same app appears in multiple sources)

Revamped 2026-07-17: kbareis/icons and macosicons.com were added, and the priority order was reshuffled to favor the "squirqle" macOS app-icon shape and official macOS Tahoe icon renders wherever available. The previous `software/` build is preserved untouched at `software-old/` in case of rollback; `software/variants/` preserves every kbareis-captured mode (light/dark/clear/tinted/legacy) for a given app even though only one is picked as the primary `software/<slug>.png`.

| Priority | Source | License | Notes |
|---|---|---|---|
| 1 | [kbareis/icons](https://github.com/kbareis/icons) | Private — personal authorization from the repo owner (a Biola-affiliated Apple colleague), not a public open-source license | Pulled in full (273 apps). Prefers the official macOS Tahoe squircle render when the colleague captured one (picking the default/light mode among light/dark/clear/tinted captures), falling back to their legacy-style capture otherwise. Every captured mode is preserved under `software/variants/`, not just the primary pick. |
| 2 | [technotica/JamfManager-Icons](https://github.com/technotica/JamfManager-Icons) | No explicit license | Pulled in full. Jamf-admin-curated collection, predominantly squirqle-shaped; used here under the same fair-use rationale it's already commonly used under in the Jamf-admin community, for identification purposes as part of Biola's own software deployment tooling (educational institution). |
| 3 | [macosicons.com](https://www.macosicons.com) (API) — **retired 2026-08-04, no longer acquired from** | Per-icon community submission — **attribution required per icon** | Used only to fill gaps in Biola's own relevant-software list that neither kbareis nor JamfManager-Icons cover, under a hard-capped paid-tier API query budget (2 keys × 50 queries/month). Each icon is an individual community member's submission, not a blanket-licensed collection — macosicons.com's terms require crediting macOSicons.com and the original creator for every icon used, not just the source as a whole. Per-icon creator credit (submitter name, profile link, download count at time of pull) is recorded in `_meta/manifest.json` under `macosicons_credit` for every slug sourced this way — see that file for the full list rather than duplicating it here. |
| 4 | [homarr-labs/dashboard-icons](https://github.com/homarr-labs/dashboard-icons) | Apache-2.0 | Filtered to software matching Installomator's supported-app list or Biola's internal Mac-lab software inventory — not pulled in full. |
| 5 | [pheralb/svgl](https://github.com/pheralb/svgl) | MIT | Pulled in full. Where svgl shipped multiple theme/style variants of the same logo (e.g. `-dark`/`-light`/`-wordmark`), only one canonical version was kept. Kept as a lower-priority fallback since the 2026-07-17 revamp. |
| 6 | [HCSTech/icons](https://github.com/HCSTech/icons) | No explicit license | Pulled in full. Same fair-use / educational-use rationale as JamfManager-Icons above — this was Biola's prior icon source before this repo existed. Kept as a last-resort fallback since the 2026-07-17 revamp. |

## `generic/monochrome/` source

| Source | License | Notes |
|---|---|---|
| [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons) | CC0-1.0 (public domain) | Pulled in full. Single-color brand glyphs, kept in a separate folder from full-color `software/` icons since they serve a different purpose (generic identification, not a primary app icon). |

## Sources evaluated but not used

- **KevinGutowski/Big-Sur-Icons** — excluded. Explicitly marked "Copyright © Apple, research purposes only" (a more pointed restriction than the fair-use sources above), and 5+ years outdated (macOS Big Sur era).
- **elrumo/macOS_Big_Sur_icons_replacements** — excluded. Despite being the original seed project behind macosicons.com, the GitHub repo itself contains no actual app-replacement icons (only the project's own website assets); all real content lives solely on the live site.
- **macosicons.com (bulk/scraped access)** — excluded. Bot-protected against bulk/automated access. Its *API* was later used as a narrow, budget-capped gap-filler in the 2026-07-17 revamp (priority 3 above) and has since been retired — see "macosicons.com retirement" below.
- **selfhst/icons** — deferred to a potential future Phase 2, not Phase 1. Broad self-hosted/homelab app coverage that would add thousands of icons largely unrelated to Biola's actual deployed software.

## Aliased icons

Some deployment lists name a product differently than any upstream source does. Rather than
renaming a canonical slug — which would break an already-published `raw.githubusercontent.com`
URL — such a product is published as an **additional** copy of an existing icon, leaving the
original slug's file and URL untouched. Both slugs are real, shipped files with identical
content and identical attribution.

| Published alias | Same icon as | Underlying source |
|---|---|---|
| `adobe-cc-full-suite` | `adobe-creative-cloud` | kbareis/icons |
| `quicktime-player` | `quicktime` | kbareis/icons |
| `unity-hub` | `unity` | homarr-labs/dashboard-icons |
| `epic-games-launcher` | `epic-games` | homarr-labs/dashboard-icons |

## macosicons.com retirement (2026-08-04)

macosicons.com is **no longer used to acquire new icons**. The icons already sourced from it
remain shipped, with their per-icon creator attribution intact in `_meta/manifest.json`, and
its priority-3 row above still describes them accurately.

It was retired because its search is fuzzy and always returns *something*, which made it
ship confidently wrong art — "Pro Tools Studio" resolved to Logic Pro (a competitor's DAW),
"Line Budgeter" to the LINE messenger, and several Avid/iZotope apps to generic folder
icons. Its CDN also returns `403`/`504` on a large fraction of stored objects. A relevance
gate was added to the acquisition script to catch the mismatches, but combined with a small
metered query budget the yield no longer justified the source. Future gaps are filled from
kbareis/icons, JamfManager-Icons, and dashboard-icons instead.

## macosicons.com usage note

The free-tier API terms state the plan "is for personal/OSS use only. Pro plans are required for production commercial software." This repo's use is Biola's own internal IT deployment tooling (not a commercial product sold to others), which is why the free tier was used — flagged here for future reference in case Biola's usage pattern changes and a paid tier becomes warranted.

## Fair use / educational rationale

Biola University is an educational institution, and the unlicensed sources above (HCSTech/icons, JamfManager-Icons) are used for the narrow purpose of app identification within internal IT deployment tooling — the same purpose and community convention under which these collections already circulate among Jamf administrators. Individual software logos/trademarks remain the property of their respective owners; inclusion here is not an endorsement and does not imply any relationship with the trademark holders.
