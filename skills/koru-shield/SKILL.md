---
name: koru-shield
description: Manage Koru Shield internet security - block/unblock domains, check filtering status, view blocked activity, manage schedules and filter categories
---

# Koru Shield

Koru Shield is a DNS-based internet security and parental control service. It lets account owners manage protection profiles, control which domains are allowed or denied, apply content categories, set schedules, review DNS activity, and see enrolled devices.

## Connect to Koru Shield

There are two ways to interact with the service:

1. **MCP server.** Run the local server with `npx -y korushield-mcp-server` and provide the `KORU_SHIELD_API_KEY` environment variable, or connect to the hosted remote MCP server at `https://mcp.korushield.com/mcp` using a Bearer token.
2. **Direct REST API.** Send requests to `https://my.korushield.com/api` with the header `Authorization: Bearer <key>`.

Create or copy an API key in the Koru Shield dashboard at `https://my.korushield.com` under **API Keys**. Treat the key as a secret. Do not include it in prompts, source files, logs, or shared output. When a client prompts for authentication, provide the key through that client's secure configuration flow.

## Available tools

1. **`list_profiles`**: List all DNS protection profiles on the account, such as Kids, Work, or IoT. Start here to discover profile IDs.
2. **`get_profile`**: Get details of one profile. Requires `profile_id`.
3. **`list_rules`**: List custom allow and deny rules for a profile. Requires `profile_id`.
4. **`create_rule`**: Create a custom allow or deny rule for a domain on a profile. Requires `profile_id`, `kind` (`allow` or `deny`), and `domain`; accepts an optional `note`.
5. **`delete_rule`**: Delete a custom rule from a profile. Destructive. Requires `profile_id` and `rule_id`.
6. **`list_filter_categories`**: List filter categories, such as adult content, gambling, and social media, and show whether each is enabled. Requires `profile_id`.
7. **`set_filter_category`**: Enable or disable a filter category. Requires `profile_id`, `slug`, and an `enabled` boolean.
8. **`simulate_policy`**: Check what the policy would do for a domain right now. Read-only. Requires `profile_id` and `domain`.
9. **`get_logs`**: Get recent DNS query logs. The action filter can be `allowed`, `blocked`, `refused`, `error`, or `rate_limited`. Accepts an optional `profile_id` and `limit` up to 100.
10. **`analytics_summary`**: Get summary statistics including total queries, blocked percentage, IPv4 and IPv6 counts, and encrypted queries. Accepts an optional `profile_id` and time window.
11. **`list_schedules`**: List time-based schedules on a profile. Requires `profile_id`.
12. **`create_schedule`**: Create a time-based schedule. Requires `profile_id`, `name`, an IANA timezone, a `days` array, and `start` and `end` times in `HH:MM` format.
13. **`delete_schedule`**: Delete a schedule. Destructive. Requires `profile_id` and `schedule_id`.
14. **`list_devices`**: List devices enrolled on a profile. Requires `profile_id`.
15. **`get_entitlements`**: Get the account plan, limits, and current usage.
16. **`get_referral_code`**: Get the account's referral code and link.

## Example requests

- "Block TikTok on my kids profile"
- "Show me what was blocked today"
- "Would youtube.com be blocked right now?"
- "Turn on adult content filtering"
- "Add a bedtime schedule 9pm to 7am on weekdays"

## Safe operation

- List profiles first to discover the correct profile IDs. Confirm the intended profile before changing its settings.
- Use `simulate_policy` to preview the current policy for a domain before creating a rule. Then create an allow or deny rule only when the user requests that change.
- Always confirm with the user before using `delete_rule` or `delete_schedule`, because those actions are destructive.
- For changes to filter categories or schedules, make sure the requested category, days, times, and timezone are clear before applying them.
- Use read-only tools such as `simulate_policy`, `get_logs`, and `analytics_summary` to answer questions without changing settings.
