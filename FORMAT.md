# Brightloop — FORMAT: What We Will Make, One By One

Stack: Django (Python) + SQLite. Frontend: Django templates. No LocalStorage as database. No Supabase for this project.
Rule: Finish one step, test it, push it, THEN start the next step. Never start 2 steps at once. Freeze at 2:00pm, video 2:00-3:00pm.

## Step 0 — DONE (you pushed this)
Login page code — pushed to GitHub.
Covers: sign-in, create account, forgot password link, demo Admin / Staff / Customer buttons.
Test already done: login page loads, password rule checked in Django (more than 8 chars, upper, lower, special).

## Step 1 — Admin Portal
What you will see: /admin-portal/ — only Admin can open it.
Covers PDF: "Admin controls the whole system, only admin can add a new member of staff."
You can do: see all products, plans, subscriptions, invoices, revenue, overdue; create product, plan, discount, staff.
Test before push: Admin 200, Staff blocked, Customer blocked.

## Step 2 — Staff Portal
What you will see: /staff-portal/ — Staff only.
Covers PDF: "Internal staff handle day-to-day work with limited access."
You can do: new subscription, confirm Draft invoices, record payments, chase overdue. You CANNOT create discounts or staff here.
Test before push: Staff 200, Customer blocked, no discount/staff buttons visible.

## Step 3 — Customer Portal
What you will see: /portal/ — Customer only sees own data.
Covers PDF: "Customers see only their own subscriptions and invoices through a portal."
You can do: see my subscriptions, my invoices, paid vs outstanding, plans I can ask for.
Test before push: Customer A sees only own data, Customer B (new signup) sees empty, not Customer A's data.

## Step 4 — Products + Variants
What you will see: /products/ and /products/new/
Covers PDF: product name, type, sales price, cost price, notes + variants, e.g. choosing Odoo brand adds 560 to the price.
Test before push: Create Brightloop CRM, variant Brand: Odoo +560, check price adds correctly in a subscription line.

## Step 5 — Plans + Quotation Templates
What you will see: /plans/, /plans/new/, /templates/
Covers PDF: plan cost, billing daily / weekly / monthly / yearly, minimum quantity, dates available, auto-close vs manual close / pause / renew per plan; quotation template with plan + product lines, valid for a set number of days.
Test before push: Create Pro Monthly plan, create a template from it with validity days.

## Step 6 — Subscriptions
What you will see: /subscriptions/, /subscriptions/new/, subscription detail page.
Covers PDF: subscription number, customer, plan, start date, expiry date, payment terms, lines (product, quantity, unit price, taxes, amount), status Draft -> Quotation -> Confirmed -> Active -> Closed.
Test before push: Create SUB-0001, add 2 lines, advance status step by step, pause and renew respect the plan's flags.

## Step 7 — Invoices
What you will see: /invoices/, invoice detail page, Generate invoice button on a subscription.
Covers PDF: invoice created from subscription with customer, lines, taxes, totals already filled; taxes calculated automatically; confirm, cancel, send, print; Draft -> Confirmed -> Paid; nothing billed twice or skipped.
Test before push: Generate invoice once -> total 3681.60 for demo (3120 + 561.60 tax). Generate again same month -> blocked, still 1 invoice.

## Step 8 — Discounts (Admin only)
What you will see: /discounts/, /discounts/new/
Covers PDF: only admin creates discount rules — fixed amount or percentage, minimum purchase or quantity, start and end dates, usage limit; applies to specific products or whole subscriptions; appears on next invoice on its own; stops when it expires or runs out.
Test before push: Staff cannot open discount creation. Admin discount applies on next invoice, then stops after limit/expiry.

## Step 9 — Payments
What you will see: /payments/, /payments/new/, payment list on each invoice.
Covers PDF: each payment recorded with method, amount, date, note, against the right invoice; see which invoices are paid and which are still outstanding, so overdue can be chased.
Test before push: Record partial payment -> outstanding falls. Record full payment -> invoice becomes Paid.

## Step 10 — Finance Dashboard + Final Polish + FREEZE
What you will see: / (dashboard) — cards + filters + summary.
Covers PDF: active subscriptions, revenue, payments, overdue invoices, with filters and summary view; every page responds in under 2 seconds even with thousands of subscriptions (we use totals + 25 per page, not loading all rows).
Test before push: Dashboard loads, filter by Draft / Confirmed / Paid works, phone view has no sideways scroll, `python manage.py check` = no issues.
FREEZE at 2:00pm — no new code after this step.

## Step 11 — Video (2:00-3:00pm, NOT a code step)
See VIDEO_SCRIPT.md. Record demo in order: Problem -> Login/Roles -> Product/Plan -> Subscription -> Invoice (no-double proof) -> Payment/Discount -> Dashboard -> Close. Upload, team leader submits GitHub repo link + video link before 3pm.

## How we will do it, one by one
1. I give you the step files + test + push command for that step only.
2. You copy those files, test, push, and tell me "Step X pushed".
3. Only then I give you the next step.
4. If a step fails its test, we fix that step first — we do not jump ahead.
