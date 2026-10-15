---
name: uzum-seller-analytics
description: >
  Use when the user asks about their own Uzum Market seller business —
  revenue, profit, stock levels, products running out, FBS orders,
  returns, supply invoices, expenses (logistics, storage, commission), or
  comparing their shops. Works in Uzbek, Russian and English, e.g. "how
  much profit did I make last month", "qaysi mahsulot tugayapti",
  "сколько заказов ждут сборки".
---

Answer using the `uzum-seller` MCP tools. They read the seller's own data
through the official Uzum Seller OpenAPI (read-only). Reply in the language
the user writes in; format money as UZS with thousands separators
(e.g. 1 250 000 so'm / сум).

## Before you start

- If a tool says the subscription is inactive, the daily limit is reached,
  or no Uzum token is connected, relay that message and its link as-is.
  `subscription_status` shows plan, limits, days left and enabled shops.
- Sellers may have several shops. Shop-scoped tools take an optional
  `shop_id`; without it the default (first enabled) shop is used. When the
  question is about "all shops" or is ambiguous and `get_shops` returns
  more than one, ask or use `all_shops=true` on the finance tools.

## Tools

- `get_shops()` — enabled shops (id + name).
- `get_finance_orders(date_from, date_to, shop_id?, all_shops?, statuses?, size, page)` —
  sold items with `sellPrice`, `amount`, `sellerProfit` (net after Uzum
  commission), `purchasePrice` (cost), `commission`, `logisticDeliveryFee`.
  The main source for revenue and profit.
- `get_finance_expenses(date_from, date_to, shop_id?, all_shops?, size, page)` —
  itemized charges (logistics, storage, commission, penalties).
- `get_shop_products(shop_id?, search_query?, sort_by?, order?, filter?, size, page)` —
  SKUs with stock (`quantityAvailable`), sold/returned counts.
- `get_fbs_sku_stocks(size, page)` — FBS stock.
- `get_fbs_orders(status?, size, page)`, `get_fbs_orders_count(status?)`, `get_fbs_order(order_id)`.
- `get_invoices(shop_id?)`, `get_returns(shop_id?)` — supply and return invoices.

Dates are `YYYY-MM-DD`. "Last month" means the previous calendar month in
Tashkent time.

## Recipes

- **Revenue / profit for a period** → `get_finance_orders` for the range;
  page through until all `totalElements` are read (use `size` up to 100).
  Gross revenue = Σ `sellPrice × amount`; net profit = Σ `sellerProfit`;
  margin after cost = Σ (`sellerProfit` − `purchasePrice × amount`) when
  cost is filled in. Exclude `CANCELED` unless asked.
- **What will run out soon** → sales per SKU over the last 14–30 days from
  `get_finance_orders` ÷ days = daily velocity; compare with
  `quantityAvailable` from `get_shop_products`; days of cover = stock ÷
  velocity. Flag SKUs under 7–14 days.
- **Dead stock** → SKUs with stock but no sales in 30+ days; mention paid
  storage from `get_finance_expenses` if relevant.
- **Where money goes** → `get_finance_expenses`, group by type/source, show
  totals and share of revenue.
- **Returns problem** → `get_returns` plus returned counts from
  `get_shop_products`; rank SKUs by return rate.
- **Orders to pack** → `get_fbs_orders_count` by status, then
  `get_fbs_orders` for details.

Keep answers short: a headline number, a small table of the top items, and
one or two concrete suggestions. Don't dump raw JSON. If data needed for a
calculation is missing (e.g. no purchase cost set), say so and show what
can be computed.

## Limits

Funnel analytics (impressions, card views, add-to-cart, conversion),
customer reviews, payouts and discount campaigns are not available through
these tools. Say so plainly if asked.
