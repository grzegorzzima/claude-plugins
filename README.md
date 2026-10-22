# grzegorzzima-plugins

Claude Code plugins for daily architecture and Azure work.

## Installation

Add the marketplace in Claude Code:

```
/plugin marketplace add grzegorzzima/claude-plugins
```

Then install a plugin:

```
/plugin install adr-scribe@grzegorzzima-plugins
```

## Plugins

### adr-scribe

Writes Architecture Decision Records (ADRs) into `docs/adr/` from the current design discussion.

```
/adr [title]
/adr supersede <number> [title]
```

- Looks for `docs/adr/`, `doc/adr/` or `adr/`, and creates `docs/adr/` if none exists.
- Numbers each ADR from the existing `NNNN-*.md` files, for example `0003-use-service-bus-sessions.md`.
- Fills in the context, the options considered, the decision and its consequences. It asks before writing if anything important is unclear.
- `supersede <number>` marks the old ADR as superseded and links the two records.
- Adds a row to `docs/adr/README.md` if that file has an index table.
- Never commits.

The skill runs only when you invoke `/adr`. Claude does not trigger it automatically.

## Development

```
claude plugin validate .                    # validate the marketplace and plugin manifests
claude --plugin-dir ./plugins/adr-scribe    # try a plugin in a session without installing it
```

To add a plugin, create `plugins/<name>/.claude-plugin/plugin.json` and its `skills/`, then add an entry to `.claude-plugin/marketplace.json`.
