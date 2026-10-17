# Golem — Claude Code plugin

Signs every tool call into a tamper-evident ledger, blocks or gates the ones
policy refuses, and gives each session your fleet's context.

```
/plugin marketplace add GolemTeam/golem-team-plugin
/plugin install golem@golem
```

## It needs the agent

The plugin points Claude Code at a Golem agent on **this machine**
(`127.0.0.1:39393`) — that is why it needs no OAuth and no browser: the agent
holds a per-host credential, enrolled once, and authenticates upstream itself.
Without the agent running, the MCP servers and hooks resolve to nothing and
Claude Code carries on unaffected.

```bash
curl -fsSL https://app.golem.team/install.sh | GOLEM_WORKSPACE_KEY=glk_... sh
```

A workspace key comes from <https://app.golem.team/workspace-keys>.

## What it registers

- **MCP** — `golem-witness` (the in-path gateway) and `golem-context` (search
  your agents' history, pull artifacts from the ledger, see the fleet).
- **Hooks** — the six events the agent serves. `PreToolUse` is the one that can
  refuse a call.
- **`/safely`** — clamp the session to a read-only profile.
- **`golem-fleet` skill** — find out what other agents are doing before you act.

`install.sh` wires all of this too, and the agent re-wires it after every update.
The plugin exists so a Claude Code user can start from the marketplace instead.
