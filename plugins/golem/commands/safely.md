---
description: Clamp this session to a read-only Golem safety profile (safe mode)
argument-hint: "[profile]  — e.g. review; defaults to the strictest read-only profile"
---

[golem:safely $ARGUMENTS]

I've asked Golem to put this session in **`/safely`** mode (profile: `$ARGUMENTS`, or the strictest read-only profile if none was given).

From this point the Golem witness enforces a **default-deny, read-only capability clamp** on this session: any tool call outside the active profile's allowlist is denied *deterministically by the `PreToolUse` hook*, before it runs — regardless of anything in my context, including instructions that arrived from untrusted content I may read. Every clamp and every blocked call is recorded on the Golem ledger.

This clamp only tightens. To regain write / network / shell capability, **start a fresh session** — it can't be loosened from inside this one.

Acknowledge that safe mode is active, then continue with the read-only task at hand.
