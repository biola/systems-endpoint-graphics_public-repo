# Attribution

This repository aggregates icons from multiple upstream sources, deduplicated and re-rendered to a consistent format. Each shipped icon's exact source is recorded per-slug in [`_meta/manifest.json`](_meta/manifest.json); this file documents the sources themselves.

## `software/` sources (priority order — higher priority wins when the same app appears in multiple sources)

| Priority | Source | License | Notes |
|---|---|---|---|
| 1 | [homarr-labs/dashboard-icons](https://github.com/homarr-labs/dashboard-icons) | Apache-2.0 | Filtered to software matching Installomator's supported-app list or Biola's internal Mac-lab software inventory — not pulled in full. |
| 2 | [pheralb/svgl](https://github.com/pheralb/svgl) | MIT | Pulled in full. Where svgl shipped multiple theme/style variants of the same logo (e.g. `-dark`/`-light`/`-wordmark`), only one canonical version was kept. |
| 3 | [technotica/JamfManager-Icons](https://github.com/technotica/JamfManager-Icons) | No explicit license | Pulled in full. Jamf-admin-curated collection; used here under the same fair-use rationale it's already commonly used under in the Jamf-admin community, for identification purposes as part of Biola's own software deployment tooling (educational institution). |
| 4 | [HCSTech/icons](https://github.com/HCSTech/icons) | No explicit license | Pulled in full. Same fair-use / educational-use rationale as JamfManager-Icons above — this was Biola's prior icon source before this repo existed. |

## `generic/monochrome/` source

| Source | License | Notes |
|---|---|---|
| [simple-icons/simple-icons](https://github.com/simple-icons/simple-icons) | CC0-1.0 (public domain) | Pulled in full. Single-color brand glyphs, kept in a separate folder from full-color `software/` icons since they serve a different purpose (generic identification, not a primary app icon). |

## Sources evaluated but not used

- **KevinGutowski/Big-Sur-Icons** — excluded. Explicitly marked "Copyright © Apple, research purposes only" (a more pointed restriction than the fair-use sources above), and 5+ years outdated (macOS Big Sur era).
- **elrumo/macOS_Big_Sur_icons_replacements** — excluded. Despite being the original seed project behind macosicons.com, the GitHub repo itself contains no actual app-replacement icons (only the project's own website assets); all real content lives solely on the live site.
- **macosicons.com** — excluded. Bot-protected against bulk/automated access, and its content is individually-submitted community derivative artwork (a murkier rights picture than the single-license collections above), so it wasn't used even as a partial source.
- **selfhst/icons** — deferred to a potential future Phase 2, not Phase 1. Broad self-hosted/homelab app coverage that would add thousands of icons largely unrelated to Biola's actual deployed software.

## Fair use / educational rationale

Biola University is an educational institution, and the unlicensed sources above (HCSTech/icons, JamfManager-Icons) are used for the narrow purpose of app identification within internal IT deployment tooling — the same purpose and community convention under which these collections already circulate among Jamf administrators. Individual software logos/trademarks remain the property of their respective owners; inclusion here is not an endorsement and does not imply any relationship with the trademark holders.
