---
name: staff-the-week
description: Fill a restaurant venue's staff schedule in Excellent — find the hours nobody is scheduled for and the open shifts, then draft shifts into the week for a manager to publish. Use for "staff next week", "who's covering Saturday brunch?", "fill the open bar shifts", "build the schedule for the patio party".
---

# Staff the week

1. Pick the venue (`overview` lists them, with ids) and the week (this week unless the person names a date).
2. Call `schedule_week` with that `date` and `location`. Name, day by day: the stretches of opening hours
   nobody is scheduled for, open shifts, planned hours by role, the week's warnings, and whether the week is
   already published. For the busy days, `agenda` shows the events that need extra hands.
3. Propose the shifts as a list: day, start and end on the venue's clock (24-hour), role, and the person from
   the roster `schedule_week` returns, or open when nobody is named yet. Ask the person to adjust it. Don't
   schedule someone the person hasn't agreed to.
4. When they agree, call `draft_shift` once per shift (`location`, `date`, `start`, `end`, `role`, and
   `staff_id` when someone is named; optional `break_minutes` and `note`). An end at or before the start runs
   past midnight.
5. Call `schedule_week` again to show the week as it now stands, and hand back the review link. A manager
   keeps or discards each shift and publishes the week in Excellent.

Safety: shifts go into the week's draft; staff see nothing until a person publishes the week in Excellent.
Nothing is sent to staff from Claude, and nothing is published, paid or deleted.
