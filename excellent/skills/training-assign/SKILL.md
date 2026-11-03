---
name: training-assign
description: Check a restaurant team's training roster in Excellent and assign a course or an on-the-floor skill sign-off to the right people, after the person confirms. Use for "assign the wine course to the new servers", "who's on the training roster?", "add our new host and give her the onboarding course", "put bar opening on Sam's plate".
---

# Training check and assignments

1. Call `training_roster` (narrow it with `match`). It lists active team members with role and home venue,
   the published courses, and the competencies (skills a manager signs off in person), each with the id the
   assignments take. It does not show course progress or scores: for those, send the person to the roster in
   Excellent rather than guessing.
2. Agree who gets what, and by when. Read the list back: each person, the course or competency, the due date.
3. Assignments are real changes, made as the person, on a connection they allowed to make changes. Only on
   their yes:
   - `assign_course` with `staff_id`, `course_id` and an optional `due_on`;
   - `assign_competency` with `staff_id`, `competency_id` and an optional `due_on`, for a manager to sign off
     later in Excellent;
   - for someone not on the roster yet, `add_staff_member` first (Excellent then assigns any courses the
     group's standing rules give their role or venue: say which ones came back).
   Something already assigned stays as it is and nothing changes.
4. Give the change_id of each change and finish with the full list. To take one back, call `undo` with its
   change_id; `recent_changes` lists them. Undo works for 30 days while nobody has changed the record since.

Safety: every assignment is undoable for 30 days with its change_id, and none happens without the person's
yes. Nobody is messaged from Claude, no sign-off is recorded for anyone, and nothing is deleted.
