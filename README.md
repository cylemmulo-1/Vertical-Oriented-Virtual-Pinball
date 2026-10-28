<img width="1426" height="2560" alt="Screenshot (413)" src="https://github.com/user-attachments/assets/05a5ec73-44a9-49a7-899b-52b2c9bc88da" />
# VPinball Vertical
Disclaimer: This was made modstly with the help of AI, so I don't take too much credit for it. It was a decent amount of work to get right and help with but I don't want to take too much credit for this.

NOTE : This version will rotate the interface for someone using cabinet mode where you need the display in landscape even though it's in portrait. 

A portrait-oriented frontend for Visual Pinball X, designed for virtual pinball cabinets where the playfield monitor is physically rotated 90°.

---

## How the Display Works

Your playfield monitor is mounted portrait (tall), but Windows still sees it as a landscape display. The app opens a full-size landscape window and CSS-rotates the entire UI 90° so it appears upright on the physical screen.

For a 2560×1440 monitor rotated 90°, set Window Width = 2560, Window Height = 1440 in Settings.

---

## Installation

```bash
npm install
npm start
```

To build a Windows installer:
```bash
npm run build
```

---

## First-Time Setup

1. Open **⚙ Settings**
2. Set your **VPinballX64.exe** path (e.g. `C:\VPinball\VPinballX64.exe`)
3. Set your **Tables Folder** — used for the Scan feature
4. Set your **Wheel Images Folder** — images are auto-matched to table names
5. Set your **PINemHi Folder** — the folder containing `pinemhi.ini` (e.g. `C:\PINemHi`)
6. Set **Window Width / Height** to your monitor's landscape resolution
7. Click **Identify** next to the Display dropdown to flash each screen and confirm the right one
8. Save — the window repositions immediately

---

## Adding Tables

**Scan Folder** (recommended) — Click **📁 Scan** in the header. The app recursively scans your Tables Folder for `.vpx` files not already in your library, shows you a checklist, and imports the ones you select. Running Scan again will also detect any tables whose files have been deleted and offer to remove them.

**Add manually** — Click **＋** and fill in the table details. Use **🔍 VPS Lookup** to auto-fill manufacturer, year, and type from the Virtual Pinball Spreadsheet database.

**VPS All** — Click **🔍 VPS All** to bulk-fill manufacturer/year/type for all tables that are missing that info.

---

## Navigation (Keyboard / Cabinet Controls)

| Key | Action |
|-----|--------|
| **Left Shift** | Previous table |
| **Right Shift** | Next table |
| **Z** | Previous page |
| **/** | Next page |
| **1** | Cycle category right |
| **5** | Cycle category left |
| **Enter** | Launch selected table |
| **Ctrl+F** | Focus search bar |
| **Ctrl+A** | Select all on current page |
| **Ctrl+N** | Add new table |
| **Escape** | Close modal / quit |
| **F12** | Toggle DevTools |

Holding Shift auto-scrolls and accelerates. When you reach the last item on a page it automatically advances to the next page.

---

## Right-Click Menu

Right-click any table row to open the context menu:

- **Single table selected** — Play, Edit, Favorite, Select All (current page), Delete
- **Multiple tables selected** — shows count, category dropdown to move them all, Delete

To select multiple tables: **Ctrl+click** individual rows, or right-click → **Select All** to select the whole current page, then right-click → **Move to Category**.

---

##  Image Matching

Wheel images are auto-matched from your Wheel Images Folder by comparing filenames to table names. The matcher:

- Strips parenthetical suffixes like `(Williams 1997)` and `0_0` from both sides before comparing
- Uses word-overlap scoring with precision weighting — a short wheel filename won't accidentally match a longer table name
- If a table isn't matching correctly, open **Edit** and set the **Wheel Image** path manually

---

## PINemHi High Scores

Set your PINemHi folder in Settings. The app reads `pinemhi.ini` to match table names to ROM names, then reads score files from `PINemHi LeaderBoard\TOP10_Personal\`.

If a table isn't matching automatically:
1. Open **Edit** on the table
2. Set the **ROM Name Override** field (e.g. `eatpm_l4`)

Click **🔧 Debug** in the detail pane to see exactly what the app finds for any table.

---

## Categories

Manage categories in Settings (one per line). Assign tables to categories via:
- **Edit** modal — check/uncheck categories individually
- **Right-click → Move to Category** — bulk-assign multiple selected tables
- **1 / 5 keys** — cycle through categories while navigating

---

## Data Storage

All library data is saved to:
`%APPDATA%\vpinball-vertical\vpinball-vertical.json`

VPX files are never moved or modified.

---

## Troubleshooting

**Tables not showing** — Check that your Tables Folder is set in Settings and run Scan.

**Wheel images not loading** — Verify the Wheel Images Folder path. Check that image filenames loosely match table names.

**High scores not showing** — Confirm the PINemHi folder contains `pinemhi.ini` and a `PINemHi LeaderBoard\TOP10_Personal\` subfolder. Use the 🔧 Debug button.

**Focus not returning after game** — The app uses a PowerShell script (`focuser.ps1`) to reclaim focus when VPX exits. If it's not working, ensure PowerShell execution policy allows scripts.

**Window on wrong display** — Use the **Identify** button in Settings to flash each display and select the correct one.
