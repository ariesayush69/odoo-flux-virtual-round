# LIVE LINK: https://spry-pumice-fy7zmaz.tmp.now?_vercel_share=ArMHuLEtmEPem1AGgNoSyRdqUrvQ9dVM

# Brightloop — Subscription Management System (Odoo Hackathon)

One system for plans, subscriptions, recurring billing, invoices, discounts, payments and revenue reports.

## Backend used today
- **Django (Python)** — all backend logic, login, roles, invoice generation, tax, discount, payment status
- **SQLite** — database file `db.sqlite3`, one file, no separate database server
- **Frontend** — Django templates (HTML + CSS, responsive), no React, no build step
- **LocalStorage is NOT used** — data lives in SQLite, so admin, staff and customer see the same data. LocalStorage would be browser-only and would break the demo.
- **Netlify cannot host Django** — run locally with `runserver` for the demo video. For a live link later, use Render/Railway (Python host), not Netlify.

## Run in 5 steps (Mac / Windows, same)
1. `python3 -m venv venv` then activate it:
   - Mac: `source venv/bin/activate`
   - Windows: `venv\Scripts\activate`
2. `pip install -r requirements.txt`
3. `python manage.py migrate`
4. `python manage.py seed_demo`
5. `python manage.py runserver` — open http://127.0.0.1:8000/

Demo logins (demo only, change later):
- Admin: admin@brightloop.test / Admin@1234 — full control, only admin can add staff at /staff/new/
- Staff: staff@brightloop.test / Staff@1234 — day-to-day work, cannot add staff or discounts
- Customer: customer@brightloop.test / Customer@1234 — portal at /portal/ shows only own subscriptions/invoices

Admin panel also at /admin/ — create a superuser with `python manage.py createsuperuser` if you want it.

## Demo flow for the video (2 minutes)
1. Login as admin, see Finance Dashboard: active subs, revenue, outstanding, overdue.
2. Products: Brightloop CRM already seeded, variant "Brand: Odoo +560" already seeded.
3. Plans: Pro Monthly already seeded.
4. Subscriptions: SUB-0001 Active, 2 lines, variant adds 560 x 2.
5. Click "Generate invoice from this subscription" — invoice auto-fills lines + 18% tax. Click Generate again for same month — it blocks you: no double billing.
6. Confirm invoice, record a payment at /payments/new/ — when paid in full, invoice becomes Paid.
7. Discounts: only admin can create at /discounts/new/ — set % or fixed, dates, usage limit. Next invoice applies it automatically, then stops on expiry/limit.
8. Customer portal: login as customer, you see only your own data.
9. Password rules: signup needs >8 chars, 1 uppercase, 1 lowercase, 1 special character. One email = one account. Forgot password link prints in the runserver terminal in demo mode (console email backend) — for real email, set SMTP in settings.py later, never put passwords in code.

## Team split for 4 beginners (one branch, all commit)
- Person 1: Products + Plans + Variants
- Person 2: Subscriptions + status flow (Draft → Quotation → Confirmed → Active → Closed, pause/renew)
- Person 3: Invoices + Payments + Discounts
- Person 4: Dashboard + Customer portal + video + README
- Everyone: commit your own files on GitHub, team leader submits the single-branch repo link + video on hackathon.odoo.com. Do not copy code from elsewhere — original work only.

## What is covered from the PDF
Signup + unique email + password rule + reset link; Admin/Staff/Customer roles; Products + variants; Plans (daily/weekly/monthly/yearly, min qty, dates, auto-close, pause/renew per plan); Quotation templates with validity days; Subscriptions with number/customer/plan/dates/terms/lines and status flow; Invoices auto-created, auto tax, Draft → Confirmed → Paid, confirm/cancel/send/print, no double billing; Admin-only discounts (fixed/%, min purchase/qty, dates, usage limit, product or whole subscription, auto on next invoice); Payments (method/amount/date/note, paid vs outstanding/overdue); Finance dashboard with filters + summary, paged lists (25/page) + aggregates so it stays fast with thousands of rows.
