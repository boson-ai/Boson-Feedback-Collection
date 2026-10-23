---
name: report-boson-issue
description: File a bug report or feedback about a Boson product (Higgs Realtime, Avatar, TTS, or other Boson APIs) to the public boson-ai/Boson-Feedback-Collection GitHub repo. Use when the user hits a Boson product problem or asks to report one.
---

# Report a Boson issue

Target repo: `boson-ai/Boson-Feedback-Collection` (public: anyone can read what you post).

## 1. Gather

Build the report from the conversation, the workspace, and recent command output before asking the user anything. Ask only for what you cannot find. The report is complete when it has:

- **Product**: Higgs Realtime, Avatar, TTS, or Other.
- **Severity**: Blocker (cannot continue), Major (painful workaround), or Minor.
- **What happened**: a one-line summary, expected behavior, actual behavior.
- **How to reproduce**: numbered steps, plus the smallest script that triggers the problem when one exists.

Add whatever else you can find: issue type, SDK or API version, model name, endpoint or region, OS and language, request IDs with timestamps (with timezone), relevant log lines, and evidence. For TTS and Realtime, the input text and the output audio file are the most useful evidence.

## 2. Redact

Replace every secret with `***`: API keys, tokens, passwords, `Authorization` headers, cookies, and private personal data. Check the script, logs, and environment values too. The step is done when no key-like string remains anywhere in the draft or the attachments you plan to upload.

## 3. Check for duplicates

```bash
gh issue list -R boson-ai/Boson-Feedback-Collection --state all --search "<key words>"
```

If an existing issue matches, show it to the user and offer to add a comment there instead of filing a new issue.

## 4. Draft and confirm

Title: `[Realtime]`, `[Avatar]`, `[TTS]`, `[Other]`, or `[Feedback]`, then a short summary.

Write the body to a temporary file using these headings, which match the repo's issue forms (leave out a section you have nothing for):

```markdown
### Product
### Issue type
### Severity
### What happened?
Summary:
Expected:
Actual:
### How to reproduce
### Details
SDK/API version:
Model:
Endpoint/region:
OS / language:
Request IDs + timestamps (with timezone):
Logs:
### Evidence
```

Wrap code and logs in ``` fences. For feedback or feature ideas, use **Product**, **Your idea or feedback**, and **What would it help you do?** instead.

Show the user the title and body, and submit only after they approve.

## 5. Submit

```bash
gh issue create -R boson-ai/Boson-Feedback-Collection \
  --title "[TTS] Long inputs are cut off" --body-file /path/to/body.md \
  --attach ./screenshot.png
```

- `--attach` uploads images and video only and needs a recent `gh`. Zip audio files and other formats, or ask the user to drag them into the issue in the browser after it is created.
- Skip `--label`: reporters lack permission to set labels, and the Boson team labels new issues.
- If `gh` is missing or not logged in, ask the user to run `gh auth login`, or give them the title and body to paste at https://github.com/boson-ai/Boson-Feedback-Collection/issues/new/choose.

Done when you have shown the user the new issue URL.
