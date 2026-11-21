[README](../README.md) · [All docs](README.md)

# The menu and Settings

The ring icon in the menu bar opens a short menu:

- **Last: …**: how the last drop went, for when notifications are off. A click on it opens the folder with the new files selected, like a click on the notification. While a drop converts, the line shows how far it is: "Converting 3 of 10 to PNG…", with a percent for audio and video, or the time so far for a tool that doesn't report one.
- **Stop Converting**: ends the drop being converted now. Files already done stay; the one in progress leaves nothing behind. Drops queued after it still run.
- **Install ffmpeg…**: appears when a drop needed a converter that isn't installed, and the notification points to it. It runs `brew install` on macOS, `winget install` on Windows, or on Linux the system's own package manager through pkexec (the desktop asks for the admin password): `apt-get install` on Debian and Ubuntu, `dnf install` on Fedora, `pacman -S --needed` on Arch, `zypper install` on openSUSE, for that converter (several in a row: "Install ffmpeg and MuPDF…"), checks the app can now find it, and says so; then drop the files again. Without Homebrew it opens brew.sh. Without winget it first registers App Installer, which brings winget (Microsoft's own fix: a new Windows account gets it only some time after the first sign-in); if winget is still missing, the Microsoft Store opens on App Installer. On Windows, choosing it accepts the package's terms as typing the command would, and packages that install for all users, such as LibreOffice, still ask for admin rights. The package manager's last lines go to the log. Fedora's and openSUSE's own ffmpeg has no H.264 encoder (MP4, MOV and MKV out need it; RPM Fusion or Packman have the full one). Other Linux systems get the notification that names the command; the setup script (Debian and Ubuntu) installs everything at once.
- **Settings…** (Cmd+, on macOS): the Settings window, below.
- **Check for Updates… / Install Update … and Restart**.
- **Quit Pirouette**.

Stop Converting shows only while a drop converts, and Install only while a drop found a converter missing.

The **Settings window** holds everything else, in four tabs, the same on every system. Each change is saved at once; Esc closes the window.

**General**

- **Open at login**: adds or removes Pirouette in System Settings > General > Login Items. Only works for the installed app.
- **Save converted files**: next to the original (default) or in Downloads. When the original's folder can't be written to, the file goes to Downloads either way and the notification says so.
- **Shelf at the top of the screen**: on unless switched off (not on Wayland).
- **Terminal**: what Terminal on the Actions wheel opens. The list shows the terminals found on this computer: on macOS Terminal, iTerm2, Warp, Ghostty, kitty, Alacritty and WezTerm; on Windows Windows PowerShell, PowerShell 7, Windows Terminal, Command Prompt and Git Bash; on Linux GNOME Terminal, Console, Ptyxis, Konsole, Xfce Terminal, MATE Terminal, Tilix, Terminator, kitty, Alacritty, WezTerm, Ghostty and foot. The folder always goes in as its own argument, never inside a command.
- **Hide the menu bar icon** (the icon in the notification area on Windows, the tray icon on Linux): Pirouette keeps running without it. Opening Pirouette again (Spotlight, Launchpad or Applications; the Start menu; the app list) shows Settings, where it can be switched back on.
- **Hold to convert** (not on Wayland): press a file, hold it still for half a second, then drag, and the Formats wheel opens without a key. Made for touch screens, where no key can be held during a drag. Off unless switched on; a quick drag still just moves the file.
- **Install Missing Converters…** (where Install works): installs every converter the app can't find in one run of the same Install (one-step setup); the line above it names them. LibreOffice is a large download.
- **Update Converters…** (where Install works): a button that asks the same package manager for a newer version of every converter the app finds: `brew upgrade`, `winget upgrade`, or on Linux one run for all of them (one password): `apt-get install --only-upgrade`, `dnf upgrade` or `zypper update`, from the package lists the system refreshed last. Arch updates as a whole (`sudo pacman -Syu`), so there the notification says that instead of upgrading single packages. A converter the package manager didn't install, such as a LibreOffice downloaded from its website, is left alone, and so is the bsdtar built into macOS and Windows. The notification says which ones were updated, which were already up to date, and which were left alone. One package manager job runs at a time, so Install waits for it.

**Wheel**

- **Keys**: which keys open each wheel (see [*Switching wheels in one drag*](wheel-keys.md#switching-wheels-in-one-drag)), and on macOS the **Arrow keys on the wheel** switch.
- **Highlight colour**: what colour the segment under the cursor lights up in: Orange (the default), Red, Pink, Purple, Blue, Teal, Green or Graphite. The next wheel opens in it.
- **Liquid Glass** (macOS) or **See-through** (Windows, Linux), on by default; off gives a plain solid wheel. The **Transparency** slider sets how see-through it is. On macOS it goes from frosted (left: the frosted material behind it and more white on the segments, easiest to read) to clear (right: no blur; the glass stays frosted only right behind each word, so the words still read). Windows and Linux blur nothing behind a round window, so there the disc is see-through without frosting, and never less than half opaque. Saved when the knob is let go; the next wheel opens with it.
- **Wheel size**: the most segments a wheel shows at once: 8, 10 (the default) or 12. A wheel with more shows them a set at a time, with More last: rest on More (or press Up or Down) for the next set. On a wheel of more than ten every word takes the one size the tightest needs, on two lines where one doesn't fit, so none runs into the next.
- **Scale**: how big the wheel is drawn, a slider from Normal (the default) up to half as big again (150%), in steps of 5%. The whole wheel grows, words and the file's picture in the middle included, so the words get bigger at every wheel size, also at 12. It takes effect at the next wheel.
- **Formats on the wheel**: switch formats on or off per kind of file. Formats switched off stay off the wheel. **Other pictures** (PSD, TGA, JPEG XL and the rest the wheel reads but doesn't write) is a row of its own: those pictures have no format of their own to leave out, so all eleven picture formats would be one more than a wheel of ten shows, and BMP starts off there. Switch it on for a second set (with More), or switch another off and BMP on to swap them.

**Quality**: Smaller Files, Balanced (the default, what the app always did) or Best Quality, for Pictures, Video and Audio separately. It holds for a whole drop, from when it starts.

| | Smaller Files | Balanced | Best Quality |
|---|---|---|---|
| JPEG, WebP | 75 | 90 | 97 |
| HEIC, AVIF | 40 | ImageMagick's own (50) | 85 |
| H.264 (MP4, MOV, MKV) | CRF 26 | CRF 20 | CRF 17 |
| VP9 (WebM) | CRF 38 | CRF 32 | CRF 26 |
| AVI, WMV | quantiser 5 | 3 | 2 |
| MP3 (VBR) | about 130 kbit/s | 190 | 245 |
| AAC (M4A) | 160 kbit/s | 256 | 320 |
| Opus, OGG | 96 kbit/s | 160 | 256 |
| WMA | 128 kbit/s | 192 | 256 |


Lossless formats (PNG, TIFF, WAV, FLAC, AIFF) and documents have no quality to choose. The Tools wheel's Compress keeps its own, lower settings.

**About**: the version, and **Show Log**, which opens the folder with the log file.

Settings are kept in `~/Library/Application Support/io.github.oracola91.pirouette/settings.json` (Windows: `%APPDATA%\io.github.oracola91.pirouette`, Linux: `~/.config/io.github.oracola91.pirouette`). A settings file that can't be used is kept aside as `settings.json.bad` (or, if it can't be read at all, left alone and never saved over), and a notification says the settings were reset.

**Show Log** opens the folder with the log of starts, conversions, errors and update checks: `~/Library/Logs/io.github.oracola91.pirouette/pirouette.log` (Windows: `%LOCALAPPDATA%\io.github.oracola91.pirouette\logs`, Linux: `~/.local/share/io.github.oracola91.pirouette/logs`). It holds file names, not folders (tool messages are stripped of paths), is readable by the user only, and keeps at most about 1 MB.

**Quit** while conversions are running asks for a second Quit within 10 seconds, then stops them.

Only one copy runs at a time: starting the app again just says it is already running. On macOS this uses a fixed lock name in `/tmp` (from the single-instance plugin); on a Mac shared by several user accounts, another account could block it. That doesn't matter on a one-person laptop.
