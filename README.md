# Claude Code – Credit Balance Error Fix

## Problem

Users running Claude Code commands (e.g., `/init`, `/help`, or custom commands) may encounter:

```
Credit balance too low · Add funds:
```

This error appears when the Anthropic account associated with your Claude Code session has insufficient credits to process the request.

## Cause

Claude Code uses the Anthropic API under the hood. Each command that invokes the model consumes API credits. When your account balance drops to zero (or below a minimum threshold), all API-backed commands fail with this message.

Note: Built-in informational commands (like `/help`) may also surface this error if they require a network round-trip to validate session state.

## Resolution

1. **Add funds to your Anthropic account**
   - Visit [console.anthropic.com](https://console.anthropic.com) and navigate to **Billing**.
   - Add a payment method and purchase credits.

2. **Check your API key**
   - Confirm the `ANTHROPIC_API_KEY` environment variable is set to the correct key for the funded account.
   - Run `echo $ANTHROPIC_API_KEY` to verify it is set.
   - If using a different key, update it: `export ANTHROPIC_API_KEY=sk-ant-...`

3. **Verify credit balance via the API**
   ```bash
   curl https://api.anthropic.com/v1/organizations/me \
     -H "x-api-key: $ANTHROPIC_API_KEY" \
     -H "anthropic-version: 2023-06-01"
   ```

4. **Restart Claude Code** after adding funds or updating the API key.

## Prevention

- Set up **automatic recharge** in the Anthropic console billing settings.
- Configure **usage alerts** to receive notifications before your balance runs out.
- For team use, consider switching to a **committed usage plan** to avoid interruptions.

## Related

- [Anthropic Console – Billing](https://console.anthropic.com/settings/billing)
- [Claude Code Documentation](https://code.claude.com/docs/en/overview)
- [Anthropic API Reference](https://docs.anthropic.com/en/api)
