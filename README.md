# Mandate Law plugins for Claude Code

## mandate-counsel

Before your coding agent builds a change, `mandate-counsel` checks it against a list of **counsel triggers**: changes that can make a privacy policy or terms false, or create new legal obligations. Examples are a new AI feature or model provider, an agent that takes actions or spends money, new kinds of sensitive data, analytics or session-replay SDKs, and features for minors.

If a planned change matches a trigger, the agent stops before building that part and tells you which trigger matched and why. The rest of the work continues. It also connects your agent to Mandate Law's free tools at `https://mandatelaw.ai/mcp/public` (no account or sign-in): `check_change` screens a planned change against the triggers, and `check_scope` says whether a legal need is in scope and what review would cost. See [mandate-counsel/README.md](mandate-counsel/README.md) for exactly what it sends.

### Install

```
/plugin marketplace add mandate-law/claude-plugins
/plugin install mandate-counsel@mandate-law
```

### What it does and doesn't do

- A match means the change should get legal review before it ships. A non-match is not legal advice and does not mean a change is compliant.
- The connector's tools are free. Legal review itself is a fixed-fee service, arranged with the firm, never started by the plugin on its own.
- It never sends secrets, credentials, user data, or whole files. Facts are sent as short excerpts with file paths.
- To tailor the triggers to your product, copy `mandate-counsel/skills/counsel-triggers/triggers.json` to `.counsel/triggers.json` in your repository; the plugin uses that copy when it exists.

Using another coding agent? The same check works from a rules file: see https://mandatelaw.ai/agents-snippet.md.

### About

Mandate Law provides legal counsel for AI products, agents, and the consumer apps they live in: https://mandatelaw.ai. Allen Gibby, admitted in the District of Columbia only.

This repository is attorney advertising. It contains legal information, not legal advice. Using it does not create an attorney-client relationship; that requires a signed engagement letter.

Licensed under CC BY 4.0.
