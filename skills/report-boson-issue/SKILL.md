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
  --attach '/abs/path/screenshot.png#Error shown after 20 seconds'
```

Leave labels to the repo: a workflow labels new issues from the title prefix, and reporters lack permission to set labels.
If `gh` is missing or not logged in, ask the user to install it from https://cli.github.com/ and run `gh auth login`.

### Attachments

`--attach` uploads images and video (`.png`, `.jpg`, `.gif`, `.mp4`, `.mov`, ...), repeatable, up to 50 files. To place a file inside a section, reference it in the body by absolute path, such as `![Error state](/abs/path/screenshot.png)`, and pass the same path to `--attach`; `gh` swaps in the uploaded URL. Unreferenced attachments are appended to the end of the body.

- **Check support first**: `gh issue create --help | grep -- --attach`. The flag exists from `gh` 2.99.0. Without it, offer the user two options: upgrade `gh`, or file the issue without attachments and drag the files into a comment on the issue in the browser.
- **Audio and other files** (`.wav`, `.mp3`, logs, archives) cannot go through `--attach`. Ask the user to zip them and drag the zip into a comment on the issue in the browser.
- **Partial failure**: if some uploads fail, `gh` still creates the issue, prints its URL, and exits non-zero. Keep that issue and never rerun `gh issue create`, which would file a duplicate. Read it back with `gh issue view <number>` and add the missing files with `gh issue comment <number> --attach <file>`.

Done when you have shown the user the new issue URL and every intended attachment appears in it, or the user knows which files to drag in.
