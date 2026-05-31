# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this repo is

A personal Claude Code **plugin marketplace** owned by `jwmarshall`. It hosts one
or more plugins (slash commands, subagents, skills, hooks, MCP server configs) and
a marketplace manifest that lets Claude Code discover and install them.

This is a **content/configuration** repository, not an application. There is no
build, no test suite, and no runtime to start.

## Current state

- `.claude-plugin/marketplace.json` — marketplace manifest (`name: jwmarshall`).
- `scopewright/` — first plugin: a skill that scaffolds SCOPED review subagents.
  See `scopewright/README.md`.

## Layout

Follows the standard Claude Code marketplace structure:

```
.claude-plugin/
  marketplace.json        # marketplace manifest: name, owner, plugins[]
<plugin-name>/
  .claude-plugin/
    plugin.json           # plugin manifest: name, version, description
  skills/                 # skills (*/SKILL.md)
  commands/               # slash commands (*.md)
  agents/                 # subagents (*.md)
  hooks/                  # hook scripts + hooks.json
```

- The marketplace `name` field is `jwmarshall`.
- Each plugin lives in its own top-level directory and is referenced from
  `marketplace.json`'s `plugins` array (by its `source` path, e.g. `./scopewright`).
- Plugin and marketplace names are kebab-case.
- Skills reference bundled files via `${CLAUDE_PLUGIN_ROOT}/...`, which resolves to
  that plugin's own directory.

Reference docs: <https://docs.claude.com/en/docs/claude-code/plugins>

## Working conventions

- **Ask before scaffolding new plugins or changing the manifests.** The owner wants
  to approve structural decisions (naming, which plugins to include, layout) rather
  than have them inferred.
- Keep commits focused; default branch is `main`.
- A plugin's `reference/` holds specs the plugin reads at runtime (e.g. the SCOPED
  framework spec) — it ships with the plugin, it is not scratch material.
