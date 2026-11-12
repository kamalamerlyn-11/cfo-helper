# CFO Helper — Your Financial Co-Pilot

**Turn "What If" into "What Works".**

CFO Helper is an AI what-if budgeting agent for startup founders, student fest organisers and small business owners. You can move sliders, or ask a question in plain English like *"If I hire 2 engineers, can we survive 6 months?"* The agent runs the numbers with its simulation tools and shows the result on a live cash-runway chart.

Originally pitched at **Hack With Hyderabad** by a team from Acharya Nagarjuna University, led by **Chunduru Kamala Merlyn**.

**Live demo:** https://claude.ai/artifact/M3P9kGvSb6UqsLmruornZo

## Features

- **Profiles:** three ready-made profiles: Startup Founder, Student Fest Organizer and Small Business Owner.
- **Adjustable inputs:** cash, revenue, expenses, growth, new hires, salary, extra marketing and price change.
- **Instant forecast:** runway, monthly net, cash after 12 months, a 12-month chart against the baseline, and a plain-English verdict.
- **AI agent with tool calling:** the LLM never guesses numbers. It calls page functions and shows each call in the chat:
  - `get_current_plan`: reads the current inputs and results.
  - `simulate_scenario`: runs a what-if without changing the UI.
  - `apply_scenario`: updates the sliders and chart to the chosen scenario.
- **Live data stream:** simulated revenue and expense updates every 3 seconds, in the spirit of a Pathway real-time pipeline.
- **Usage-based billing (Flexprice-style demo):** ₹2 per scenario simulated and ₹10 per report exported, with an in-app usage counter. No real charges are made.
- **Shareable report:** a text report you can copy and share.

## How the agent works

```
User question ──► LLM (brain)
                    │ decides which tool to call
                    ▼
             Tools (page functions)
     get_current_plan / simulate_scenario / apply_scenario
                    │ results (real numbers from the model)
                    ▼
             LLM writes the answer ──► chat + updated chart
```

## Forecast model

For each month *m*:

- **Revenue:** `revenue × (1 + price%) × (1 − 0.5 × price%) × (1 + growth%)^(m−1)`, plus `1.2 × extra marketing` from month 2.
- **Expenses:** `expenses + hires × salary + extra marketing`.
- **Cash:** `previous cash + revenue − expenses`. The runway is the point where cash crosses ₹0.

The assumptions are deliberately simple. They're for planning, not accounting.

## Tech

- **App:** a single-file web app in plain HTML, CSS and JavaScript. The chart is an inline SVG and there's no build step.
- **AI layer:** an LLM with function calling, through the Claude artifact runtime's `sample` capability.

To run it, open `index.html` in a browser. The sliders, chart, live stream, billing and report all work offline. The AI chat works when the page is opened from its claude.ai link.

## Roadmap (from the original pitch)

- Next.js and TypeScript frontend with Recharts.
- Node.js and LangChain agent backend.
- Real Pathway streams, with Redis and Kafka.
- Real Flexprice and Stripe billing.
- PDF reports with Puppeteer, and email with SendGrid.
- OAuth sign-in.
