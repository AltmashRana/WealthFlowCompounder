# WealthFlow — Compounder

A no-nonsense tool that shows you how your money actually grows — and what your big life goals cost your retirement along the way.

Plug in your salary, savings, and portfolio. Watch the projection move in real time.

---

## What it does

- **Projects your wealth** from today to retirement, based on salary, raises, and investments
- **Splits your portfolio** across assets with different returns — anything unallocated sits as cash, growing at 0%
- **Grows your salary** with your investment amount each year, on autopilot
- **Adjusts for inflation** — every big number also shows in today's money, so it's never mistaken for real buying power
- **Prices your life goals** — a car, a house, a wedding — at the age you plan them, inflation-adjusted, and shows what pulling that money out costs your retirement
- **Separates contributions from growth**, charted side by side across your whole timeline
- **Converts your total** into USD and gold equivalents
- **Live sliders** next to every number — drag and watch the curve move. Type past a slider's max and the track just grows to fit
- **Hover the chart** to see your pot, what you put in, and what compounding added at any age
- **Share a link** that carries your whole scenario — or save privately to your browser instead
- **Light / dark mode**, remembered between visits
- **Hide Amounts** — blur every money figure with one toggle, for when someone's looking over your shoulder
- **Built-in glossary** explaining every field, result, and button

---

## Built with

Plain HTML, CSS, and JavaScript — one file, zero dependencies, works offline.

---

## How the math holds up

The number-crunching lives in one pure function (`project`), separate from the UI, so it can be checked on its own. Open `index.html#test` and check the console — 31 automated checks cover compounding, salary raises, inflation, goal pricing, and edge cases.

A few things done right under the hood:
- Contributions land at the *start* of each month and earn that month's return (annuity-due), using the true monthly compounding rate — not annual ÷ 12
- Growth is tracked directly, not backed into — so the numbers can never quietly go negative
- Inflation-adjusted figures (not raw future rupees) feed the USD/gold conversions and the chart, so a 35-year projection doesn't look like a flat line with a spike at the end

---

## Privacy

Everything runs in your browser — your numbers are never uploaded.

- **Live Rates** is the only feature that calls the internet (a public currency API, no personal data sent)
- **Share** puts your inputs in the URL itself — great for sending a scenario, but anyone with the link can see the numbers, and it may sit in browser history or chat logs
- **Save Scenario** keeps everything local, if you'd rather nothing leave your machine
