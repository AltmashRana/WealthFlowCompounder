# WealthFlow | Compounder

This is a straightforward financial tool designed to help you project your future savings based on your current salary, annual raises, and investment portfolio. It is built to provide a realistic look at how compounding works over a career timeline.

## Core Functionality

* **Compounding Projections:** Calculates wealth growth from your current age to retirement.
* **Portfolio Distribution:** Supports multiple assets with different returns. If your total portfolio split is less than 100%, the remaining balance is treated as cash with no growth.
* **Salary Growth:** Factors in annual raises so your monthly investment amount increases as your career progresses.
* **Inflation Adjustment:** Set an inflation rate and every headline figure is also shown in today's money, so a large future number is never mistaken for real purchasing power. Inflation, salary raise and goal costs all start at zero, so the tool opens showing plain compounding and you add assumptions deliberately.
* **Retirement Income:** Applies the 4% rule — the standard safe yearly withdrawal — to show the monthly income the pot actually supports. The rate is fixed rather than an input: it is a near-universal convention, and exposing it cost a field and a slider for a number almost nobody changes.
* **Life Goals:** Add big one-off expenses (a car, a house, a wedding) at the age you plan them. Each is entered at today's price, inflated to that age, and withdrawn from the pot on the day — so you see what a purchase costs your retirement, not just its sticker price. A negative amount models an expected inflow instead.
* **Contributions vs Growth:** Separates the money you put in from the money compounding added, and charts the two over your whole timeline.
* **Alternative Benchmarks:** Shows your projected total in USD and Gold equivalents based on current rates.
* **Live Sliders:** Every input in the main panel has a slider beside its number box, so you can drag and watch the projection and the curve move rather than retyping. Monthly salary runs 0 to 50 lakh and current savings 0 to 10 crore; invest value is capped by the salary it comes out of. You can always type a figure past the end of a track — the track then grows to fit, so the thumb never sits pinned at the maximum showing something untrue. Amounts that cannot sensibly be negative snap back to zero when you leave the field; a life-goal amount is the exception, since a negative there is an expected inflow.
* **Readable Timeline:** Hover anywhere on the chart to read the pot, what you paid in, and what compounding added at that exact age.
* **Shareable Link:** The address bar always holds your current scenario. Bookmark variants, or hit Share to copy a link that carries the whole setup.
* **Light / Dark Mode:** A toggle in the header, remembered between visits. The projection card stays dark in both themes as the anchor of the page.
* **Hide Amounts:** A privacy toggle that masks every money figure — outputs and input boxes alike — so the tool can be used with someone looking over your shoulder. Ages, percentages and your horizon stay readable so the page still makes sense. Nothing is edited or deleted; toggling back restores everything.
* **Live Rates:** A refresh button on the conversion rates fetches the current USD and gold prices and fills them in. See Privacy below for what that request involves.
* **Built-in Glossary:** Four collapsible cards at the foot of the page explain the method, every input field, every result, and every button.
* **Scenario Management:** Save your current inputs to your browser's local storage so you can return to them later.

## Technical Details

The tool is built as a single-file application using standard web technologies:

* **HTML5/CSS3**: Handles the layout and responsive design.
* **Vanilla JavaScript**: Manages the calculation logic and DOM updates without any external dependencies or libraries.

## How the Calculations Work

The projection engine is a pure function (`project`) with no DOM access, so the money path can be checked on its own. Open `index.html#test` and read the browser console for a pass/fail count. The 31 checks cover the compounding against a closed-form annuity-due, salary-raise ladders, inflation discounting, goal pricing and shortfall handling, and number formatting at the extremes.

Contributions are driven by the rupee **Invest Value**, not the displayed percentage. The percentage is shown to one decimal, and using it as the source of truth loses about Rs. 83/month on a typical salary — roughly Rs. 13 lakh over a 35-year horizon.

Growth is accumulated month by month rather than derived as a residual, so `wealth = contributed + growth - spent` holds exactly and growth can never come out negative.

The tool uses monthly compounding logic. It calculates a weighted average return based on your asset split. For example, if you allocate 40% to a fund with a 10% return and leave the rest unallocated, the tool applies a weighted return to the total balance. Every month, it adds your investment contribution and applies the monthly growth rate. Every year, it increases your salary and investment amount by your specified raise percentage.

Contributions are applied at the start of each month and earn that month's return (annuity-due). The monthly rate is the geometric twelfth root of the annual rate, not the annual rate divided by twelve.

Nominal totals are then discounted by your inflation rate over the same horizon to give the "today's money" figure. At zero inflation that line is identical to the headline, so it is hidden until it has something to say. The USD and gold equivalents are computed from that inflation-adjusted figure, since applying today's exchange rate to a nominal rupee amount decades away overstates the result by an order of magnitude. The timeline chart is plotted in today's money as well; in nominal terms a multi-decade curve renders as a flat line followed by a spike, which reads as though nothing happens for thirty years.

## Privacy

This is a client-side application. Your figures are never uploaded — the projection runs entirely in your browser, and Save Scenario writes only to your own browser's local storage.

Two things are worth knowing precisely:

* **Live Rates** is the one feature that reaches the internet. Pressing it makes a `GET` request to a public currency API for exchange rates. None of your figures are included in that request, but as with loading any web page, the service can see your IP address and that you asked for rates. Everything else works with no connection at all, and if the request fails your existing values are left untouched.
* **Share** encodes your inputs into the URL itself. That is what makes it work without a server, but it also means anyone you send the link to can see those figures, and the URL may be recorded in browser history or by any chat app you paste it into. Use Save Scenario instead if you would rather the numbers never leave your machine.

Note that the shareable link encodes your inputs into the URL itself. That is what makes it work without a server, but it also means anyone you send the link to can see those figures, and the URL may be recorded in browser history or by any chat app you paste it into. Use Save Scenario instead if you would rather the numbers never leave your machine.
