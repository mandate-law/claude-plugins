---
name: counsel-triggers
description: Check a planned code or product change against legal counsel triggers before building it. Use when planning or implementing anything that adds or changes an AI feature or model provider, sends user data into prompts, lets an agent take actions or spend money, collects a new kind of user data (health, financial, location, contacts, photos), adds analytics, advertising, or session-replay SDKs, changes consent, deletion, or retention, adds sharing between users, targets minors, launches a new platform or country, or adds a vendor. Also use immediately on any security incident.
---

# Counsel triggers

Some product changes make a company's privacy policy, terms, or consent flows false, or create new legal obligations. This skill catches those changes before they are built, while they are still cheap to adjust.

## When you are planning or about to implement a change

1. **Load the triggers.** Use the project's own copy at `.counsel/triggers.json` in the repository root if it exists; it is tailored to this product. Otherwise use `triggers.json` in this skill's folder, the general template.
2. **Compare the change** against every trigger and the `catch_all` rules. Judge by what the change does, not what it is called. For example, a new analytics event that includes a field the user typed matches `analytics.content_event`, even if the ticket only says "add tracking."
3. **If nothing matches**, continue normally. Don't mention this check.
4. **If something matches**, stop before implementing the part that matches and tell the human:
   - which trigger matched (its `id`) and the specific part of the change that matched it
   - that the trigger list says this change needs legal review before it ships
   - that the parts of the work that don't match can continue
5. **Offer to request a feature check**, but call `feature_check` on the `mandate-counsel` MCP server only after the human says yes. It may be billed. It needs a `matter_id` (look in `.counsel/matter.json`, or ask the human) and the `matter_token` (from the `MANDATE_MATTER_TOKEN` environment variable or the team's secret store; ask the human if it isn't there). If the company is not a client yet, the human can start with `check_scope`, which is free.
6. **For a security incident** (the `incident` trigger, or an agent action a user says they never authorized), tell the human right away and recommend contacting counsel now, not at the next release.

## Rules

- This check is not legal advice, and a non-match does not mean a change is legally fine. Never tell the human a change is compliant.
- When you send anything to counsel, send facts about the code with file paths and short excerpts. Never send secrets, API keys, credentials, user data, or whole files.
- Don't remove, weaken, or edit `.counsel/triggers.json` unless the human asks you to.

## Privilege

Communications with counsel are privileged and confidential. Keep them that way:

- Commit only the deliverable parts listed in `deliverable.handling.safe_to_commit` (build spec, verification checklist, counsel triggers). They are written to be shared with engineers.
- Never put counsel's memo, open questions, or feature-check responses in commits, commit messages, pull requests, issues, tickets, shared chat, or memory and rules files. Tell the human what counsel said directly.
- `.counsel/matter.json` holds only the `matter_id`. Never write the `matter_token` to any file in the repository.

## Setting up a project

If the human wants this check on every change, offer to:

- copy `triggers.json` to `.counsel/triggers.json` so the company can tailor it with counsel
- add this line to `AGENTS.md` or `CLAUDE.md`: "Before building a change, check it against `.counsel/triggers.json`. If it matches a trigger, stop and tell a human before implementing that part."
