# systems-endpoint-graphics_public-repo

Biola University IT Systems Engineering's collection of icons and graphics for software deployed to endpoints (primarily via Jamf / Installomator / Baseline). The goal: never have to search for or manually upload an icon again — reference a stable URL from this repo instead.

## Using an icon

Every icon is served as a raw file straight from GitHub:

```
https://raw.githubusercontent.com/biola/systems-endpoint-graphics_public-repo/main/software/<slug>.png
```

For example, Slack's icon: `https://raw.githubusercontent.com/biola/systems-endpoint-graphics_public-repo/main/software/slack.png`

All `software/*.png` files are 512x512 PNGs with the icon content normalized to fill ~90% of the canvas (a consistent margin regardless of source), so icons from different sources look consistent side-by-side — this matters because tools like [Baseline](https://github.com/SecondSonConsulting/Baseline) (built on [swiftDialog](https://github.com/swiftDialog/swiftDialog)) display supplied PNGs as-is with no automatic padding of their own.

## Folder structure

```
software/
├── <slug>.png             # primary asset — 512x512, ~90% content fill, transparent padding
├── svg/<slug>.svg         # vector original, only when the winning source provided one
└── variants/<slug>/       # kbareis-sourced apps only: every captured mode (Tahoe light/
                            # dark/clear/tinted + legacy), even the ones not picked as primary

software-old/               # the pre-2026-07-17-revamp software/ build, kept for rollback

generic/
└── monochrome/
    ├── <slug>.svg           # single-color brand glyph (simple-icons), transparent background
    └── on-light/<slug>.png  # same glyph pre-composited on white — safe on any background,
                              # since transparent black-on-transparent glyphs vanish on dark UIs

_meta/
├── manifest.json       # slug -> source/license/original-filename (+ per-icon creator credit
│                        # for macosicons.com-sourced icons) for every shipped icon
├── manifest-old.json   # manifest.json as it was before the 2026-07-17 revamp
├── DEDUP_LOG.md         # what got dropped as a duplicate and why, per pipeline run
└── RENDER_FAILURES.md   # any source files that failed to render (malformed SVGs, etc.)
```

## Naming

Slugs are lowercase-kebab-case, normalized from the original app/product name (versions/years stripped — e.g. "Adobe Photoshop 2024" and "Adobe Photoshop 2025" both resolve to `adobe-photoshop`, since none of our sources track a distinct icon per release year).

## Sources & licensing

See [ATTRIBUTION.md](ATTRIBUTION.md) for the full per-source license breakdown. Icons are pulled from multiple upstream collections, deduplicated, and standardized — see [LICENSE.md](LICENSE.md) for how licensing works across a mixed-source repo like this one.

## Adding new icons

This repo is built and maintained via a scripted pipeline (acquire → dedupe → standardize → commit), not by hand-uploading individual files. If an icon you need is missing, check `_meta/manifest.json` for known gaps, or reach out to IT Systems Engineering to have it added in the next pipeline run.

## Phasing

**Phase 1** (superseded 2026-07-17): curated small sources pulled in full, plus `dashboard-icons` filtered to software Biola actually deploys (Installomator's supported-app list + an internal Mac-lab software inventory). `simple-icons` is included in full for generic monochrome glyphs. The `software/` build from this phase is preserved at `software-old/`.

**Phase 2 — squirqle/Tahoe revamp** (current, 2026-07-17): re-prioritized `software/` around the "squirqle" macOS app-icon shape and official Tahoe icon renders, in priority order: [kbareis/icons](https://github.com/kbareis/icons) (private, personally authorized) → JamfManager-Icons → macosicons.com (API, budget-capped gap-fill for Biola's relevant software) → dashboard-icons → svgl → HCSTech-icons (last-resort fallbacks). `simple-icons` generic monochrome glyphs are untouched by this revamp.

**Phase 3** (not yet built): broader `dashboard-icons` coverage and `selfhst/icons` (self-hosted/homelab app icons), added only if real gaps show up in day-to-day use — deferred initially to avoid shipping thousands of icons for software Biola doesn't deploy.
