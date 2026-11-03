---
name: invoice-an-event
description: Draft the invoice for a private event in Excellent from the event's agreed menu and figures, for the person to review and send from the invoice page. Use for "invoice the Patel dinner", "bill the Friday buyout", "draft the final invoice for the wedding", "add a deposit installment".
---

# Invoice an event

1. Find the event with `search` (`kind` event) or `list_events`, then call `get_event`. Read back the party
   size, the menu its documents state, each document's status and client total, and any invoices it already
   has with what is paid and owed.
2. If the event already has an invoice, don't draft a second one. Call `get_invoice` for it; if it is still an
   unsent draft nobody has paid, `revise_invoice_draft` changes its title, lines, tax or fee (the lines you pass
   replace every line), and `add_invoice_installment` adds a payment to its schedule.
3. Otherwise build the lines with the person: label, a whole quantity and a unit price, from the signed
   contract or proposal. If the document says some prices are still to be confirmed or no tax and service
   rates are set yet, its total is partial: say so, and ask for the missing figures instead of guessing. Never
   invent a price.
4. Call `draft_invoice` with the `event_id`, the `lines` (unit prices in cents), and `tax_minor` and `fee_minor`
   in cents if given. Excellent works out every line, the subtotal and the total with its own math, and sets
   the deposit from the group's deposit schedule for the party size. Read back the figures it returns, in
   dollars.
5. Hand back the review link. The person checks it and sends it from the invoice page in Excellent. To find it
   again, call `get_review_link` with `kind` invoice and the invoice's `id`.

Safety: the invoice is a draft waiting for review. Nothing is sent to the guest, shared or charged from
Claude, no payment is recorded, and nothing is deleted.
