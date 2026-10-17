# AVS Business Facts (source of truth for every autopilot run)

## Identity
- AVS Cleaning Services, Birmingham. Founder: Alexandre Sene.
- Inbox: avscleaningservices6@gmail.com | Phone: 07828 714805
- Sign-off: "Alexandre / Founder, AVS Cleaning Services / avscleaningservices6@gmail.com | 07828 714805"
- Positioning: premium, not the cheapest. Proof points: dated photo report of every room sent same day;
  48-hour re-clean guarantee; vetted, insured cleaners (ID + right to work checked); one point of contact.
- Public liability: £1m, Simply Business, valid to 21 Sep 2027 (certificate PDF is attached to the
  Melvyn Danes thread 1a143f45990f8621 if a prospect asks for it).
- Stage 1 target: £15k/month revenue. Recurring work is the priority.

## Price list (Oct 2026), never invent or discount
End of tenancy / turnover / deep clean (empty property):
| Size | Price |
|---|---|
| 1-bed | £220 |
| 2-bed | £290 |
| 3-bed | £380 |
| 4-bed HMO | £580 |
| 5-bed HMO | £700 |
| 6-bed HMO | £820 |
| Single HMO room | £120 |
| Furnished | +15% |

Communal areas per visit: £180 single HMO · £340 block up to ~10 flats · £520 larger block with lifts/bin stores.
Regular weekly/fortnightly communal contracts and anything not on this list: "quoted individually", so flag
it for Alexandre and never make up a number.
Every clean includes inside oven, hob, extractor, fridge; descaled bathrooms; every room dusted, wiped, floors finished.
Payment: one-off jobs prepaid by Stripe card link; a slot is confirmed and a cleaner assigned only once paid.

## Hard rules
1. NEVER send email to clients, prospects or cleaners. Create Gmail DRAFTS only (reply in the existing thread).
2. Before drafting into a thread, check `list_drafts` so the same thread never gets two drafts.
3. Never delete records, emails or drafts.
4. Anyone who asks not to be contacted gets Outreach Status = "Opted Out", Sales Stage = "Do Not Contact",
   and no draft.
5. Never offer a job to a cleaner whose Insurance Alert is not OK/EXPIRING (Recruitment base → Cleaners).
6. Only use publicly listed business contact details for prospects. No private individuals' personal data.
7. Don't invent numbers. Anything not found = "unknown".

## Airtable map
Base "AVS - Customers" = `appge0DudNjJ2Yg19`
- Customers (CRM / pipeline) `tbl9yc1i8NKUsvpNv`
  - Customer `fldT8kXwqBOIqA8t5` · Email `fldksWN6w9ZRdGZOn` · Phone `fldOrGzZbk7s2nzzz`
  - Customer Type `flduDLaa9lXloxoEh` (Residential / Commercial / Airbnb / Short Stay / Other)
  - Customer Status `fld72iLWV6vJqFjCB` (Lead / Active / Paused / Inactive / Do Not Contact)
  - Sales Stage `fldilQaxUAPvtRZ5H` (New Prospect / Contact Scheduled / Contacted / Interested / Quote Sent /
    Follow-up / Won / Lost / Do Not Contact / Not a fit)
  - Outreach Status `fldcuFb7peaNyqq11` (Not Contacted / Scheduled / Sent - Unconfirmed / Replied / Bounced / Opted Out)
  - Business Sector `fldNSIfOlkWTdmz0l` · Birmingham Area `fldjP4OHuj3OGPUX4` · Website `fldiylFH5dDcBsGEy`
  - Last Outreach Date `fldUAMEupcHwfFbgm` · Next Follow-up `fldDmq4w0QQty58r6`
  - Cleaning Opportunity `fldrbw88qDf8RArsH` · Customer Notes `fldWx93cEhfZyUiGo` (Gmail thread ids live here)
  - Potential Monthly Value `fldZvfk5I0Yr5f8bb`
- Booking Requests (enquiries/quotes) `tblrMxl8uklfLndy6`: Status, Quote, Quote Sent, Customer Accepted, Payment Status

Base "AVS - Jobs & Operations" = `app7Jbexdn61FOFcG`
- Job Cards `tblAvIgI4rwQp0xH6`: Job Date, Assigned Cleaner, Status, Acceptance Status, Dispatch Status,
  QC Status, Offer Response Overdue, Late Arrival Alert Needed, Ready to Pay
- Cleaner Completion Reports `tbls0d7o0kK2QZ62W` · Cleaner Issue Reports `tbllUMBFnAyhLGbJz`

Base "AVS Recruitment & People" = `app9STIGnImDe8czh`
- Applications `tblyGf8cmtER5Z1ac` · Cleaners `tblfJOLGnZuB6GakP` (Ready for Jobs, Insurance Alert)

Base "AVS - Finance" = `appHVEwMaPCsZ6XAx`: Invoices `tbl2bB7AElexEXWBX`, Cleaner Payments `tblnr2i3IY62BQTbq`
Base "AVS - Management HQ" = `appeOtLWT8g3G7aqq`: Management Actions `tblHTxLnk91bqzuIV`, KPI Dashboard `tblcHylmeB6brasvZ`

## Tally forms
- "Book an AVS Clean" `rjNdDM` (client enquiries)
- "Clean with AVS" `GxNJ92` (cleaner applications)

## Prospecting area rotation
Digbeth → City Centre / Jewellery Quarter → Selly Oak / Bournbrook → Selly Park → Harborne → Edgbaston →
Moseley / Kings Heath → Solihull / Shirley → Sutton Coldfield → Erdington → Walsall / West Bromwich.
Pick the earliest area with the fewest Customers records whose Birmingham Area contains it.
Priority targets: letting agents and portfolio landlords (5-50 units), HMO / student-let operators,
block managers, serviced-apartment operators. Skip retail, cafes, barbers (these were "Not a fit").
