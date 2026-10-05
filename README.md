# Weekly Expense Tracker — setup guide

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
3. From now on, open **Weekly Expense Tracker from the Home Screen icon**. The installed app keeps its own data, separate from Safari.
4. Set up your card: name, credit limit, cycle start day (`10` for a 10th–9th cycle), and optionally a spending target.
   Use **Settings → Add another card** for a second card with its own cycle.

## 4. The Sunday reminder

Reminders app → new reminder "Card check-in" → tap ⓘ → turn on **Date** and **Time** (this Sunday, 7:00 PM) → **Repeat: Weekly**.
You can paste the app link into the reminder's URL field too.

Prefer Shortcuts? Shortcuts → Automation → **+** → Time of Day → Sunday, Weekly → Run Immediately → action **Show Notification**.

## 5. Each Sunday

Open your card's app, read **available credit** (or **current balance**, your choice per check-in), and type it in. Weekly Expense Tracker shows:

- **Spent this cycle** = limit − available credit (or the balance), minus anything that isn't this cycle's spending
- **This week** vs **the week before**
- With a target: whether you're over or under pace, and the weekly amount that keeps you on target for the rest of the cycle
- **History**: every cycle with its total and each check-in; tap a check-in to edit it

### Bills you haven't paid yet are handled for you

Between a statement closing and the day you pay it, your card balance still includes that bill.
If you set **I pay this card on day** in Settings, the app leaves that bill out of your new spending automatically
(using the statement total it has on record) and stops doing so from your pay day.

The only time it asks is when it has no record of a statement you haven't paid yet, usually your first week:
it shows one extra box, "[Card] statement balance, [dates]". Type the balance from your statement, or leave it blank if it's paid.

### Getting an exact final total

Sunday check-ins rarely land on statement day. For an exact cycle total, add a check-in dated the last day of the cycle (e.g. the 9th).
The app reminds you to do this for a week after each cycle closes.

## Budget per payment (default once pay days are set)

Set **I pay this card on day** on every card (e.g. 15), then a budget in **Settings → Combined budget** with
**Budget counts: What I pay each month**. The All cards tab then tracks each month's total payment:

- **Tiles** for each card's statement in the next payment, and a **Total to pay** tile with the budget bar and how much room is left
  (and roughly how much a week, on which cards, until their statements close).
- **Spending today goes on**: which payment a purchase made today will be part of. With Amex closing on the 9th and
  Wealthsimple on the 24th, both paid on the 15th: Amex spending from the 10th and Wealthsimple spending from the 25th land on the
  following month's payment.
- **Then**: the payment after next, already building up.
- **Past payments**: every month's total paid, split by card.

Example (Amex 10th–9th, Wealthsimple 25th–24th, both paid on the 15th):
the Oct 15 payment = Amex Sep 10 – Oct 9 + Wealthsimple Aug 25 – Sep 24.

## One budget across both cards (by spending date)

Choose **Budget counts: What I spend in a budget month** to budget by when you spend instead of when you pay.

Once you have two or more cards, an **All cards** tab appears.

1. Set a **monthly budget across all cards** (e.g. 3250) and the day your **budget month** starts.
   It defaults to your first card's cycle day; keep it at 10 to line up with the Amex.
2. Each Sunday, tap **Check in all cards** and enter each card's number on one screen. Leave a card blank to skip it.

The tab shows the combined total for the budget month, a per-card split, whether you're over or under pace,
the weekly amount that keeps you on budget, stacked week-by-week bars, and every past month.

**How cards with different cycles add up.** Each check-in tells the app how much a card went up since its last check-in.
That amount is spread evenly over the days it covers, and only the days inside the budget month count toward it.
So a card that closes on the 21st still lands in the right budget month, nothing is counted twice, and nothing is lost between months.
The card whose cycle matches the budget month is exact; for the other card, a week that straddles the 10th is split by day.

**Tiles.** The top of the All cards tab shows one tile per card (spent so far this budget month) and a total tile with your budget bar.
The budget month ends on the day before your start day (the 9th) and everything resets to $0 the next morning (the 10th).

**Next payment.** In Settings, set **I pay this card on day** for each card (e.g. 15 for both).
The All cards tab then shows which statement each card's next payment covers, the amount, and the total to pay.
Once every statement in that payment has closed (for an Amex closing on the 9th and payment on the 15th: the 9th through the 15th),
the panel moves to the top of the screen.

**Keep your totals complete:** when a card's statement closes between two Sundays, add a check-in dated its closing day
(the app nudges you for a week afterwards). Otherwise the days between your last Sunday and the close aren't counted.

## Backups

Your data lives only in the installed app on your phone. **Deleting the Home Screen icon deletes the data.**
Use **Settings → Export backup** now and then (save to Files or email it to yourself); **Restore backup** brings it back.
**Export CSV** gives you every check-in as a flat table for Excel or Power BI.

## Updating the app later

Edit the files, bump the version at the top of `sw.js` (e.g. `expense-tracker-v5` → `expense-tracker-v6`), and upload them to the repo again
(on the repo page: **Add file → Upload files**, drag them in, **Commit changes** — same-named files are replaced).
The phone picks up the new version the second time you open the app. Your data isn't affected.
