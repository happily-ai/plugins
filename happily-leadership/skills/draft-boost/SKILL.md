---
name: draft-boost
description: Draft a Boost (Happily's manager-written performance review) or other review for someone on your team, from your own judgement and their Happily record: past Boosts, team goals and key results the person owns, focus items, recognition and feedback threads. Use when a manager asks to write, draft or prepare a Boost, quarterly review or performance feedback for someone.
---

Read [the evidence and cross-app guidance](../../references/evidence-and-context.md). A Boost is the manager's evaluation. Happily evidence supports it; it does not replace it.

## The manager's judgement comes first

If the manager gives their own assessment, build the draft around it. Keep every rating they give exactly as given, and keep each point they make as a main point. Add Happily evidence that supports or adds detail to each one. If the evidence is thin on one of their points, keep the point and say it rests on their observation. Do not swap in your own ratings or second-guess theirs unless they ask.

If they give no assessment, write a draft that waits for one:

- Leave goal and culture ratings (1-4) as clearly marked placeholders. You may add a suggested rating with its evidence, labelled as a suggestion for them to confirm.
- Add marked placeholders or short questions where only they can judge, such as their own examples, how the person handled things Happily doesn't record, and the overall verdict.
- Never present the draft as finished or submitted.

## Gather evidence in this order

1. `whoami`: connected identity, company and management scope.
2. `get_person_context` for the report, by exact email. A scope denial ends the Happily part.
3. `get_boost_history`: past ratings and recurring development areas, so the new Boost continues them rather than starting over.
4. `get_team_goals` for the person's team: find key results where the person is a listed owner, and use their start, current and target values and last update. A team-owned goal is not the person's achievement unless they own the key result or other evidence ties them to it. Use `get_kr_progress_history` if the trajectory matters.
5. `get_focus_items`: current and carried-over work.
6. `get_person_recognition`: specific contributions others noticed, with dates and who gave them.
7. `get_feedback_threads`, then `get_feedback_thread` for the few threads that bear on the review: concerns raised, agreements and follow-ups. A reply is not a resolution.

Do not skip step 4 because the other tools returned plenty. Key-result results are often the strongest evidence for the goals rating.

## No goals or key results

Many teams and companies don't use goals or key results in Happily. If `get_team_goals` returns none, or the person owns none, say so once, neutrally, and carry on. The Boost still works. It rests on the manager's judgement, supported by past Boosts, focus items, recognition and feedback. The Boost form's own goals section and rating stay; fill them from the work the person actually did. Never invent goals, key results or targets, and never treat their absence as the person's shortfall.

## Get the period right

Every piece of evidence has a date. Say when each contribution happened, using its own date or the period its record names, for example "the July 2026 Boost" or "recognized on 3 Sep". Work out quarters from the calendar: January to March is Q1, and so on. "This quarter" means the quarter containing today. A Boost reviews work from before its own date, so a July Boost's points are not this quarter's work. Recognition or a runbook from September is Q3 work, even if the review is being written in Q4. When the draft covers the period since the last Boost, state that window. If a date is missing, say so instead of guessing.

## The draft

Match the format the manager asks for, and keep it easy to edit and paste. By default:

- **Highlight:** two to four specific contributions, each with its source and date.
- **Goals:** results against owned key results, or the work done when there are no goals, plus the rating or its placeholder.
- **Culture:** how they worked with others, with evidence, plus the rating or its placeholder.
- **Development:** one or two growth areas that build on past Boosts and the manager's view.

After the draft, list in a short note the evidence used, anything stale or missing, and what still needs the manager's input. This skill drafts only. There is no Happily tool to submit a Boost, so tell the manager to paste it into Happily themselves.
