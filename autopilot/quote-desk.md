# AVS Quote Desk (hourly, 08:07-20:07 UK)

Keeps the booking form's promise: "We'll confirm your date and send your secure payment link within 2 hours."
Read `business.md` first; its hard rules override everything here.

1. Fetch "Book an AVS Clean" (Tally `rjNdDM`) submissions from the last 26 hours. Skip any already processed
   (a Booking Request with the same email + preferred date, or a draft/sent email to them in the last 2 days).
2. For each new booking:
   - Re-check the price from the price list. The form's `total_price` field is a hint, not the authority.
     Unusual scope (mould, rubbish, heavy dirt) still gets the list price, flagged "check scope".
   - Create the Airtable Booking Request with the Quote amount and leave Quote Sent unticked. Keep the form's
     `source` hidden field (ad/campaign tracking) in Customer Notes.
   - Create a Stripe Payment Link for the exact GBP amount.
   - Draft (never send) the quote email: fixed price, what's included, photo report + 48h re-clean, the
     payment link, and "no key safe codes by email".
   - "Something else" requests: no price; draft a reply asking only for what's needed to price it.
3. Make sure the customer exists in Customers (Lead / Quote Sent).

Output: "No new bookings." or one line per booking with flags.

## The form (Tally rjNdDM)
- Prices are shown on every option, and the furnished question (+15%) appears only for property cleans.
- A `total_price` calculated field shows "Your price: £X" on the thank-you page (hidden for "Something else").
- Hidden field `source`: add `?source=facebook` (or `google`, `flyer`, …) to the form link in ads to track
  which channel each booking came from.
