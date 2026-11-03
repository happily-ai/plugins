---
name: keep-key-results-current
description: Keep key results up to date from the apps their numbers come from (HubSpot, spreadsheets, analytics and other connected tools). Covers setting up how a key result is measured and refreshed (its source, counting rule, owner mapping, cadence and note format, saved on the key result itself) and running the refresh: pulling each number from its source and previewing every due update together for one confirmation. Use when the user asks to refresh, sync or update key results from a source, to set up or change how a key result is tracked, for a weekly or monthly update round, or when a scheduled task asks for due key results.
---

Read [the evidence and cross-app guidance](../../references/evidence-and-context.md), [the update recipe guide](../../references/update-recipes.md) and [the goal-update skill](../update-goals/SKILL.md). Every write follows the goal-update skill: preview first, apply only on the user's yes to that exact preview.

A key result's **update recipe** is plain text in its `description`, starting with "How this is updated". It says where the number comes from, what counts, how each owner's number is found, how often to refresh, and what the update note says. `get_team_goals` returns it. The Happily console doesn't show it, but keeps it through edits and copies it to next quarter's key result. The recipe is shared: anyone's assistant, in Claude or ChatGPT, refreshes the key result the same way.

## Setting up a recipe

Do this when a key result has no recipe and the user wants it kept current, or when they create a key result whose number lives in another app.

1. **Find the source.** Ask where the number lives today and how they'd check it by hand. Use only connectors the user has here; if the source isn't connected, say so and stop.
2. **Agree the rule in their words.** What counts and what doesn't, the time window, which amount or field, how each owner's number is found, the unit and currency. Point out choices that change the number (for example open versus closed deals, created date versus last activity) and let the user decide. Don't settle them yourself.
3. **Run it once and show it.** Pull the current numbers, per owner when the key result is split, with a short list of what's included. Flag anything that looks wrong, such as items with no amount or values in another currency, and agree how to treat it.
4. **Save the recipe.** Write it in the recipe format from the guide and preview it as `edit_key_result` with `description`. Include the cadence (weekly, monthly, quarterly) and the day.
5. **Log the first values.** For a new key result, pass them when creating it (`current_value`, or `owner_values` per owner) with the recipe as its `description`, so it is created current in one preview. For an existing key result, put the recipe and the first values in one `propose_goal_changes` batch. If the source has no number yet, create the key result with `awaiting_measurement: true` and no `current_value`, and say it will read "Not measured yet" until the first refresh. Never log 0 as a stand-in.

## Refreshing

Do this when the user asks to refresh key results, or a scheduled task asks for the due ones.

1. **Find what's due.** Call `get_team_goals` for the team. Take key results whose description starts with "How this is updated", that aren't past (`cycle_state` past) or updated automatically by Happily, and whose last update is older than their cadence. Include any the user named, due or not.
2. **Pull each number exactly as its recipe says.** Same filters, same window, same field, same owner mapping. Don't improve the rule on the fly.
3. **Hold what you can't trust.** If the source returns something the recipe says to hold (for example an owner whose items have no amount), leave that update out and say why. A key result still Awaiting first measurement stays that way until the source returns a real number; its first refresh is a normal `update_progress`. If the source has nothing yet, leave it out and say it's still not measured.
4. **Preview everything together.** Put every update into one `propose_goal_changes` call (up to 10 per team; run another batch for more). Use the recipe's note format, with the key fact first. Show `preview_markdown` and ask once.
5. **Apply on yes**, then say in one line what moved and what was held.

When a refresh needs a judgment call the recipe doesn't cover, such as a new owner who isn't in the source or a new kind of item, ask the user. Then offer to add their answer to the recipe (`edit_key_result` with `description`) so it's settled next time.

## Scheduling

Claude and ChatGPT can run "refresh the key results that are due for <team>" on a schedule. A scheduled run pulls the numbers and lists the updates it would make, then asks the user. It never applies on its own. Confirmation tokens last ten minutes, so when the user says yes later, call `propose_goal_changes` again with the same numbers (pull them again if the source may have moved), show that preview and apply on a yes to it. Suggest a schedule that matches the shortest cadence among the team's recipes.

Key results that Happily updates automatically from a connected app (`automated_kr`) are kept current by Happily. Leave them out.
