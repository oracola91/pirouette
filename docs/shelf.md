[README](../README.md) · [All docs](README.md)

# The shelf

On Windows and on Linux under X11 the shelf sits at the top centre of the screen: drag files to the top edge without Shift and it opens to take them; while it holds files a pill stays there, and pointing at it opens the shelf. Drag the list out to take every held file at once, click a name to show that file, and × lets go of them all. Wayland lets no app place a window at the top of the screen, so there is no shelf there. On macOS:


Drag files toward the top of the screen and the shelf opens to take them: out of the notch on a MacBook, under the ring icon on other screens (in the top right corner when the icon can't be seen). Drop them there, go to the folder where they belong, and drag them out of the shelf again.

- Holding files only remembers where they are. Nothing is copied or moved until they are dragged out, and the drag's source is told it was a copy, so it never removes the originals.
- Dragged out, Finder does what it does with its own drags: moves them on the same disk, copies them to another one, and Option makes a copy. Files that landed somewhere leave the shelf. The shelf itself never moves or deletes anything.
- While it holds files a small sign stays: the newest file's icon and how many, beside the notch or in a pill under the ring icon. Point at it to see them, click to show them in Finder, and the × lets go of them all.
- What it holds survives a restart (`shelf.json` next to the settings, the paths only). A file that was moved, renamed or deleted in the meantime is dropped from the shelf, never guessed at.
- With Shift held the drag belongs to the wheel and the shelf steps aside.
- To keep it away, switch off **Shelf at the top of the screen** in Settings > General.

Windows (above the clock) and Linux follow.
