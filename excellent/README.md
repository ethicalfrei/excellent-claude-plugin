# Excellent for Claude

Run your restaurant group's private dining and events by talking to Claude. This plugin connects Claude to
[Excellent](https://beexcellent.ai) and adds ready-made workflows for the work a group's events and
operations team does every week: answering an inquiry, turning it into a booked event, the Monday look at
the week ahead, tomorrow's pre-shift note, staffing the schedule, assigning training, invoicing an event,
and thank-you cards after it.

You ask as yourself, behind your own Excellent permissions. Claude reads your group's live data (events,
inquiries, rooms and holds, invoices, contacts, staff schedules, the training roster) and drafts work for
you to review and send in Excellent.

## What's inside

- **The Excellent connector** (`.mcp.json`): `https://beexcellent.ai/api/mcp`. You sign in to Excellent and
  approve the connection the first time you use it (OAuth). No API key or password is stored in the plugin.
- **Skills** (`skills/`):

  | Skill | Ask it like |
  |---|---|
  | `inquiry-reply` | "Answer the new inquiry for 40 on the 14th." |
  | `book-from-inquiry` | "Convert that inquiry and put a hold on the wine room for Friday at 7." |
  | `week-ahead` | "Monday recap: what's this week look like?" |
  | `preshift-note` | "Build tomorrow's pre-shift note." |
  | `staff-the-week` | "Who's covering Saturday brunch? Fill the open shifts." |
  | `training-assign` | "Assign the wine course to the new servers, due in two weeks." |
  | `invoice-an-event` | "Draft the invoice for the Patel dinner." |
  | `thank-you-cards` | "Thank-you cards for last weekend's events." |

## What it will and won't do

- **Drafts wait for you.** Replies to inquiries, invoices, pre-shift notes, staff shifts, proposals and
  thank-you cards go into Excellent's review queues. Each comes back with a review link; you read it, edit
  it if you like, and send, publish or discard it in Excellent, signed in as yourself.
- **Changes are undoable.** On a connection you allowed to make changes, Claude can convert an inquiry,
  book a room, place a hold, change a guest count or assign training, always after asking you. Each change
  comes back with a change id that undoes it for 30 days.
- **It never sends, publishes, charges or deletes.** No email or text goes to a guest or your staff from
  Claude, no schedule or post is published, no card is charged, no payment is recorded, and nothing is
  deleted.
- Prices and totals are worked out by Excellent from your own menus, packages and deposit schedule, not by
  the model.

## Install

**Claude Code / Cowork**

```
/plugin marketplace add ethicalfrei/excellent-claude-plugin
/plugin install excellent@excellent
```

Then run `/mcp` and sign in to Excellent when asked.

**Claude (web, desktop and phone):** add Excellent from Claude's connectors directory, or as a custom
connector with the URL `https://beexcellent.ai/api/mcp`. Setup guide:
[beexcellent.ai/mcp](https://beexcellent.ai/mcp).

## Data handling

This plugin sends data to exactly one place: **Excellent** (`https://beexcellent.ai`), through the
connector above, only when Claude calls an Excellent tool on your behalf. What it sends is the tool's input
(for example, the inquiry Claude is answering or the invoice lines you agreed); what comes back is your
group's Excellent data that your account may see. The skills themselves are instructions only; they contain
no code and send nothing on their own.

- Privacy policy: <https://beexcellent.ai/privacy>
- Security: <https://beexcellent.ai/security>
- Support: <support@beexcellent.ai>

## License

MIT — see [LICENSE](LICENSE).
