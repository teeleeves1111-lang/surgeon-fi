# Surgeon FI app — working rules

A financial-independence calculator for NJ surgical residents and attendings. Tom (a vascular surgeon) uses it to give a live talk to residents, who then run their own numbers on their phones. Live at surgeon-fi.vercel.app.

## Build and deploy
- The whole app is one file: `index.html` (HTML, CSS and JS inline). Keep it that way: no build step, no new files the page needs, and no new libraries beyond Chart.js from the CDN.
- Pushing to `main` deploys (Vercel auto-deploys from this repo). Tom wants changes committed and pushed to `main` directly, not left as PRs.
- `UPDATING.md` is the yearly checklist for dollar figures (IRS limits, tax brackets, salaries). Follow it for any figure that changes each year.

## Before every push
1. Syntax-check the script: pull the `<script>` blocks out and run `node --check` on them.
2. Load the page in headless Playwright and check for page errors. Chart.js may not load in a sandbox; stub it with
   `page.add_init_script('window.Chart = function() { this.destroy = function(){}; }')`.
   The Quick setup dialog opens on first load; call `closeSetup()` or fill it and call `applySetup()`.
3. Check every new or changed number independently (in Python, from the current year's rules), not just by reading the code.
4. Check that the talk demo's numbers haven't moved unless the change was meant to move them (see below).

## Numbers must agree everywhere
- All tabs run on one engine: `pbSim()` / `pbFlat()` (My Plan), with `project()` underneath. The "if nothing changes" path is `pbFlat(c)`. Don't write a second projection.
- In estimate mode the plan only invests cash the budget actually has (capped). Any advice built on top of it (a raise, an amount, an age) must use the same cap. Advice built without the cap can promise an age the plan never shows.
- One figure, one wording: if two places show the same quantity, they must show the same number.

## The demo surgeon
A made-up composite. Keep it non-identifiable and don't add details from Tom's own finances.
- Age 35, $700k salary, two kids in daycare at $2,800/mo, $1.3M house already owned, $250k student loans refinanced, 403(b) only, both Roths, $500/mo brokerage, net worth $100k, one financed car.
- Don't use: three kids, "five years out," $700–800k with twice-yearly bonuses, or "negative every month."

## Tone and content
- Write for a busy resident on a phone: short, plain, no jargon left unexplained. Tom has already cut the app once for being too wordy. Don't add bulk back.
- Say "can stop working" or "work optional," not "call optional."
- Investing guidance stays a plain three-fund portfolio (US and international total-market index funds, bonds added toward retirement).
- Default salaries are conservative first offers, not career averages.
- Headline numbers must be realistic: nobody invests every leftover dollar, and most new attendings can't fund a brokerage right away. The message isn't "live on beans and rice."
- Tom wants honest pushback on framing or math errors, not just the change he asked for.
