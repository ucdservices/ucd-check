# Platform notes

Facts checked on 27 November 2026, from the current official docs and from `gh skill --help` on this machine (GitHub CLI 2.103.0, released 21 October 2026). Later files in this repo follow these notes. Where a doc and `AGENT_PROMPT.md` disagree, the doc wins, and the difference is listed at the end.

`gh skill` is in public preview. GitHub's docs say it needs GitHub CLI 2.90.0 or later.

## Skill folder locations

A skill is a folder with `SKILL.md` inside it. The folder name for this product is `ucd`. The repository keeps the authoring copy at `skills/ucd/`, which is the layout `gh skill` discovers. Installing copies that folder into a tool's own skills directory. The copy is what the tool loads. `evals/` stays in this repository and is not part of the skill folder.

### Where each tool reads skills

| Tool | Project | Personal |
|---|---|---|
| GitHub Copilot (cloud agent, code review, Copilot CLI, Copilot app, VS Code agent mode) | `.github/skills/`, `.claude/skills/`, `.agents/skills/` | `~/.copilot/skills/`, `~/.agents/skills/` |
| VS Code agent skills | Copilot harness: `.github/skills/` and `~/.copilot/skills/`. The VS Code docs also list Claude at `.claude/skills/` and `~/.claude/skills/`, and Codex at `.agents/skills/` and `~/.agents/skills/`. | Same table, personal column |
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Cursor | `.agents/skills/`, `.cursor/skills/`, and for compatibility `.claude/skills/` and `.codex/skills/` | `~/.agents/skills/`, `~/.cursor/skills/`, and for compatibility `~/.claude/skills/` and `~/.codex/skills/` |

Cursor walks these folders recursively and loads every `SKILL.md` it finds. A skill's name is the folder that contains `SKILL.md`.

### Where `gh skill install` writes

From `gh skill install --help` and the GitHub CLI host registry (`internal/skills/registry/registry.go`):

| `--agent` | `--scope project` (default) | `--scope user` |
|---|---|---|
| `github-copilot` | `.agents/skills/` | `~/.copilot/skills/` |
| `claude-code` | `.claude/skills/` | `~/.claude/skills/` |
| `cursor` | `.agents/skills/` | `~/.cursor/skills/` |

Project scope uses the git root. Copilot and Cursor share `.agents/skills/` at project scope, so installing for both writes the folder once. Claude Code is not part of that shared directory. The default agent, when the command is not interactive, is `github-copilot`. The default scope is `project`.

`--dir` overrides `--agent` and `--scope`. `--from-local` installs from a local directory instead of `OWNER/REPO`. Files are copied, not symlinked, and the CLI injects source-tracking metadata into the installed copy's frontmatter.

Manual install is a copy of `skills/ucd/` into one of the directories in the first table. The folder must stay named `ucd`.

## Frontmatter

### Agent Skills specification

Required: `name`, `description`. Optional: `license`, `compatibility`, `metadata`, `allowed-tools`.

`name` is 1 to 64 characters, lowercase letters, numbers and hyphens, must not start or end with a hyphen, must not contain `--`, and must match the parent folder. `description` is 1 to 1024 characters. `allowed-tools` is a space-separated string. This skill does not set `allowed-tools`.

### GitHub Copilot docs

The Copilot docs require `name` and `description`, and list `license` as optional. They also describe `allowed-tools`. They do not list `argument-hint`.

### VS Code

VS Code documents `name` and `description` as required, and documents `argument-hint`, `user-invocable`, `disable-model-invocation` and other fields. `name` must match the parent directory.

### Claude Code

Claude Code documents a wider set, including `argument-hint`. Its page "Using skill frontmatter outside Claude Code" says that outside Claude Code the allowed fields are only `name`, `description`, `license`, `compatibility`, `metadata` and `allowed-tools`. It shows this failure for anything else:

```text
Unexpected key(s) in SKILL.md frontmatter: argument-hint. Allowed properties are: allowed-tools, compatibility, description, license, metadata, name
```

Claude Code itself ignores a field it does not recognise. Uploads to claude.ai and the Skills API reject unknown keys.

### Cursor

Cursor's documented fields are `name`, `description`, `paths`, `disable-model-invocation`, `icon`, `color` and `metadata`. `name` must match the parent folder. `argument-hint` is not listed. Cursor warns when frontmatter does not parse, or when `description` is missing. It does not say an unknown key fails to load.

### What this skill uses

`name`, `description` and `license` only. `argument-hint` is left out. See the differences at the end.

## How a skill is invoked

| Tool | Slash command |
|---|---|
| VS Code / Copilot chat | Type `/` in chat, choose the skill, and add any extra words after it. Typing `/ucd` loads the skill. Copilot can also load it when the request matches the description. |
| Copilot CLI | Put the skill name in the prompt with a leading slash, for example `Use the /ucd skill to check app/views/email.njk`. `/skills list`, `/skills get ucd` and `/skills reload` manage skills. They are not the check. |
| Claude Code | Type `/ucd`. The `name` field is the command. Claude can also load the skill when the request matches the description. |
| Cursor | Type `/` in Agent chat and choose `ucd`. The skill attaches to that message. |

There is one command, `/ucd`. An optional path can follow it in the message. The skill decides which of the six checks apply. It does not register six commands.

## Copilot code review

Copilot code review can use repository skills when they are relevant. It reads skills, custom instructions and agent instructions from the pull request's head branch, not the base branch.

GitHub's how-to pages say:

- To make review use a skill more reliably, give the skill directory a review-focused name such as `code-review`.
- Skills already in `.github/skills/` can be used automatically when they are relevant.
- Review comments can attribute the skill that was used.

The concepts page lists project skills in `.github/skills/`, `.claude/skills/` and `.agents/skills/` as available to Copilot code review, cloud agent and VS Code. The code review how-to still names `.github/skills/` in particular.

This product keeps the folder name `ucd`, because that is the command. For a review on GitHub, copy or install the skill into the repository (`.github/skills/ucd/` is the path the code review how-to names). The description says that it reviews service templates, so review can select it when the changed files are relevant. A directory named `code-review` would be more likely to be selected, and this repo does not use that name.

When the skill runs as a review and there is nobody to ask, it posts findings as review comments with suggested changes and does not commit. That behaviour is specified in `skills/ucd/SKILL.md`.

## `gh skill` syntax

Checked with `gh skill --help`, `gh skill install --help`, `gh skill update --help` and `gh skill publish --help`.

Discover:

```bash
gh skill install OWNER/REPO
```

Without a skill name, a non-interactive run lists the skills it finds.

Install one skill:

```bash
gh skill install OWNER/REPO SKILL
gh skill install OWNER/REPO SKILL@v1.0.0
gh skill install OWNER/REPO --all
gh skill install ./local-repo SKILL --from-local
```

Flags used by this product:

- `--agent github-copilot`, `--agent claude-code`, `--agent cursor` (repeatable in the CLI; this repo's install docs pass one agent per command)
- `--scope project` or `--scope user`
- `--from-local` for a local checkout
- `--pin TAG` to lock a version so `gh skill update` skips it
- `--force` to overwrite

Version resolution when you do not pin: the latest tagged release, otherwise the default branch.

Update:

```bash
gh skill update
gh skill update SKILL
gh skill update --all
gh skill update --dry-run
gh skill update --force --all
```

`gh skill update` scans installed skills in known agent directories at project and user scope. Skills installed by hand, with no GitHub metadata in the frontmatter, are skipped in non-interactive mode.

Publish (not run for this release):

```bash
gh skill publish --dry-run
gh skill publish --tag v1.0.0
```

`--dry-run` validates and does not publish. A real publish creates a GitHub release. This repository does not run that.

Validation looks for `skills/*/SKILL.md` (and a few other layouts), checks the name rules, checks that `name` matches the directory, checks that `name` and `description` are present, checks that `allowed-tools` is a string if set, and strips install metadata (`metadata.github-*`) from what it publishes.

## Differences from the brief

1. **`argument-hint` is not in the frontmatter.** The brief allowed it only if every targeted tool accepts it without failing validation. The Agent Skills spec does not define it. Claude's own docs show that packaging and claude.ai upload fail with `Unexpected key(s) in SKILL.md frontmatter: argument-hint`. Cursor does not document it. VS Code and Claude Code do document it for their own chat UI. It is omitted so the skill stays on the spec's fields.
2. **Copilot code review prefers a directory named `code-review`, inside `.github/skills/`.** The product name and command stay `ucd`. Install docs tell people who want review on GitHub to put the folder in `.github/skills/ucd/` as well as using `gh skill install`, which writes `.agents/skills/ucd/` for Copilot at project scope.
3. **`gh skill install` for Copilot does not write `.github/skills/`.** Copilot still reads `.agents/skills/`. Both paths are documented above. The install section of the README gives the CLI command and the manual copy.

## Sources

- [Agent Skills specification](https://agentskills.io/specification) (fetched 27 November 2026)
- [Agent skills (GitHub Copilot concepts)](https://docs.github.com/en/copilot/concepts/customizations/agent-skills) (fetched 27 November 2026)
- [Adding agent skills for GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills) (fetched 27 November 2026)
- [Adding agent skills for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-skills) (fetched 27 November 2026)
- [GitHub Copilot code review](https://docs.github.com/en/copilot/concepts/agent-capabilities/agent-powered-workflows-and-operations/code-review) (fetched 27 November 2026)
- [Using GitHub Copilot code review](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-code-review) (fetched 27 November 2026)
- [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills) (fetched 27 November 2026)
- [Extend Claude with skills](https://code.claude.com/docs/en/skills) (fetched 27 November 2026)
- [Agent Skills (Cursor)](https://cursor.com/docs/skills) (fetched 27 November 2026)
- [GitHub CLI skill host registry](https://github.com/cli/cli/blob/trunk/internal/skills/registry/registry.go) (fetched 27 November 2026)
- `gh skill --help`, `gh skill install --help`, `gh skill update --help`, `gh skill publish --help` (GitHub CLI 2.103.0)
