# Changelog

All notable changes to this plugin will be documented here.

## 1.0.0 (initial release)

- Added the `monee-mate` MCP server pointing at `https://moneemate.com/mcp/moneemate`.
- Auth uses OAuth with dynamic client registration (scope `mcp:use`), so there is no access token or client ID to configure. Works with any Monee Mate account, including the free plan.
- Added the `monee-mate` skill: read before writing, avoid duplicate records, confirm before creating, editing or deleting, and never claim to move real money.
- Added the `monee-mate-safety` rule with the same guardrails for Monee Mate tool calls.
- Logo: Monee Mate's official mark, from moneemate.com.
