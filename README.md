# Restaurant Manager

A complete restaurant management system built with **Flask + SQLite** — no external services needed.

## What it does (end to end)

| Stage | Screen | What happens |
|---|---|---|
| Seating | **Floor** (`/`) | Live table map (free / occupied) + today's sales, open orders, low-stock alerts |
| Ordering | **Table** (`/table/<id>`) | Waiter adds dishes with notes; items can be removed until the kitchen starts them |
| Cooking | **Kitchen** (`/kitchen`) | Ticket board: New → Preparing → Ready; auto-refreshes every 15s |
| Serving | Table screen | Waiter marks ready items as served |
| Billing | **Bill** (`/order/<id>/bill`) | Discount %, 5% GST, cash/card/UPI, printable receipt; table is freed |
| Stock | **Inventory** (`/inventory`) | Ingredients auto-deducted from each dish's recipe when a bill is paid; low-stock flags; restocking |
| Menu | **Menu** (`/menu`) | Add dishes, edit prices, switch items off when sold out |
| Insights | **Reports** (`/reports`) | Daily revenue, best sellers, payment-method split; JSON at `/api/summary` |

## Run it

```bash
pip install -r requirements.txt
python app.py          # http://127.0.0.1:5000
pytest -q              # run the test suite
```

The database (`restaurant.db`) and sample data (menu, recipes, ingredients, 8 tables) are created automatically on first run. Delete `restaurant.db` to reset.

## Project layout

```
app.py          Flask app factory + all routes and business logic
schema.sql      Database schema
seed.py         Sample restaurant data
templates/      Jinja pages (dashboard, table, kitchen, bill, menu, inventory, reports)
static/         style.css
test_app.py     End-to-end tests (order -> kitchen -> bill -> stock -> report)
```

## Customising

- **Tax rate:** change `GST_RATE` at the top of `app.py`.
- **Restaurant name:** edit `templates/base.html` and `templates/bill.html`.
- **Currency:** edit the `money` filter at the bottom of `create_app`.

## Ideas for next steps

- Login with roles (waiter / chef / manager)
- Table reservations
- Split bills and tips
- Purchase orders to suppliers when stock is low
- Switch SQLite to PostgreSQL for multi-outlet use
