---
name: prepare-one-on-one
description: Walk into a 1:1 knowing what the person moved on their key results, where they're stuck or slower, and where to focus. Combines their Happily goals, focus items and recognition with relevant calendar details and prior meeting commitments. Use when preparing for a 1:1, check-in or coaching conversation with a particular person.
---

Read [the evidence and cross-app guidance](../../references/evidence-and-context.md). Establish the connected Happily identity, company and management scope with `whoami`.

Resolve the target from the user's request or a relevant upcoming calendar event. For “my next 1:1,” use the connected calendar if available, excluding canceled events. Do not treat every two-attendee meeting as a management 1:1. If multiple people/events plausibly match, ask a concise clarification before retrieving personal records. Use exact attendee email and a verified Happily identity; never merge names or infer reporting relationships from the event.

Start with `get_person_goal_progress` for the authorized person, with `window_days` (or dates) covering the time since your last 1:1 with them, 30 days if you don't know. It returns the key results they own, how each moved, its pace and signals, and their focus items split into goal-linked work and work outside any goal. Add `get_person_context` for wider context, `get_person_recognition` for recent recognition, and `get_boost_history` or development context when relevant to the conversation. Team goals can provide context, but do not attribute a team-owned goal to the individual without evidence: ownership is the key result's owner list.

## Focus the conversation on their goals

Use `highlights` to shape the conversation rather than list every key result:

- **Progress.** Key results that moved closer or reached target (`highlights.progress`). Name the change with its numbers and dates. A win the manager hasn't recognized yet is worth an offer to recognize it ([give-recognition](../give-recognition/SKILL.md)); never send it from prep.
- **Where they may be stuck.** Read `highlights.notes_to_read`: the owner's latest notes on key results that need attention often name what's in the way. Quote them as the person's words, not as verified facts. Goal-linked focus items that keep carrying over point at the same thing.
- **Slower-moving items.** `highlights.slower_moving` lists key results behind pace, quiet for a while or never updated. A quiet key result may just be unreported, so ask for the latest number before treating it as behind.
- **What needs a conversation.** `highlights.needs_a_conversation` lists key results off track, at risk or moving the wrong way. Pick the one or two that matter most for the person's goals and turn each into a curious question about support, not a verdict.
- **Work outside their goals.** `highlights.work_outside_goals` is open work linked to no goal. Ask whether it belongs under an existing goal or deserves its own key result; offer to draft one with [update-goals](../update-goals/SKILL.md) only if the manager wants it.

If the person mentions a newer number for a key result during the 1:1 or the manager relays one, offer to record it then rather than wait for the next update round ([update-goals](../update-goals/SKILL.md), preview first). If they own no key result, say so plainly and use their focus items and team goals instead. A scope denial must not be bypassed through another data source. If Happily is unavailable, offer a clearly limited preparation from the independently authorized meeting context.

For the verified report, use `get_feedback_threads` to find relevant recent feedback in the manager's own Happily inbox, then `get_feedback_thread` to read the dated replies for the few threads that could change this conversation. Follow pagination when a selected discussion is incomplete; a filtered empty page with `next_cursor` is not an empty inbox. Look for the employee's concern, the manager's response, an explicit agreement and later evidence. A response or “thank you” does not prove resolution. Do not revive an old concern as new because its update date changed. Explain when a conversation is ongoing, explicitly resolved, or unclear, citing the thread and message dates. Anonymous feedback never appears under a report's email. Don't connect it to the person you're preparing for: don't mention it in their prep at all, and never use it as context for their concerns.

With authorized meeting notes or work communications, find the last relevant 1:1 and any explicit commitments, support requests or decisions since it. Distinguish “no record found” from “not done,” and employee statements from independently measured outcomes. Avoid broad inbox searches and unrelated private calendar details. Do not reconstruct anonymous survey feedback or identify its authors.

Prepare a short, practical private brief:

- Confirm the person and meeting time/timezone, including tentative status where relevant.
- Lead with what moved on their key results and contributions worth recognizing, with sources.
- Name where they may be stuck or slower, in their own words where notes exist, and suggest the one or two areas to focus on given their goals.
- Surface previous commitments that need checking and relevant current focus.
- If the manager wants to change the report's focus as a result, follow [the focus-update skill](../update-focus/SKILL.md): it's a suggestion the report decides on, never a direct edit.
- Suggest a small set of open questions and support offers grounded in the evidence. Use curiosity rather than presenting metrics as a verdict.
- State material gaps or stale evidence that would change the conversation.

Adapt the format to the user. If there is no recorded prior conversation, start with current priorities and support needs instead of inventing a history. Never claim a calendar event occurred merely because it is in the past.

For an authorized ongoing responsibility, use [the recurring-work guidance](../../references/proactive-leadership.md). Reuse existing preparation for this meeting occurrence, check what has materially changed, and avoid a second notification from the weekly brief or calendar watch. The manager's current Weekly Insights email may suggest a question, but corroborate relevant evidence and scope before using personal details.

Keep the private preparation separate from a proposed shared agenda. Do not put sensitive Happily metrics or private third-party notes into calendar descriptions or messages without authorization and an audience check. The skill does not send messages, update events, or change employee records on its own.
