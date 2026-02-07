# Model: GPT-5.1-Codex-Max

**User:**
Why can't I use codex in CLI 

```
D:\xenium-multisection-pipeline codex
╭──────────────────────────────────────────────────────╮
│ >_ OpenAI Codex (v0.66.0)                            │
│                                                      │
│ model:     gpt-5.1-codex-max high   /model to change │
│ directory: D:\xenium-multisection-pipeline           │
╰──────────────────────────────────────────────────────╯

  Tip: Use /feedback to send logs to the maintainers when something looks off.

⚠ MCP client for `tooluniverse` failed to start: MCP startup failed: program not found

⚠ MCP startup incomplete (failed: tooluniverse)


› why can't I use codemachine


■ unexpected status 401 Unauthorized:
```

**ChatGPT:**
A 401 in the Codex CLI means the request never authenticated successfully. The most common fixes are:

1. **Re-authenticate the CLI.** Run `openai auth login` (or follow the CLI prompt) to refresh your token. Make sure the account you log in with has access to the `gpt-5.1-codex-max` tier.
2. **Check your environment variables.** If you use API keys, ensure `OPENAI_API_KEY` (and `OPENAI_BASE_URL` if customized) are set in the same shell where you launch `codex`.
3. **Update the CLI.** Older Codex CLI builds can fail auth; run `pip install --upgrade openai-codex` (or your package manager) to get the latest version.
4. **Remove stale config.** Delete the CLI config directory (e.g., `~/.config/openai-codex` on Linux/macOS or `%AppData%\openai-codex` on Windows) and log in again.

After re-login, test the credentials with a simple call like `openai api models.list`. If that works but the Codex UI still throws 401, it usually means your account or API key lacks permission for that specific model; switch to a model you’re allowed to use or ask your org admin to enable it.

**User:**
jUST HAD ANOTHER ONE BACK TO BACK WITH HIM

**ChatGPT:**
If it’s happening back-to-back even after logging in, try a full reset of the CLI auth state and verify you’re using the intended account/project:

1. **Log out, then log in again.** Run `openai auth logout` followed by `openai auth login` to force a fresh session.
2. **Confirm which account/project the CLI is using.** If your org uses projects, make sure any `OPENAI_PROJECT` (or similar) variable points to the right project for Codex access.
3. **Check for multiple keys.** If you have multiple `OPENAI_API_KEY` values across shells or profiles, remove old ones and keep only the valid key in the active shell.
4. **Delete cached auth files (last resort).** Remove the CLI config directory and re-authenticate.

If you can share the output of `openai auth status` (redacting secrets), I can help pinpoint where the auth mismatch is happening.
