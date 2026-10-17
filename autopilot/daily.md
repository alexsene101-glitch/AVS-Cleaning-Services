# AVS Daily Autopilot (weekdays, before 8am)

Goal: by the time Alexandre picks up the phone, every admin task is either done or sitting as a ready-to-send
Gmail draft, and he has a call list. Read `business.md` first; its hard rules override everything here.

Look-back window: since the last weekday run (Monday covers Fri 07:00 onwards). Today's date is in London time.

## 1. Inbox sweep
Search Gmail `in:inbox newer_than:3d -category:promotions` (read full threads with get_thread, not previews).
Classify each new inbound message:
- **Prospect reply**: sender email/domain matches a Customers record. Go to step 2.
- **New client enquiry**: someone asking for a clean/quote, plus new Tally "Book an AVS Clean" submissions
  and new Airtable Booking Requests. Go to step 3.
- **Cleaner applicant**: Indeed (`indeedemail.com`), Tally "Clean with AVS", or applicant emails. Go to step 5.
- **Cleaner / job message**: an existing cleaner about a job. Summarise it in the brief.
- **Bounce** (mailer-daemon "failed permanently" / "Address not found"): set that Customer's Outreach Status = Bounced,
  add a note, and list it under "find a phone number".
- **Auto-reply**: note it on the Customer record. No other action.
- Ignore newsletters, receipts and personal mail.

## 2. Prospect replies
For each one, update Airtable Customers: Outreach Status = Replied; Sales Stage = Interested (positive),
Lost (no / not now; set Next Follow-up +90 days for a nurture check-in), or Do Not Contact (opt-out).
Positive or question: draft a reply in the thread that answers exactly what they asked, using the price list. Push for
a 10-minute call or the chance to quote their next changeover. If they ask for insurance, say the certificate is
attached and flag "ATTACH INSURANCE PDF" in the brief, because drafts can't carry the attachment.
Put every replied prospect at the TOP of today's call list.

## 3. New enquiries → quote drafts
1. Make sure an Airtable Booking Request exists; create one if not (Status per the table's options).
2. Extract: property type, bedrooms, clean type, furnished?, area/postcode, preferred date, frequency.
3. If anything needed to price is missing, draft a short reply asking only for those details.
4. Otherwise draft the quote (premium tone, itemised price from the price list, what's included, recurring option
   if it fits, Stripe prepayment terms). Put the price in Booking Request → Quote. Do NOT tick Quote Sent; Alexandre
   ticks it when he sends.
5. Anything not on the price list: no number. Flag it as "needs custom price".

## 4. Follow-ups due
Query Customers where Next Follow-up <= today AND Sales Stage in (Contacted, Quote Sent, Follow-up, Interested)
AND Outreach Status not in (Replied*, Bounced, Opted Out). (*Interested/Replied leads with no response from us in
2+ working days still count.)
For each: find the thread (id in Customer Notes, else search `in:sent to:<email>`). Count OUR sent messages
in it:
- 1 sent → **Touch 2**: 2-3 line nudge with a new angle (photo report proof, 48h re-clean guarantee, availability
  this week, end-of-tenancy season). Ask one question.
- 2 sent → **Touch 3, close the loop**: polite last note ("I'll leave it here; if cleaning ever comes up, here's my
  number"). Then Sales Stage = Lost, Next Follow-up = +90 days.
- Quote Sent with no reply → nudge about the quote, and offer a call or a trial clean.
- 3+ sent → no draft. Set Sales Stage = Lost, Next Follow-up = +90 days.
After drafting: Sales Stage = Follow-up, Next Follow-up = +5 working days, and add the note "Touch N drafted <date>".
Don't change Last Outreach Date until the draft actually appears in `in:sent`. On each run, check yesterday's drafts:
if they were sent, set Last Outreach Date to the send date.
Cap at 25 follow-up drafts per day; the oldest due go first.

## 5. Cleaner applicants
Follow the AVS Cleaner Applicants rules: self-employed, paid per job, own public liability insurance required,
areas, next step is the "Clean with AVS" Tally form + availability. Apologise if they chased. Reply in the Indeed
thread (draft). Make sure each applicant exists in Recruitment → Applications (create if missing).

## 6. Ops check (Airtable + Stripe)
- Job Cards dated today or tomorrow: no Assigned Cleaner, Acceptance Status not accepted, Offer Response Overdue,
  Late Arrival Alert Needed.
- Booking Requests where Customer Accepted = true and Payment Status not paid: check Stripe (paid checkout sessions /
  payment links, last 7 days). If Stripe shows it paid, flag "PAID - ready to dispatch" (do not dispatch automatically).
- Completion Reports awaiting QC; Ready to Pay queue count.
- Cleaners with Insurance Alert = EXPIRING / EXPIRED.
- Anything from a client or cleaner unanswered for 48+ hours.

## 7. Today's call list (10 names)
Rank in this order:
1. Prospects who replied / are Interested / have a quote out (call within 24h of a reply).
2. Prospects emailed 2-7 days ago with no reply who have a phone number ("I sent you a note on Thursday…").
3. Phone-only leads never contacted (Sales Stage empty or New Prospect, Phone present, not "Not a fit").
For each: name, number, why today (one line), a one-sentence opener, and the single ask (book a 10-min call /
quote next changeover / trial clean). If a high-value lead has no number, look up the public business number on their
website and write it to Airtable Phone.

## 8. Output: the morning brief (this final message is pushed to Alexandre's phone)
Keep it under ~350 words, in this order, and leave out any section that is empty:
```
AVS Morning Brief, <Day DD Mon>
🔥 Hot: <replies / paid jobs / anything urgent, 1 line each>
📞 Call list (10): Name · number · why · opener
✉️ Drafts ready in Gmail: N follow-ups · N quotes · N applicant replies · N prospect replies
⚠️ Ops: <unassigned jobs, unpaid accepted quotes, QC/payments waiting, insurance>
🧹 Done for you: <Airtable updates made, bounces marked, records created>
Pipeline: contacted N · replied N · quoted N · won N (this week)
```
