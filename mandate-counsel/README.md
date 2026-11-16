# Mandate Counsel

Before your coding agent builds a change, Mandate Counsel checks it against a list of **counsel triggers**: changes that can make a privacy policy or terms false, or create new legal obligations. Examples are a new AI feature or model provider, an agent that takes actions or spends money, new kinds of sensitive data, analytics or session-replay SDKs, and features for minors.

If a planned change matches a trigger, the agent stops before building that part and tells you which trigger matched and why. The rest of the work continues.

## What's included

- **A skill, `counsel-triggers`,** with a copy of the trigger list (`skills/counsel-triggers/triggers.json`). The comparison happens in your agent; nothing is sent anywhere for it.
- **A connector to Mandate Law's free tools** at `https://mandatelaw.ai/mcp/public` (no account or sign-in):
  - `check_change`: screens a short description of a planned change against the triggers.
  - `check_scope`: says whether a legal need is in scope, what each fitting service covers, and its fixed fee.
  - `get_counsel_triggers`: returns the current trigger list.
  - `conflict_check`: records names for a conflict check, for the attorney's review. The agent uses it only if you ask.

## What it sends, and where

The plugin runs no scripts, hooks, or commands, and installs nothing. The only data that leaves your machine is what your agent passes to one of the connector's tools at `https://mandatelaw.ai/mcp/public`: a short description of a change or a legal need, or the names you give for a conflict check. The skill tells the agent never to send code, file contents, secrets, credentials, or user data. Scope checks and change checks aren't stored, only counted anonymously. Conflict-check names are stored encrypted for the attorney's review. Details: https://mandatelaw.ai/privacy and https://mandatelaw.ai/connector.

## Tailoring the triggers

Copy `skills/counsel-triggers/triggers.json` to `.counsel/triggers.json` in your repository. The skill uses that copy when it exists, so a company can tailor it with counsel.

## Not legal advice

A match means the change should get legal review before it ships. A non-match is not legal advice and does not mean a change is compliant. Mandate Law is the law practice of Allen Gibby, admitted in the District of Columbia only. Using this plugin does not create an attorney-client relationship; that requires a signed engagement letter. This plugin is attorney advertising.

## License

CC BY 4.0. Terms of use: https://mandatelaw.ai/terms.
