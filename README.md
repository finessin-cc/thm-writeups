# thm-writeups

Personal TryHackMe writeup collection.

Each file covers one room — methodology, commands, findings, and key takeaways.
Writeups are generated using a Claude AI tool and reviewed manually before publishing.

---

## Structure

```
thm-writeups/
├── room-name.md
├── another-room.md
└── ...
```

Each writeup follows a consistent template:

```
Overview
Reconnaissance
Enumeration
Exploitation
Privilege Escalation
Flags
Key Takeaways
Tools Used
```

---

## Automation

Writeups are produced with an AI-powered generator built on top of the Claude API.

Workflow:
1. Enter the room name, difficulty, and categories
2. Claude generates a structured draft in ~10 seconds
3. Review the draft, insert real flags, adjust details
4. Download the `.md` file and commit

```bash
git add room-name.md
git commit -m "writeup: Room Name"
git push origin main
```

Total time per writeup: approximately 5 minutes.

---

## Profile

TryHackMe: [finessin](https://tryhackme.com/p/finessin)  
Portfolio: [finessin-cc.github.io](https://finessin-cc.github.io)
