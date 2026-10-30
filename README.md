# SPENDSENCE

A private, offline-first personal finance tracker that runs entirely in your browser. No server, no account, no tracking — all data is stored on your own device.

Built as a single `index.html` file (plain HTML, CSS and JavaScript — no frameworks, no build step).

---

## Contents

- [Features](#features)
- [Getting started](#getting-started)
- [Deploying](#deploying)
- [How to use it](#how-to-use-it)
- [Your data and privacy](#your-data-and-privacy)
- [Project structure](#project-structure)
- [Browser support](#browser-support)
- [Known limitations](#known-limitations)
- [Troubleshooting](#troubleshooting)

---

## Features

### Everyday tracking
| Feature | What it does |
|---|---|
| **Transactions** | Add, edit, delete, search, filter and sort income and expenses. Undo available after deleting. |
| **Quick add** | Type a sentence on the Overview page, e.g. `Swiggy 450 food`, `+50000 salary`, `uber 220 yesterday`. Amount, category and date are filled in automatically. Categories are learned from your past entries. |
| **Multiple accounts** | Cash, bank, wallet and credit card, each with its own balance. Transfer money between them. |
| **Split expenses** | Enter names in "Split with" (e.g. `Rahul, Priya`) to split a bill equally. Track who owes you and mark them settled. |
| **Fuel & vehicles** | Log fill-ups with odometer, litres and price. See km/L, cost per km, and a km/L trend chart per vehicle. |

### Planning
| Feature | What it does |
|---|---|
| **Monthly budget** | One overall limit per month, or a default for every month. |
| **Per-category limits** | A separate limit for Food, Fuel, Shopping, etc. Alerts appear at 80% and when exceeded. |
| **Recurring transactions** | Salary, rent, SIPs, subscriptions — post themselves every month (and backfill if you were away). Pause or delete anytime. |
| **Savings goals** | e.g. "Bike down payment — ₹1,50,000 by March". Shows a progress bar and the monthly amount needed. |

### Bills & cards
| Feature | What it does |
|---|---|
| **Bills** | EMI, credit card, current bills, vehicle service and vehicle insurance, with optional monthly repeat. |
| **Due this week strip** | Overview shows everything due in the next 7 days, including credit-card due dates. |
| **Reminders** | Optional browser notifications 1–2 days before a bill is due. |
| **Credit cards** | Set a limit, statement day and due day. See amount owed, limit used, credit available and next dates. |

### Reports
- Monthly snapshot (income, expenses, savings rate, daily average, top category).
- **"Where did I overspend?"** insights card.
- **Month vs month** comparison by category.
- **Year view** with 12-month income/expense chart.
- Export to **Excel, CSV, PDF, JPG, PNG**.

### Safety & convenience
- **Bank CSV import** with automatic categorising and duplicate skipping.
- **App lock** with a PIN.
- **Auto-backup** to a file in a synced folder (Drive, OneDrive, Dropbox).
- **Installable app (PWA)** — add to your phone's home screen and use offline.
- Light and dark theme, display currency selector (USD, INR, EUR, GBP, JPY, AED, AUD, CAD).

---

## Getting started

### Run locally
Just open `index.html` in a browser. Everything works except install-to-home-screen, notifications on some browsers, and offline mode — those need HTTPS or `localhost`.

To run it on `localhost` (enables everything):
```bash
# Python 3
python3 -m http.server 8000
# then open http://localhost:8000
```

### First launch
The app starts with a few sample transactions so you can see how it looks. Click **Clear sample data** on the Overview page when you're ready to start fresh.

---

## Deploying

### Netlify (drag and drop)
1. Go to <https://app.netlify.com/drop>.
2. Drag this folder onto the page.
3. You get an HTTPS link immediately.

### Netlify + GitHub (auto-deploy on every push)
1. Push this folder to a GitHub repository.
2. On Netlify: **Add new site → Import an existing project → GitHub**, choose the repo.
3. Leave the build command empty and set the publish directory to `.`.

### GitHub Pages
1. Push this folder to GitHub.
2. **Settings → Pages → Deploy from a branch → `main` / root**.

> **Important:** Do not commit a downloaded backup file to a public repository. It contains your financial data.

---

## How to use it

### Quick add
On Overview, type into the box at the top:

| You type | Result |
|---|---|
| `Swiggy 450 food` | Expense ₹450, "Swiggy", Food & dining |
| `uber 220 yesterday` | Expense ₹220, "Uber", Transport, dated yesterday |
| `+50000 salary` | Income ₹50,000, "Salary" |
| `petrol 1500` | Expense ₹1,500, Vehicle fuel |

If a word isn't recognised, Pocketwise looks for a similar past entry and reuses its category; otherwise it uses "Other". You can always edit afterwards.

### Setting category limits
**Budgets → Category limits.** Type a monthly amount next to a category and click away to save. Leave blank for no limit. Limits repeat every month.

### Recurring transactions
**Goals → Add recurring.** Pick the first date; it repeats on that day each month (short months use the last day). Posted entries are marked 🔁 in the Transactions list.

### Savings goals
**Goals → New goal.** Enter a target, how much you have already, and a target date. Use **Add money** to record progress. This tracks the goal only — it does not create a transaction.

### Accounts, transfers and credit cards
**Accounts → + Account.**
- For a **credit card**, set the limit, statement day and due day.
- To **pay a card**, use **Transfer** from your bank account to the card.
- Choose which account each transaction belongs to in the Add transaction form.

### Splitting an expense
In the Add transaction form, type names in **Split with**, separated by commas. The amount is divided equally among you and everyone listed. Find balances under **Accounts → Who owes you**. **Settle all** records the repayment as income.

> The full amount you paid still counts as your expense. The balance evens out when the person settles.

### Tracking several vehicles
Name fuel entries as `Vehicle - Station`, e.g. `Honda City - Indian Oil`. The part before ` - ` is treated as the vehicle. Efficiency needs two or more fill-ups per vehicle, and assumes you fill the tank each time.

### Bill reminders
1. **Overview → Add bill** (choose EMI, Credit card, Vehicle service, etc.).
2. Click **🔔 Enable reminders** when prompted and allow notifications.
3. You get one notification per bill per day when it is due within 2 days.

Notifications are checked when the app is opened or in the foreground. Browsers do not reliably run background checks for a static site.

### Importing a bank statement
**Reports → Import bank CSV.**
- Supported date formats: `YYYY-MM-DD`, `DD/MM/YYYY`, `DD-MM-YYYY`, `DD/MM/YY`, and common text dates.
- Works with separate **Debit / Credit** columns, or one **Amount** column (you choose whether positive means money in or out).
- Rows with the same date, amount and description as an existing transaction are skipped.
- Review the Transactions list afterwards and correct any categories.

### App lock
**Reports → Set / change PIN** (4–8 digits). The app locks when opened and after being away for 1 minute. Remove it from the same section.

> The PIN hides the screen; it does not encrypt the stored data. Anyone with access to your unlocked browser profile could still read it from the browser's storage.

### Auto-backup
**Reports → Choose auto-backup file.** Pick a file inside a folder that syncs to the cloud (Google Drive, OneDrive, Dropbox). Pocketwise rewrites it a few seconds after every change. If the browser asks for permission after a restart, click the button again to reconnect.

Not supported in Firefox or Safari — use **Download backup** instead and keep a copy somewhere safe.

### Restoring or moving data
**Reports → Restore backup** and select a backup `.json` file. This **replaces** the current data on that device.

---

## Your data and privacy

- Everything is stored in your browser's `localStorage` (plus one small `IndexedDB` entry for the auto-backup file handle).
- Nothing is sent to any server. There are no analytics or accounts.
- The only external request is loading the Inter and Manrope fonts from Google Fonts. The app still works if they fail to load.
- Data is **per browser and per device**. Clearing site data, using a private window or switching browsers will show an empty app — restore from a backup.
- The currency selector changes display only. Amounts are never converted.

---

## Project structure

```
pocketwise/
├── index.html            # The whole app (HTML + CSS + JS)
├── manifest.webmanifest  # PWA metadata (name, icon, colors)
├── sw.js                 # Service worker for offline use
├── netlify.toml          # Netlify settings and headers
├── README.md
└── .gitignore
```

### Storage keys
| Key | Contents |
|---|---|
| `pocketwise` | Transactions |
| `pocketwise-bills` | Bills |
| `pocketwise-budgets` | Monthly budgets |
| `pocketwise-x` | Category limits, recurring items, goals, accounts, transfers |
| `pocketwise-user` | Name and email |
| `pocketwise-pin` | Hashed PIN |
| `pocketwise-currency`, `pocketwise-theme` | Preferences |

### Backup file format
A JSON file: `{ app, version, tx, bills, budgets, currency, profile, x }`. Backups made by the older version of the app still restore correctly.

---

## Browser support

| Capability | Chrome / Edge | Safari / iOS | Firefox |
|---|---|---|---|
| Core app | yes | yes | yes |
| Install to home screen | yes | yes (Share → Add to Home Screen) | Android only |
| Bill notifications | yes | iOS 16.4+, only when installed to the home screen | yes |
| Auto-backup to a file | yes desktop and Android | No | No |

---

## Known limitations

- **No fingerprint / Face ID unlock.** PIN only.
- **No cross-device sync.** Use backups to move data.
- **Total balance on Overview** is income minus expenses across all transactions and ignores opening balances entered on accounts. Per-account balances on the Accounts page include them.
- **Splits are equal only.** Unequal splits are not supported yet.
- **Reminders need the app opened** (or installed) to fire; there is no background server.
- **CSV categorising** is a best guess based on keywords and your history.
- Deleting an account moves its transactions to your first account.

---

## Troubleshooting

**"Install" option doesn't appear.** You must be on HTTPS (or `localhost`). Opening the file straight from disk won't work. On iOS, use Share → Add to Home Screen.

**Notifications never arrive.** Check the browser's site permissions. On iPhone, the app must be added to the home screen first.

**My data disappeared.** Browser data was cleared, or you are in a different browser, profile or private window. Restore from a backup.

**I updated the site but still see the old version.** Hard-refresh (Ctrl/Cmd + Shift + R), or close and reopen the installed app once. The service worker fetches from the network first, so updates should appear on the next load.

**I forgot my PIN.** Clear the site's data in your browser settings — **this erases all stored data**, so keep backups.

**Auto-backup says "paused".** The browser needs permission again after a restart. Click **Choose auto-backup file** and select the same file.

---

## Keyboard shortcut

Press **N** anywhere (outside a text field) to add a transaction.
