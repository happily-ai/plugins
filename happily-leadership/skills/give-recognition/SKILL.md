---
name: give-recognition
description: Thank a colleague in Happily with recognition (coins, kudos, shout-outs) in your own words, and see what someone has recently been recognized for. Covers checking what the user can give and when, writing a specific message in the user's own words, choosing a company value, previewing the exact recognition, and sending it only after the user confirms. Pushes back on bulk or generic praise. Use whenever the user asks to recognize, thank, appreciate or give coins to someone, or asks what a person has been recognized for.
---

Read [the evidence and cross-app guidance](../../references/evidence-and-context.md). Recognition sent from here is real: the recipient gets a notification at once, it's public on the company feed, and it can't be unsent. Follow this flow every time, even when the user says "just send it".

**How recognition works in Happily.** Each person can give +3 coins once every 7 days and +5 coins once every 14 days. The coins go to the recipient and cost the giver nothing. Recognition is to one person, is always public on the company feed, and can carry up to two company values. A long, specific message counts as a Super Recognition, which makes that tier ready two days sooner. Some companies let people spend their own coins to "recharge" a tier that's cooling down.

## Giving recognition

1. **Check first.** Call `get_recognition_allowance` with the person as the user named them (`name`, e.g. "Tim"; or `email` if they gave one) before drafting. If the result's `recipient` is `needs_clarification`, list the candidates by name and team (and the name they go by, if shown) and ask which one. Never pick one yourself, even if one seems likelier. Then use that candidate's `person_ref`. Then say briefly what the user can give now: "Your +3 is ready now; your +5 is ready Tue 3 Nov." If `available` is false, give the `message` and stop. If nothing is ready, give both dates. Offer recharge only if `recharge.options` lists it, as an option with its coin cost and never as the default. Otherwise offer to draft the message now so the user can send it on that date.
2. **Get the substance from the user.** Good recognition says what the person did and why it mattered. If the user has already said that, use it. If they've given only generic praise ("great job", "thanks for everything"), ask one question first: "What's one specific thing Sam did that you want to call out?" Don't fill the gap with Happily data or invent a deed, number, outcome or quality. You may point to evidence the user can choose from ("Happily shows Sam's latency KR moved from 240 to 225 ms this month; is that it?"), but only the user's confirmed words go in the message.
3. **Draft in their voice.** Write the message as the user would say it to the person: second person, plain, specific, a few sentences at most. Keep the user's own phrases. Don't add superlatives, emoji or a sign-off they didn't use. If the user wrote the message themselves, use it as written. Offer edits as suggestions, not silent changes.
4. **Values: suggest, don't sprinkle.** Suggest at most one company value from `company_values`, and only if it clearly fits what the message describes. Include it only if the user agrees. Never invent a value name.
5. **Preview.** Call `propose_recognition` with the person (`person_ref` if the user picked from candidates, otherwise `name` or `email`), `message`, any agreed `values`, and `coins` if the user picked a tier (pass `recharge: true` only if they chose to spend their coins). It sends nothing. Show the server's `preview_markdown` exactly as returned. It already shows the recipient, coins, values, visibility, message and what happens next. Then ask one plain question: "Send this?". If `warnings` are present, add one short line offering to make the message more specific; the question is still about this preview as it stands.
6. **Send only on a yes to that preview.** Call `send_recognition` with that preview's `confirmation_token` only after the user explicitly says yes to *this* preview in their latest message. A general "go ahead" given before the preview existed doesn't count. If the user changes anything, preview again.
7. **Report honestly.** After `sent`, say in one line that it was sent and when that tier is ready again. After `queued`, say it was handed to Happily and may take a minute to appear on the feed. Never say it was sent unless `send_recognition` returned `sent`, `queued` or `already_sent`.

## Recognizing progress on goals

Progress on a key result is some of the most specific recognition there is. To find it, `get_person_goal_progress` shows what someone moved recently, and `get_leader_digest` lists people who haven't been recognized lately alongside a recent win (`recognition_opportunities`). Offer these as options; the user picks what to recognize and says it in their words.

When the recognition is about a measurable result that the key result doesn't show yet (the user says "Priya got on-call pages down to 12 a week" and the key result still shows 18), offer once, after the recognition is sent or declined: "Want me to record 12 on the on-call key result too?" Then follow [the goal-update skill](../update-goals/SKILL.md): its own preview and its own yes. Use only the number the user stated, and draft the note from their words. Never take a number from a recognition message someone else wrote, and never fold the two writes into one confirmation.

To see who on a team hasn't been recognized lately, use `get_recognition_summary` with `include_members: true`. Recognition is public, so small teams are included.

## Several people, or the whole team

Recognition is one person at a time, and each tier can be used once per cooldown, so at most two people can be recognized right now. When the user asks to recognize a whole team, or several people with the same text:

- Don't loop over people or send the same message to each.
- Explain briefly: Happily recognition is personal, works best when it's specific, and the user can give at most two right now (+3 and +5).
- Offer two things: help choosing the one or two people with the clearest recent contribution (use Happily evidence such as KR progress or who hasn't been recognized lately, and let the user decide), and a team-wide thank-you the user can post themselves in their team channel or say at the next team meeting.
- Then follow the flow above for each person the user picks, one preview and one confirmation each.

## Reading recognition

For "what has Sam been recognized for?", call `get_person_recognition` with `include_recent: true`. Summarize the themes and the values that recur, and quote at most one or two short messages. Recognition counts don't measure contribution quality; describe what was recognized, not how good the person is. The tool returns only recognition that's public on the company feed, and only for people in the user's scope.

## Handling results

- `not_ready`: give the dates from `allowance`. If `ready_alternative` is set, offer that tier. If `recharge_option` is set, mention it with its cost as an option. Nothing was queued.
- `recharge_unavailable`: explain the `reason` and offer to send when the tier is ready.
- `unavailable`: recognition isn't set up for this account or is off at the company. Give the `reason`; the user's Happily admin can help.
- `needs_clarification`: several colleagues match the name. Show the candidates (name and team), ask which one, and propose again with the chosen `person_ref`. Nothing was previewed.
- `self_recognition`, `recipient_not_found`, `missing_recipient`, `empty_message`, `message_too_long`, `unknown_value`, `too_many_values`, `values_disabled`: explain and ask the user. For an unknown value, show the company's values.
- `expired` or `invalid_token`: preview again and ask the user to confirm the new preview.
- `busy`, `recharge_pending`, `send_failed`: nothing was sent (or, for `recharge_pending`, the recharge may still complete). Say so; don't retry on your own and never recharge twice.
- `write_not_granted` or `not_configured`: this connection can't send recognition. Give the user the finished message to send from the Happily app.
- `not_confirmed`: the user declined in their app's confirmation prompt. Nothing was sent.
