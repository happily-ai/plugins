---
name: update-focus
description: Mark focus items done, reword or add them, and suggest focus to your direct reports, with every change previewed first. Covers marking your own focus items done or open again, rewording or adding one of your own, sending a direct report a focus suggestion (a new wording for one of their items, or a new focus), withdrawing a suggestion you sent, and undoing a change. Every change is previewed as an exact before → after and written only after the user confirms that preview. Use whenever the user asks to mark, tick, close, finish, reopen, reword, rename, add, suggest or undo a focus item, or to change what someone is focusing on.
---

Read [the evidence and cross-app guidance](../../references/evidence-and-context.md). Changing focus is a write to Happily. An incorrect write is unacceptable, so follow this flow every time, even when the user says "just do it" or "no need to confirm".

**Whose focus it is decides what can happen.** Focus items belong to the person who holds them.

- **Your own focus:** you can mark an item done or open again (`set_status`), reword it (`reword`), or add one (`add`).
- **A direct report's focus:** you can't change it. As their direct manager you can send a suggestion: `suggest_reword` for one of their items, or `suggest_add` for a new focus. They see it the next time they open their focus in Happily, with your name on it, and choose to use it, edit it or keep their own. There is no notification, and their reason stays private; you get the short reply they send.
- **Anyone else's focus** (skip-level, other teams, and admins too): view only.

Say this plainly when it matters. Don't present a suggestion as a change, and never say a report's item "was updated".

1. **Find the item.** For a report, call `get_focus_items` first if you haven't. Then call `propose_focus_change` with `email` (omit it for the user's own focus), the item as the user referred to it (`item`, e.g. "alerting"), and one `change`. It writes nothing.
   - `needs_clarification`: show the candidates by their text and status, and ask which one is meant. Never pick one yourself, even if one looks likelier. Re-propose with the chosen `item_ref`.
   - `not_found` or `list_refreshed`: show the current items and ask.
2. **Pass only what the user said.** Use the user's wording for `text` and `note`. Never write or polish a focus item or a "why this matters" note for them. If the wording is missing (`missing_fields`), ask for it. You may offer a tighter version as a suggestion (focus items read best as an action in 6 words or fewer), but propose only the words the user agrees to.
3. **Show the preview.** Show the server's `preview_markdown` exactly as returned, then ask one plain question: "Apply this change?" for your own focus, or "Send this suggestion?" for a report. Don't rebuild the table or paraphrase it.
4. **Apply only on a yes to that preview.** Call `apply_focus_change` with that preview's `confirmation_token` only after the user explicitly confirms *this* preview in their latest message. A yes to an earlier or different preview doesn't count, and neither does a general instruction given before the preview existed. If the user changes anything, propose again.
5. **One change at a time.** Several items mean several previews, each confirmed on its own.
6. **Report honestly.** After `applied`, show `result_markdown` and mention undo (or "withdraw it", for a suggestion). Never say something changed unless `apply_focus_change` returned `applied` or `already_applied`.

When the request isn't something Happily allows:

- **"Mark Priya's alerting one done"** (someone else's status): the result is `scope_denied`. Say that only Priya can mark Priya's items done, and offer the `alternatives` from the result: Priya can tick it in Happily, you can mention it in your reply to Priya's check-in, or you can suggest new wording. Don't retry another way.
- **"Reword / add to Priya's focus"**: the result is `needs_suggestion`. Ask whether to send it as a suggestion instead; on a yes, propose `suggest_reword` or `suggest_add` with the same words and preview it.
- **Remove or delete an item:** there is no remove. Offer to mark it done instead.
- **Carry an item over:** open items stay on the list by themselves. Happily refreshes the list on check-in days, and the refresh may reword, combine or retire items. Nothing needs doing.

Handling results:

- `conflict`: the list changed after the preview (it was refreshed, or an item was ticked in the app), and nothing was written. Say so and offer a fresh preview.
- `expired` or `invalid_token`: propose again and ask the user to confirm the new preview.
- `suggestion_limit`: the person already has 2 suggestions waiting. Say when they clear, and offer to withdraw one of the user's own (`your_pending_suggestions`).
- `suggestion_pending_for_item`, `duplicate_item`, `no_change`, `no_focus_list`: explain the reason in one line.
- `write_not_granted` or `not_configured`: this connection can't change focus. Tell the user what to do in Happily themselves.
- `cannot_revert`: the item changed since, so offer a direct change instead.
- `not_confirmed`: the user declined in their app's confirmation prompt. Nothing was written.
- Undo: `propose_focus_change` with `change.kind` `revert_change` and the earlier `change_id`. Undoing a suggestion withdraws it.

To read focus, use `get_focus_items`. It shows each item's status (open or done), what carried over, and, for the direct manager, their own suggestions still waiting. Quote items by their text, never by position.
