# Brightloop — Portals, One By One

Built in order, push each portal separately. Do not push all 3 at once — that breaks the 5-pushes-per-hour target and makes a bad commit hard to undo.

## Portal 1 — Admin Portal — PUSH FIRST
- URL: `/admin-portal/` — Admin only. Staff gets redirected, Customer gets redirected.
- What it does: all products, plans, subscriptions, invoices, revenue, overdue; create product, plan, discount, staff — all from one page.
- Files: `core/views.py` (admin_portal), `core/urls.py`, `core/templates/admin_portal.html`, `core/context_processors.py`, `brightloop/settings.py`, `core/templates/base.html` (role nav)
- Test: login admin -> 200. Login staff -> redirected. Login customer -> redirected.
- Push:
```
git pull
git add core/views.py core/urls.py core/templates/admin_portal.html core/context_processors.py brightloop/settings.py core/templates/base.html
git commit -m "feat: admin portal - full control, staff and discounts"
git push origin main
```

## Portal 2 — Staff Portal — PUSH SECOND
- URL: `/staff-portal/` — Staff (and Admin) only. Customer gets redirected.
- What it does: day-to-day only — active subs, Draft invoices to confirm, overdue to chase, recent subs/payments, new subscription, record payment.
- What it does NOT do: no discount creation button, no staff creation button. Those views block staff too, not just the button.
- Files: `core/views.py` (staff_portal), `core/urls.py`, `core/templates/staff_portal.html`
- Test: login staff -> 200. Login customer -> redirected.
- Push:
```
git pull
git add core/views.py core/urls.py core/templates/staff_portal.html
git commit -m "feat: staff portal - day-to-day work only, no discounts or staff creation"
git push origin main
```

## Portal 3 — Customer Portal — PUSH THIRD
- URL: `/portal/` — Customer sees ONLY own subscriptions/invoices, plus plans they can ask for.
- What it does: my subs count, my invoices count, my overdue, total I have paid, my invoice table with paid/outstanding, plans list.
- Files: `core/views.py` (customer_portal upgraded), `core/templates/portal.html`
- Test: login customer -> 200 and only own SUB-0001 / own invoices appear. Login as a second customer (signup a new account) -> sees empty, not SUB-0001.
- Push:
```
git pull
git add core/views.py core/templates/portal.html
git commit -m "feat: customer portal upgraded - own data only, plans view"
git push origin main
```

## Demo accounts (from seed_demo)
- Admin: admin@brightloop.test / Admin@1234 -> Admin Portal
- Staff: staff@brightloop.test / Staff@1234 -> Staff Portal
- Customer: customer@brightloop.test / Customer@1234 -> My Portal
