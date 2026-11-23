# Weekly Schedule

A small offline web app for my week. It shows what to do next today, the time markers for each day, and a to-do list. It runs from my phone's home screen, works without internet, and updates itself when I'm online.

## What's inside

| File | What it does |
|---|---|
| `index.html` | The whole app: schedule, week overview, modalities, to-do page |
| `sw.js` | Service worker: saves the app for offline use and fetches updates when online |
| `manifest.json` | Lets the phone install it as an app (name, icon, colours) |
| `icon-192.png`, `icon-512.png` | Home-screen icons |
| `README.md` | This file |

## Features

**Schedule page**
- Opens on today, with the next unfinished activity shown at the top.
- Core activities in order: classes, study, PMSR, TVN. No fixed clock times, only time markers as anchors.
- Time markers (wake, back from class, off to TVN, back from TVN, sleep) appear between activities. The top box shows the next one coming up.
- Tick an activity when it's done and the next one lights up. Ticks clear when a new day starts.
- Week overview and a list of modality limits (cooking, major movement, freshen up, washing clothes, assignments, hardware with T.M.).

**To-do page**
- Tap a usual item to add it to the list.
- Add new items with an optional max time. Tick "Save to usual items" to keep an item for next time.
- Tick, delete, or *Clear done*. The list does not reset by itself.

## How time works

- Uses the phone's own clock, so no internet is needed to know the day or time.
- Checks the time every minute and whenever the app is reopened.
- **A new day starts at 6am, not midnight.** Between midnight and 6am the app still shows the previous day, which matches the 1am sleep time.

## Hosting on GitHub Pages (one time)

1. Create a **public** repository on GitHub, for example `schedule`.
2. Upload every file in this folder to the root of the repo and commit.
3. Go to **Settings → Pages**, set **Branch** to `main` and folder `/ (root)`, then save.
4. After about a minute the app is live at `https://YOUR-USERNAME.github.io/schedule/`.

## Installing on the phone

Open the link once while online, then:

- **Android (Chrome):** menu ⋮ → **Add to Home screen** / **Install app**
- **iPhone (Safari):** Share → **Add to Home Screen**

Test it: turn on airplane mode and open the app from the home screen. It should load fully.

## Updating

1. Edit `index.html` (or get a new version) and upload it to the repo, replacing the old one.
2. Open the app on the phone while online. It loads the new version and saves it for offline use.

When offline, the app opens the last version it saved.

## Where my data is kept

- Schedule ticks and the to-do list are stored **on the phone only**, in the browser's local storage.
- Updating the app does not erase them.
- Clearing the browser's site data, or uninstalling the app, does erase them.

## Changing the schedule

All schedule content is near the top of the `<script>` in `index.html`:

- `D` holds each day's list in order. `M("10pm","Off to TVN")` makes a time marker; `tvn(5)`, `study(...)`, `pmsr3` and `pmsr1` make activities.
- `NOTE` holds the open or free window text shown for each day.
- `DEF` on the to-do page holds the built-in usual items.

## Reminders

A web app can't set phone alarms. Reminders come from `schedule-markers.ics`, a separate calendar file of weekly repeating events for each time marker. "Off to TVN" and "Sleep" also get a 15-minute heads-up. Import it into the phone's calendar. If the markers change, delete the old events before importing a new file. For the 6am wake-up, use a real alarm in the Clock app.

## Known limits

- On iPhone, a home-screen app that isn't opened for several weeks may lose its offline copy. Opening it once while online restores it.
- Class times are not set yet. They'll be added once the class timetable is out.
