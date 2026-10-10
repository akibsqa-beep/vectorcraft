# VectorCraft app icons

The native apps share one icon on macOS and Linux: a regal engraved dragon in the VectorCraft palette.
Windows uses a separate, clean Bézier-path icon in pastel colors, selected for the Windows build. The
Windows artwork is a real SVG path drawing, not a scaled-up bitmap.

## Shared macOS/Linux icon

The master artwork is `vectorcraft.svg`; `vectorcraft-small.svg` is its lighter scalable version.
The macOS files add Apple's transparent margin (tile = 824/1024 of the canvas); Linux uses the tile
edge to edge. Windows no longer uses these shared assets for its executable, window, taskbar, or
brand mark.

## Windows icon

`vectorcraft-windows.svg` is the canonical Windows artwork: a smooth lavender vector path with mint
and blue anchor nodes and peach control handles on a warm cream rounded tile. It was drawn as clean
SVG geometry from the pastel Bézier-path concept selected by the user. Its 128 px and 256 px PNGs
are used by the Windows in-app brand mark, window/taskbar, and MSI wizard; the multi-size `.ico` is
embedded in the executable and used by the Start Menu shortcut and MSI product entry.

## Files

| File | What | Used by |
|---|---|---|
| `vectorcraft.svg` | shared master vector | macOS/Linux icon outputs below |
| `vectorcraft-small.svg` | lighter shared vector | Linux scalable icon |
| `vectorcraft-1024.png` | shared full tile, 1024 px | docs and store listings |
| `vectorcraft-macos-512.png` | shared tile with Apple margin, 512 px | macOS runtime Dock icon |
| `vectorcraft.icns` | shared macOS icon set, 16 to 1024 px | macOS app bundle |
| `hicolor/<size>/apps/ai.storyteller.vectorcraft.png` | shared Linux theme icons, 16 to 512 px; 256 px also used by Linux at runtime | Linux launchers and runtime window icon |
| `hicolor/scalable/apps/ai.storyteller.vectorcraft.svg` | shared Linux scalable icon | Linux launchers |
| `vectorcraft-windows.svg` | pastel Bézier-path master vector | source for Windows-specific icon outputs |
| `vectorcraft-windows-128.png` | Windows icon at 128 px | in-app brand mark and About box on Windows |
| `vectorcraft-windows-256.png` | Windows icon at 256 px | Windows runtime window/taskbar icon and MSI wizard artwork |
| `vectorcraft-windows.ico` | Windows icon, 16 to 256 px | embedded in the `.exe`, Start Menu and MSI product icon |

## How it reaches each OS

- **macOS:** the app sets the Dock / app-switcher icon at runtime; the `.app` carries `vectorcraft.icns`.
- **Windows:** `apps/vectorcraft/build.rs` embeds `vectorcraft-windows.ico`; `apps/vectorcraft/src/main.rs`
  uses the 256 px PNG for the window and taskbar; `crates/ui-egui/src/brand.rs` uses the 128 px PNG.
  The MSI gets the same artwork for its shortcut, product entry, and wizard.
- **Linux:** install `packaging/linux/ai.storyteller.vectorcraft.desktop` and `hicolor/` to the usual
  application and icon directories. The app ID is `ai.storyteller.vectorcraft` so docks match the
  launcher icon.

## Regenerate

Edit the shared `vectorcraft.svg` (and `vectorcraft-small.svg`) or the Windows-specific
`vectorcraft-windows.svg`, then run `packaging/icons.sh`. It needs `resvg`; packing Windows `.ico`
files also runs `cargo xtask ico`, and macOS `.icns` regeneration uses Apple's `iconutil`. The
outputs are committed, so ordinary app builds and packaging do not need these tools.
