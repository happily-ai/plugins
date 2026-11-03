# Recurring leadership work

## Weekly Insights is an input, not a second brief to forward

Find the authentic Happily Weekly Insights for Managers email for the connected manager and company using authorized email tools. Match the sender, recipient, subject and reporting period; forwarding to another authorized mailbox does not change the report's audience. Read the actual content. Never infer a current report from a search snippet, send date alone, or an old email with a similar subject. Do not search unrelated mailboxes or inspect every employee by default.

Treat the report as a dated synthesis that can lag current events. Attribute its claims to the report until corroborated. Read its relevant linked sources where available, check current Happily evidence, and connect only verified identities/teams. Different periods, denominators or metric definitions are not conflicting facts to average together. An individual mentioned in a report is not proof of a reporting relationship or permission to bypass Happily's scope or anonymity limits.

The brief should answer: what changed since the report, what previous commitment this relates to, and which upcoming conversation or decision can address it. Recognize verified wins as well as risks. A report recommendation is not proof the manager accepted it or that an action remains unfinished.

If the current report has not arrived at the agreed time, label that gap and use fresh available sources. Retry once at the agreed later time (suggest noon on Monday). Send an addendum only if the newly arrived report changes a decision; otherwise update the private baseline silently. Report an ongoing access/delivery problem once, not on every check. Never present the previous report as this week's.

## Minimal private state

Keep state in the host's durable private responsibility notes or supported task storage, not the shared plugin, source repository or Happily server. Include:

- Responsibility identity, user/company/scope, timezone, saved schedule IDs, sources and known credential expiry.
- Last successful source checks and coverage; report message ID and reporting period already consumed.
- Stable finding keys (source + entity + issue/commitment), last observed status/value/period, source date, owner/due date when verified, and last delivered state/time.
- Meeting occurrence identity (calendar event UID/original occurrence where available), current time/status, matched person, existing prep link, evidence revision and last delivered prep revision.

Store short facts and source references rather than full employee narratives, emails, transcripts or credentials. Use one responsibility to coordinate weekly briefs and watches where possible. Independent schedules must share state; serialize updates if supported. If the host cannot provide reliable shared state, consolidate under one responsibility or disclose the limitation. Recheck delivery history before notifying to avoid overlapping runs repeating the same finding.

## Start each check from the digest

Call `whoami` first. If `access.expires_in_days` is 7 or fewer, tell the user once, with `access.renewal`, and record that you did. Then call `get_leader_digest` with `start_date` set to the last successful check minus two days (the overlap catches late updates) and `end_date` today. Every row carries a `finding_key`. Compare those keys, and each row's `signals`, with the delivered history: a key you already delivered with the same signals is not news. Read `get_person_goal_progress`, `get_kr_progress_history` or a feedback thread only for the few findings you are about to raise.

## Moments worth a heads-up

The digest applies the first gate: whether a signal is worth a look. You apply the second: whether it is new, actionable now, and worth this leader's attention. Thresholds are editable defaults; save the leader's changes in the private state.

| Moment | Where it shows up | Raise it when |
| --- | --- | --- |
| A key result reached its target or moved closer | `goal_movements` (`reached_target`, `moved_closer`) | Always worth one line in a brief. Pair it with a recognition offer when the owner hasn't been recognized lately. |
| A key result slipped | `goal_attention` (`off_track`, `at_risk`, `behind_pace`) or `goal_movements` (`moved_back`) | The first time a key shows a worse signal than the baseline. Not again until it gets worse, recovers or its cycle is ending. |
| A key result went quiet | `goal_attention` (`stalled`, default 21 days; `never_updated`) | Once when it crosses the gate. Group never-updated ones into one line. |
| Work was finished but the number wasn't updated | `kr_update_opportunities` | Offer to update now instead of waiting for the next round (see the goal-update skill). Finished work is a reason to ask for the number, never the number itself. |
| Someone hasn't been recognized lately | `recognition_opportunities` (default 45 days) | At most one nudge a week, naming the specific win in `recent_wins`. Skip people with no win to name. |
| A goal or key result would help | `goal_suggestions` (`work_outside_goals`, `no_key_result`, `team_without_goals`, `next_cycle_due`) | At most one a week, and `next_cycle_due` in the last three weeks of a cycle. Offer a draft; never create one unasked. |
| Feedback is waiting for a reply | `feedback_waiting` | After two working days, once more at five, then stop. Names and counts only. |
| A 1:1 is coming up | The host calendar | Once per occurrence, within 24 hours (Friday covers Monday morning). |

Engagement and pulse movement come from `get_team_trend_history` and `get_pulse_trend`, not the digest. Raise a drop only when it persists (two weeks or two months in a row) or another source corroborates it, and only as a team-level observation.

## The notification budget

- A weekly brief: at most three actions and one win.
- Unchanged findings are never listed again. One line can count them ("5 earlier items are still open"). A check with nothing new is one line or no message, never a recap.
- Between briefs: at most one message a day and three a week. Anything over budget waits for the brief, ranked by how soon it needs action.
- No watch messages outside the leader's working hours, apart from the Friday lookahead.
- If the leader dismisses a kind of heads-up three times in a row, ask once whether to drop it or change its threshold, and save the answer.

## What a notification may contain

A message can land on a lock screen or in a shared channel. Use names, counts, dates, key result titles and links. Never quote feedback text, key result notes or focus item texts in it; keep those in the conversation the leader opens. Anonymous feedback is a count on its own line.

## What earns a notification

Notify for a materially changed decision, risk, verified progress/resolution, owner or deadline; a newly relevant commitment; or a meeting entering its preparation window with no suitable prep. A deadline approaching can make an unchanged item actionable, but explain the new timing and suppress duplicate reminders within that window. Use the moments above and the user's priorities, not engagement scores on their own.

Do not notify just because a tool was polled, a source timestamp advanced, a document was edited without a relevant change, a metric moved within incomparable coverage, or a known gap remains. Do not repeatedly list all outstanding concerns. Check the dot's existing email/calendar alert history and link or extend its existing work instead of sending a second version. Establish a first baseline without calling old findings new. If previous state is unavailable, say so once and rebuild it; do not invent a comparison.

Prepare once per real meeting occurrence. A recurring series gets a new occurrence, not a permanent “already prepared” flag. Cancelled meetings do not need prep. A time-only reschedule updates existing prep and warrants a concise notice only if it changes the user's plan; it is not a fresh substantive brief. A new commitment or material signal can justify an updated prep. Confirm meetings are appropriate management conversations before retrieving personal evidence. Friday's final check may include Monday morning meetings so the 24-hour window does not miss them over the weekend.

When sources fail, preserve the last valid baseline and label freshness. Unknown completion is not unfinished work; a missing issue is not a resolved issue. Alert once for a blocking connection failure, then only on a relevant state change or recovery. Before a known credential expiry, notify once; after expiry stop Happily-dependent checks/claims until renewed access is verified. Do not mint or extend credentials. Tell the user if the remaining calendar/email work continues under their existing authorization.

Scheduled and watch runs never write. They may offer an update, a recognition or a reply. When the leader says yes in the conversation, start the normal preview flow then: confirmation tokens last ten minutes, so a preview made during a scheduled run has expired by the time it is read. Suggest a read-only Happily connection for scheduled work; write consent can be given when the leader acts.

All output is private to the requesting user unless a separately authorized audience is specified. Preparing a brief does not authorize emailing a colleague, writing employee records, posting in team channels or adding sensitive context to calendar descriptions.

## Feedback conversations and changed evidence

For a relevant report, use `get_feedback_threads` over the period since the previous successful check, with a small overlap to account for index timing. Use `get_feedback_thread` for selected new or updated discussions. Dates on the source index may represent wall time stored as UTC; preserve message dates/timezones and do not invent exact instants. Keep thread IDs, message positions and the last observed reply or commitment in the same private baseline used by weekly briefs and 1:1 preparation. Do not save bulk conversation text or reproduce it in notifications.

An updated thread is a reason to inspect, not automatically a notification. A routine acknowledgment, unchanged concern or the manager's own already-known reply does not merit another alert. Notify when new evidence changes the needed action, a commitment changes, a concern is explicitly resolved, or an upcoming 1:1 creates a timely need to prepare. A reply count or `source_replied` flag cannot establish resolution. If source access fails or pagination remains incomplete, retain the last successful baseline and disclose the material gap; never mark missing threads resolved. Cross-check an explicit resolution against later contradictory evidence before retiring a prior alert.

This access is limited to feedback in the connected manager's own inbox. Named threads come from current reports. Anonymous threads carry no identity: never try to attribute them. It does not authorize other managers' conversations, private coaching sessions or external messages. Do not bypass denial by querying another source. Scheduled and watch runs never propose or send replies. They may say that feedback is waiting for the manager's answer.
