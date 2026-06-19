# 🎯 Darts Score Tracker

A simple, offline score tracker for playing darts at home. Enter what you shoot
each round, get guided through a standard game, and play a few different modes.

It's a **single file** (`index.html`) with no installation, no dependencies, and
no internet required.

## How to use it

Just open `index.html` in any web browser — on your phone, tablet, or laptop.

- **On a computer:** double-click the file, or drag it into a browser window.
- **On a phone/tablet:** put the file on the device and open it, or serve the
  folder from a computer on your network:
  ```
  python3 -m http.server
  ```
  then visit `http://<your-computer-ip>:8000` on the phone.

Your game is saved automatically in the browser, so an accidental refresh won't
lose your progress.

## Game modes

| Mode | What it is |
|------|------------|
| **501 · Double out** | The classic standard game. Start at 501, race to exactly 0, finish on a double. |
| **X01 · Custom** | Same idea but choose the start score (301 / 501 / 701) and whether you need a double to finish. |
| **Cricket** | Close 15–20 and the bull (3 marks each), then score on your closed numbers while opponents are still open. |
| **Around the Clock** | Race from 1 → 20 → bull. Hit your current target to advance. |
| **Tic-Tac-Toe** | A 3×3 grid of numbers. Hit a square's number 3× to claim it; first to three in a row wins. Best with 2 players. |

Supports **1–4 players** with editable names (Tic-Tac-Toe is best with 2).

## How scoring works

1. Pick a game mode and set up your players, then tap **Start game**.
2. Each turn, throw 3 darts. Enter each one **either way**:
   - **Tap the visual dartboard** right where the dart landed (it figures out
     single / double / treble / bull automatically), **or**
   - choose **Single / Double / Treble** and tap the number on the buttons
     (or **Bull** / **Miss**).
3. **Validate before you commit:** each dart you enter drops a numbered marker
   (1, 2, 3) on the dartboard so you can see exactly where the three throws
   landed and fix any mistakes first.
4. Tap **End turn** to commit and pass to the next player.

Helpful guidance appears as you play:

- **Checkout suggestions** in X01 (e.g. "needs 100 — try T20 → D20").
- **Bust detection** for double-out games (going below 0, landing on 1, or
  hitting 0 without a double resets the turn).
- A **"How to play"** panel on the setup screen explains each mode in plain English.

Use **Undo dart** (⌫) to fix a mis-tap, or **Undo turn** to revert the last
committed turn. **Rematch** restarts with the same players; **New game** returns
to setup.

## 📷 Camera auto-score (experimental)

You can let your phone's camera watch the board and place darts for you.

> **Heads up — this is genuinely experimental.** Reliable automatic dart
> detection normally needs multiple cameras and trained ML models. With one
> phone camera the app does its best with frame-differencing + perspective
> math, but it *will* misread throws depending on lighting and angle. Treat
> every detection as a suggestion and correct it — that's why Undo and tapping
> still work.

### Requirement: a secure (https) page
Phone browsers only allow camera access on a **secure page**, so opening the
downloaded file directly (`file://…`) will **not** work. Serve it over https:

- **Easiest — GitHub Pages:** in the repo, go to **Settings → Pages**, choose
  this branch as the source, and open the `https://…github.io/…` URL it gives
  you on your phone.
- Or host `index.html` on any https static host.

(`http://localhost` also counts as secure if you're testing on a computer.)

### Using it
1. **Prop your phone** on a stand/ledge so it faces the board and stays put.
2. Start a game and tap **📷 Camera auto-score (beta)** — allow camera access.
3. **① Calibrate:** tap the four outer edges of the scoring area in the video,
   in order — **top** (above 20), **right** (outside 6), **bottom** (below 3),
   **left** (outside 11). This teaches the app the board's perspective.
4. Clear the board, then tap **② Set empty board** to capture a reference shot.
5. Throw. When a dart settles, the app drops a numbered marker where it thinks
   it landed and adds it to your turn.
6. **Wrong?** Tap the dart's real spot on the live video (that uses the precise
   calibration and is the most reliable way), or use **Undo dart** / the board
   below. Then tap **End turn**.

If a throw is missed or misread, just tap it on the video — calibrated taps are
accurate; the fully-automatic detection is the best-effort part.
