[README](../README.md) · [All docs](README.md)

# Development

## Status (macOS)

| Step | State |
|---|---|
| 1. Proof: Shift+drag shows the wheel, a drop hands over the file path | Done, tested by hand |
| 2. Converter core (ImageMagick, ffmpeg, pandoc, LibreOffice) | Done. All 49 format pairs pass from the command line; Word to PDF tested by hand |
| 3. Finished wheel: glass, motion, hub icon, haptics, screen edges | Done, tested by hand |
| 4. Menu bar app: Open at Login, where files go, which formats show | Done, tested by hand |
| 5. Testing with real files | In daily use |
| 6. Install as an app | Done: `scripts/install-macos.sh` |

**Windows** and **Linux:** built on GitHub (`.exe`, `.msi`, `.deb`, `.AppImage`), waiting on hands-on tests.

## Run it from the source

Needs Rust, Node.js and the Xcode Command Line Tools, plus the converters:

```sh
brew install ffmpeg imagemagick pandoc mupdf-tools
brew install --cask libreoffice
```

Then:

```sh
npm install --ignore-scripts
cd src-tauri
cargo build
./target/debug/pirouette
```

The app has no Dock icon. It shows an orange icon in the menu bar, and that menu has Quit.

### Without the wheel

The same converter runs from the command line. It prints the path of each new file:

```sh
./target/debug/pirouette --convert pdf "report.docx" "budget.xlsx"
```

## Test it by hand

1. Start it from Terminal as above.
2. Drag a file in Finder and hold Shift while dragging. The wheel appears under the cursor.
3. Over the wheel, the dragged file shrinks to a small icon so its name doesn't cover the wheel. Move over the segments. The one under the cursor turns orange, moves out toward the cursor, and the middle says what it will become ("To PDF"). For one file it says roughly how big it will be instead, once the app has worked that out ("2.2 MB → ~410 KB"): for pictures (a piece of the middle converted and scaled up), sound (its length at the bit rate used; MP3's rate follows the music, so that one is rougher) and video that is only copied into another container. Video that is encoded again, documents and PDFs have no estimate. On a Force Touch trackpad each new segment gives a light tick. Over the middle it says "Cancel".
4. Drop on a segment. The new file appears next to the original and a notification confirms it. Click the notification: Finder opens with the new file selected.
5. Drop in the middle. The file slides back and nothing happens. Outside the wheel the drop works as usual in macOS: it slides back, or Finder moves the file if you let go over a folder.

6. Drag a file without Shift toward the top of the screen. The shelf opens ("Drop to hold here"); drop it there. The file stays where it was, and a small sign stays at the top.
7. Open another folder on the same disk, point at the sign and drag the shelf out into that folder. The file moves there and the shelf empties. With Option held it is copied instead.

Also worth trying: several files at once, a file with no extension, text dragged from a browser (no wheel should appear), a second screen, and LibreOffice open at the same time.
