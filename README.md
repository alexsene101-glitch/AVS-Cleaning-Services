# AVS Cleaning Services

Notes and source for the automation around AVS Cleaning (Birmingham). The live system is **AVS OS**:
scheduled Claude tasks plus a few artifact pages, with Airtable as the system of record.

## What runs (claude.ai → Scheduled tasks)
| Task | When | Does |
|---|---|---|
| AVS OS sync | Hourly (full 06:00, light 18:00, quick otherwise) | Gmail replies, booking-form acknowledgements, **price-list quote drafts with a Stripe payment link**, applicant vetting, outreach follow-ups, Stripe → Airtable, AVS OS snapshot |
| AVS daily lead outreach | Weekdays 09:47 | Finds new leads, sends cold emails and one follow-up, hands interested leads over |
| AVS daily job briefing | Hourly | Job briefing |
| AVS applicant tracker | Daily 21:52 | Records applicants from Gmail and the "Clean with AVS" form in Airtable |
| AVS Friday pay run | Fri 08:56 | Who to pay this week |

Airtable is on the free plan (1,000 API calls a month), so every task rations its calls.

## Quoting
The "Book an AVS Clean" form (https://tally.so/r/rjNdDM) shows the customer a fixed price (furnished +15%).
AVS OS sync acknowledges the booking, then saves a **Gmail draft** with the quote and a Stripe payment link.
Alexandre reviews and sends it. Anything off the price list comes to him as "Price needed".
Prices live in [`autopilot/business.md`](autopilot/business.md); if they change, the AVS OS sync task and the
form must be updated too.

## Calling
[`tools/prospect-tracker.html`](tools/prospect-tracker.html) is the AVS Prospect Tracker
(https://claude.ai/artifact/KeVkbjC5z52KAXCaVheGVg). Tap **Call** on a prospect for a tailored opener,
objection handlers and the price card, then log the outcome (no answer, voicemail, interested, trial booked,
not now). Follow-up dates set themselves. "Interested" offers a ready-to-paste rates email. It uses the page's
own storage, so it costs no Airtable calls.
