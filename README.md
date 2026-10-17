# AVS Cleaning Services: Autopilot

Automation that takes the admin and outreach prep off Alexandre's plate, so his time goes on calls,
emails and closing.

## How it works
Four scheduled Claude runs read Gmail, Airtable, Stripe and Tally, then **prepare** everything:
replies, quotes and follow-ups appear as **Gmail drafts**, Airtable is kept up to date, and a short
brief is pushed to his phone. Nothing is ever sent to a client, prospect or cleaner automatically.

| Run | When (UK time) | Playbook | What you get |
|---|---|---|---|
| Daily Autopilot | Mon-Fri 07:55 | [`autopilot/daily.md`](autopilot/daily.md) | Morning brief, 10-name call list, drafts for follow-ups / quotes / applicants / prospect replies, CRM updated, ops alerts |
| Monday Prospecting | Mon 08:52 | [`autopilot/weekly-prospecting.md`](autopilot/weekly-prospecting.md) | 15 new researched prospects in Airtable + personalised first-email drafts |
| Quote Desk | Every hour 08:07–20:07 | [`autopilot/quote-desk.md`](autopilot/quote-desk.md) | Each booking-form submission turned into an Airtable record, a Stripe payment link and a quote draft, inside the form's 2-hour promise |
| Friday Review | Fri 15:57 | [`autopilot/friday-review.md`](autopilot/friday-review.md) | Scorecard vs £15k target + next week's top 3 actions (written to Management Actions) |

Facts, prices, rules and Airtable IDs all live in [`autopilot/business.md`](autopilot/business.md).
**Change prices or rules there**, then ask Claude to "sync the autopilot tasks" so the scheduled runs
pick up the change.

## Call Cockpit
[`tools/call-cockpit.html`](tools/call-cockpit.html) is published at https://claude.ai/artifact/S52EFfpAZCD7JTmjUEGDfV.
It reads the Airtable Customers table live and sorts leads into three queues: **Warm** (replied, interested,
quote out), **Follow-up** (emailed 2+ days ago or due today) and **Cold** (phone-only, never contacted).
Each lead gets a tailored opener, objection handlers and the price card. Pick an outcome and save: Sales Stage,
Next Follow-up and a dated call note are written back to Airtable. "Interested: send rates" makes the next
Daily Autopilot draft the rates email.

## Alexandre's daily loop (≈10 min admin)
1. Read the morning brief on your phone.
2. Open Gmail → Drafts. Skim and send (or tweak). Attach the insurance PDF where the brief says so.
3. Open the Call Cockpit and work the queues. Log every call with one tap; the autopilot does the follow-up.

## Follow-up cadence
Day 0 first email → Day 5 nudge (new angle) → Day 12 close-the-loop → Lost + 90-day nurture check-in.
A reply at any point stops the sequence and moves the lead to the top of the call list.
