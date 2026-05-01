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
| Track 3 — Copilot Power User | People familiar with Copilot, new to CLI | ~45–60 min |

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

## Track 3: Copilot Power User — CLI & Advanced Workflows

**Prerequisite:** Participants should already be comfortable with GitHub basics and Copilot chat. This track focuses on the CLI and advanced prompting patterns.

### Learning Objectives
- Install and authenticate the GitHub Copilot CLI extension
- Use `gh copilot explain` and `gh copilot suggest`
- Write effective prompts using context and constraints
- Use custom instructions for repo-level Copilot behavior

---

### Module 3.1 — Getting Started with Copilot CLI

**Goal:** Install and run first commands.

**Setup (prereqs):**
```bash
# Install GitHub CLI (if not already installed)
brew install gh   # macOS
# or: https://cli.github.com/

# Authenticate
gh auth login

# Install Copilot CLI extension
gh extension install github/gh-copilot

# Verify
gh copilot --help
```

**First commands:**
```bash
# Explain a shell command
gh copilot explain "git rebase -i HEAD~3"

# Suggest a shell command from natural language
gh copilot suggest "find all files modified in the last 7 days and larger than 1MB"

# Suggest in a specific context (git, gh, or shell)
gh copilot suggest --target shell "compress a directory into a .tar.gz file"
```

> 📸 **Screenshot cue:** Capture your terminal showing the output of `gh copilot explain` or `gh copilot suggest` — great for showing non-CLI users what this looks like in practice.

**Instructor talking points:**
- `explain` = "what does this do?" for shell/git/gh commands
- `suggest` = "do this thing" in natural language → outputs a command to run
- The CLI is especially powerful for unfamiliar git commands or complex shell one-liners

---

### Module 3.2 — Advanced Prompting Patterns

**Goal:** Learn prompting strategies that get better results from Copilot.

**Pattern 1: Add constraints**
> ❌ "Add tests"
> ✅ "Add unit tests for the calculator.js add() and subtract() functions using Vitest. Mock the DOM. Don't modify the existing functions."

**Pattern 2: Specify output format**
> "Explain this function as bullet points a junior dev can follow, max 5 bullets."

**Pattern 3: Role + task + context**
> "You are a security reviewer. Identify any XSS or injection vulnerabilities in this HTML. List them by severity."

**Pattern 4: Iterative refinement**
> "That's good, but the localStorage key name should follow our convention: `app__<feature>__<key>`. Update the key name only."

**Lab exercise:**
1. Clone the calculator repo from Track 1
2. Open VS Code with Copilot
3. Use `@workspace` in Copilot Chat: *"Give me a full audit of accessibility issues in this app. Reference WCAG 2.1 AA."*

   > 📸 **Screenshot cue:** Capture the Copilot Chat panel showing the `@workspace` audit response.

4. Ask Copilot to fix the top 3 issues it finds
5. Commit the changes and push

   > 📸 **Screenshot cue:** Capture the VS Code Source Control panel showing your staged changes before committing.

---

### Module 3.3 — Custom Instructions

**Goal:** Configure Copilot to always follow your team's conventions.

**Steps:**
1. In the repo, create `.github/copilot-instructions.md`
2. Add team conventions, e.g.:
```markdown
# Copilot Instructions

- Use vanilla JS (no frameworks) for this project
- All CSS custom properties should be defined in :root
- Function names should be camelCase
- Always add JSDoc comments to exported functions
- When suggesting tests, use Vitest
```
3. In VS Code, make a code change and observe how Copilot suggestions reflect these instructions

   > 📸 **Screenshot cue:** Capture a Copilot suggestion in VS Code that visibly follows a rule from your instructions file (e.g., JSDoc comment auto-added).

4. Assign the cloud agent a new issue and verify it follows the instructions automatically

   > 📸 **Screenshot cue:** Capture the PR from the cloud agent showing code that clearly follows your custom instructions (e.g., camelCase function names, CSS variables in `:root`).

**Instructor talking points:**
- Custom instructions are repo-level by default — great for team standardization
- The cloud agent also reads custom instructions automatically
- This is how orgs ensure AI output matches their coding standards

---

## Slide Deck Outline

### Slide 1 — Title
*"Day in the Life: GitHub Platform + Copilot"*
Tagline: From idea to deployed feature — all in a browser.

### Slide 2 — What We're Building Today
- Calculator app, live on the internet, in < 10 minutes
- A feature PR, reviewed by AI, merged by you
- Choose your path: Newcomer or Power User

### Slide 3 — The GitHub Platform Map
Visual: `Repo → Issues → Cloud Agent → PR → Review → Merge → Deploy`
Key message: Copilot lives at every step of this flow

### Slide 4 — Copilot Cloud Agent: How It Works
- Runs in an isolated GitHub Actions environment
- You delegate a task → it plans, codes, opens a PR
- You always review and approve — Copilot cannot merge

### Slide 5 — Entry Points for the Cloud Agent
- New repository form
- GitHub Issues (assign to Copilot)
- Agents tab / dashboard
- VS Code / JetBrains / Eclipse
- GitHub CLI, Mobile, MCP

### Slide 6 — Track 1 Flow (Visual)
`Create Repo → Copilot Builds App → Enable Pages → Verify → Assign Change to Agent → Review PR → Copilot Review → Merge → Delete Branch`
> 📸 **Slide asset:** Use participant screenshots from the debrief — new repo form prompt, live calculator, Copilot PR review comment — as real examples on this slide.

### Slide 7 — Prompting the Cloud Agent (Tips)
- Be specific: task + constraints + context
- Include file/folder scopes if needed
- Add "do not modify X" guardrails
- Put all context upfront — agent won't see later comments

### Slide 8 — Copilot PR Review
- Request like any human reviewer
- Works on your code, others' code, AI-generated code
- Line-level comments + summary
> 📸 **Slide asset:** Use a participant screenshot of an actual Copilot review comment from the lab.

### Slide 9 — Track 2: Collaboration Guardrails
- CODEOWNERS: right reviewer, automatically, every time
- Rulesets: enforce PR requirements, block direct pushes, require status checks
- Secret scanning + push protection: stops credentials before they land
- Key message: guardrails don't slow down AI — they make AI output trustworthy
> 📸 **Slide asset:** Capture the PR merge box showing CODEOWNERS review request + Ruleset status checks side by side.

### Slide 10 — Track 3: Copilot CLI
- `gh copilot explain` → understand any command
- `gh copilot suggest` → generate commands from English
- Show live demo of 2–3 examples
> 📸 **Slide asset:** Use a participant terminal screenshot showing `gh copilot suggest` output, or capture the instructor demo live.

### Slide 11 — Track 3: Advanced Prompting
- Constraints, role-setting, output format, iteration
- `.github/copilot-instructions.md` for team conventions
- `@workspace` context in VS Code

### Slide 12 — Debrief Prompts
- What surprised you?
- Where did you get stuck?
- One thing you'd use Monday morning?

### Slide 12 — Resources
- docs.github.com/copilot
- github.blog (cloud agent announcement)
- github.com/github/awesome-copilot
- GitHub Skills: skills.github.com

---

## Pre-Workshop Setup Checklist (Instructor)

- [ ] All participants have GitHub accounts added to the Enterprise Cloud org
- [ ] Copilot Business licenses assigned to all participants
- [ ] Copilot cloud agent enabled at org level (Settings → Copilot → Coding agent)
- [ ] GitHub Pages not blocked by org policy
- [ ] Participants have `gh` CLI installed (or Codespaces available as fallback for Track 2)
- [ ] Slide deck shared as PDF or live link before session
- [ ] Workshop guide URL shared in chat at start

---

## Todos (Execution)

See SQL tracking below. Deliverables:
1. `workshop-guide.md` — full participant + instructor guide
2. `slide-deck-outline.md` — structured slide content (already in this plan above)

---

## Screenshot Reference List

A consolidated list of all screenshot cues for instructors preparing slide assets, and for participants to use as a checklist during the debrief.

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
| 23 | Module 3.1 | Terminal output of `gh copilot explain` or `gh copilot suggest` |
| 24 | Module 3.2, Step 3 | VS Code Copilot Chat panel showing `@workspace` audit response |
| 25 | Module 3.2, Step 5 | VS Code Source Control panel with staged changes |
| 26 | Module 3.3, Step 3 | VS Code showing a Copilot suggestion following a custom instruction |
| 27 | Module 3.3, Step 4 | Cloud agent PR showing code that follows custom instruction rules |

### Instructor Slide Assets

| Slide | Recommended screenshot source |
|-------|-------------------------------|
| Slide 6 — Track 1 Flow | Screenshots #1, #5, #12 (new repo prompt, live app, Copilot review) |
| Slide 8 — PR Review | Screenshot #12 (Copilot inline review comment) |
| Slide 9 — Guardrails | Screenshot #22 (PR merge box with CODEOWNERS + Ruleset) |
| Slide 10 — Copilot CLI | Screenshot #23 (terminal `gh copilot suggest` output) |
| Debrief Slide | Screenshot #6 (calculator showing result) and #15 (dark mode live) |

