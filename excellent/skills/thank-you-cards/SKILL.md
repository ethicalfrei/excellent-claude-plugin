---
name: thank-you-cards
description: Draft thank-you cards for guests after their events in Excellent, from each event's facts and its guest photo wall, for the team to review and publish. Use for "send thank-yous for last weekend's events", "thank-you card for the Lee wedding", "follow up with last week's hosts".
---

# Thank-you cards after events

1. Find the events. For a recent batch call `list_events` with `status` completed and pick the ones in the
   window the person names; for one event call `search` with `kind` event. Read back the list and ask which
   ones to draft.
2. For each one the person picks, call `draft_thank_you_card` with its `event_id`. Excellent writes it from
   the event's own facts and its guest photo wall.
3. Give the person each card's review link. They read it, and publish or discard it from the event page in
   Excellent. To find a link again, call `get_review_link` with `kind` card and the card's `id`.

Don't draft a card for an event that hasn't happened yet or was lost, and draft one card per event. If Excellent
refuses one, pass on the reason it gives.

Safety: every card is a draft waiting for review; nothing is published or sent to a guest from Claude, and
nothing is changed, charged or deleted.
