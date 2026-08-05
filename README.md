# Oh My Pi — Personal Harness Setup

Personal, versioned collection of skills, agents, rules, and prompts for Oh My Pi (OMP). This repo is the source of truth: a setup script (see Roadmap) clones it and installs the content into your OMP config folders — user-wide or per project.

## Layout

| Path | What it is | Installs to (user) | Installs to (project) |
|---|---|---|---|
| `skills/<name>/SKILL.md` | Skills: named capability packs the model loads on demand | `~/.omp/agent/skills/<name>/` | `<repo>/.omp/skills/<name>/` |
| `agents/<name>.md` | Custom task agents the `task` tool can dispatch | `~/.omp/agent/agents/` | `<repo>/.omp/agents/` |
| `rules/<name>.md` | Rules applied automatically when they match | `~/.omp/agent/rules/` | `<repo>/.omp/rules/` |
| `prompts/<name>.md` | Reusable prompt files | `~/.omp/agent/prompts/` | `<repo>/.omp/prompts/` |
| `templates/` | Starter files for new content | — (never installed) | — (never installed) |

`skills/` holds real content. `agents/`, `rules/`, and `prompts/` are empty folders kept in git via a `.gitkeep` placeholder — drop the placeholder once the folder holds its first real file.

## How OMP discovers this content

- **User level**: `~/.omp/agent/...`. With `omp --profile <name>` it becomes `~/.omp/profiles/<name>/agent/...`.
- **Project level**: the nearest `<ancestor>/.omp/` walking up from the working directory — the repo root is the natural place.
- **Precedence**: project overrides user; user agents override OMP's bundled agents (e.g. `scout`, `reviewer`); dedup is by name, first match wins — keep names unique across your whole config.
- **Skills layout is non-recursive**: exactly `<skills-root>/<name>/SKILL.md`, one level deep. Nested subfolders are not discovered.

## Adding a skill

1. Copy the template: `cp -R templates/skill skills/<your-skill-name>`
2. Fill in the frontmatter and body (fields below).
3. Keep reference assets inside the skill folder and access them as `skill://<your-skill-name>/...`.

SKILL.md frontmatter:

| Field | Purpose |
|---|---|
| `name` | Skill name; defaults to the folder name. |
| `description` | **Required.** One or two sentences: what it does and when to use it. Matching quality depends on this. |
| `globs` | Optional. File patterns that make the skill relevant, e.g. `["**/*.ts"]`. |
| `alwaysApply` | Optional. `true` = loaded in every session. |
| `hide` | Optional. `true` = omitted from the system-prompt skill list; still reachable via `skill://<name>`. |
| `disableModelInvocation` | Optional. `true` = same as `hide` (Agent Skills compatibility). |

Body: short and actionable — when to use it, the method (numbered steps), and boundaries (what it must not do).

## Adding an agent

1. Copy the template: `cp templates/agent.md agents/<your-agent-name>.md`
2. Fill in the frontmatter; the markdown body is the agent's instructions.

Required: `name`, `description`, and either a `systemPrompt` frontmatter field or instructions in the body. Optional fields: `tools` (allowlist; `yield` is added automatically), `spawns` (`*` or CSV), `model` (selector or `@role` alias), `thinkingLevel`, `output` (structured-output schema), `blocking`, `autoloadSkills`, `readSummarize`, `prewalk`.

## Adding a rule or prompt

- **Rule**: `cp templates/rule.md rules/<name>.md` — rules apply automatically when their conditions match; a top-level `RULES.md` in the agent dir is always applied.
- **Prompt**: `cp templates/prompt.md prompts/<name>.md` — the body is the prompt text.

## Installing

The setup script is the next step for this repo (see Roadmap). Until it exists, install manually.

POSIX (macOS/Linux) — user install:

```bash
install -d ~/.omp/agent/{skills,agents,rules,prompts}
cp -R skills/* ~/.omp/agent/skills/
cp agents/*.md ~/.omp/agent/agents/
cp rules/*.md ~/.omp/agent/rules/
cp prompts/*.md ~/.omp/agent/prompts/
```

PowerShell (Windows) — user install:

```powershell
$dst = "$HOME\.omp\agent"
New-Item -ItemType Directory -Force "$dst\skills","$dst\agents","$dst\rules","$dst\prompts" | Out-Null
Copy-Item skills\* $dst\skills -Recurse -Force
Copy-Item agents\*.md $dst\agents -Force
Copy-Item rules\*.md $dst\rules -Force
Copy-Item prompts\*.md $dst\prompts -Force
```

Project install: same commands against `<repo>/.omp/...` instead. Re-running replaces the previous copy — the repo remains the single source of truth, so edit here and reinstall.

## Roadmap

- [ ] `scripts/install.sh` (macOS/Linux) and `scripts/install.ps1` (Windows):
  - `--user` (default): install into `~/.omp/agent/...`; `--profile <name>` targets `~/.omp/profiles/<name>/agent/...`
  - `--project`: install into `<cwd>/.omp/...`
  - `--link`: symlink instead of copy, so repo edits apply immediately
  - idempotent re-runs; never touches `templates/`
- [ ] Slash commands (`commands/*.md`) if needed
- [ ] MCP server config if needed

## License

MIT — see [LICENSE](LICENSE).
