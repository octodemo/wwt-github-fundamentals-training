# Workshop Plan: Day in the Life of a Dev — GitHub Platform & Copilot

## Overview

A hybrid (live intro + self-paced labs) workshop for **50+ participants** using **GitHub Enterprise Cloud** with **Copilot Business**. Structured as a choose-your-own-adventure across two tracks — one for GitHub newcomers, one for Copilot power users already familiar with the platform.

**Deliverables:**
1. Workshop Guide (instructor + participant steps, markdown)
2. Slide Deck Outline

---

## Problem Statement

Participants need a realistic, repeatable "day in the life" experience that shows how GitHub + Copilot fit together end-to-end — from creating a project through code changes, peer/AI review, merge, and cleanup. The workshop must be self-service-friendly for 50+ attendees and require minimal instructor support during labs.

---

## Workshop Structure

### Format
- **Intro block** (live, instructor-led): Set the stage, demo the full flow once
- **Lab blocks** (self-paced): Participants work through their chosen track
- **Debrief block** (live): Surface learnings, Q&A, share screenshots

### Tracks
| Track | Audience | Duration |
|-------|----------|----------|
| Track 1 — GitHub Newcomer | People new to GitHub | ~60 min |
| Track 2 — Collaboration Guardrails | Anyone who manages or contributes to shared repos | ~30–45 min |
| Track 3 — Copilot Power User | People familiar with Copilot, new to CLI | ~30 min |

Participants self-select their track during the intro. Both tracks can run simultaneously.

---

## Track 1: GitHub Newcomer — End-to-End Dev Workflow

### Learning Objectives
- Create a repository using the new-repo Copilot prompt
- Understand GitHub Pages deployment
- Use Copilot cloud agent to make a code change
- Open, review, and merge a pull request with Copilot review
- Delete a feature branch

---

### Module 1.1 — Create a Repository with Copilot

**Goal:** Spin up a real project with working starter code, no local environment needed.

**Steps (participant):**
1. Navigate to `github.com/new` (New Repository page)
2. Name the repo (e.g., `my-calculator-app`)
3. Locate the **"Add a Copilot prompt"** field on the new repo form
4. Enter the following prompt:
   > *"Build a simple calculator web app deployed on GitHub Pages. Include a README with step-by-step instructions on how to deploy, including any repository settings changes needed to enable GitHub Pages."*

   > 📸 **Screenshot cue:** Capture the new repo form with your prompt filled in — before clicking Create.

5. Click **Create repository** — Copilot cloud agent starts a session in the background
6. Navigate to the **Agents** tab or panel to monitor progress

   > 📸 **Screenshot cue:** Capture the Agents panel/tab showing the session actively running (status: "In progress").

7. When Copilot finishes, a draft PR is opened — review the files created

   > 📸 **Screenshot cue:** Capture the auto-generated PR showing the list of files Copilot created (Files Changed tab).

**Instructor talking points:**
- This is the "new repository" entry point for the cloud agent (docs: `docs.github.com/en/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions`)
- Copilot runs in an isolated GitHub Actions environment
- Every change lands in a PR — you are always the reviewer, Copilot can never merge

---

### Module 1.2 — Enable GitHub Pages & Validate Deployment

**Goal:** Follow README instructions to deploy the calculator.

**Steps (participant):**
1. Merge the PR created by Copilot in Module 1.1
2. Go to **Settings → Pages**

   > 📸 **Screenshot cue:** Capture the Pages settings screen showing the Source dropdown before you save.

3. Under "Source," select **Deploy from a branch** → choose `main` → `/ (root)` or `/docs` (follow README)
4. Click **Save** — a GitHub Actions workflow triggers the deployment
5. Wait ~60 seconds, then click the Pages URL to verify the calculator loads and works

   > 📸 **Screenshot cue:** Capture the live calculator app in your browser — show the URL bar so the `.github.io` domain is visible.

6. Test: Click a few calculator buttons — confirm basic math operations

   > 📸 **Screenshot cue:** Capture the calculator mid-use (e.g., showing "42" as a result) — great for the debrief slide or sharing in chat!

**Instructor talking points:**
- GitHub Pages is free static hosting built into every repo
- The deployment URL pattern: `https://<username>.github.io/<repo-name>`
- If the calculator doesn't render, check Actions tab for workflow errors

---

### Module 1.3 — Request a Change with the Cloud Agent

**Goal:** Experience the cloud agent workflow for feature development.

**Steps (participant):**
1. Navigate to the **Agents** tab on GitHub.com (or use the dashboard panel)
2. Click **New session** (or start from an Issue — see tip below)
3. Assign Copilot to a new issue, OR use the Agents panel directly with this prompt:

   > **Example Prompt A (recommended for newcomers):**
   > *"Add a light mode / dark mode toggle to the calculator. If one already exists, skip this task and let me know. The toggle should be in the top-right corner and persist the user's preference using localStorage."*

   > **Example Prompt B (alternative):**
   > *"Add a 'calculation history' section below the calculator that shows the last 5 calculations. Include a 'Clear History' button."*

   > 📸 **Screenshot cue:** Capture the "Assign to Copilot" dialog (or Agents panel new session form) with your prompt typed in — before submitting.

4. Optionally add an **Optional prompt** with constraints:
   > *"Do not use any external CSS frameworks. Keep it in plain HTML/CSS/JS."*
5. Watch the session log in the **Agents panel** or **VS Code sidebar** to track Copilot's progress

   > 📸 **Screenshot cue:** Capture the session log mid-run, showing Copilot's plan or one of its steps (e.g., "Creating feature branch," "Modifying index.html").

**Tips for participants:**
- The issue-based workflow: Create an Issue → Assignees → select **Copilot**
- You can provide extra context in the "Optional prompt" field
- Copilot will not react to comments added *after* assignment — put all context upfront
- You can change the model Copilot uses via the dropdown (e.g., Claude Sonnet, GPT-4o)

**Instructor talking points:**
- Cloud agent uses the issue title, description, and any comments at time of assignment
- It runs in a GitHub Actions workspace — isolated, secure, auditable
- Session logs show every decision Copilot made — great for learning and review

---

### Module 1.4 — Review the PR & Request Copilot Review

**Goal:** Review AI-generated code and use Copilot as a code reviewer.

**Steps (participant):**
1. When Copilot finishes its session, it opens a **Pull Request** automatically

   > 📸 **Screenshot cue:** Capture the PR overview page showing Copilot as the author and the auto-generated PR title/description.

2. Open the PR and review the **Files Changed** tab:
   - Does the dark mode toggle appear in the correct location?
   - Is the localStorage logic correct?
   - Are there any obvious issues?

   > 📸 **Screenshot cue:** Capture a specific changed file in the diff view — ideally one showing the toggle CSS or JS logic.

3. In the PR's **Reviewers** section (right sidebar), click the gear icon
4. Type **Copilot** and select it from the list — click **Request review**

   > 📸 **Screenshot cue:** Capture the Reviewers sidebar showing Copilot listed as a requested reviewer.

5. Wait a moment — Copilot will add an automated review with line-level comments
6. Read Copilot's review feedback

   > 📸 **Screenshot cue:** Capture one of Copilot's inline review comments on a specific line of code.

**Instructor talking points:**
- Copilot PR review works on your own code, your teammate's code, and AI-generated code
- This is "AI reviewing AI" — a powerful safeguard against subtle bugs
- Copilot's review appears just like a human reviewer's — with inline comments and a summary
- You can request Copilot review on *any* PR in a repo where Copilot is enabled

---

### Module 1.5 — Approve, Merge, and Clean Up

**Goal:** Complete the dev workflow with a clean merge and branch deletion.

**Steps (participant):**
1. After reading the Copilot review, make a decision:
   - If satisfied: Click **Approve** → then **Merge pull request**
   - If Copilot flagged issues: Leave a comment on the PR asking Copilot to fix them (in the PR, not the issue)

   > 📸 **Screenshot cue:** Capture the green merge confirmation banner ("Pull request successfully merged and closed").

2. After merging, click **Delete branch** to remove the feature branch

   > 📸 **Screenshot cue:** Capture the "Branch deleted" confirmation that appears right after deletion.

3. Navigate to the deployed GitHub Pages URL and verify the dark mode toggle appears

   > 📸 **Screenshot cue:** Capture the live site with the dark mode toggle — take one screenshot in light mode and one in dark mode!

**Instructor talking points:**
- Only humans can approve and merge — Copilot cannot self-merge
- Deleting the feature branch is best practice — keeps the repo clean
- The Pages site updates automatically after merge (via Actions)

---

## Track 2: Collaboration Guardrails — CODEOWNERS & Repository Rules

**Best taken after:** Track 1 (or on its own for anyone managing shared repos).
**Who it's for:** Developers, tech leads, and platform engineers who want to enforce consistent contribution standards — whether protecting `main` from direct pushes, requiring reviewers for specific files, or locking down secrets.

### Learning Objectives
- Understand what CODEOWNERS is and why it matters
- Create a CODEOWNERS file that maps file paths to required reviewers
- Configure repository rulesets to enforce PR requirements and branch protections
- Enable secret scanning and push protection
- See how these guardrails interact with the Copilot cloud agent workflow

---

### Module 2.1 — Creating a CODEOWNERS File

**Goal:** Automatically require the right reviewers based on what files are changed in a PR.

**What is CODEOWNERS?**
A `CODEOWNERS` file tells GitHub who is responsible for specific files or directories. When a PR touches those files, the designated owners are automatically added as required reviewers. No more "oops, forgot to tag someone."

**Steps (participant):**
1. In your calculator repo, navigate to **Add file → Create new file**
2. Name it `.github/CODEOWNERS`
3. Add rules using this syntax — owner can be a username, team, or email:

```
# All files: default reviewer
*  @your-github-username

# JavaScript files require a JS lead review
*.js  @your-github-username

# Deployment config requires ops team
.github/workflows/  @octodemo/workshop-instructors
```

> 📸 **Screenshot cue:** Capture the CODEOWNERS file in the GitHub editor before committing.

4. Commit directly to `main`
5. Now create a new branch, modify any `.js` file, and open a PR
6. Observe: your username appears automatically in the **Reviewers** sidebar as a required reviewer

> 📸 **Screenshot cue:** Capture the PR Reviewers sidebar showing auto-assigned code owners (indicated by the shield icon).

**Instructor talking points:**
- CODEOWNERS works best on repos with `main` branch protection — without it, PRs can still be merged without the required review
- Teams (e.g., `@org/team-name`) are more scalable than individual usernames — if someone leaves, the team still owns the file
- The cloud agent respects CODEOWNERS — it will request review from code owners when it raises a PR
- CODEOWNERS syntax supports globs: `docs/**` owns everything under `/docs`

---

### Module 2.2 — Setting Up Repository Rulesets

**Goal:** Enforce branch protection and contribution policies without relying on people to remember.

**What are Rulesets?**
Repository Rulesets (the modern successor to branch protection rules) let you define exactly what must happen before code can be merged into any branch. They're more flexible than classic branch protections and can be layered.

**Steps (participant):**
1. Go to **Settings → Rules → Rulesets**
2. Click **New ruleset → New branch ruleset**
3. Name it: `Protect main`
4. Set **Enforcement status** to **Active**
5. Under **Target branches**, click **Add target → Include default branch**
6. Enable the following rules:

| Rule | Setting | Why |
|------|---------|-----|
| **Restrict deletions** | ✅ On | Prevent accidental deletion of `main` |
| **Require a pull request before merging** | ✅ On, Required approvals: 1 | No direct pushes to `main` |
| **Require review from Code Owners** | ✅ On | Enforces CODEOWNERS from Module 2.1 |
| **Block force pushes** | ✅ On | Preserves commit history |
| **Require status checks to pass** | Optional — enable if repo has CI | Ensures tests pass before merge |

> 📸 **Screenshot cue:** Capture the Ruleset configuration screen with your rules enabled before saving.

7. Click **Create** to save the ruleset
8. Try to push directly to `main` — observe the push is blocked

> 📸 **Screenshot cue:** Capture the error message when attempting a direct push to `main` ("Changes must be made through a pull request").

**Instructor talking points:**
- Rulesets can be applied at the **organization level** — set once, enforce everywhere across all repos
- Unlike classic branch protection rules, Rulesets support **bypass lists** — you can grant org admins an exception without disabling protections for everyone
- The Copilot cloud agent always works on feature branches, so Rulesets don't block its workflow — in fact, they reinforce it
- For Enterprise: Rulesets can be pushed down from the org/enterprise level, so individual repo owners can't override them

---

### Module 2.3 — Enable Secret Scanning & Push Protection

**Goal:** Prevent secrets and credentials from ever reaching the repo.

**What is it?**
GitHub's secret scanning automatically detects 200+ credential patterns (AWS keys, GitHub tokens, Stripe keys, etc.) across your entire repo history. Push protection goes further — it blocks a push at the moment a secret is detected, before it ever lands on GitHub.

**Steps (participant):**
1. Go to **Settings → Security & analysis**
2. Under **Secret scanning**, click **Enable**
3. Under **Push protection**, click **Enable**

> 📸 **Screenshot cue:** Capture the Security & analysis page with both Secret scanning and Push protection showing as enabled (green).

4. **Try it:** Create a new branch, add a fake AWS key pattern to any file:
   ```
   # test-secret.txt
   AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
   ```
5. Attempt to commit and push — observe GitHub blocks the push and explains why
6. Delete the file, push clean

> 📸 **Screenshot cue:** Capture the push protection block message in your terminal or browser.

**Instructor talking points:**
- Secret scanning scans your *entire commit history*, not just new code — it will alert on secrets committed in the past
- Push protection works even if someone tries to sneak a secret into an AI-generated PR — Copilot's output gets scanned too
- Organizations can add **custom patterns** for internal credential formats (e.g., internal API keys that GitHub doesn't know about)
- For Enterprise: alerts go to security teams, not just repo owners — great for compliance

---

### Module 2.4 — See It All Work Together (Bonus)

**Goal:** Observe how guardrails shape the full contribution workflow, including Copilot's.

**Steps (participant):**
1. With your ruleset and CODEOWNERS active, go back to your calculator repo
2. Create a new Issue and assign it to Copilot (cloud agent)
3. Watch Copilot open a PR — notice it:
   - Works on a feature branch (respects ruleset)
   - Requests review from the code owners you defined
   - Cannot merge on its own (ruleset requires human approval)
4. Review and merge the PR — observe the full guardrailed flow end to end

> 📸 **Screenshot cue:** Capture the PR showing CODEOWNERS review request + Ruleset status check in the merge box simultaneously.

**Instructor talking points:**
- This is the key message: **guardrails don't slow down AI — they make AI output trustworthy**
- Every PR, whether from a human or Copilot, goes through the same gates
- This is how platform teams give developers (and AI) freedom to move fast without breaking things

---

## Track 3: Copilot Power User — GitHub Copilot CLI in 30 Minutes

**Who it's for:** Participants already comfortable with Copilot Chat and basic GitHub. This track introduces the **GitHub Copilot CLI** — a full agentic coding assistant that lives in your terminal, distinct from the browser-based Copilot Chat experience.

> **Important distinction:** This is *not* `gh copilot suggest` (a lightweight `gh` extension). The **GitHub Copilot CLI** (`copilot`) is a standalone product — the same agentic engine that powers the cloud agent, running locally and synchronously in your terminal. You talk to it in natural language, it reads your code, runs commands, and can hand work off to the cloud agent via `/delegate`.

**Does not require Track 1.** Navigate to any repo you have write access to before starting.

**The structure is intentional:** You'll plan and kick off a task with the CLI first — hand it off to the cloud agent with `/delegate` — then explore the CLI's most powerful commands while the agent works — then come back and review the PR without ever leaving your terminal.

### Learning Objectives
- Install and launch the GitHub Copilot CLI
- Use natural language to explore, plan, and modify a codebase from the terminal
- Use `/plan` to think through a feature before writing a line of code
- Use `/delegate` to hand a session off to the cloud agent and create a PR
- Use `/review`, `/diff`, and `/pr` to do a meaningful code review in the terminal

### Time Map

| Block | Time | What you're doing |
|-------|------|-------------------|
| Module 3.1 | 0–5 min | Install, launch, and `/delegate` a task to the cloud agent |
| Module 3.2 | 5–20 min | Explore key CLI workflows while the agent runs |
| Module 3.3 | 20–30 min | Come back — review and merge the PR without leaving the terminal |

---

### Module 3.1 — Install, Launch, and Delegate

**Goal:** Get the CLI running and immediately hand a non-trivial task to the cloud agent so it works while you explore.

#### Setup (~2 min)

```bash
# Install (macOS/Linux)
brew install copilot-cli
# or:
curl -fsSL https://gh.io/copilot-install | bash

# Windows
winget install GitHub.Copilot

# Launch in your repo directory
cd your-repo
copilot
```

On first launch you'll be prompted to `/login` — follow the on-screen auth flow. Then you're in.

> 📸 **Screenshot cue:** Capture the Copilot CLI splash screen on first launch.

---

#### Fire off a task and `/delegate` it (~3 min)

Once you're in the CLI, describe a real task — something that would take you 30–60 min manually. Pick one:

> 🟡 **Option A — Refactor (any small JS/TS project):**
> *"Refactor the JavaScript into a proper ES module architecture. Extract all business logic into a Calculator class with clearly named methods. Each method needs JSDoc with @param and @returns. Do not touch the HTML or CSS. Add an ARCHITECTURE.md summarizing the module design."*

> 🟡 **Option B — Add CI (any repo without GitHub Actions):**
> *"Create a GitHub Actions CI workflow that runs on every PR to main. Lint the code with an appropriate linter, run any existing tests, and block merge if either fails. Add a passing/failing status badge to the README."*

> 🔴 **Option C — Issue triage bot (any repo):**
> *"Create a GitHub Actions workflow that triages new issues automatically. When an issue opens: scan the title and body for keywords, apply appropriate labels (bug, enhancement, documentation, question, help wanted), and post a comment asking for reproduction steps if it looks like a bug. Use only the built-in GITHUB_TOKEN."*

Type your chosen prompt into the CLI. Let it respond with a plan, then run:

```
/delegate
```

This hands the current session to the **cloud agent on GitHub**, which will implement the plan and open a PR for your review. The CLI confirms with a link to the session.

> 📸 **Screenshot cue:** Capture the CLI after `/delegate` — showing the confirmation message and the link to the cloud agent session on GitHub.

**Don't wait for it.** Move to Module 3.2 immediately.

---

### Module 3.2 — Key CLI Workflows

**Goal:** While the cloud agent works, learn the CLI patterns that change how you interact with code every day.

---

#### Block 1: Plan Before You Code with `/plan`

`/plan` tells the CLI to think through a feature and produce a structured implementation plan *before* touching any files. Use it on your own ideas, or on code you've just inherited.

In the CLI (still in your repo), try:

```
/plan add comprehensive keyboard navigation support to this app
```

Or on an unfamiliar codebase:

```
/plan refactor the validation logic to remove duplication across these three files
```

The CLI will:
- Read the relevant files
- Identify risks and dependencies
- Produce a step-by-step implementation plan
- Ask if you want to proceed or adjust

> 💡 This is the move senior devs make that junior devs skip — planning surfaces the hard parts before they bite you mid-implementation.

> 📸 **Screenshot cue:** Capture the `/plan` output showing the CLI's proposed implementation steps for your request.

---

#### Block 2: Ask Questions About Your Codebase

The CLI has full context of your repo. Ask it things you'd normally spend 20 minutes grepping for:

```
What does the calculate() function actually do, and what are its edge cases?
```

```
Where is localStorage being used in this project and is it consistent?
```

```
Are there any security issues in this codebase I should know about before shipping?
```

```
Explain the data flow from when a user clicks a button to when the result is displayed.
```

Use `@` to reference specific files for focused questions:

```
@src/calculator.js what would break if I changed the return type of evaluate() from string to number?
```

Use `#` to pull in GitHub context:

```
#42 what's the current status of this issue and is there anything blocking it?
```

> 📸 **Screenshot cue:** Capture the CLI answering one of the codebase questions above — ideally one where it surfaces something non-obvious.

---

#### Block 3: Make Changes and `/diff` Before You Commit

Ask the CLI to make a targeted change directly:

```
Add input validation to the calculator — if the user types a non-numeric character, show a red border and an inline error message. Do not modify any other behavior.
```

The CLI will propose changes, show you what it wants to do, and ask for confirmation before writing anything.

After changes are made, review them:

```
/diff
```

This shows a clean summary of everything changed in the current directory — great before committing or opening a PR.

> 📸 **Screenshot cue:** Capture `/diff` output showing the CLI's changes in a readable format.

---

#### Block 4: Run Shell Commands Without Leaving Context

Use `!` to run shell commands inline without exiting the conversation:

```
! git log --oneline -10
! git status
! npm test
```

The CLI sees the output and can act on it. For example:

```
! npm test
```
...then immediately ask:
```
Two tests are failing — what's causing it and fix it.
```

The CLI will read the test output and patch the code in one step.

> 💡 This is the loop that makes the CLI feel like a pair programmer rather than a chatbot — you run, it sees, it fixes.

> 📸 **Screenshot cue:** Capture a sequence of `! npm test` followed by the CLI diagnosing and fixing the failure.

---

### Module 3.3 — Review the Cloud Agent PR in the Terminal

**Goal:** The cloud agent should have a PR open by now. Review it without switching to a browser.

#### Check in on the agent

```
/pr
```

This shows the PR status for the current branch — or lists recent PRs. Navigate to the agent's PR.

> 📸 **Screenshot cue:** Capture `/pr` output showing the cloud agent's open PR with its title and status checks.

---

#### Run a real code review

```
/review
```

The CLI runs its **code review agent** against the current PR diff — looking for bugs, edge cases, missing error handling, and logic issues. It's the same quality bar as requesting a Copilot review on GitHub.com, but you're doing it from the terminal.

Read the output carefully. It will flag specific lines. If something looks wrong, ask the CLI to explain or fix it:

```
The review flagged a potential issue in line 47 — explain the risk and suggest a fix.
```

> 📸 **Screenshot cue:** Capture `/review` output highlighting a specific issue in the agent's code.

---

#### Merge or request changes

If you're happy with the PR:

```
/pr merge --squash --delete-branch
```

If you want the cloud agent to iterate, leave a comment on the PR on GitHub.com (or use `gh pr comment` from a second terminal) describing the change needed — the agent will pick it up and push a new commit.

> 📸 **Screenshot cue:** Capture the merge confirmation in the CLI, or the PR comment requesting changes.

---

**Instructor talking points:**
- `/delegate` is the bridge between local agentic work and the cloud agent — you plan locally, delegate the execution, review the result. This is the full async loop.
- The CLI's `@file` and `#issue` references give it GitHub context that raw terminal tools don't have — it's not just a shell wrapper
- `/review` in the CLI and requesting Copilot review on GitHub.com use the same underlying model — pick whichever fits your flow
- The `!` prefix makes the CLI a true pair programmer: it sees command output and reacts to it, not just to what you type
- Participants can use `/share` to export this session as a markdown or HTML file — great for notes or sharing with the team



## Pre-Workshop Setup Checklist (Instructor)

- [ ] All participants have GitHub accounts added to the Enterprise Cloud org
- [ ] Copilot Business licenses assigned to all participants
- [ ] Copilot cloud agent enabled at org level (Settings → Copilot → Coding agent)
- [ ] GitHub Pages not blocked by org policy
- [ ] Participants in Track 3 have GitHub Copilot CLI installed (`brew install copilot-cli` or `curl -fsSL https://gh.io/copilot-install | bash`)
- [ ] Workshop guide URL shared in chat at start

---

## Screenshot Reference List

### Track 1 — GitHub Newcomer

| # | When to take it | What to capture |
|---|----------------|-----------------|
| 1 | Module 1.1, Step 4 | New repo form with Copilot prompt filled in |
| 2 | Module 1.1, Step 6 | Agents panel showing session "In progress" |
| 3 | Module 1.1, Step 7 | Auto-generated PR — Files Changed tab |
| 4 | Module 1.2, Step 2 | Pages settings — Source dropdown before saving |
| 5 | Module 1.2, Step 5 | Live calculator in browser with `.github.io` URL visible |
| 6 | Module 1.2, Step 6 | Calculator showing a result (e.g., "42") — fun debrief share! |
| 7 | Module 1.3, Step 3 | "Assign to Copilot" dialog or Agents panel with prompt typed |
| 8 | Module 1.3, Step 5 | Session log mid-run showing Copilot's plan/steps |
| 9 | Module 1.4, Step 1 | PR overview — Copilot as author, auto-generated title |
| 10 | Module 1.4, Step 2 | Files Changed diff showing toggle CSS or JS |
| 11 | Module 1.4, Step 4 | Reviewers sidebar with Copilot listed as requested reviewer |
| 12 | Module 1.4, Step 6 | Copilot inline review comment on a specific line |
| 13 | Module 1.5, Step 1 | Green "Pull request successfully merged" banner |
| 14 | Module 1.5, Step 2 | "Branch deleted" confirmation |
| 15 | Module 1.5, Step 3 | Live site with dark mode toggle — light AND dark mode (2 shots!) |

### Track 2 — Collaboration Guardrails

| # | When to take it | What to capture |
|---|----------------|-----------------|
| 16 | Module 2.1, Step 3 | CODEOWNERS file in GitHub editor before committing |
| 17 | Module 2.1, Step 6 | PR Reviewers sidebar showing auto-assigned code owners (shield icon) |
| 18 | Module 2.2, Step 6 | Ruleset config screen with rules enabled before saving |
| 19 | Module 2.2, Step 8 | Push blocked error: "Changes must be made through a pull request" |
| 20 | Module 2.3, Step 3 | Security & analysis page — Secret scanning + Push protection enabled |
| 21 | Module 2.3, Step 5 | Push protection block message in terminal or browser |
| 22 | Module 2.4, Step 3 | PR merge box showing CODEOWNERS review request + Ruleset status check |

### Track 3 — Copilot Power User

| # | When to take it | What to capture |
|---|----------------|-----------------|
| 23 | Module 3.1 Setup | Copilot CLI splash screen on first launch |
| 24 | Module 3.1 `/delegate` | CLI confirmation message + link to cloud agent session after `/delegate` |
| 25 | Module 3.2, Block 1 | `/plan` output showing proposed implementation steps |
| 26 | Module 3.2, Block 2 | CLI answering a codebase question with a non-obvious insight |
| 27 | Module 3.2, Block 3 | `/diff` output showing the CLI's changes in a readable format |
| 28 | Module 3.2, Block 4 | `! npm test` followed by CLI diagnosing and fixing the failure |
| 29 | Module 3.3, Check in | `/pr` output showing the cloud agent's open PR |
| 30 | Module 3.3, Review | `/review` output highlighting a specific issue in the agent's code |
| 31 | Module 3.3, Merge | Merge confirmation in CLI or PR comment requesting changes |


