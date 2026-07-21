# AGENT_SETUP.md — instructions for a Claude agent installing this skill

You (Claude) have been given this repo's link and asked to set up the **resume-studio** skill for your user. Follow the path that matches your environment, then run the verification step. Keep the user's effort to near zero.

## 1. Detect your environment

- **Claude Code (CLI)** — you have shell access to the user's machine and `~/.claude/skills/` is a real, writable path.
- **Claude.ai / Cowork (cloud or desktop app)** — you run in a sandbox; skills are installed by the USER clicking "Save skill" on a `.skill` file card. You cannot install it yourself.

## 2A. Claude Code path

```bash
git clone --depth 1 https://github.com/Sidgit11/resume-studio /tmp/resume-studio-repo
mkdir -p ~/.claude/skills/resume-studio
cp -r /tmp/resume-studio-repo/SKILL.md /tmp/resume-studio-repo/references /tmp/resume-studio-repo/scripts ~/.claude/skills/resume-studio/
pip install python-docx --break-system-packages 2>/dev/null || pip install python-docx
```

Do NOT copy `evals/`, `README.md`, `AGENT_SETUP.md`, or the `.skill` file — the skill only needs `SKILL.md`, `references/`, `scripts/`.

## 2B. Claude.ai / Cowork path

1. Download the packaged skill file from the repo:
   `https://raw.githubusercontent.com/Sidgit11/resume-studio/main/resume-studio.skill`
   (fetch it into your workspace; if raw fetch fails, clone the repo and use the `.skill` file from it).
2. Send that `.skill` file to the user using your file-delivery tool.
3. Tell the user: **"Click Save skill on the card above — that's the one click. It's then available in every session."**

## 3. Verify and hand off

1. Confirm installation: the skill list should now include `resume-studio` (in Claude Code, check the folder exists; in Claude.ai, ask the user to confirm they clicked Save).
2. Ask the user ONE question: *"Where should your career memory live?"* Recommend a permanent, connected folder (not a throwaway session workspace) — the skill stores everything in a `resume-studio/` folder there, and that folder is what makes memory persist across sessions.
3. Tell the user how to start, exactly this simple:
   > You're set. Whenever you're ready, say: **"Build my professional profile — here's my old resume and some notes."** Attach anything: old resumes, LinkedIn PDF, performance reviews, random notes. Messy is fine.

## Troubleshooting

- `python-docx` missing at render time → install it (`pip install python-docx --break-system-packages`); the skill's script needs it only when producing `.docx` files.
- User's org blocks skill saving → fall back to reading `SKILL.md` from the repo at the start of each resume session and following it directly; everything still works, it just isn't one-click.
- Never modify the user's `resume-studio/` data folder during setup — setup touches skill files only.
