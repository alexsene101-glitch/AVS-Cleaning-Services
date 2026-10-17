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

## One-tap admin (AVS OS)
[`tools/avs-os.html`](tools/avs-os.html) is the AVS OS page (https://claude.ai/artifact/M61V3BACQanML2ttEevhr9).
Its buttons write to Airtable directly through your Airtable connector:
- **Bookings:** Quote sent, Paid, Lost, and Create job. Create job makes the Job Card and gives you a
  WhatsApp offer to copy to the cleaner.
- **Jobs:** Cleaner accepted, Completed, Photos OK (approve pay), Cleaner paid (with a bank reference).
- **Cleaners:** tick the vetting checks and set the insurance expiry date.
- **Needs you:** Done clears an item, and the hourly sync won't add it back.
- **Call times:** add slots and the sync offers them to vetted applicants by email.

Each tap uses one Airtable call. [`autopilot/avs-os-sync-prompt.md`](autopilot/avs-os-sync-prompt.md) is a
copy of the live hourly sync instructions.

The Sunday money check-in now pulls Wise through Era by itself and only asks for statements from the banks
that aren't connected.
