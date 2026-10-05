# Field_app

An offline field data-entry app for 10×10 grid surveys, built to run on an iPad. It replaces handwriting recognition with tap-based counters, so there is no more `1` vs `I`, `2` vs `z`, or `0` vs `o`.

It mirrors the layout of the original Numbers sheet: 100 cells numbered 1–10 across the first row, 11–20 across the second, and so on. Each cell records **stems**, **galls**, and **notes**.

## Features

- **10×10 grid** of buttons so you always see where you are in the plot. Green = done, yellow = started, a dot = has notes. Each cell shows its stems/galls.
- **Big +/− counters** for stems and galls, with +5, +10, and 0 shortcuts. You can also tap the number and type it on a numeric-only keypad.
- **Notes box** that works with Apple Pencil (Scribble) or dictation.
- **Done → Next** marks a cell complete and jumps to the next one. Blank counts are saved as 0, so a real zero is recorded rather than left empty. **← Prev** goes back.
- **Sessions:** Site, Date, and Observer are set once at the top. "New session" copies the site and observer, and each session's data is kept separate. Switch or delete sessions from the **Sessions** button.
- **Autosave:** every tap is saved on the device immediately.
- **Export CSV** through the iPad share sheet (Files, AirDrop, email, etc.).
- **Works with no internet** once installed (see below).

## CSV format

One row per cell that has data:

| site | date | obs | cell | row | col | stems | galls | notes |
|------|------|-----|------|-----|-----|-------|-------|-------|

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

- Open **Grids** from the home screen, fill in Site / Date / Obs, and tap cells.
- When you're back in range, tap **Export CSV** and save it to Files or send it to yourself.

## Tips and cautions

- **Data lives only on the iPad.** Export the CSV after every session and don't treat the app as your only copy. Home screen apps are much less likely to have storage cleared than regular Safari tabs, but a backup habit is cheap insurance.
- **Updates need internet.** If you change the app, load it once on wifi (you may need to close and reopen it, or bump the cache version in `app/sw.js`) *before* the trip, not at the site.
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
