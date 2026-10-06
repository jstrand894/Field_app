# Field_app

An offline field data-entry app for 10×10 grid surveys, built to run on an iPad. It replaces handwriting recognition with tap-based counters, so there is no more `1` vs `I`, `2` vs `z`, or `0` vs `o`.

It mirrors the layout of the original Numbers sheet: 100 cells numbered 1–10 across the first row, 11–20 across the second, and so on. Each cell records **stems** (counted separately by two observers, added up for you), **galls**, **chomps**, **% mature**, **average height**, and **notes**.

## Features

- **10×10 grid** of buttons so you always see where you are in the plot. Green = done, yellow = started, a dot = has notes. Each cell shows its stems/galls.
- **Centered entry panel** with big +/− counters for **Stems (Observer 1)**, **Stems (Observer 2)**, **Galls**, and **Chomps** (number of stems eaten), with +5, +10, and 0 shortcuts. The stems total is added automatically.
- **% Mature** (0–100, −/+ moves by 10, with −5/+5/100 shortcuts). **% Immature** (100 minus mature) is worked out for you in the CSV.
- **Avg height** takes decimals like `14.5` or `22.9` (−/+ moves by 1, with ±0.1 fine-tune buttons). Write the decimal point with the Pencil, and a comma is read as a point.
- **Apple Pencil input:** write numbers directly in the count boxes. Look-alike letters are fixed (`I`→1, `o`→0, `z`→2, ...) and you can write sums like `3+4`, which are added when you lift off.
- **Zigzag walking order:** cells are visited 1→10, then 20→11, then 21→30, and so on. The **← / →** arrows at the top of the cell screen show the previous and next cell number in that order, and **Done ✓ →** follows the same path.
- **Undo and clear:** every box header has a clear icon (right) to clear just that variable and an undo icon (left) to undo the last change to just that variable, the main **Undo** steps back through your changes in that cell (taps, writing, clears, Done), and **Clear cell** wipes the whole cell (also undoable).
- **Sanity check:** a red warning shows (and a **!** appears on that cell in the grid) if chomps are more than total stems. It never blocks you.
- **Hidden backup copy:** every save is also copied to a second storage area on the iPad (plus a snapshot every 10 minutes, keeping the latest 12). If the main data is ever missing when the app opens, it is restored automatically. **Sessions → Restore from backup copy** lets you roll back to any snapshot, and your current data is backed up first.
- **Import a CSV:** **Sessions → Import a CSV** loads a file previously exported by this app as a new session (cells come in marked done). Useful for moving data between iPads or recovering from a file.
- **Keeps the screen on:** the app asks the iPad not to auto-lock while it is open. iPadOS usually refuses this in **Low Power Mode**, so the iPad's own lock timer applies there. **Sessions** shows whether stay-awake is on.
- **Cell to cell uses the same two-card slide as the transect:** the arrows, **Done ✓** and **No toadflax** all slide the whole card away while the next cell's card slides in at the same speed (left/right arrows go the matching direction; Done and No toadflax always move forward). **Done ✓** also pops a green check with confetti and **No toadflax** a gold "0", so you can tell which you pressed. (Off when the iPad's Reduce Motion is on.)
- **Notes and Sketch pads:** two blank white pads sit on either side of the grid in landscape (below the grid in portrait), and under the timeline on the Transect screen, for writing notes and drawing pictures with the Pencil, a finger, or a mouse. Each has five pen colors, an eraser (wipe over a stroke to remove it), undo (last stroke) and clear. They save with the session (separate for every grid and transect session) and come back after closing the app. Each stroke is saved in the background as its own tiny record in a separate on-device database (not in the main saved data), which keeps drawing fast no matter how much you have drawn. Because of that they are not in the hidden backup copy, not in the CSV, and **Reset grid / Reset transect** leaves them alone.
- **Pad speed check (for troubleshooting):** tap a pad's title ("Notes" or "Sketch") five times quickly to show how the last stroke was received (number of moves, time, longest gap between moves, cancelled and ignored touches). Tap five times again to hide it. While you draw with the Pencil, a finger or palm resting on the pad is ignored.
- **Whole grid on screen:** in landscape the Grid sheet keeps square cells and sizes them to the screen height, centered, so all 100 are visible at once without scrolling (portrait is unchanged).
- **Frame screen fits any iPad:** on shorter screens (iPad mini, 10.2" or 9.7" in landscape) the transect frame form shrinks step by step until everything fits, and the **Undo / Clear frame / Done** buttons are pinned to the bottom so they are always reachable.
- **Nothing stretches or refreshes:** the page itself is locked, so swiping up or down on the full grid does not stretch the numbers and there is no pull-to-refresh. A screen only scrolls (on its own) when it is genuinely taller than the display, such as the grid in portrait on a small iPad.
- **Page stays put:** while an entry screen is open, the page behind it is locked and the cell grid is updated in place, so it no longer jumps or scrolls.
- **Reset grid:** the red **Reset grid** button in the top bar (also under Sessions) erases every cell in the current session (site, date, observers are kept). It asks twice, and a backup copy is saved first (restore it from Sessions → Restore from backup copy).
- **Export prompt:** finishing the last cell in the walk offers to export a CSV right away.
- **Keyboard only where you want it:** the number boxes, notes and weed names never show the iPad keyboard (write with the Pencil or use the buttons). The only exceptions are the **Site** and **Observer** boxes: tap them with a finger and the keyboard appears (with a cursor); tap them with the Pencil and it stays hidden so you can handwrite.
- **Sun-readable:** high-contrast colors, heavier borders and bolder text. Each tap also gives a quick visual pop on the box.
- **Notes box** for Apple Pencil (Scribble).
- **Done → Next** marks a cell complete and jumps to the next one. Blank stems, galls, and chomps are saved as 0, so a real zero is recorded rather than left empty. % mature and height stay blank unless you enter them. **← Prev** goes back.
- **Compact site / date / observer bar:** on both the Grid and Transect screens, Site, Date and Observers are shown as one slim bar in the top row, which leaves more room for the grid. Tap it and a panel drops down from the top with large input boxes over a darkened, blurred screen; tap **Done**, the dark area, or press Esc to close it (it slides back up). The bar updates as you type.
- **Sessions:** Site, Date, Observer 1, and Observer 2 are set once (the names label the stems counters). "New session" copies the site and observers, and each session's data is kept separate. Switch or delete sessions from the **Sessions** button.
- **Autosave:** every tap is saved on the device immediately.
- **Export CSV** through the iPad share sheet (Files, AirDrop, email, etc.).
- **Works with no internet** once installed (see below).

## Main menu and the Transect (SIMP) sheet

The app opens on a **main menu** titled *Toadflax Field Data Collection*. Each sampling method has a clean card with an icon, a small diagram (the 10×10 grid with its zigzag walking path, and a top-down picture of the 20 m transect: a measuring tape on a reel with a numbered quadrat frame every 2 m, laid across the ground), chips for what you record, a one-line how-to, and a progress bar showing how far along your current session is. The two data sheets: **Grid** (everything above) and **Transect**, a digital version of the SIMP 2026 form. Use **‹ Menu** at the top left of either sheet to switch. Each sheet has its own sessions and its own CSV export.

**Distance ruler:** each transect is 20 m long and the frames are every 2 m starting at 2 m, so frame 1 = 2 m, frame 2 = 4 m, ... frame 10 = 20 m. A tape-measure style ruler (rounded segments with tick marks that fill green as frames are finished) sits above the numbered bubbles, both on the transect screen and inside each frame (the current frame is highlighted and its distance is shown next to the frame title), so you always know where you are on the line. The CSV has a `distance_m` column.

**Reset transect:** the red **Reset transect** button in the top bar of the transect screen (also under Sessions) erases every frame in the current transect, asks twice, and saves a backup copy first.

**New transect:** a **＋ New transect** button at the top of the transect screen (next to Sessions) starts a fresh one, and finishing frame 10 offers to export a backup and then asks whether to start a new transect. The finished transect stays saved under Sessions.

**Motion:** moving to the next or previous frame slides the whole card (border, header, ruler, boxes and buttons) off to one side while the next card slides in from the other side, at exactly the same speed and distance, like two cards on a table. Swipe left for the next frame, right for the previous one. On the transect screen the line behaves like a carousel: the bubble in the middle grows while the ones at the edges shrink and fade (frame 1 is the biggest at the start of the line and frame 10 at the end), the frames pop in one after another when you open it, returning from a frame glides back to the next-up frame, and the next-up bubble gently pulses. Turn on iPad *Reduce Motion* and the animations switch off.

**Timeline:** the transect screen shows the 10 frames as a horizontal line you swipe along (green = done, yellow = started, gold ring = next up), with a **Continue: frame N** button that jumps to the next unfinished frame. Inside a frame, a row of 10 dots shows where you are on the line (tap one to jump), and you can **swipe left or right with a finger** to move to the next or previous frame. Pencil strokes never trigger a swipe, so writing numbers is safe.

The paper form puts the 10 frames in two separate tables, so you scroll between cover and heights. Here **each frame has all of its information on one screen**, and you finish it before moving to the next:

- **Cover (%)** for Target, Other, Forb, Shrub, Grass, Ground, Litter, and Moss (−/+ moves by 5). **Target** is the gold box with a star so it stands out, and it has **5** and **10** shortcut buttons (it never needs Rest). **Total** and **Damage** sit in the top bar so the cover boxes have the room.
- **Total** adds up automatically and turns green at 100, amber otherwise (it never blocks you).
- **Rest button:** every cover box has a **Rest** button that fills that box with whatever is left to reach 100 (100 minus all the other cover boxes), so you can enter 5 target, 10 forb, 25 grass, then tap Rest on litter.
- **Other weeds:** the Other category is a list. Write the weed's name in the white box at the top of each weed's card (Pencil) and its percent below. Tap **＋ Add another other weed** (up to 5) for more; the ✕ on a box removes it. New frames start with the weed names from the previous frame (values blank), since the same weeds usually repeat. Any weed you have named earlier in the same transect but that is not in the current frame shows as a **Seen:** chip next to the Cover heading; tap it to fill an empty weed box (or add a new one) without writing the name again.
- **Damage** is a 1 / 2 / 3 / 4 button set in the top bar. Tap a number to choose it, tap it again to clear it.
- **Undo** is at the top of the frame screen (and the grid cell screen) as well as at the bottom.
- **Counts and heights** as a Mature / Immature table: Count, Tall, Short, and Avg. The number boxes are tall for Pencil writing. The three height boxes per row have no −/+ buttons (heights are decimals like 14.5, so you just write them); the Count boxes keep −/+.
- **← / →** move between frames, **Done ✓ → frame N** saves and advances, and **Undo** and **Clear frame** work like in the grid.
- Site, Date, and the two observers are set once at the top; a new transect copies them from the last one. The hidden backup copy covers transect data too.

Transect CSV columns: `site, date, obs1, obs2, frame, distance_m, target, other_total, other1_name, other1_pct, (other2_name, other2_pct, ... as many as used), forb, shrub, grass, ground, litter, moss, total, damage, mature_count, immature_count, mature_tall, mature_short, mature_avg, immature_tall, immature_short, immature_avg`.

## CSV format (Grid)

One row per cell that has data:

| site | date | obs1 | obs2 | cell | row | col | stems_obs1 | stems_obs2 | stems_total | galls | chomps | pct_mature | pct_immature | avg_height | notes |
|------|------|------|------|------|-----|-----|-----------|-----------|-------------|-------|--------|-----------|-------------|-----------|-------|

`row` and `col` (1–10) are derived from the cell number, so the file reads straight into R or Excel with no reshaping.

```r
d <- read.csv("grid_SiteName_2026-10-05.csv")
```

## Getting it on your iPad

The app is a set of static files in [`app/`](app/). It must be hosted once over https so Safari can install it; after that it runs entirely from the iPad.

### 1. Host it with GitHub Pages (one time)

GitHub Pages can only publish from the repo root or a `/docs` folder, so publish from the root and the app will live at `/app/`.

1. Push this repo to GitHub.
2. On GitHub, open the repo, then **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose the `main` branch and the `/ (root)` folder, then **Save**.
4. After a minute or two the app is live at:

   `https://jstrand894.github.io/Field_app/app/`

### 2. Install on the iPad (on wifi)

1. Open the URL above in **Safari** (it must be Safari for Add to Home Screen to install it as an app).
2. Tap the **Share** button, then **Add to Home Screen**, then **Add**.
3. Open the app from the home screen icon **once while still on wifi** so it caches its files.
4. Turn on **Airplane Mode** and launch it again to confirm it works with no connection.

### 3. In the field

- Open **Grids** from the home screen, fill in Site / Date / Observer 1 / Observer 2, and tap cells.
- When you're back in range, tap **Export CSV** and save it to Files or send it to yourself.

## Tips and cautions

- **Data lives only on the iPad.** Export the CSV after every session and don't treat the app as your only copy. Home screen apps are much less likely to have storage cleared than regular Safari tabs, but a backup habit is cheap insurance.
- **Updates need internet.** The app checks for a new version whenever it opens online. After pushing a change, open it once on wifi (and reopen it if needed) *before* the trip, not at the site.
- Delete a session only after exporting it.

## Files

| File | Purpose |
|------|---------|
| `app/index.html` | The whole app (HTML, CSS, JavaScript) |
| `app/sw.js` | Service worker that caches the app for offline use |
| `app/manifest.webmanifest` | Makes it installable with a name and icon |
| `app/icon-180.png`, `app/icon-512.png` | Home screen icons |

## Running locally

```bash
cd app
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

## Version

The current version is shown at the bottom of the app screen. To change it, edit `VERSION` near the top of the script in `app/index.html`.

Created by Jackson R Strand. © 2026 Jackson R Strand.
