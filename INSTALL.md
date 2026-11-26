# Installing build-then-break

Three ways. Pick one. All of them install the skill at the user level, so it works in every project.

After any of them, start a fresh Claude Code session so the skill loads.

## 1. Ask Claude Code to install it from GitHub

Paste this into Claude Code:

```text
Please install the build-then-break skill for Claude Code from this public repo:
https://github.com/jiffi-co/build-then-break

Install it at the user level so it works in every project, and set it up so you always use it:

1. Before you install anything, read the skill's files and tell me in plain English what it does and whether anything in it runs commands or touches my files.

2. Download the repo to a temporary folder (git clone, or the zip from GitHub if git isn't available). Copy its skills/build-then-break folder to ~/.claude/skills/build-then-break/ so SKILL.md sits directly in that folder, with the references/ folder beside it. On Windows, ~ is my user folder. If a build-then-break skill is already there, show me what would change and ask before replacing it. Delete the temporary folder when you're done.

3. Add this section to ~/.claude/CLAUDE.md. If the file doesn't exist, create it. If it does exist, add the section at the end and don't change anything already in it.

   ## Build, then break
   For any task that writes, edits, refactors, debugs or reviews code, and before calling any plan or analysis done, use the build-then-break skill and follow it. Match effort to the stakes as the skill describes.

4. Show me the final folder structure and the exact section you added to CLAUDE.md, then tell me to start a fresh session so it all loads.
```

## 2. Ask Claude Code to install it from a zip

If someone sent you `build-then-break.zip`, paste this in and add the path to the file:

```text
I've downloaded a Claude Code skill called build-then-break as a zip. It's here: [drag the zip in or paste the path, e.g. ~/Downloads/build-then-break.zip]

Please install it at the user level so it works in every project, and set it up so you always use it:

1. Unzip it into ~/.claude/skills/build-then-break/ so SKILL.md sits directly in that folder, with the references/ folder beside it. Leave out any __MACOSX or .DS_Store files.

2. Add this section to ~/.claude/CLAUDE.md. If the file doesn't exist, create it. If it does exist, add the section at the end and don't change anything already in it.

   ## Build, then break
   For any task that writes, edits, refactors, debugs or reviews code, and before calling any plan or analysis done, use the build-then-break skill and follow it. Match effort to the stakes as the skill describes.

3. Show me the final folder structure and the exact section you added to CLAUDE.md, then tell me to start a fresh session so it all loads.
```

## 3. Do it by hand

Mac or Linux, in a terminal:

```sh
git clone --depth 1 https://github.com/jiffi-co/build-then-break /tmp/build-then-break
mkdir -p ~/.claude/skills
cp -R /tmp/build-then-break/skills/build-then-break ~/.claude/skills/
rm -rf /tmp/build-then-break
```

Windows, in PowerShell:

```powershell
git clone --depth 1 https://github.com/jiffi-co/build-then-break "$env:TEMP\build-then-break"
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -Force "$env:TEMP\build-then-break\skills\build-then-break" "$env:USERPROFILE\.claude\skills\"
Remove-Item -Recurse -Force "$env:TEMP\build-then-break"
```

Then add this to the end of `~/.claude/CLAUDE.md` (create the file if it isn't there):

```markdown
## Build, then break
For any task that writes, edits, refactors, debugs or reviews code, and before calling any plan or analysis done, use the build-then-break skill and follow it. Match effort to the stakes as the skill describes.
```

## Check it worked

You should have:

```text
~/.claude/skills/build-then-break/
├── SKILL.md
└── references/
    ├── examples.md
    └── worked-example.md
```

In a fresh Claude Code session, ask: "Which skills do you have?" You should see build-then-break in the list.

## Removing it

Delete the `~/.claude/skills/build-then-break` folder and remove the "Build, then break" section from `~/.claude/CLAUDE.md`.
