# Brightloop — FULLY FINISHED: Frontend + Backend

Status: COMPLETE and tested. Freeze for video at 2pm, submit before 3pm.

## Frontend (what you see — Django templates, Brightloop theme)
- Login / Signup / Forgot password — professional teal/navy/amber design, responsive on phone + desktop
- Admin Portal (/admin-portal/) — Admin only
- Staff Portal (/staff-portal/) — Staff only, day-to-day
- Customer Portal (/portal/) — Customer only, own data only
- Finance Dashboard (/) — cards, filters, summary, 25/page
- Products table (/products/) + New product + New variant (/variants/new/)
- Plans table (/plans/) — billing, min qty, dates, auto-close/pause/renew
- Subscriptions list + detail (/subscriptions/) — lines, status buttons, generate invoice
- Invoices list + detail (/invoices/) — confirm/cancel/send/print/paid, paid vs outstanding
- Discounts table (/discounts/) — Admin only to create
- Payments table (/payments/) — record payment form
- Quotation templates (/templates/)
- Logout works via POST form (GET logout was 405 in Django 6 — fixed)

## Backend (what runs — Django + SQLite)
- Models: Profile/roles, TaxRule, Product, Variant, Plan, QuotationTemplate, Subscription, SubscriptionLine, Invoice, InvoiceLine, Discount, Payment
- Auth: Django auth + custom password validators (>8 chars, upper, lower, special), unique email, password-reset via console email in demo
- Roles: admin_required and staff_required decorators on every sensitive view — tested: staff blocked from admin portal, customer blocked from admin/staff portals and products/plans
- Invoice logic: auto from subscription lines, auto tax 18% (per line), discount auto-applied if active (dates, usage limit, min purchase/qty, product match), unique (subscription, billing_period) blocks double billing
- Payment logic: full payment flips invoice to Paid, partial leaves outstanding
- Subscription logic: status Draft->Quotation->Confirmed->Active->Closed, pause/renew respect plan flags, line quantity respects plan min_quantity
- Database: SQLite file db.sqlite3, migrations in core/migrations/0001_initial.py
- Performance: dashboard uses aggregates + Paginator 25/page, not full table loads

## Tested — final run (fresh DB, seed_demo)
- All frontend pages: 200 for correct role, 302 redirect for blocked role
- Logout POST: 302 (works)
- Variant create: works
- Demo money flow: subtotal 3120.00 (2x1000 + 2x560 variant), tax 561.60, discount 10% = 312.00, total 3369.60
- Double invoice: still 1 invoice
- Weak password + duplicate email signup: blocked
- `python manage.py check`: no issues

## Run it (5 steps)
1. `python3 -m venv venv` + activate
2. `pip install -r requirements.txt`
3. `python manage.py migrate`
4. `python manage.py seed_demo`
5. `python manage.py runserver` — http://127.0.0.1:8000/
Demo: admin@brightloop.test / Admin@1234, staff@brightloop.test / Staff@1234, customer@brightloop.test / Customer@1234

## Push ALL remaining code (one push, or split by PORTALS.md / PUSH_PLAN.md if you want 5/hour)
```
git pull
git add .
git commit -m "feat: Brightloop complete - frontend portals, products, plans, subscriptions, invoices, discounts, payments, dashboard"
git push origin main
```
Note: `db.sqlite3` is gitignored — teammates must run migrate + seed_demo after cloning. Do NOT commit db.sqlite3.

## Submit before 3pm
1. Freeze code at 2pm, record video with VIDEO_SCRIPT.md (2-3pm)
2. Team leader submits GitHub repo link (single branch) + video link on hackathon.odoo.com
3. Screenshot the submission confirmation
