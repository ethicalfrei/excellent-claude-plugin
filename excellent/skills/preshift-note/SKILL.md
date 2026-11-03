---
name: preshift-note
description: Write tomorrow's (or any day's) pre-shift note for a restaurant team in Excellent from the day's events and who is working, then leave it as a draft for a manager to publish. Use for "build tomorrow's pre-shift", "line-up notes for Saturday", "what should the team know before service tonight".
---

# Pre-shift note

1. Settle the day (tomorrow unless the person says otherwise) and, for a group with several venues, which
   venue (`overview` lists them).
2. Call `agenda` with `from` that day and `days` 1 for the day's bookings: time, rooms, host and any balance.
   For each event, call `get_event` for its party size, rooms, host and the menu its documents state (and any
   item those documents disagree on: flag it for the manager rather than picking one).
3. Call `schedule_today` for that day to see who is on, in which role, and any open shift nobody has yet.
4. Ask the person for what the records don't hold: specials, 86'd items, allergies they know of, VIPs, focus
   for the night. Never invent a guest detail.
5. Write the note in short lines a server can read in a minute: events with times, rooms and headcounts;
   menu notes; who is on and open shifts; the manager's points. Offer a Spanish version alongside.
6. Call `draft_preshift_note` with the `date`, `body_en` and, if wanted, `body_es`. If that day already has a
   note (draft or published), Excellent leaves it exactly as it is and stages nothing: say so.
7. Hand back the review link. A manager publishes it in Excellent; staff see nothing before that.

Safety: the note is a draft waiting for review in Excellent; nothing reaches staff from Claude, and nothing
is booked, changed, sent or deleted.
