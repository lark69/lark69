# GitHub Profile Customization Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create, customize, and automate the special GitHub profile repository `lark69/lark69` with a modern Cyber Terminal aesthetic, featuring Gabriel's core projects (Portex SaaS, Portex PDV in Rust/Tauri, Locadora), categorized tech stacks, real-time telemetry stats, and an automated contribution graph Snake Game animation.

**Architecture:** A public GitHub special repository (`<username>/<username>`) containing a high-contrast dark-mode `README.md` formatted with terminal CLI aesthetics, SVGs, and Shields badges, paired with a GitHub Actions cron workflow (`.github/workflows/snake.yml`) that generates and deploys the contribution grid snake SVG to an `output` branch.

**Tech Stack:** GitHub Flavored Markdown, SVG, Shields.io badges, GitHub Actions (`platane/snk`, `crazy-max/ghaction-github-pages`), GitHub CLI (`gh`).

**Spec:** [docs/superpowers/specs/2026-11-01-github-profile-design.md](file:///home/gabrielportela/github-profile/docs/superpowers/specs/2026-11-01-github-profile-design.md)

## Global Constraints
* The repository must be named exactly `lark69/lark69` and must be public.
* Language across all copy, terminal commands, and descriptions must be English.
* All external SVGs and stats cards must support dark mode without breaking on light mode.
* Featured systems must highlight:
  1. Portex SaaS (TypeScript, PostgreSQL, Docker)
  2. Portex PDV (`sistema-tickets-gpc` — Rust, Tauri, TypeScript)
  3. Locadora (Web rental management)
* GitHub Actions workflow must run automatically via cron and allow manual dispatch (`workflow_dispatch`).

## Review Focus
* `gh repo create` failing if repo already exists: check existence first and handle accordingly.
* Actions workflow failing due to missing `write` permissions for `GITHUB_TOKEN`: set `permissions: contents: write` explicitly in the workflow file.
* Missing snake SVG on initial visit: trigger the GitHub Action immediately after pushing to populate the `output` branch.
* Broken SVG links or clashing colors in GitHub dark mode: verify raw URL paths and test rendering.
* Light mode visibility: ensure high-contrast colors and fallback text are readable.

---

### Task 1: Repository Initialization and Local Git Setup

**Files:**
- Create: `/home/gabrielportela/github-profile/.gitignore`
- Remote: `https://github.com/lark69/lark69`

**Interfaces:**
- Produces: Initialized Git repository tracking remote `origin` pointing to `lark69/lark69`.

- [ ] **Step 1: Check if remote repository `lark69/lark69` exists**
Run: `gh repo view lark69/lark69 2>&1`
Expected: "Could not resolve to a Repository" or repository details.

- [ ] **Step 2: Create public repository `lark69/lark69` if not present**
Run: `gh repo create lark69/lark69 --public --description "Gabriel Portela's GitHub Profile" --confirm`
Expected: Repository created successfully.

- [ ] **Step 3: Initialize local git repository in `/home/gabrielportela/github-profile` and link origin**
Run:
```bash
cd /home/gabrielportela/github-profile
git init -b main
git remote add origin https://github.com/lark69/lark69.git || git remote set-url origin https://github.com/lark69/lark69.git
```
Expected: `git remote -v` lists `origin` pointing to `lark69/lark69.git`.

- [ ] **Step 4: Create `.gitignore` to prevent committing superpowers brainstorm cache**
Create: `/home/gabrielportela/github-profile/.gitignore` with:
```gitignore
.superpowers/
node_modules/
.DS_Store
```

- [ ] **Step 5: Commit initial repository scaffolding**
Run:
```bash
git add .gitignore docs/
git commit -m "chore: initial profile repository structure and design specs"
```

---

### Task 2: Author Production `README.md` (Cyber Terminal Design)

**Files:**
- Create: `/home/gabrielportela/github-profile/README.md`

**Interfaces:**
- Consumes: Specifications from `docs/superpowers/specs/2026-11-01-github-profile-design.md`.
- Produces: Fully formatted, responsive `README.md` with:
  1. Terminal Header Box (CLI commands, status)
  2. Featured Systems Section (Portex SaaS, Portex PDV in Rust/Tauri, Locadora)
  3. Categorized Tech Stack Badges
  4. Real-time GitHub Stats & Top Languages cards (Tokyo Night theme)
  5. Contribution Graph Snake Game SVG reference (`https://raw.githubusercontent.com/lark69/lark69/output/github-contribution-grid-snake.svg`)
  6. Terminal Contact Section (LinkedIn, Portfolio, Contact)

- [ ] **Step 1: Draft the `README.md` content matching all spec constraints**
Write `/home/gabrielportela/github-profile/README.md` with exact HTML and Markdown structures:
- Terminal mockup with prompt:
  ```markdown
  ```bash
  gabriel@github:~$ whoami
  > Gabriel Portela | Full Stack & Systems Engineer • SaaS & POS Architecture
  
  gabriel@github:~$ cat mission.txt
  > Building high-performance desktop POS systems with Rust & Tauri, scalable cloud SaaS platforms, and modern web architectures.
  ```
- Featured systems table or cards showcasing:
  - `Portex SaaS`: Subscription & cloud billing engine for POS environments (TypeScript, Node.js, PostgreSQL, Docker)
  - `Portex PDV`: High-performance offline-first Desktop POS application built with Rust, Tauri & TypeScript
  - `Locadora`: Web rental management platform
- Tech Stack Shields badges organized by:
  - Systems & Backend: Rust, Tauri, Node.js, TypeScript, PostgreSQL, Docker
  - Frontend & UI: React, Vite, HTML5, CSS3, Modern Web Design
  - Tools & Practices: Git, Linux, Clean Architecture, REST APIs
- Dynamic Telemetry cards using GitHub Readme Stats (`theme=tokyonight`, `hide_border=true`, `bg_color=0d1117`)
- Snake game contribution animation pointing to branch `output`
- Contact commands (`gabriel@github:~$ connect --linkedin`)

- [ ] **Step 2: Validate Markdown and badge image links**
Run: `grep -E "https://" /home/gabrielportela/github-profile/README.md`
Check: Ensure all badge URLs and GitHub Stats URLs are valid and well-formed.

- [ ] **Step 3: Commit `README.md`**
Run:
```bash
git add README.md
git commit -m "feat: author cyber terminal profile README with featured projects and telemetry"
```

---

### Task 3: GitHub Actions Workflow for Contribution Graph Snake Game

**Files:**
- Create: `/home/gabrielportela/github-profile/.github/workflows/snake.yml`

**Interfaces:**
- Produces: Daily automated action producing `github-contribution-grid-snake.svg` and `github-contribution-grid-snake-dark.svg` pushed to branch `output`.

- [ ] **Step 1: Create `.github/workflows/snake.yml`**
Create: `/home/gabrielportela/github-profile/.github/workflows/snake.yml` with:
```yaml
name: Generate Snake Contribution Animation

on:
  schedule:
    # Run every 24 hours at midnight UTC
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: Generate GitHub Contribution Grid Snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: lark69
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark&color_snake=#00f0ff&color_dots=#161b22,#004d40,#00796b,#00bfa5,#64ffda

      - name: Push Snake SVG to Output Branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- [ ] **Step 2: Validate YAML syntax**
Run: `python3 -c "import yaml; yaml.safe_load(open('/home/gabrielportela/github-profile/.github/workflows/snake.yml'))"`
Expected: Clean exit without syntax errors.

- [ ] **Step 3: Commit workflow file**
Run:
```bash
git add .github/workflows/snake.yml
git commit -m "ci: add automated snake contribution animation workflow"
```

---

### Task 4: Deployment, Workflow Execution, and Live Verification

**Files:**
- Repository: `lark69/lark69` (main and output branches)

**Interfaces:**
- Consumes: All commits from Tasks 1, 2, and 3.
- Produces: Live GitHub profile visible at `https://github.com/lark69`.

- [ ] **Step 1: Push main branch to remote**
Run: `git push -u origin main`
Expected: Remote branch `main` updated.

- [ ] **Step 2: Ensure Actions permissions allow write access**
Run:
```bash
gh api --method PUT repos/lark69/lark69/actions/permissions/workflow \
  -f default_workflow_permissions='write' \
  -F can_approve_pull_request_reviews=true 2>&1 || true
```

- [ ] **Step 3: Trigger the Snake Generation workflow manually**
Run: `gh workflow run snake.yml --repo lark69/lark69`
Expected: Workflow dispatched.

- [ ] **Step 4: Monitor workflow run until completion**
Run: `gh run list --repo lark69/lark69 --limit 1` and wait for status `completed (success)`.
Expected: Run completes successfully.

- [ ] **Step 5: Verify the `output` branch exists with generated SVGs**
Run: `gh api repos/lark69/lark69/branches/output`
Expected: Branch `output` exists.

- [ ] **Step 6: Verify Profile Live Status**
Run: `curl -s -o /dev/null -w "%{http_code}" https://github.com/lark69`
Expected: HTTP 200.
