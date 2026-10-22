# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A Claude Code plugin marketplace (`grzegorzzima-plugins`) for architecture and Azure work. There is no build, lint, or test tooling. Everything is JSON manifests plus Markdown skill files.

## Layout and how the pieces connect

- `.claude-plugin/marketplace.json` is the marketplace manifest. Each entry in `plugins[]` points at a plugin directory through `source` (relative path, e.g. `./plugins/adr-scribe`).
- `plugins/<name>/.claude-plugin/plugin.json` is the plugin manifest. It holds `name`, `description`, `version`, and `author`. Its `name` must match the marketplace entry's `name`.
- `plugins/<name>/skills/<skill>/SKILL.md` defines a skill. The frontmatter carries `name`, `description`, `argument-hint`, and `disable-model-invocation`. The body can reference sibling files, such as `template.md`, with relative links.

To add a plugin, create its directory with `plugin.json` and its skills, then add a matching entry to `marketplace.json`. When you change a plugin, bump `version` in its `plugin.json`.

## Current plugins

- **adr-scribe**: the `/adr` skill writes Architecture Decision Records into `docs/adr/` of the *target* project, not this repo. It fills in `template.md` and supports `supersede <number>`. `disable-model-invocation: true` means the skill runs only when the user invokes it explicitly.

## Validating and testing locally

```
claude plugin validate .                       # check marketplace/plugin manifests
claude --plugin-dir ./plugins/adr-scribe       # load one plugin in a session for testing
```

Inside Claude Code, run `/plugin marketplace add <path-to-this-repo>` to install the marketplace from the local checkout.
