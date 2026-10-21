# Sess agent starter: agent instructions

## What it does
A weekend planner. `agent.mjs` asks a person two questions on one private Sess link: where and when, then three plans from the real MET Norway forecast. It verifies each signed receipt with `@sess.si/sdk`, completes the Session and prints the plan. `weather.mjs` holds the weather, the plan rule and their attribution. No AI model is used.

## Run it
```
npm install --ignore-scripts
SESS_API_KEY=… SESS_DEMO_CONTACT=… npm start
```
`SESS_DEMO_CONTACT` is your project URL or team email (MET Norway asks for it). Never print, log or commit the key or the Sess link: anyone holding the link can answer.

## Add or change a question
Each question is a `form(title, description, action, components)` in `agent.mjs`, built from text components, `field(name, label, choices, help)` and one action. Read the answer only after `sess.receipts.verifyResponse`.

## Keep it short (Sess limits, in characters; Sess never truncates)
- Title: a question or a task, about 40; at most 80.
- Button: a verb, 1–3 words; at most 24.
- Field label and choice label: short; at most 60. Help: one hint; at most 160.
- Description 280, heading 60, record caption 200, record row name 40 and value 200, text 4,000; at most 5 buttons.

A longer value is refused with `400 INVALID_SCHEMA`, naming the `field`, the `limit` and the `length`. Shorten that value and run again.

## Rules
`agent.mjs`, `weather.mjs` and `README.md` are generated from `w1991e/sess-sdk` `create-agent/template` and must stay byte-identical. Change them there first.
