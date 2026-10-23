# Boson Feedback Collection

Report problems with Boson products during the hackathon: Higgs Realtime, Avatar, TTS, and anything else.
This repo is public: everything you post here, including attachments, is visible to anyone.

## How to file an issue (about 2 minutes)

1. Go to **Issues → New issue** and pick the form for your product, or **Feature request or feedback** for ideas.
2. Fill the required fields: product, severity, what happened, and how to reproduce.
   Everything else is optional; partial info is better than none. Any language or format is fine.
3. Add evidence if you have it: request IDs with timestamps (include the timezone), logs, a short script,
   screenshots, or recordings. Drag and drop files into the evidence field.
   GitHub does not accept raw audio files, so zip `.wav` / `.mp3` files first.

## Let your AI agent file it

Coding agents such as Claude Code, Codex, or Cursor can collect the details, redact secrets, and file the issue for you.
You need the [GitHub CLI](https://cli.github.com/) logged in (`gh auth login`). Then tell your agent:

```text
Read https://raw.githubusercontent.com/boson-ai/Boson-Feedback-Collection/main/skills/report-boson-issue/SKILL.md
and follow it to report the problem I just hit.
```

The agent shows you the draft and files it only after you approve.
To keep the skill installed for Claude Code, save it once:

```bash
mkdir -p ~/.claude/skills/report-boson-issue
curl -fsSL https://raw.githubusercontent.com/boson-ai/Boson-Feedback-Collection/main/skills/report-boson-issue/SKILL.md \
  -o ~/.claude/skills/report-boson-issue/SKILL.md
```

**AI agents:** to file an issue in this repo, follow [`skills/report-boson-issue/SKILL.md`](skills/report-boson-issue/SKILL.md).

## What a good report looks like

> **Product:** TTS · **Severity:** Major
>
> **What happened?**
> Summary: Long inputs are cut off.
> Expected: The full paragraph is spoken.
> Actual: Audio stops after about 20 seconds; the last two sentences are missing.
>
> **How to reproduce**
> Send the attached 600-character paragraph to the TTS endpoint with default settings.
>
> **Details:** SDK version, model name, region, macOS / Python,
> request `req_8f2c1a` at 2026-10-23 14:05 UTC+8
>
> **Evidence:** input text pasted, `output.zip` attached

## What happens after filing

Every report starts with `needs-triage` and an `area:*` label for its product. The Boson team then updates the labels:

| Label | Meaning |
|---|---|
| `needs-triage` | New, not reviewed yet |
| `needs-info` | We need more details; please reply on the issue |
| `confirmed` | We reproduced it |
| `duplicate` | Already reported; we link the original issue |

## What NOT to post

- API keys, access tokens, passwords, or `Authorization` headers
- Private or personal data (yours or anyone else's)
- Unredacted logs or screenshots: replace secrets with `***` before posting

If you posted a secret by mistake, rotate it immediately and tell an organizer.

## Maintainers

Create the labels in [`.github/labels.yml`](.github/labels.yml) before participants start filing.
GitHub silently skips form labels that do not exist in the repo.
