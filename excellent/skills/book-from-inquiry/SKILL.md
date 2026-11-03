---
name: book-from-inquiry
description: Turn an inquiry into an event in Excellent and put it in a room — convert the lead, then book the room or place a soft hold, each change undoable for 30 days. Use for "book the Smith party in the wine room", "put a hold on the patio for Friday", "convert that inquiry into an event", "pencil them in".
---

# Book an event from an inquiry

These are real changes, made as the person, on a connection they allowed to make changes. Ask before each
one, every time.

1. Find the inquiry with `list_leads` or `search` (`kind` lead). Find the room with `space_availability` for
   the date and party size (`list_spaces` gives room ids and capacities). Read back the plan: the event it
   will create, the room, the start and end time with the venue's time zone, and the party size.
2. When the person says yes, do only what they agreed to:
   - `convert_lead_to_event` with the `lead_id`. It makes a lead-stage event with the inquiry's date, party
     size and message, and the inquiry's contact as host. A lead converted already returns its event.
   - Then either `book_room` (the `event_id`, `space`, `starts_at`, `ends_at`, as ISO times with the time zone)
     to book it into the room, or `place_hold` (`space`, the window and `holder_name`) for a soft, ranked hold
     that lapses in 14 days unless they say otherwise. Excellent refuses a booking over a confirmed booking, a
     block, an active hold or the room's capacity; read the refusal back rather than trying another room
     without asking.
   - Only if asked: `set_event_guest_count` for a new party size, or `set_event_status` to tentative or
     confirmed. Confirming is refused while a hold sits on the room.
3. After each change, give its change_id. Finish with the list of every change_id you made.
4. To take a change back, call `undo` with its change_id. `recent_changes` lists what this connection changed.
   Undo works for 30 days, once, while nobody has changed the record since.
5. If the person wants a proposal next, `draft_event_document` with `kind` proposal drafts one priced from the
   venue's own menus; hand back its review link. It is not shared until the person finalizes it in Excellent.

If a change tool is refused because the connection may not make changes, say so plainly and tell the person
they can book it in Excellent's calendar, or reconnect with changes allowed.

Safety: every change here is undoable for 30 days with its change_id, and none happens without the person's
yes. Nothing is sent to the guest, no contract is signed, no deposit is charged, and nothing is deleted.
