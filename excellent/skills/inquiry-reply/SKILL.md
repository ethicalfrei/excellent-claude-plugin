---
name: inquiry-reply
description: Answer a private-dining or event inquiry in Excellent — read the inquiry, check which rooms are free that day for the party size, and draft a reply for the person to review and send. Use for "answer the new inquiry", "reply to the Garcia rehearsal dinner request", "do we have room for 40 on the 14th?", "write back to that lead".
---

# Answer an inquiry

1. Find the inquiry. For the newest ones call `list_leads` with `status` new; for a named one call `search`
   with `kind` lead. Read back who is asking, the date, the party size and what they wrote.
2. Check the rooms for that day with `space_availability` (the inquiry's `date` and `party_size`; for a group
   with several venues, pass the venue's `location` from `overview`). Say which rooms fit the party and
   when each is free. A free stretch is not a reservation.
3. Write the reply with the person: warm, short, in the guest's language (English or Spanish). Offer only
   rooms and times you just saw free. Quote no price, deposit or minimum unless the person gives it to you.
   Ask the person anything you would otherwise guess.
4. Call `draft_lead_reply` with the inquiry's `lead_id`, a `subject`, the `body` and the `locale`. The
   inquiry needs an email address; if it has none, say so and stop.
5. Hand back the review link from the result. The person reads it, can edit it, and sends it from Excellent,
   signed in as themselves; only then does the inquiry move to contacted. To find the link again later, call
   `get_review_link` with `kind` reply and the draft's `id`.

If the person wants to hold or book the room as well, use the `book-from-inquiry` skill and ask first.

Safety: this skill only reads and drafts. The reply is a draft waiting in Excellent's review queue; nothing
is sent to the guest from Claude, and nothing is booked, held, charged or deleted.
