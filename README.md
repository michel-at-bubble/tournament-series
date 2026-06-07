# tournament-series
Dutch Blood Bowl Tournament Series

A lightweight, self-contained results portal for the Dutch Blood Bowl Tournament Series.
It shows the ongoing league standings and the final ranking per tournament, read live
from a Google Sheet. Bilingual (Dutch / English) and mobile-friendly.

🔗 **Live:** https://series.blood-bowl.nl

## What it does

- **League standings** — the ongoing ranking, sorted by points, with the top 4 highlighted.
- **Tournaments** — the final ranking per tournament, picked from a list with date and status.
- **Status markers** per tournament:
  - 🏆 counts toward the current standings
  - ⏳ played, results still to come
  - 🕜 upcoming tournament
  - 📜 historic, no longer counts
- **NAF numbers** link to the coach's page on the NAF site.
- **Language** (NL/EN) based on the browser locale, switchable by hand.
- **Shareable links** — the active view and language are kept in the URL.

## How it works

The portal is a single `index.html` file: HTML, CSS and JavaScript in one, with no
build step and no external dependencies (apart from the web fonts). Data is fetched
live from a Google Sheet through its public CSV endpoint, so there is no server,
database or API key involved. The Sheet is the single source of truth.

## Maintenance

### Updating results

All data lives in the linked Google Sheet. The portal reads these tabs:

- **Deelnemers** — the league standings (columns: Naam, NAF #, Punten).
- **Toernooien** — the list of tournaments (name, date, expiry date, number of
  participants, and the tab code of the final ranking).
- **One tab per tournament** holding the final ranking (Resultaat, Deelnemer,
  NAF nummer, Team, Punten).

Adding a tournament needs no code changes: add a tab with the final ranking and a row
in the Toernooien tab. Once the participant count is filled in there, the tournament
counts as "results known".

> The Sheet must stay shared as **"anyone with the link → viewer"**, otherwise the
> portal cannot load the data.

### Changing the portal

Configuration lives at the top of `index.html` in the `CONFIG` block (Sheet ID, tab
names, columns). The Dutch and English interface strings live in the `TRANSLATIONS`
block. Commits to `main` go live within ~1 minute.

## Hosting

Hosted on GitHub Pages, served from the custom domain `series.blood-bowl.nl`.

## Credits

Tournament data is kept with **Score!**, the Blood Bowl Tournament Tool by
Joris (Yavatol) Dormans.
