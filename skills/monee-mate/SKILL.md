---
name: monee-mate
description: Use the Monee Mate MCP tools to answer questions about the user's personal finances and to record or edit expenses, income, transfers, budgets, credit card charges and invoices, loans with people and shared group expenses. Use when the user mentions Monee Mate or asks about their expenses, income, budgets, cards, accounts, loans or "how much did I spend", in any language.
---

# Monee Mate

Monee Mate (https://moneemate.com) is a personal-finance app. This plugin connects the agent to the user's account through the **Monee Mate** MCP server. The connector is free to use with any Monee Mate account; if tools fail with an authorization error, tell the user to sign in again via OAuth.

## Golden rules

1. **Read before you write.** Start with `get-profile` (timezone = what "today" means, primary/international currency). Discover ids with `list-accounts`, `list-categories`, `list-credit-cards`, `list-people`, `list-groups`. Never guess ids.
2. **Never duplicate records.** Before any `create-*`, check whether it already exists (e.g. `list-transactions` with `search`, a tight date range and the account; `list-credit-card-transactions` for the invoice). If something similar exists, ask the user instead of creating a second one. Never retry a create blindly after an error/timeout — list first to see if it went through.
3. **Confirm before creating, editing or deleting.** Summarize what you will do (type, amount, currency, account/card, category, date, description) and wait for a "yes". For batches, show the full list once and get one confirmation.
4. **Deletes are permanent.** All `delete-*` tools require `confirm: true`; only set it after explicit user confirmation. Prefer `archive-*` (accounts, categories, cards) and `end-recurring-transaction` / `delete-recurring-transaction` scope `pending` when the user just wants something "out of the way" or "cancelled".
5. **Monee Mate does not move real money.** `pay-invoice`, `complete-transaction`, `create-group-settlement`, `create-people-transaction` only *record* things. Never claim you paid a bank, card or person; never ask for bank credentials.
6. **People & invitations.** `create-person` with an email and `update-person-email` email a real person. Only use an email the user gave you and confirm first.
7. **Sensitive settings.** `update-currency-settings` does not reconvert past amounts and `update-timezone` shifts every date — always confirm.
8. **Language.** Answer in the user's language. Format amounts with the user's currency (e.g. `$1,250.00` for USD).

## Useful recipes

- "How am I doing this month?" → `get-dashboard`, then `list-budgets`.
- "What did I spend on?" → `get-spending-by-category` for the range (don't sum `list-transactions` by hand).
- Record an expense → `get-profile` → `list-accounts` + `list-categories type=expense` → duplicate check → confirm → `create-transaction`.
- Card charge → `list-credit-cards` (current invoice `due_date`) → duplicate check with `list-credit-card-transactions` → confirm → `create-credit-card-transaction`. Currency must be one of the user's currencies or in `list-currency-rates`.
- Edit a transaction → read it with `list-transactions`; `update-transaction` replaces **all** fields, so send back unchanged values plus the row's `group_name` and `occurrence_number`.
- Group split → `get-group` for member ids; splits must add up exactly to `total_amount` (put rounding remainder on one member).
- Loans → choose `lent` / `borrowed` / `payment_made` / `payment_received` carefully; amounts are always positive.
