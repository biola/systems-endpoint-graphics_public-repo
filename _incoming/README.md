# `_incoming/` — upload icon source art here

Drop an image in this folder to get it published as an icon. You can do it entirely from a
browser: **Add file → Upload files** on this folder in GitHub. No tooling, no local checkout.

The pipeline picks up anything here on its next run, and for each file it:

1. renders it to `software/<slug>.png` — 512×512, content normalized to ~90% fill, so it
   matches every other icon in Baseline/swiftDialog regardless of what size you supplied;
2. records where it came from in [`_meta/manifest.json`](../_meta/manifest.json);
3. moves the original into the pipeline's own `local-icons/` store, where it takes
   **priority over every upstream collection** — a human who went and found the right art
   for a named deployment beats any bulk source, permanently;
4. removes the file from this folder, so what's left here is only what still needs attention.

## Name the file as the slug you want published

**The filename becomes the URL**, so it has to be the exact slug — lowercase, kebab-case,
no spaces:

```
toon-boom-harmony.png   ->  .../software/toon-boom-harmony.png
inkscape.jpg            ->  .../software/inkscape.png
```

Anything else is **left in place and reported** rather than guessed at. `Harmony icon.jpg`
would otherwise publish as `harmony-icon`, and a published
`raw.githubusercontent.com` URL is the one thing this repo exists to keep stable — so a
wrong guess is worse than a rejected upload. Rename it and it'll be picked up next run.

If you're replacing a bad icon, use the slug that's already shipping and it will be
overwritten (and will stay overwritten — hand-supplied art outranks the source it replaces).

## Accepted formats

`.png` · `.svg` · `.jpg` / `.jpeg` · `.webp` · `.avif` · `.icns`

Whatever the vendor published is fine — it gets converted on the way in. Two notes:

- **Any size works**, square or not. The renderer trims to the artwork's bounds and scales
  preserving aspect ratio, so a 240×180 or an 1024×1024 both land correctly framed. Bigger is
  better than smaller, since upscaling can't add detail.
- **Transparency is kept if it's there, and not invented if it isn't.** A JPEG has no alpha
  channel, so its background (usually white) ships as part of the icon. That's deliberate —
  backgrounds aren't keyed out automatically, because doing so puts holes in logos that use
  white inside the mark. If you want a transparent background, supply a PNG/SVG that already
  has one, or ask IT Systems Engineering.

A great source for macOS app art is the installed app itself, which carries the official
icon at full resolution:

```bash
APP=/Applications/Inkscape.app
ICNS=$(plutil -extract CFBundleIconFile raw "$APP/Contents/Info.plist")
cp "$APP/Contents/Resources/${ICNS%.icns}.icns" ~/Desktop/inkscape.icns
```

## Notes

- This folder is **public**, like the rest of the repo. Don't upload anything you wouldn't
  publish.
- Files here are *not* the shipped icons — `software/` is. Nothing here is served to Jamf.
- Uploading straight into `software/` also works and is no longer dangerous (the pipeline
  detects and adopts it), but it skips normalization until the next run, so the icon renders
  at a different size than its neighbours in the meantime. This folder is the tidier path.
