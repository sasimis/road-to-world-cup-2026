# Road to World Cup 2026

Welcome to an interactive, browser-based tournament companion connected to the shared `WorldCup26` Google Sheet. It turns the match schedule and results into a colourful match centre, live group tables, and a complete knockout tree from the Round of 32 to the final.

https://sasimis.github.io/road-to-world-cup-2026/

## What it includes

- All 104 matches from the workbook in google sheets
- Existing group-stage results preloaded from the source data
- Live group standings that recalculate when scores change
- Round-of-32 qualification placeholders such as `2A`, `1F`, and `3ABCDF`
- A clickable knockout bracket that carries each selected winner into the next match
- Local SVG country flags for dependable rendering on Windows, macOS, and Linux
- Responsive layouts for desktop and mobile
- Printable bracket and JSON prediction export
- Automatic Google Sheet refresh on launch and every 60 seconds
- Full-screen match presentation with oversized flags, country names, score, date, and venue
- Mobile-first progressive match rendering, lazy flag loading, and reduced visual effects

## Live Google Sheet connection

The site reads its teams, schedule, stage labels, branch rules, and results from the public Google Sheet:

<https://docs.google.com/spreadsheets/d/1tvoPbpXmwkwtVDLVJo62wM_etwknNg9ZXDrMZHLJl6k/edit?usp=sharing>

The webpage checks the `world_cup_matches` and `teams` tabs when it opens and then every 60 seconds. The header displays **Sheet live** after a successful refresh. **Sync now** performs an immediate check.

The sheet must remain accessible to anyone with the link. If it becomes private or the device is offline, the webpage continues using its bundled fallback data and shows **Offline data**.

## How the bracket works

The knockout routing comes from the match labels in the workbook. For example:

- Match 73 is `2A vs 2B`
- Match 76 is `1F vs 2C`
- Match 89 is `W73 vs W75`
- Match 101 is `W97 vs W98`
- The final is `Winner101 vs Winner102`

Round-of-32 teams are assigned automatically from the current group tables. `1A` resolves to the current Group A winner, `2A` to the current runner-up, and the eight best third-placed teams are ranked across all twelve groups. Their exact opponents are then assigned collectively with all 495 combinations from Annex C of the [FIFA World Cup 2026 Regulations](https://digitalhub.fifa.com/m/636f5c9c6f29771f/original/FWC2026_regulations_EN.pdf).

For scenario planning, click any Round-of-32 country to open the flag-and-name team picker. First- and second-place slots only offer teams from the required group; third-place slots only offer currently qualifying third-place teams from the groups permitted by that match. Used countries are blocked unless the selection can be completed as a valid swap, so a country can never appear twice.

Group ties follow FIFA's order: head-to-head points, head-to-head goal difference, head-to-head goals, overall goal difference, overall goals, team conduct score, and FIFA ranking. The optional `teams` sheet columns E and F can supply team-conduct scores and FIFA ranking positions when those final tie-breakers are needed; otherwise the page keeps a stable provisional order.

After the Round of 32 there are no free-form team selections. Participants are carried forward strictly from the workbook's winner routes (`W73`, `W89`, and so on), so a team can only enter a later match by winning the correct preceding branch.

The workbook contains a circular label for match 100 (`W95 vs W100`). The webpage uses the logically consistent route `W95 vs W96`.

## Where edits are saved

Changes made directly in the webpage are stored in the current browser's `localStorage` under the key `roadto26-state`. They do **not** write back to the Google Sheet, XLSX, or a CSV file. The Google Sheet is the shared source of truth: when its data changes, the next sync imports the new sheet results.

- Refreshing or reopening the page in the same browser keeps the changes.
- Clearing browser site data removes them.
- **Export picks** downloads a portable JSON copy.
- **Reset** restores the results originally imported from the workbook.

## Run locally

Open `index.html` in a modern browser. The application is self-contained and requires no build step or server.

## Project structure

```text
.
├── index.html                 # Semantic page structure
├── assets/
│   ├── css/
│   │   └── styles.css         # Responsive tournament presentation
│   ├── js/
│   │   ├── app.js             # Sync, standings, bracket and UI logic
│   │   └── data.js            # Bundled offline tournament fallback
│   └── flags/                 # Local SVG country flags
├── .nojekyll                  # Serve static assets unchanged on GitHub Pages
└── README.md
```



## Disclaimer

This is an independent fan-made tournament tracker and is not affiliated with or endorsed by FIFA.
