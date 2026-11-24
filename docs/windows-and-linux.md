[README](../README.md) · [All docs](README.md)

# On Windows and Linux

Install steps are in [INSTALL.md](../INSTALL.md). What works differently from macOS:

**Windows** (`src-tauri/src/win32.rs`)

- **Trigger:** Windows has no shared drag pasteboard to watch, so the wheel opens when a drag that started in File Explorer, on the desktop or in an Open/Save dialog has Shift held. Which files are dragged becomes known when the drag reaches the wheel; until then it says "Drop here".
- **Drop target:** our own, on the wheel window and the windows WebView2 creates inside it. It always reports "copy" (or "refuse" in the middle). Tauri's built-in drop handler leaves the result unset, so Windows hands File Explorer the source's own allowed effects back, which can include "move" and so delete the original. That is why it is not used here.
- **Look:** no system glass, so the page draws a solid disc with a shadow. No file icon in the middle.
- **Open at Login:** a value under the user's Run key in the registry.
- **No console windows:** the converters run without flashing a console.

**Linux** (`src-tauri/src/linux.rs`)

- **X11:** like Windows. A drag that starts in a file manager (Files/Nautilus, Nemo, Caja, Thunar, Dolphin, PCManFM) or on the desktop, with Shift held, opens the wheel at the cursor.
- **Wayland:** apps can't watch the pointer, so the wheel opens from a keyboard shortcut running `pirouette --show`, which reaches the running app over a socket in `XDG_RUNTIME_DIR`. That wheel waits for a file; Esc, a click in the middle or 20 seconds close it.
- **Wayland on GNOME:** GNOME Shell can see drags, so the app installs a small GNOME Shell extension of its own (`src-tauri/gnome-shell/`, `src-tauri/src/gnome_shell.rs`) into `~/.local/share/gnome-shell/extensions` and turns it on the first time. While a drag goes on, the extension sends the app which app the drag started in and the keys held, over the same socket every 30 ms, and moves the wheel the app opens under the pointer (a Wayland app can't place its own windows). The app opens and switches the wheel from that as it does on X11. GNOME Shell loads a new or updated extension at the next login; the app says so once.
- **Drop target:** our own GTK handlers instead of WebKit's. They answer "copy" over a format and nothing elsewhere, never "move" even with Shift held, and never ask the file manager to delete the original.
- **Menu bar icon:** shown through AppIndicator.
- **Open at Login:** an entry in `~/.config/autostart`.
- **Converter:** falls back to ImageMagick 6's `convert` and the `libreoffice` command, checks pandoc is 2.15 or newer, and Aptos stands in as Noto Sans.
