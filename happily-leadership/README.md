# Happily

Lead with what's actually happening on your team. Happily brings your team's goals and key results, recognition, feedback and engagement into Claude and ChatGPT for managers and leaders whose company uses [Happily.ai](https://happily.ai).

## What you can do

- **Get a weekly heads-up.** See which key results moved, which stalled or fell behind pace, who hasn't been recognized lately and which feedback is waiting for your reply.
- **Prepare for a 1:1.** Each person's progress, blockers and slower-moving goals, plus the work they've finished, in one place.
- **Keep key results current.** Mention a new number and Happily previews the update for you to confirm, without waiting for the next check-in.
- **Recognize good work** in your own words, tied to a company value.
- **Reply to feedback** in your own voice, including anonymous feedback, one reply at a time.
- **Understand your team.** Engagement trends, participation, development skills and Boost history, with every metric explained in plain language.

Try asking:

- "What moved on my team's goals this week?"
- "Help me prepare for my 1:1 with Jordan."
- "Who on my team should I recognize?"

## Install

In Claude Code:

```
/plugin install happily-leadership --marketplace happily-ai/plugins
```

On claude.ai, add Happily from the plugin directory.

## Skills

| Skill | What it does |
| --- | --- |
| **Set Up Happily** (`setup`) | Connects Happily, checks your role and team, and offers a weekly brief. |
| **Weekly Heads-up** (`proactive-leadership`) | Runs a regular check that reports only what's new since last time. |
| **Leadership Brief** (`leadership-brief`) | Shows what needs your attention from goals, team signals and commitments. |
| **1:1 Prep** (`prepare-one-on-one`) | Prepares a 1:1 from the person's goals, focus, recognition and feedback. |
| **Update Goals** (`update-goals`) | Creates and updates goals and key results, previewing every change first. |
| **Sync Key Results** (`keep-key-results-current`) | Keeps key results in step with the apps their numbers come from. |
| **Update Focus Items** (`update-focus`) | Marks focus items done, rewords them and sends focus suggestions. |
| **Give Recognition** (`give-recognition`) | Writes and sends recognition after you confirm the preview. |
| **Reply to Feedback** (`reply-to-feedback`) | Reads and replies to feedback in your Happily inbox. |
| **Draft a Boost** (`draft-boost`) | Drafts a Boost or other performance review from real evidence. |
| **Development Plan** (`development-plan`) | Builds a development or growth plan for someone on your team. |

## How it keeps your team's trust

- You only see what you can already see in Happily. Your role and team decide every answer.
- Survey and engagement results for groups smaller than four people stay hidden, and anonymous feedback stays anonymous.
- Nothing changes in Happily until you confirm an exact preview. You choose which kinds of changes to allow when you connect, and your company admin can turn connections off at any time.
- Recognition and feedback replies can't be unsent once you confirm them.

## What it connects to

This plugin connects to one service: the Happily MCP server at the URL in `.mcp.json`, run by Happily.ai. You sign in with your Happily account through OAuth. Requests carry only the inputs each tool needs, such as a team, a person or a date range, and answers come from your Happily workspace. The plugin has no hooks and runs no local code.

Some skills can also use other connectors you've already authorized in your assistant, such as your calendar or meeting notes, when you ask them to. Happily doesn't receive that data unless a skill writes a change you confirm.

## Requirements

- A Happily.ai account.
- Your company admin turns on AI assistant connections in Happily.

## Privacy and support

- Privacy policy: https://happily.ai/privacy-policy
- Terms of service: https://happily.ai/terms-of-service
- Help and support: https://happily.ai/ai-assistants#help or support@happily.ai
