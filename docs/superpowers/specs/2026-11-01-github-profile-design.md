# Design Doc: GitHub Profile Customization (`lark69`)

## 1. Intent and The Why
Create an impactful, highly professional, and modern GitHub profile README for **Gabriel Portela** (`lark69`). The goal is to project deep technical capability, software engineering maturity, and clean visual taste to international recruiters, engineering leaders, and clients.

## 2. Goals, Non-Goals, and Anti-Goals
* **Goals:**
  * Deliver a distinctive **Cyber Terminal (Hacker Dev)** aesthetic using clean CLI styling and curated neon accents.
  * Highlight the real core software ecosystem as the primary showcase:
    1. **Portex SaaS** (Subscription & cloud billing layer — TypeScript, Node.js, PostgreSQL, Docker).
    2. **Portex PDV / Tickets System** (`sistema-tickets-gpc` — High-performance desktop Point of Sale system built with **Rust**, **Tauri**, and **TypeScript**).
    3. **Locadora** (Web-based rental & catalog management system deployed with modern web technologies).
  * Structure content in **English** for global reach and maximum market appeal.
  * Implement automated daily GitHub Actions to run the contribution graph Snake Game animation (`platane/snk`).
  * Include real-time dynamic GitHub stats and top languages cards matching the dark cyberpunk palette.
  * Present terminal-styled quick-contact links (LinkedIn, Portfolio, Email).
* **Non-Goals:**
  * Over-engineering with custom server-side re-generation scripts when standard Actions and verified dynamic endpoints do this reliably.
  * Displaying low-signal vanity metrics.
* **Anti-Goals:**
  * Generic "AI-slop" or cluttered junior template look with dozens of random badges, conflicting colors, or distracting low-res GIFs.

## 3. Constraints
* GitHub's markdown sanitizer restricts custom CSS stylesheets and `<script>` tags; styling must be delivered via SVG assets, Shields.io badges, and valid GitHub Markdown/HTML formatting.
* High contrast dark-mode optimization while maintaining readability on light mode.
* The repository must be named exactly `lark69/lark69`, public, and initialized with a default branch.
* GitHub Action requires repository read/write permissions for workflow runs to commit the generated snake SVG to the `output` branch.

## 4. Approaches Considered
* **Approach 1: Automated Profile with GitHub Actions & Dynamic Telemetry (Selected)**
  * Uses GitHub Actions (`.github/workflows/snake.yml`) on a daily schedule to render the contribution graph snake animation.
  * Consumes dynamic stats SVGs configured with the Tokyo Night / Radical dark palette.
  * *Trade-off:* Requires repository workflow permissions; in return, delivers a living, automated profile that updates continuously.
* **Approach 2: Pure Static Markdown**
  * Single `README.md` without CI/CD actions.
  * *Trade-off:* Simpler setup, but sacrifices the dynamic snake animation and automated engineering flair.
* **Approach 3: Custom Node.js GraphQL Cron Generator**
  * *Trade-off:* Unnecessary complexity and brittle maintenance for no meaningful end-user visual difference.

## 5. Architectural & Layout Decisions
* **Header:** macOS/CLI terminal window mockup featuring:
  * Prompt: `gabriel@github:~$ whoami` -> Gabriel Portela (Full Stack & Systems Engineer &bull; SaaS & POS Architecture).
  * Prompt: `gabriel@github:~$ cat mission.txt` -> Engineering scalable SaaS platforms, high-performance desktop POS systems with Rust & Tauri, and modern web applications.
* **Featured Systems (Main Spotlight):**
  1. `Portex SaaS` — Cloud subscription & licensing platform for POS systems (TypeScript, Node.js, PostgreSQL, Docker).
  2. `Portex PDV / Ticket System` (`sistema-tickets-gpc`) — High-performance desktop Point of Sale (POS) client engine built with Rust, Tauri, and TypeScript.
  3. `Locadora` — Modern web rental management platform.
* **Core Capabilities (Categorized Badges):**
  * *Systems & Backend:* Rust, Node.js, TypeScript, PostgreSQL, Docker, RESTful APIs.
  * *Desktop & Frontend:* Tauri, React, Vite, HTML5/CSS3, Modern Web Design.
  * *Engineering Practices:* Clean Code, Desktop & Cloud Architecture, Automated CI/CD.
* **Telemetry & Automation:**
  * GitHub Readme Stats (Dark / Tokyo Night theme).
  * Top Languages card (featuring Rust, TypeScript, etc.).
  * Contribution Graph Snake Game SVG generated via GitHub Actions.
* **Terminal Contact:**
  * LinkedIn: `https://linkedin.com/in/gabriel-carmo-72871940a`
  * Portfolio & Direct Contact links.

## 6. What's Left to the Builder
1. Create the special GitHub repository `lark69/lark69` using `gh repo create`.
2. Author the production `README.md` matching all specification requirements.
3. Add `.github/workflows/snake.yml` to generate the snake SVGs on schedule and push to `output`.
4. Trigger the initial workflow run and verify all badges, SVG telemetry cards, and links render properly on GitHub.
