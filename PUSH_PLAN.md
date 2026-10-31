# Brightloop — Professional Push Plan (Today: 9am - 3pm)

## The rule for today
- **Build ends at 2:00pm sharp. 2:00-3:00pm is VIDEO ONLY. No new features after 2pm.**
- **Minimum: 1 push per hour. Target: 5 pushes per hour = 1 push every ~12 minutes.**
- **Never push broken code.** Before every push, run: `python manage.py check` — if it says "no issues", only then push.
- **One branch only for Odoo submission.** Push to `main` only. Team leader submits that repo link + video link on hackathon.odoo.com.
- Before every push: `git pull` first, then add, commit, push. One person pushes at a time — if Git says conflict, STOP and fix together, do not force-push.

## Push command template (copy-paste, change only the message + files)
```
git pull
git add <files for this push>
git commit -m "feat: <what this push adds, in plain words>"
git push origin main
```

## Hour 1: 11:00 - 12:00 — Look professional + core pages
| # | Time | Push | Files | Test before push |
|---|------|------|-------|------------------|
| 1 | 11:00 | `style: professional Brightloop theme + login design` | core/templates/base.html, login.html, form.html | check + login page loads |
| 2 | 11:15 | `feat: finance dashboard cards + filters` | dashboard.html | dashboard shows 4 numbers |
| 3 | 11:30 | `feat: products and plans pages` | list.html, products/plans views already done | create 1 product + 1 plan |
| 4 | 11:45 | `feat: subscriptions list, detail and status flow` | subscriptions.html, subscription_detail.html | Draft -> Active works |
| 5 | 12:00 | `docs: hour-1 checkpoint + README update` | README.md, PUSH_PLAN.md | full login -> dashboard -> subscription flow |

## Hour 2: 12:00 - 1:00 — Money flow (the heart of the PDF)
| # | Time | Push | Files | Test before push |
|---|------|------|-------|------------------|
| 6 | 12:10 | `feat: generate invoice from subscription` | views.py invoice_generate, invoice_detail.html | INV total = lines + tax - discount |
| 7 | 12:25 | `feat: invoice confirm, send, print, cancel` | invoice_detail.html | status changes, print works |
| 8 | 12:40 | `feat: record payments, auto Paid when fully paid` | payments views/templates | pay full amount -> Paid |
| 9 | 12:55 | `feat: admin-only discounts, auto on next invoice` | discount views/templates | discount applies, then stops |
| 10 | 1:00 | `docs: hour-2 checkpoint, no-double-billing proof` | README.md | generate same invoice twice = blocked |

## Hour 3: 1:00 - 2:00 — Portal, polish, FREEZE
| # | Time | Push | Files | Test before push |
|---|------|------|-------|------------------|
| 11 | 1:10 | `feat: customer portal only-own-data + staff creation` | portal.html, staff view | customer cannot see others |
| 12 | 1:25 | `feat: quotation templates + search and pagination` | templates, subscriptions list | search + 25/page works |
| 13 | 1:40 | `fix: phone responsive check + validation messages` | base.html CSS | phone width: no sideways scroll |
| 14 | 1:55 | `chore: clean repo, requirements, gitignore` | requirements.txt, .gitignore | fresh clone: migrate + seed works |
| 15 | 2:00 | `freeze: build complete, video starts` | VIDEO_SCRIPT.md | NO new code after this |

If you fall behind, SKIP a polish push — never skip Push 5, 10, 15 (the checkpoints). A working checkpoint beats a fancy unfinished feature.

## Hour 4: 2:00 - 3:00 — VIDEO ONLY (see VIDEO_SCRIPT.md)
1. 2:00-2:15 — Record screen demo (follow script, no retakes for small mistakes)
2. 2:15-2:40 — Trim, add title slide: team name, problem, stack (Django + SQLite)
3. 2:40-2:55 — Upload video, get link
4. 2:55-3:00 — Team leader submits GitHub repo link + video link, screenshot the confirmation

## What "professional" means for judges
- Same colours/fonts on every page (teal #0e8a8c, navy #14213d, amber #f2a541 — from INDEX.html)
- Every button works, every form shows a clear error if wrong
- No passwords visible in frontend code (INDEX.html had demo passwords in JS — Django version checks passwords in SQLite, never in the page)
- README explains: problem, stack, how to run, demo logins, demo flow
- Commit messages in plain words, not "update" / "fix stuff"
