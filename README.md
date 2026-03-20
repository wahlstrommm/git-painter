# Git Painter

Turn any image into your GitHub contribution graph.

Upload a photo, adjust how it looks on the grid, preview the resulting coverage, and download a bash script that creates backdated git commits to paint the image on your GitHub profile.

## How it works

1. Open `index.html` in your browser
2. Pick a mode:
   - **Image** — drop a photo, logo, or pixel art
   - **Text** — type short bitmap-style text directly in the app
   - **Preset** — choose a ready-made icon like heart, moon, cat, arrow, rocket, tree, or coffee
   - **Draw** — stamp presets and paint the grid by hand with contribution levels 0-4
3. Use the controls to adjust how it maps to the 52×7 contribution grid:
   - **Zoom** — scale the image up/down within the grid
   - **Position X/Y** — move it around
   - **Threshold** — control how aggressively light/dark maps to commit levels
   - **Invert** — flip light and dark
   - **Text Style** — choose between `Pixel`, `Bold`, and `Slanted`
   - **Text Scale / Letter spacing** — tune text layout for the narrow grid
4. Pick a target year and enter your repo URL
5. Review the preview stats:
   - **Total commits** — estimated number of commits the script will create
   - **Active days** — days with one or more commits
   - **Coverage** — percentage of dated cells used in the year
6. Click **Download git-painter.sh**
7. Run the script — it creates a repo with backdated commits that paint your image

## Prerequisites

- An **empty** GitHub repo (no README, no .gitignore)
- The repo must **not** be a fork
- `main` must be the default branch
- `git` 2.28+ and `bash`
- `git config user.name` and `git config user.email` must be set before running the generated script

## Usage

```bash
chmod +x git-painter.sh
./git-painter.sh
```

The script creates a local repo (`git-painter-art/`), makes all the commits, and pushes to your repo. If you enable overwrite in the UI, the generated script defaults to `FORCE_PUSH=true` and asks for confirmation before replacing remote history.

Accepted repo URL formats:

- `https://github.com/user/repo.git`
- `https://github.com/user/repo`
- `git@github.com:user/repo.git`

## How the colors work

GitHub's contribution graph has 5 levels (empty → dark green). The tool maps image brightness to commit counts:

| Level | Color | Commits |
|-------|-------|---------|
| 0 | Empty | 0 |
| 1 | Light green | 1 |
| 2 | Medium green | ~25% of max |
| 3 | Dark green | ~50% of max |
| 4 | Darkest green | max (default 20) |

You can adjust "Max commits" to control the intensity.

## Improvements in this version

- Better validation for repository URLs before download
- Clear status messages for invalid input or image load errors
- Preview stats for commits, active days, and yearly coverage
- Generated script now checks for missing git identity
- `FORCE_PUSH=true` now also recreates the local working directory instead of showing a misleading error
- Added explicit overwrite/force-push control in the UI with confirmation in the generated script
- Added `Text mode` with built-in bitmap lettering and three styles: `Pixel`, `Bold`, and `Slanted`
- Added a separate `Preset mode` with ready-made shapes: `Heart`, `Star`, `Smiley`, `Lightning`, `Moon`, `Check`, `Arrow`, `Diamond`, `Cat`, `Rocket`, `Crown`, `Flame`, `Sun`, `Tree`, and `Coffee`
- Added visible preset cards/gallery for quicker preset picking
- Fixed preset rendering by switching presets to hand-tuned 7-row graph motifs instead of scaling larger source art
- Updated preset gallery cards so they match the exact preset that appears in the contribution preview
- Added `Draw mode` with manual painting, brush levels 0-4, drag-to-draw, one-click `Fill`, `Undo`, `Redo`, `Line`, `Mirror`, clear canvas, and preset stamping so you can place multiple motifs and draw over them

## Tech

Single `index.html` file. No dependencies. No build step. No server. Just open it in a browser.
