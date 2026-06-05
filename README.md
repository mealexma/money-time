# Money Time — a fun live salary ticker

A single self-contained `index.html` web app. You press **Start** and it shows your
earnings ticking up in real time (after-tax). It's just for fun — to glance at during
a boring meeting. (Built for my wife.)

## Location & hosting

- **Local git repo:** `C:\Users\alexa\Work\money-time` (just `index.html` + `.git`). This is the single source of truth.
- **GitHub repo:** https://github.com/mealexma/money-time (public, account `mealexma`)
- **Live site (GitHub Pages, `main` branch, root):** https://mealexma.github.io/money-time/
- **`gh` CLI** is installed at `C:\Program Files\GitHub CLI\gh.exe` and authenticated as `mealexma`.
  It is **not on PATH** in fresh shells — call it by full path.
- **Deploy** = commit + `git push`; Pages rebuilds in ~30s.

## The hardcoded math (no inputs in the UI)

- 45 000 kr/month salary, 35 h/week → ~296.70 kr/h gross
- 32% tax → ~201.76 kr/h net (this is the big number shown)
- Constants live at the top of the `<script>` block: `MONTHLY_GROSS`, `HOURS_PER_WEEK`, `TAX_RATE`, `CURRENCY`.

## Features / design

- **Fintech look** (modeled on a Dribbble reference): off-white background, Inter font,
  deep-green "balance card" hero with the big number + a "before tax" pill, a white
  "Treats" list card, green pill buttons.
- **Treats:** a fun ladder (cookie → coffee → … → vacation) showing what you've "earned"
  so far + the next one with a countdown ETA. Defined in the `TREATS` array.
- **Start/Stop button:** Start → "Stop" (pauses, keeps the total) → "Resume".
  Reset zeroes everything. Pause logic uses `state.accumulated` + `state.startedAt`.
- **Mobile-first**, fullscreen when added to an iPhone home screen (apple-mobile-web-app
  meta tags, safe-area padding, no scroll bounce).
- **Storage:** `localStorage` — the start time + accumulated total persist across tab
  close, browser restart, and reboot. On reopen the ticker catches up to where it would
  have been (it's just elapsed-time math). Per-browser/device; Reset clears it.

## How to edit & redeploy

```powershell
$gh = "C:\Program Files\GitHub CLI\gh.exe"   # if you need gh; plain git is on PATH
Set-Location "C:\Users\alexa\Work\money-time"
# ...edit index.html...
git add -A
git commit -m "your message"
git push                                      # Pages rebuilds in ~30s
```

Check the live build status:

```powershell
& "C:\Program Files\GitHub CLI\gh.exe" api repos/mealexma/money-time/pages/builds/latest --jq ".status"
```

## Install on iPhone (one time)

1. Open https://mealexma.github.io/money-time/ in **Safari**.
2. **Share → Add to Home Screen → Add**.
3. Launch from the 💰 icon — opens fullscreen, no browser bars.

## Status & possible next steps

Deployed and working. Ideas discussed but not done:

- Celebrate when a new treat unlocks (sparkle/animation).
- Tune the treat ladder amounts or copy.
