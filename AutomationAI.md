# How I Automated My TryHackMe Writeups Using GitHub Actions

| Metadata | Value |
| :--- | :--- |
| **Project Type** | DevOps / Automation / Scripting |
| **Target Platform** | GitHub Actions |
| **Goal** | Reduce writeup publication time to < 10 seconds |
| **Status** | 🚀 Fully Operational |

---

## 📝 Executive Summary
As a cybersecurity student active on **TryHackMe**, documenting rooms and building a portfolio is essential. However, manually creating Markdown skeletons, copying templates, and updating the main repository index (`README.md`) is highly repetitive and time-consuming. 

To solve this, I designed and implemented a custom **CI/CD automation workflow** using **GitHub Actions**. Now, publishing a structured writeup skeleton with a synchronized index update takes exactly **one click** and less than 10 seconds, leaving room only for actual flag submission.

---

## 🛠️ The Problem & Solution

### The Lazy (Efficient) Developer's Mindset:
* **Before:** Finish a room ➔ Create a `.md` file ➔ Copy-paste a structural template ➔ Fill out metadata ➔ Open `README.md` ➔ Manually append a new row to the tracking table ➔ Run Git commands (`add`, `commit`, `push`). Total time: ~5-7 minutes of boring routine.
* **After:** Finish a room ➔ Go to GitHub Actions ➔ Enter Room Name & Type ➔ Click "Run". Total time: **5 seconds**.

---

## ⚙️ Technical Implementation

The system is powered by a custom GitHub Workflow definition (`.github/workflows/auto_writeup.yml`). It triggers on-demand (`workflow_dispatch`) and dynamically adapts based on user inputs.

### Key Features:
1. **Dynamic Templating:** The automation distinguishes between **CTF (Challenge)** rooms (focusing on Recon, Exploitation, and PrivEsc) and **Walkthrough (Guided)** rooms (focusing on theoretical tasks, answers, and concepts).
2. **Automated Indexing:** A Bash script uses `sed` stream editing to instantly parse `README.md` and insert the new room into the main tracking table right below the header.
3. **Frictionless Deployment:** The runner natively configures a `github-actions[bot]` Git identity, stages the generated files, and pushes them directly back into the repository root.

---

## 🚀 How It Works (The Flow)

Whenever I complete a room, I execute the following process from any device (even a smartphone):

1. **Trigger:** Navigate to the **Actions** tab in my repository.
2. **Input:** Select the `Generate Writeup Automatically` workflow and fill in the required parameters:
   * **Room Name:** (e.g., `Pickle Rick`)
   * **Room Type:** `CTF (Challenge)` or `Walkthrough (Guided/Theory)`
   * **Difficulty:** `Easy`, `Medium`, etc.
3. **Execution:** The automated runner triggers, builds the clean Markdown file in the root directory, updates the index table, and commits the changes.

---

## 🧠 Key Takeaways

* **Efficiency First:** In cybersecurity, scripting and automating routine tasks separates high-velocity analysts from the rest. 
* **Portfolio Showcase:** This automation ensures that my portfolio stays clean, uniform, and updated without causing documentation fatigue. 
* **Tooling Learned:** Gained practical experience with GitHub Actions syntax, workflow permissions, Bash string manipulation, and CI/CD pipelines.

* ### Key Features:
1. **AI-Powered Parsing:** Dynamic integration with a free LLM endpoint that accepts a raw dump of the TryHackMe room text, analyzes tasks, hints, and instructions, and synthesizes an intelligent, bespoke writeup.
2. **Context-Aware Formatting:** Automatically structures files into professional penetration testing summaries or clean training guides based on the underlying machine logic.
3. **Automated Indexing:** Utilizes Unix `sed` tools to dynamically rebuild the repository's `README.md` catalog upon code integration.
