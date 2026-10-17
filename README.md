# AVS Cleaning Services: Autopilot

Automation that takes the admin and outreach prep off Alexandre's plate, so his time goes on calls,
emails and closing.

## How it works
Three scheduled Claude runs read Gmail, Airtable, Stripe and Tally, then **prepare** everything:
replies, quotes and follow-ups appear as **Gmail drafts**, Airtable is kept up to date, and a short
brief is pushed to his phone. Nothing is ever sent to a client, prospect or cleaner automatically.

| Run | When (UK time) | Playbook | What you get |
|---|---|---|---|
| Daily Autopilot | Mon-Fri 07:55 | [`autopilot/daily.md`](autopilot/daily.md) | Morning brief, 10-name call list, drafts for follow-ups / quotes / applicants / prospect replies, CRM updated, ops alerts |
| Monday Prospecting | Mon 08:52 | [`autopilot/weekly-prospecting.md`](autopilot/weekly-prospecting.md) | 15 new researched prospects in Airtable + personalised first-email drafts |
| Friday Review | Fri 15:57 | [`autopilot/friday-review.md`](autopilot/friday-review.md) | Scorecard vs £15k target + next week's top 3 actions (written to Management Actions) |

Facts, prices, rules and Airtable IDs all live in [`autopilot/business.md`](autopilot/business.md).
**Change prices or rules there**, then ask Claude to "sync the autopilot tasks" so the scheduled runs
pick up the change.

## Alexandre's daily loop (≈10 min admin)
1. Read the morning brief on your phone.
2. Open Gmail → Drafts. Skim and send (or tweak). Attach the insurance PDF where the brief says so.
3. Work the call list. After each call, change the lead's **Sales Stage** in Airtable
   (Interested / Quote Sent / Won / Lost). The autopilot schedules the follow-ups from there.

## Follow-up cadence
Day 0 first email → Day 5 nudge (new angle) → Day 12 close-the-loop → Lost + 90-day nurture check-in.
A reply at any point stops the sequence and moves the lead to the top of the call list.
