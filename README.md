# Monee Mate for Grok and Cursor

Connect Grok (xAI) and Cursor to your **[Monee Mate](https://moneemate.com)** personal-finance account. Ask the agent how your finances are doing, record expenses and income, and review budgets, credit cards, loans with people and shared group expenses, all from the chat.

> **Free.** The connector works with any Monee Mate account, including the free plan. You only need to sign in with OAuth.

## What's included

| Component | File | Description |
| --- | --- | --- |
| MCP server | `mcp.json` | Remote server (streamable HTTP) `https://moneemate.com/mcp/moneemate`, authenticated with OAuth. |
| Skill | `skills/monee-mate/SKILL.md` | How to use the tools safely: read before writing, avoid duplicates, confirm before creating/deleting, never pay banks. |
| Rule | `rules/monee-mate-safety.mdc` | Safety guardrails for Monee Mate tool calls (on demand). |

No tokens or variables are needed: authentication is handled with OAuth.

## Installation

### Grok (xAI)

1. Install **Monee Mate** from the Grok plugin marketplace.
2. When prompted, sign in at moneemate.com and authorize Grok (OAuth).
3. Try: *"How are my finances this month?"*

### Cursor

1. Install **Monee Mate** from the Cursor Marketplace (or test it locally, see below).
2. Open **Customize → MCP** and find the **Monee Mate** server.
3. Click **Connect / Login**. moneemate.com opens so you can sign in and authorize Cursor (OAuth with dynamic client registration). Back in Cursor, the tools are available.
4. Try: *"How are my finances this month?"* or *"Record a $25 grocery expense today on my checking account"*.

To disconnect, sign out of the server in Customize → MCP or revoke access from your Monee Mate account.

## Support and privacy

- Support: [support@moneemate.com](mailto:support@moneemate.com)
- Privacy policy: https://moneemate.com/privacy

## Available tools (69)

| Category | Tools |
| --- | --- |
| Profile and overview | `get-profile`, `get-dashboard`, `get-spending-by-category`, `update-timezone`, `update-currency-settings` |
| Accounts | `list-accounts`, `create-account`, `update-account`, `archive-account`, `restore-account`, `delete-account` |
| Categories | `list-categories`, `create-category`, `update-category`, `archive-category`, `restore-category`, `delete-category` |
| Transactions (expenses, income, transfers) | `list-transactions`, `create-transaction`, `update-transaction`, `delete-transaction`, `complete-transaction`, `uncomplete-transaction`, `set-transaction-ignored` |
| Recurring transactions | `list-recurring-transactions`, `end-recurring-transaction`, `delete-recurring-transaction` |
| Budgets | `list-budgets`, `create-budget`, `update-budget`, `close-budget-month`, `delete-budget` |
| Credit cards and invoices | `list-credit-cards`, `create-credit-card`, `update-credit-card`, `archive-credit-card`, `restore-credit-card`, `delete-credit-card`, `list-credit-card-transactions`, `create-credit-card-transaction`, `update-credit-card-transaction`, `delete-credit-card-transaction`, `list-past-invoices`, `pay-invoice`, `unpay-invoice` |
| Currencies | `list-currency-rates`, `upsert-currency-rate`, `delete-currency-rate` |
| People and loans | `list-people`, `get-person`, `get-people-balances`, `create-person`, `update-person`, `update-person-email`, `delete-person`, `list-people-transactions`, `create-people-transaction`, `update-people-transaction`, `delete-people-transaction` |
| Groups and shared expenses | `list-groups`, `get-group`, `create-group`, `update-group`, `delete-group`, `create-group-expense`, `update-group-expense-account`, `delete-group-expense`, `create-group-settlement`, `update-group-settlement-account` |

Important: Monee Mate **records** transactions; it does not move real money. `pay-invoice` and `create-group-settlement` only mark something as paid in the app. Delete tools are permanent and require explicit confirmation. `create-person` with an email and `update-person-email` can send an email invitation to that person.

## Test locally (Cursor)

1. Copy this folder to `~/.cursor/plugins/local/monee-mate` (a real copy; symlinks pointing outside that folder are ignored).
2. Restart Cursor or run **Developer: Reload Window**.
3. Open **Customize** and check that the `monee-mate` skill, the rule and the **Monee Mate** MCP server appear.
4. Connect with OAuth and try a read-only request (`get-profile`, `get-dashboard`).

If the Marketplace version is already installed, it takes precedence over the local copy. On Enterprise, **Allow Local Plugin Imports** is required.

## License

MIT © Darwin Arevalo
