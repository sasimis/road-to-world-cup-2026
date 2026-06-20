# Road to World Cup 2026

An interactive, browser-based tournament companion connected to the shared `WorldCup26` Google Sheet. It turns the match schedule and results into a colourful match centre, live group tables, and a complete knockout tree from the Round of 32 to the final.

## What it includes

- All 104 matches from the workbook
- Existing group-stage results preloaded from the source data
- Live group standings that recalculate when scores change
- Round-of-32 qualification placeholders such as `2A`, `1F`, and `3ABCDF`
- A clickable knockout bracket that carries each selected winner into the next match
- Local SVG country flags for dependable rendering on Windows, macOS, and Linux
- Responsive layouts for desktop and mobile
- Printable bracket and JSON prediction export
- Automatic Google Sheet refresh on launch and every 60 seconds
- Full-screen match presentation with oversized flags, country names, score, date, and venue

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
- The final is `W101 vs W102`

Round-of-32 teams intentionally remain unassigned until qualification is known. Each dropdown is restricted by its workbook rule: `2A` only offers Group A teams and `1F` only offers Group F teams. A combined third-place slot such as `3ABCDF` only displays the teams currently ranked third in the listed groups.

Once a team is selected in any Round-of-32 slot, it is removed from every other dropdown so the same country cannot enter the bracket twice. If updated scores move a selected team out of an eligible third-place position, that invalid selection is automatically cleared.

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

## GitHub Pages

This repository can be published directly with GitHub Pages: choose the repository's default branch and the root folder in **Settings → Pages**.

## Disclaimer

This is an independent fan-made tournament tracker and is not affiliated with or endorsed by FIFA.
