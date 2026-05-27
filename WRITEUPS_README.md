# Writeup Automation — AI-Powered Publishing Flow

Automated TryHackMe writeup generation using Claude AI.
From room name to GitHub commit in under 7 minutes.

---

## How it works

```
Room name
    ↓
AI generates writeup (Claude Sonnet)
    ↓
Review + insert real flags (2–3 min)
    ↓
Download .md → place in writeups/
    ↓
git add → commit → push
```

---

## The tool

A web app built as a Claude AI artifact — runs in the browser, no installation required.

What it does:
- Takes the room name, difficulty, and categories as input
- Calls the Claude API (`claude-sonnet-4-20250514`)
- Generates a structured `.md` writeup in ~10 seconds
- Provides a download button and ready-to-paste git commands

---

## Writeup structure

Every generated file follows this template:

```markdown
---
title: Room Name
date: YYYY-MM-DD
difficulty: Easy / Medium / Hard
categories: [Web, Linux, Privesc, ...]
platform: TryHackMe
status: completed
---

## Overview
## Reconnaissance
## Enumeration
## Exploitation
## Privilege Escalation
## Flags / Answers
## Key Takeaways
## Tools Used
```

---

## Publishing flow

After downloading the `.md` file:

```bash
mv ~/Downloads/room-name.md writeups/

git add writeups/room-name.md
git commit -m "writeup: Room Name"
git push origin main
```

---

## What still requires manual input

The AI generates structure and technical content based on the room type.
The only manual steps are:

- Insert real flags (replacing `FLAG{REDACTED}` placeholders)
- Adjust any room-specific details if needed
- Run git push

Total time: approximately 5 minutes per room.

---

## Stack

| Component       | Technology                          |
|-----------------|-------------------------------------|
| AI generation   | Claude Sonnet (`claude-sonnet-4-20250514`) |
| Interface       | HTML/JS artifact in Claude.ai       |
| Writeup hosting | GitHub (`cybersec-journey/writeups/`) |
| Portfolio site  | GitHub Pages (`finessin-cc.github.io`) |

---

## Before and after

|                        | Before             | After              |
|------------------------|--------------------|--------------------|
| Time per writeup       | 30–60 min          | 5–7 min            |
| Rooms published/week   | ~0 (kept delaying) | Every room cleared |
| Structure              | Undefined          | Consistent template |

---

Part of [cybersec-journey](https://github.com/finessin-cc/cybersec-journey) — my path into cybersecurity.
