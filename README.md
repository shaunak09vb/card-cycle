# Card Cycle — setup guide

A small iPhone app for weekly credit card check-ins, grouped by statement cycle (e.g. the 10th to the 9th).
It's a web app you install on your Home Screen. No Mac, no App Store, no server, and your numbers never leave your phone.

## What's in the folder

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `manifest.webmanifest` | Tells the iPhone its name and icon |
| `sw.js` | Lets it open with no internet |
| `apple-touch-icon.png`, `icon-192.png`, `icon-512.png` | Icons |

## 1. Try it on your Windows laptop (optional)

In the unzipped folder, open PowerShell and run:

```
python -m http.server 8000
```

Then open http://localhost:8000 in Chrome. Press F12 → device toolbar (Ctrl+Shift+M) to see it at phone size.
Data you enter here stays on your laptop; it won't appear on your phone.

## 2. Put it online for free (GitHub Pages, ~5 minutes)

1. Sign in at github.com → **New repository** → name it `card-cycle` → **Public** → Create.
2. On the new repo page click **uploading an existing file**, drag in all 6 files (not the folder), **Commit changes**.
3. **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → **Save**.
4. Wait a minute and refresh. Your app is at `https://YOUR-USERNAME.github.io/card-cycle/`.

The repo holds only the app's code. Your spending data is stored on your phone, never in GitHub.

## 3. Install on your iPhone

1. Open that link in **Safari** (it must be Safari).
2. Tap **Share** → **Add to Home Screen** → **Add**.
3. From now on, open **Card Cycle from the Home Screen icon**. The installed app keeps its own data, separate from Safari.
4. Set up your card: name, credit limit, cycle start day (`10` for a 10th–9th cycle), and optionally a spending target.
   Use **Settings → Add another card** for a second card with its own cycle.

## 4. The Sunday reminder

Reminders app → new reminder "Card check-in" → tap ⓘ → turn on **Date** and **Time** (this Sunday, 7:00 PM) → **Repeat: Weekly**.
You can paste the app link into the reminder's URL field too.

Prefer Shortcuts? Shortcuts → Automation → **+** → Time of Day → Sunday, Weekly → Run Immediately → action **Show Notification**.

## 5. Each Sunday

Open your card's app, read **available credit** (or **current balance**, your choice per check-in), and type it in. Card Cycle shows:

- **Spent this cycle** = limit − available credit (or the balance), minus anything that isn't this cycle's spending
- **This week** vs **the week before**
- With a target: whether you're over or under pace, and the weekly amount that keeps you on target for the rest of the cycle
- **History**: every cycle with its total and each check-in; tap a check-in to edit it

### The one field to understand: "Unpaid from last statement"

Right after your statement closes, your balance still includes last cycle's charges until you pay them.
Enter that unpaid amount and the app subtracts it, so it isn't counted as new spending. Once your statement is paid, it's 0.
If you pay extra toward the current cycle's charges, enter that payment as a negative number.

### Getting an exact final total

Sunday check-ins rarely land on statement day. For an exact cycle total, add a check-in dated the last day of the cycle (e.g. the 9th).
The app reminds you to do this for a week after each cycle closes.

## Backups

Your data lives only in the installed app on your phone. **Deleting the Home Screen icon deletes the data.**
Use **Settings → Export backup** now and then (save to Files or email it to yourself); **Restore backup** brings it back.
**Export CSV** gives you every check-in as a flat table for Excel or Power BI.

## Updating the app later

Edit the files, change `card-cycle-v1` to `card-cycle-v2` at the top of `sw.js`, and upload them to the repo again.
The phone picks up the new version the second time you open the app. Your data isn't affected.
