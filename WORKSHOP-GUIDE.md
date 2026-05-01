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

## Track 3: Copilot Power User — Cloud Agent + CLI in 30 Minutes

**Who it's for:** Participants already comfortable with Copilot Chat and basic GitHub. This track skips the basics and goes straight to workflows that make a senior dev's day meaningfully faster.

**Does not require Track 1.** You can use any repo you have write access to. If you don't have one handy, fork a public repo or use one from a previous session.

**The structure is intentional:** You'll kick off a cloud agent task *first* — then use the CLI while it runs in the background — then come back to review the PR like a senior engineer. This mirrors how the async agent workflow actually fits into a real workday.

### Learning Objectives
- Delegate a non-trivial engineering task to the cloud agent with a precise prompt
- Master the CLI commands that matter most day-to-day
- Plan a feature and create issues from the terminal using `gh copilot suggest`
- Kick off a new cloud agent session without ever leaving the terminal
- Review an agent-generated PR using CLI tools and Copilot Chat together

### Time Map

| Block | Time | What you're doing |
|-------|------|-------------------|
| Module 3.1 | 0–5 min | Fire off a cloud agent task — then leave it running |
| Module 3.2 | 5–20 min | CLI deep dive while the agent works |
| Module 3.3 | 20–30 min | Come back — review and merge the PR like a senior dev |

---

### Module 3.1 — Delegate Something Worth Delegating (Cloud Agent)

**Goal:** Give the cloud agent a task that would actually take you 30–60 minutes to do manually. Fire it off and walk away.

**Pick one of the following prompts** based on what repo you're working in. Assign it via the **Agents tab**, **GitHub Issues → assign to Copilot**, or — as you'll learn in Module 3.2 — straight from your terminal.

> 🟡 **Option A — Refactor (use with the calculator app or any small JS/TS project):**
> *"Refactor the JavaScript into a proper ES module architecture. Extract all business logic into a class with clearly named methods. Each method must have JSDoc documentation including @param and @returns. Do not change any HTML structure or CSS. Add a `ARCHITECTURE.md` explaining the module design."*

> 🟡 **Option B — Add CI (use with any repo that doesn't have GitHub Actions yet):**
> *"Create a GitHub Actions CI workflow that runs on every PR targeting main. It should: lint the code (pick an appropriate linter for the language), run any existing tests, and block the merge if either step fails. Add a status badge to the README pointing to this workflow."*

> 🔴 **Option C — Triage bot (use with any repo, no existing code required):**
> *"Create a GitHub Actions workflow that automatically triages new issues. When an issue is opened: scan the title and body for keywords, apply appropriate labels (bug, enhancement, documentation, question, help wanted), and post a comment acknowledging the issue and asking for any missing reproduction steps if it looks like a bug. Use only the GitHub Actions built-in token — no external API keys."*

**Steps:**
1. Pick your option, copy the prompt
2. Navigate to **Issues → New Issue**, write a descriptive title, paste the prompt as the body
3. In the Assignees field, select **Copilot**
4. Add any optional context in the prompt field (e.g., "This is a vanilla JS project, no frameworks")
5. Click **Submit** — the agent starts running in the background

> 📸 **Screenshot cue:** Capture the Issue with Copilot assigned and the agent session status starting.

6. **Don't wait** — move immediately to Module 3.2 while the agent works

---

### Module 3.2 — CLI Power Moves

**Goal:** Learn the CLI commands that senior devs actually use daily. No toy examples.

#### Setup (first time only, ~2 min)

```bash
# Install GitHub CLI if needed
brew install gh          # macOS
# winget install GitHub.cli  # Windows

# Authenticate
gh auth login

# Install Copilot extension
gh extension install github/gh-copilot

# Confirm
gh copilot --help
```

---

#### Block 1: Understand Anything with `gh copilot explain`

Use this whenever you encounter a command you don't fully trust or understand. It explains shell, git, and `gh` commands — including flags and side effects.

```bash
# What does this actually do? (dangerous if misunderstood)
gh copilot explain "git reflog expire --expire=now --all && git gc --prune=now --aggressive"

# Understand a rebase workflow
gh copilot explain "git rebase -i HEAD~4"

# Demystify a gh command you've seen in a workflow
gh copilot explain "gh pr merge --auto --squash --delete-branch"

# What are the risks here?
gh copilot explain "git push origin --force-with-lease"
```

> 💡 **Use this in code review too** — paste any unfamiliar shell command from a workflow file and ask Copilot to explain it before approving.

> 📸 **Screenshot cue:** Capture `gh copilot explain` output for one of the above — ideally the `reflog` or `force-with-lease` one where the explanation is genuinely useful.

---

#### Block 2: Feature Planning with `gh copilot suggest`

`gh copilot suggest` isn't just for one-liners — use it to plan and scaffold your GitHub workflow from the terminal.

```bash
# Find the right git command when you can't remember it
gh copilot suggest --target git "squash my last 3 commits into one with a new message before I push"

# Generate a well-formed commit message
gh copilot suggest --target shell "write a conventional commit message for changes that add a dark mode toggle using CSS custom properties and localStorage"

# Recover from a mistake
gh copilot suggest --target git "I accidentally committed directly to main — undo the last commit but keep my changes staged"

# Build a complex find command
gh copilot suggest --target shell "find all JavaScript files modified in the last 3 days that contain the word 'TODO', print the filename and line number"
```

> 📸 **Screenshot cue:** Capture a `gh copilot suggest` response where you actually ran the suggested command — show both the suggestion and the output.

---

#### Block 3: `gh` CLI for Your Daily GitHub Workflow

These aren't Copilot-specific — they're the `gh` commands that replace context-switching to the browser.

```bash
# See what's on your plate
gh issue list --assignee @me --state open
gh pr list --author @me --state open

# Check recent Actions runs without opening the browser
gh run list --limit 5
gh run watch   # live-tail the most recent run

# View a PR in your terminal (great in code review)
gh pr list
gh pr view <number>
gh pr diff <number>

# Check out a PR branch locally to test it
gh pr checkout <number>

# Close the loop: merge from terminal when you're done reviewing
gh pr merge <number> --squash --delete-branch
```

> 📸 **Screenshot cue:** Capture `gh pr list` or `gh run list` showing real output from your repo.

---

#### Block 4: The Power Combo — Create an Issue and Assign to Copilot Without Leaving the Terminal

This is the workflow that makes the async agent model click. You never open a browser.

```bash
gh issue create \
  --title "Add keyboard navigation to calculator" \
  --body "Users should be able to operate the calculator entirely with the keyboard. Map number keys (0–9), operators (+, -, *, /), Enter for equals, Escape to clear, Backspace to delete last digit. Highlight the active button on keypress. Do not modify the existing click handlers." \
  --label "enhancement" \
  --assignee @copilot
```

> 📸 **Screenshot cue:** Capture the terminal output after running this command, showing the new issue URL — then open it in the browser and capture Copilot already assigned and the session starting.

> 💡 **Instructor talking point:** This is the full loop — plan it in your head, write it at the terminal, Copilot starts working. You can queue up 3 agent tasks before your morning standup and have PRs waiting for you when it's done.

---

### Module 3.3 — Review the Agent PR Like a Senior Dev

**Goal:** Come back to the PR from Module 3.1. Don't just skim and approve — do a real review using CLI tools and Copilot Chat together.

**By now the agent should have a PR open.** Check:

```bash
gh pr list --state open
```

**Step 1 — Read it in the terminal first**

```bash
gh pr view <number>        # summary, description, checks status
gh pr diff <number>        # full diff in terminal
```

**Step 2 — Check out the branch and poke around**

```bash
gh pr checkout <number>
# Now you're on the agent's branch — explore, run it, test it
```

> 📸 **Screenshot cue:** Capture `gh pr diff` output in the terminal showing a meaningful chunk of the agent's changes.

**Step 3 — Ask Copilot to review it too**

Open VS Code on this branch (or GitHub.com PR view) and ask:

- In Copilot Chat: *"Review the changes in this PR. Focus on edge cases, error handling, and anything that could break existing behavior. Be specific about line numbers."*
- Or request a formal Copilot review via the Reviewers sidebar on the PR

> 📸 **Screenshot cue:** Capture a Copilot Chat response calling out a specific issue in the PR, or a Copilot PR review inline comment.

**Step 4 — Request changes or merge**

If the PR looks good:
```bash
gh pr merge <number> --squash --delete-branch
```

If you want changes first, leave a comment on the PR (not the issue):
```bash
gh pr comment <number> --body "The error handling in calculate() doesn't account for sequential operator presses — please add a guard for that case and re-run the tests."
```

> 📸 **Screenshot cue:** Capture the green merge confirmation in terminal, or the PR comment you left requesting changes.

**Instructor talking points:**
- The async agent workflow changes how you think about delegation — treat Copilot like a junior dev who works while you sleep
- `gh pr checkout` + Copilot Chat is a faster review loop than switching to the browser and back
- Copilot reviewing Copilot's own PR (via `gh pr comment` asking for a fix) is a real workflow — the agent will iterate on the PR based on your feedback
- The CLI commands in Module 3.2 are the same ones that power GitHub Actions workflows — learning them here makes reading `.yml` files much less intimidating

---

## Pre-Workshop Setup Checklist (Instructor)

- [ ] All participants have GitHub accounts added to the Enterprise Cloud org
- [ ] Copilot Business licenses assigned to all participants
- [ ] Copilot cloud agent enabled at org level (Settings → Copilot → Coding agent)
- [ ] GitHub Pages not blocked by org policy
- [ ] Participants in Track 3 have `gh` CLI installed (or Codespaces available as fallback)
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
| 23 | Module 3.1, Step 5 | Issue with Copilot assigned + agent session starting |
| 24 | Module 3.2, Block 1 | `gh copilot explain` output for a complex/risky command |
| 25 | Module 3.2, Block 2 | `gh copilot suggest` response + the resulting command output |
| 26 | Module 3.2, Block 3 | `gh pr list` or `gh run list` showing real repo output |
| 27 | Module 3.2, Block 4 | Terminal after `gh issue create --assignee @copilot` + browser showing agent started |
| 28 | Module 3.3, Step 2 | `gh pr diff` output in terminal |
| 29 | Module 3.3, Step 3 | Copilot Chat or PR review calling out a specific issue |
| 30 | Module 3.3, Step 4 | Merge confirmation in terminal OR PR comment requesting changes |


