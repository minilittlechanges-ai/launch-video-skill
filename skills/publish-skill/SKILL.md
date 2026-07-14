---
name: publish-skill
description: "Publish (upload) a Claude agent skill to a public GitHub `skills` mono-repo in the skills.sh layout, so it becomes installable via `npx skills add <owner>/skills` and discoverable. Use when you have a SKILL.md (or skill folder) and want it live on GitHub: it sets up the skills/<name>/ structure, YAML frontmatter, .claude-plugin/plugin.json, and the README index tables, then commits and pushes. Handles both first-time repo creation and adding a new skill to an existing skills repo."
---

# Publish Skill to GitHub

Take a skill (a `SKILL.md`, optionally with `references/` and `scripts/`) and publish it to a public GitHub `skills` mono-repo following the skills.sh convention.

## Target layout

```
<owner>/skills
├─ .claude-plugin/plugin.json     "skills": ["./skills/"]
├─ README.md                      table of all skills + npx install
├─ LICENSE                        MIT
├─ assets/                        images used by README (keep OUT of skills/)
└─ skills/
   ├─ README.md                   index table
   └─ <skill-name>/
      ├─ SKILL.md                 YAML frontmatter + instructions
      ├─ references/              (optional) usage docs
      └─ scripts/                 (optional) runnable scripts
```

## Steps

1. **Frontmatter.** The skill's `SKILL.md` must start with YAML frontmatter:
   ```
   ---
   name: <kebab-name>
   description: "One paragraph — what it does AND when to use it. Make it trigger-rich; this is what gets matched and indexed."
   ---
   ```
   Runnable (tool-using) skills may also add `allowed-tools`, `argument-hint`, `effort`, `disable-model-invocation`.

2. **Place it** at `skills/<name>/SKILL.md`. Put any hero/cover image in the root `assets/` folder, never inside the skill folder.

3. **Manifest.** Root `.claude-plugin/plugin.json`:
   ```json
   { "name": "...", "version": "...", "description": "...",
     "author": { "name": "...", "url": "..." },
     "homepage": "...", "repository": "...",
     "license": "MIT", "keywords": ["skills", "..."], "skills": ["./skills/"] }
   ```

4. **Index in both READMEs.** Add a row to the root `README.md` table and to `skills/README.md`. Keeping a `skills/README.md` also gives `skills/` a second entry, so GitHub shows it as a folder instead of collapsing `skills/<only-skill>` into one row.

5. **Commit as the brand, not a personal email.** Use the account's GitHub no-reply address so a personal account never shows up as a contributor:
   ```bash
   id=$(gh api users/<owner> --jq .id)
   git -c user.name="<owner>" \
       -c user.email="${id}+<owner>@users.noreply.github.com" \
       commit -m "..."
   ```

6. **Push.**
   - First time: `gh repo create <owner>/skills --public --source=. --remote=origin --push`
   - After that: `git push`
   - Auth: either a `gh` login **as `<owner>`**, or a `GH_TOKEN` for headless work. `gh repo create` uses `GH_TOKEN`; a plain `git push` needs it fed in:
     ```bash
     git -c credential.helper='!f(){ echo username=x-access-token; echo "password=$GH_TOKEN"; };f' push
     ```
   - Gotcha: a **fine-grained** PAT cannot create repos (`Resource not accessible ... createRepository`). Use a **classic** token with the **`repo`** scope, or create the empty repo in the browser first and only push.

7. **Verify.**
   ```bash
   curl -s -o /dev/null -w "%{http_code}\n" \
     https://raw.githubusercontent.com/<owner>/skills/main/skills/<name>/SKILL.md   # expect 200
   gh api "repos/<owner>/skills/git/trees/main?recursive=1" --jq '.tree[].path'      # check layout
   ```

## Install (what users run)

```bash
npx skills add <owner>/skills                    # all skills
npx skills add <owner>/skills --skill <name>     # one skill
```
