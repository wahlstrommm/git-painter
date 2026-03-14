# Git Painter

Turn any image into your GitHub contribution graph.

Upload a photo, adjust how it looks on the grid, and download a bash script that creates backdated git commits to paint the image on your GitHub profile.

## How it works

1. Open `index.html` in your browser
2. Drop an image (selfie, logo, pixel art — anything)
3. Use the controls to adjust how it maps to the 52×7 contribution grid:
   - **Zoom** — scale the image up/down within the grid
   - **Position X/Y** — move it around
   - **Threshold** — control how aggressively light/dark maps to commit levels
   - **Invert** — flip light and dark
4. Pick a target year and enter your repo URL
5. Click **Download git-painter.sh**
6. Run the script — it creates a repo with backdated commits that paint your image

## Prerequisites

- An **empty** GitHub repo (no README, no .gitignore)
- The repo must **not** be a fork
- `main` must be the default branch
- `git` 2.28+ and `bash`

## Usage

```bash
chmod +x git-painter.sh
./git-painter.sh
```

The script creates a local repo (`git-painter-art/`), makes all the commits, and pushes to your repo. Visit your GitHub profile to see the result.

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

## Tech

Single `index.html` file. No dependencies. No build step. No server. Just open it in a browser.
