[README](../README.md) · [All docs](README.md)

# Keys: switching wheels and the keyboard wheel

## Switching wheels in one drag

**Arrow keys** while a wheel is open: Left and Right move a highlight round the wheel, Up and Down show the next or the previous set of a full wheel. Drop the file on the middle and it goes to the highlighted item; the mouse over a segment still wins. On macOS they are off until switched on in Settings > Wheel > Arrow keys on the wheel: reading the keys while another app is in front needs Input Monitoring (System Settings > Privacy & Security), and macOS asks for it when you switch them on, never before. Windows and Linux read them always. On Wayland they work on the shortcut's wheel, and on GNOME also during a Shift+drag: the app's GNOME Shell extension takes the arrow keys while the wheel is open and hands them to it (a log-out and back in after the update loads the new extension).

Once a wheel is open, the keys keep choosing: add Option (Alt) and it becomes the Tools wheel, press Control instead and it becomes the Actions wheel, keep only Shift and it is the formats again. With no keys held the wheel stays as it is, so they can be let go on the way to a segment. On Linux this works with X11; the Wayland shortcut opens the formats wheel only.

**Keys** in Settings > Wheel sets which keys open each wheel: Shift alone, Shift with Option (Alt on Windows and Linux), Shift with Control, or Off. Picking keys another wheel already has swaps the two over, so no two wheels share keys; a wheel that is Off simply doesn't open. The keys that switch an open wheel follow the same choice.

A wheel shows at most ten segments. When it has more to offer, it shows them a set at a time with **More** as the last segment: rest the file on More for a moment and the next set appears; stay there and it goes on round the sets, every 1.2 seconds. Move off More onto the item you want. A drop on More does nothing, like a drop in the middle.

## The wheel from the keyboard

Select files in the file manager and hand them to the wheel, no drag needed:

- **macOS**: Finder's right-click menu > **Open in Pirouette Wheel**, at the bottom of the menu below Quick Actions (with many Services installed, Finder groups them in a Services submenu; other apps show it under their menu's Services). Finder hands over the files itself, so Pirouette asks for no permission. A key for it can be set in System Settings > Keyboard > Keyboard Shortcuts > Services (Files and Folders).
- **Windows**: File Explorer's right-click > **Send to > Pirouette**: a shortcut in your own SendTo folder, made at start and switched off in Settings > General.
- **Linux**: Files' right-click > **Open With** > Pirouette (the app's own desktop entry lists the file types it takes).

The wheel opens in the middle with the keyboard: Left and Right pick a segment, Up and Down show the next or previous set, **Enter** applies the picked item, **Esc** closes, and a tap of Option (Alt) or Control switches to the Tools or Actions wheel (the one those keys open during a drag) and the same tap again goes back; **Tab** and Shift+Tab go round all three. The wheel stays switched with the key let go, so Left, Right and Enter work on it (holding Control with an arrow is the system's: on macOS it moves to another desktop). It closes by itself after a minute. On macOS the keys need no Input Monitoring here: the wheel has the keyboard itself. (Council 2026-11-10: the system hands over the selection; no global hotkey and no reading of another app's selection.)
