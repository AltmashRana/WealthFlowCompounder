# WealthFlow

WealthFlow is a straightforward financial tool designed to help you project your future savings based on your current salary, annual raises, and investment portfolio. It is built to provide a realistic look at how compounding works over a career timeline.

## Core Functionality

* **Compounding Projections:** Calculates wealth growth from your current age to retirement.
* **Portfolio Distribution:** Supports multiple assets with different returns. If your total portfolio split is less than 100%, the remaining balance is treated as cash with no growth.
* **Salary Growth:** Factors in annual raises so your monthly investment amount increases as your career progresses.
* **Alternative Benchmarks:** Shows your projected total in USD and Gold equivalents based on current rates.
* **Scenario Management:** Save your current inputs to your browser's local storage so you can return to them later.

## How the Calculations Work

The tool uses monthly compounding logic. It calculates a weighted average return based on your asset split. For example, if you allocate 40% to a fund with a 10% return and leave the rest unallocated, the tool applies a weighted return to the total balance. Every month, it adds your investment contribution and applies the monthly growth rate. Every year, it increases your salary and investment amount by your specified raise percentage.

## Privacy

This is a client-side application. No data is sent to a server or stored in a database. Your financial information stays in your browser's local storage and is only accessible to you on your device.
