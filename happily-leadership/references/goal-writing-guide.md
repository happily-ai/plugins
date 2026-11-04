# Writing goals, key results and updates

Use this guide when helping someone write or change a goal, key result or progress update in Happily. It describes what good looks like. The MCP enforces only the limits marked **Limit**; everything else is advice. Offer it as a suggestion, never as a rewrite the user didn't ask for.

## Goal

| Field | Good practice | Example |
|---|---|---|
| **Title** | The outcome the team wants, in plain words. Start with a verb or describe the end state. Keep numbers out; they belong in key results. **Limit: 30 characters.** | "Make checkout effortless" (not "Checkout latency 300ms") |
| **Description** | Why the goal matters and what success looks like, in one or two plain sentences. No numbers, owners, dates, current values or counting rules (see **Where each detail goes**). If it's left empty, Happily repeats the title. **Limit: 300 characters.** | "Slow checkout is our top support complaint. Success is customers paying without waiting." |
| **Parent goals** | Link to the goal on a team above that this goal moves forward. Only goals on teams above, and not archived goals, can be parents. | Platform's "Make checkout effortless" under Engineering's "Win enterprise customers" |
| **Number of key results** | Two to four per goal. More than five usually means the goal is two goals. **Limit: 5 when creating a goal in one step**; more can be added afterwards. | |

## Key result

| Field | Good practice | Example |
|---|---|---|
| **Title** | A measurable result with the target in it. Describe the result, not the task. | "Cut p95 checkout latency to 300ms", "Onboard 3 design partners" (not "Work on latency") |
| **Starting value** | The baseline progress is measured from: where the number stood at the start of the period, measured the same way the target is. For counts within the period this is usually 0. | 500 |
| **Target** | Where it should end up by the end of the cycle. It can be lower than the start for numbers that should go down. It can't equal the start. | 300 |
| **Unit** | A short plural noun or symbol, used the same way every time. Values are never converted between units. | "ms", "%", "customers", "deploys" |
| **Owners** | One or two people accountable for the number. They must be current members of the company. | sam.rivera@northwind.test |
| **Tracking** | "One shared value" (default) for a team number. "Each owner tracks their own number" only when two or more owners each own a slice that adds up to the target. | |
| **Current value** | Only when the key result starts part-way: the result reached so far, measured from the starting value. Leave it out to start at the starting value. | 7 (with starting value 0, target 40: 17.5%) |
| **Cycle** | The period it's measured over: "Q4 2026", "H2 2026" or "2026". Leave it empty for an evergreen key result. Past cycles can't be changed. | "Q4 2026" |
| **Description** | The update recipe: how the number is counted and kept up to date, in [the recipe format](update-recipes.md) ("How this is updated", then Source, What counts, Value, Owners, Cadence, Note, Hold when; leave out lines that don't apply). The rule only: no latest values or dated checks. The console doesn't show it; assistants read it. **Limit: 2,000 characters.** | "How this is updated / What counts: unique external registrations in Q4 2026, excluding internal accounts and tests. / Cadence: weekly." |

## Where each detail goes

Each field has one job. Put a detail where it belongs, even when the user gives everything in one paragraph.

| Detail | Where it goes | Not in |
|---|---|---|
| Why the goal matters, what success looks like | Goal description | Key result descriptions |
| The target and its unit | Key result title, target and unit | Goal title or description |
| Who is accountable | Key result owners | Any description |
| The period | Key result cycle | Goal title or description |
| How a number is counted: source, what's in and out, definitions, cadence | That key result's description, as a recipe | Goal description |
| The latest value, when it was checked, what moved it | An update (value and note) | Any description |

A goal description that lists owners, current values or counting rules is the most common mistake. It crowds the goal card in the console, goes stale on the first update, and leaves the key results with no recipe to refresh them from.

Example. A user writes: "Q4 MyCulture growth. I own all three. Checked 30 October: 50 registrations, 15.6% activation. Activation means a ready candidate result within 14 days, excluding self-tests. Weekly updates."

- Goal description: "Grow MyCulture into a product employers find, use and pay for. Success is more new customers signing up, getting a ready result quickly, and choosing to pay."
- Activation key result description: "How this is updated / What counts: registrations at least 14 days old. Activated means a completed, ready candidate result within 14 days, excluding self-tests, staff and sample data. / Value: activated ÷ eligible registrations, as a %. / Cadence: weekly."
- 50 registrations and 15.6% activation: current values on their key results, each with a note on when it was checked.
- "I own all three": the owners field. "Q4": the cycle.

Drafting the split is a suggestion like any other: show it as a preview and let the user confirm it.

## Progress update

| Field | Good practice | Example |
|---|---|---|
| **Value** | The latest number, in the key result's own unit. Only the number the person stated; never estimate or round it. | 225 |
| **Note** | What moved, why, and what happens next, in one to three sentences (about 280 characters). Lead with the most important fact: notifications show only the first 140 characters. Work facts only; the team reads it. **Limit: 500 characters.** | "Read replicas now serve 50% of traffic. p95 dropped 15 ms. Rolling out to 100% next week." |
| **Status** | Leave it automatic. Happily works it out from progress and how far the cycle has gone. Set it by hand only when your judgement differs from the pace (for example, a big jump is about to land), and say why in a note. A status set by hand stays until someone changes it, or until the key result reaches 100%. | |

## Where an update note appears

| Place | Who sees it | How much |
|---|---|---|
| Key result timeline (console and mobile app) | Everyone who can see the goal | The full note |
| Push notification to co-owners | Other owners of the key result | First 140 characters, quoted |
| Push notification to the owner's manager | The manager, only when the update has a note or changes status | First 140 characters, in the notification's detail view |
| Weekly digest and AI summaries | The manager; assistants that read history | Read from the timeline |

Notifications only go out for key results in the current cycle. A value change with no note and no status change reaches the manager only through the weekly digest.

## How status is worked out

For a key result with a cycle, Happily compares progress with how much of the cycle has passed. A new key result still at its starting value a few weeks into the quarter therefore shows "off track" until the first update; that's expected. For evergreen key results, status follows progress alone.

## When suggesting improvements

- Show the preview with the user's own words first. Mention any `suggestions` from the preview as optional ideas, in one line each.
- If the user wants an improved version, propose it as a new preview. Never change a title, number or note without their go-ahead.
- Don't block a change for style reasons. Only the limits marked **Limit** stop a change.
