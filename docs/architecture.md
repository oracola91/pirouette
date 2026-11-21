[README](../README.md) · [All docs](README.md)

# How it works

- **Trigger** (`src-tauri/src/trigger.rs`): every 30 ms it reads the drag pasteboard's change count, the mouse buttons and the Shift key. These are shared by the window server, so no permission prompt is needed.
- **Wheel window** (`src-tauri/src/wheel_window.rs`): the native parts. Glass behind the ring: Apple's Liquid Glass on macOS 26 and later, the frosted material before (both follow light/dark mode and Reduce Transparency), the dragged file's icon in the middle, placement at the cursor kept inside the screen, and the fade in and out.
- **Drop target** (`src-tauri/src/drop_view.rs`): a transparent native view on top of the wheel takes the drop. It shrinks the dragged file to a small icon, tells the page which segment to light up, and queues the conversion.
- **Formats** (`src-tauri/src/formats.rs`): what each kind of file can become, and which tools the Tools wheel offers for it.
- **Converter** (`src-tauri/src/convert.rs`): picks the tool and its settings, then places the result safely.
- **Queue** (`src-tauri/src/main.rs`): one worker converts drops in order, keeps the menu's progress line current, then posts the notification.
- **Installing converters** (`src-tauri/src/converters.rs`): remembers the converters drops found missing, offers them in the menu, and runs `brew install` or `winget install` with fixed package names, never a shell line.
- **Showing results** (`src-tauri/src/reveal.rs`): opens Finder, Explorer or the Linux file manager with the new files selected, through each system's own call rather than a command line.
- **Shelf** (`src-tauri/src/shelf.rs`, `shelf_window.rs`): the held paths and where the shelf goes (the notch, under the menu bar icon, or the corner), and on macOS a native panel above the menu bar that takes drops and starts the drag out. The trigger tells it when a file drag comes near.
- **Wheel** (`src/`): plain HTML, CSS and JavaScript in a transparent window. No frontend framework and no npm runtime packages. It opens and closes along the same path with no bounce, and follows Reduce Motion, Increase Contrast and dark mode.

## Layout

```
src/                       wheel UI (index.html, wheel.css, wheel.js)
src-tauri/                 Rust app
  src/main.rs              app setup, drop queue, notifications, --convert, --show, --update
  src/update.rs            update checks and installs
  src/log.rs               the log file
  src/trigger.rs           Shift+drag on macOS; opening, closing and dropping for all
  src/wheel.rs             wheel geometry: which segment is under a point
  src/formats.rs           formats and tools offered per file type
  src/convert.rs           the conversions
  src/menu.rs              menu bar icon and its short menu
  src/converters.rs        installing a missing converter from the menu
  src/reveal.rs            showing results selected in the file manager
  src/mac_notification.rs  macOS notifications, whose click shows the files
  src/settings.rs          saved choices (where files go, hidden formats)
  src/settings_window.rs   the Settings window (src/settings.html, .css, .js)
  src/services.rs          macOS Services entry for the keyboard wheel
  src/send_to.rs           Windows Send To entry for the keyboard wheel
  src/login.rs             Open at Login on each system
  src/drop_view.rs         macOS: the drop target over the wheel
  src/shelf.rs             the shelf: held files, where it goes
  src/shelf_window.rs      macOS: the shelf panel, drop in and drag out
  src/wheel_window.rs      macOS: glass, hub icon, placement, fades
  src/win32.rs             Windows: trigger, placement, drop target
  src/linux.rs             Linux: X11 trigger, Wayland shortcut and drags, placement, drop target
  src/gnome_shell.rs       Linux: installs the GNOME Shell extension, reads its drag reports
  gnome-shell/             the GNOME Shell extension (Shift+drag on Wayland)
  tauri.conf.json          window and bundle settings
  tauri.windows.conf.json  Windows window settings and installer types
  tauri.linux.conf.json    Linux window settings and package types
  Info.plist               marks it a menu bar app on macOS (no Dock icon)
.github/workflows/build.yml  Windows and Linux builds; a version tag publishes a release
.github/workflows/test.yml   unit tests on Linux, Windows and macOS for every pull request
scripts/install-macos.sh   build and install in /Applications on this Mac
scripts/install-linux.sh   one-command setup on Ubuntu and Debian
scripts/release-macos.sh   add the macOS .dmg to a release
scripts/macos-signing-cert.sh  make the Mac code-signing certificate, once
INSTALL.md                 installing, updating, uninstalling, making a release
SECURITY.md                how to report a security problem
docs/                      the longer guides linked from the README; images in docs/images
ROADMAP.md                 what comes next, in order
```
