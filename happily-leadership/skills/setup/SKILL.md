---
name: setup
description: Connect Happily, check your account and the team you manage, and choose a weekly brief after your Weekly Insights email plus timely 1:1 prep.
---

Verify that the Happily tools are available. If authentication is needed, use the client's Connect or MCP authentication flow. People sign in on Happily's own page in the browser, with an emailed code or their company's single sign-on. Never ask for a password, passcode or credential in chat, an environment file, or a plugin manifest. Do not substitute backend service-account credentials.

Call Happily `whoami` to verify the person, company, role and team. Explain the actual scope; company-wide access is not implied by being a manager. If the account/company is wrong, stop data collection and help reconnect. A missing employee team for a company administrator is not permission to guess one.

Learn the user's immediate purpose and relevant priorities, language and timezone from context; ask only for missing preferences that affect the work. Offer the leadership brief or 1:1 workflow as the first useful result.

Check which calendar, meeting-note, email or project tools are already available and authorized. These are optional sources, not Happily plugin dependencies. Do not install or authorize another service automatically. Explain which relevant context can be used and which is unavailable. Never claim a disconnected source was checked.

For cross-app work, read [the evidence guidance](../../references/evidence-and-context.md). Use the existing connections through the assistant; do not forward their contents to the Happily server.

After verifying access, offer one concrete ongoing setup: “Would you like a weekly brief after your manager insights email, plus timely 1:1 preparation and alerts only when something meaningful changes?” If the user has already requested this, proceed without asking again. Do not turn installation or connecting an account into consent to monitoring. Each manager chooses their own responsibility; never copy another user's account, company, schedule, baseline or permissions.

Use [proactive leadership](../proactive-leadership/SKILL.md) to configure and verify the responsibility. With an authorized email connection, find recent authentic Weekly Insights for Managers messages for this user and company. Check actual receipt times and timezone before suggesting a Monday time shortly after typical delivery. If the mailbox or pattern cannot be verified, explain that limitation and agree a fallback time; do not require email for Happily-only use. Optional apps remain optional.

Prefer the user's dot for ongoing work when available. Inspect existing matching responsibilities and schedules before saving; extend an existing one instead of duplicating it. Confirm the saved responsibility, cadence/timezone, next run, private delivery destination, coverage, and where to pause it. Read back when the Happily connection ends (`whoami` `access.expires_at`) and say the assistant will warn a week before. Scheduled work only reads, so a connection without write permissions is enough for it. A successful setup conversation without a saved schedule is not completed activation. If the host cannot schedule or the dot cannot access the plugin, provide the precise handoff and mark activation incomplete. Do not substitute a local computer schedule for a cloud dot without explaining the dependency. Installation alone creates no schedule.
