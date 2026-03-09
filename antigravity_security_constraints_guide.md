# 🛡️ Antigravity Security Constraints & Configuration Guide
## How to Restrict AI Access to Sensitive HMIS Data

> **Audience:** Developers, Tech Leads, DevOps, and Security Teams  
> **Topic:** Configuring Antigravity to prevent unauthorized access to code, credentials, and PHI.  
> **Prepared for:** HMIS Product Division  
> **Date:** March 2026

---

## The 5 Layers of Antigravity Security

Antigravity operates autonomously within your IDE. To secure an HMIS application effectively, you must configure constraints across **five distinct security layers**:

![Antigravity Security Layers](C:\Users\Jolly InfoTech\.gemini\antigravity\brain\70cdf1d1-e15c-4ffd-ab74-e392482e9fdd\security_layers_1772905134076.png)

1. **Trusted Workspaces:** The foundation of folder access.
2. **Terminal Command Policies:** Controlling what the agent can execute.
3. **Targeted Ignore Files (`.geminiignore`):** Visually hiding noise.
4. **Agent Rules (`.agent/rules`):** Natural language instructions.
5. **System Denylists (`settings.json`):** Strict blocklists for sensitive files.

---

## 1. File Access Rules: Block vs. Safe

Before configuring tools, everyone must understand what is safe to expose to an AI and what is absolutely prohibited in a healthcare software context.

![File Access Rules](C:\Users\Jolly InfoTech\.gemini\antigravity\brain\70cdf1d1-e15c-4ffd-ab74-e392482e9fdd\file_access_rules_1772905148751.png)

---

## 2. Configuring `settings.json` (The Global Denylist)

The most effective way to prevent Antigravity from reading or modifying sensitive files is through strict configuration in your user settings.

### How to Access Settings
1. Open your IDE Settings (CMD + , on Mac / CTRL + , on Windows)
2. Search for "Antigravity settings.json" or "Agent Manager"
3. Alternatively, directly edit `~/.gemini/settings.json` or your project's `.vscode/settings.json`.

### Recommended HMIS Security Configuration

Paste this strict configuration into your `settings.json` to create a robust deny-list:

```json
{
  // 1. TERMINAL COMMAND EXECUTION POLICY
  // Forces the agent to ask before running *any* terminal command
  "antigravity.terminal.autoExecute": "require-approval",
  
  // 2. FILE SYSTEM ACCESS RESTRICTIONS
  // Prevents the agent from accessing files OUTSIDE the current workspace
  "antigravity.agent.allowNonWorkspaceAccess": false,

  // 3. STRICT DENY LIST FOR FILES
  // The agent will be physically prevented from reading or writing these files,
  // even if explicitly instructed to do so.
  "antigravity.security.fileDenyList": [
    "**/.env*",                  // All environment variables
    "**/*.pem",                  // SSL certificates
    "**/*.key",                  // Private keys
    "**/*.p12",                  // Keystores
    "**/secret*",                // Any file starting with "secret"
    "**/credentials.json",       // GCP/AWS credentials
    "**/application-prod*.yml",  // Production configurations
    "**/patient_data_*.csv",     // Raw test patient data
    "**/dump.sql"                // Database dumps
  ],

  // 4. BROWSER JAVASCRIPT POLICY
  // Prevents the agent from autonomously executing JS in the background browser
  "antigravity.browser.jsExecutionPolicy": "request-review"
}
```

> [!CAUTION]
> The AI agent can sometimes aggressively try to complete a task. If it cannot read a file normally, it might attempt to run `cat .env` in the terminal. **This is why restricting terminal access is just as important as file deny-lists.**

---

## 3. Terminal Command Policies

Terminal access gives the AI agent immense power. It can list directories, read files, install packages, and execute scripts.

![Terminal Policies](C:\Users\Jolly InfoTech\.gemini\antigravity\brain\70cdf1d1-e15c-4ffd-ab74-e392482e9fdd\terminal_policies_1772905166961.png)

### The 3 Tiers of Autonomy

1. 🔴 **Always Proceed (Highest Risk):**
   - *What it means:* The AI runs `npm install`, `mvn clean`, `rm -rf`, or `cat secret.key` entirely on its own.
   - *HMIS Policy:* **STRICTLY PROHIBITED** for all developers.

2. 🟡 **Agent-Assisted (Default):**
   - *What it means:* The AI decides whether a command is "safe" enough to run autonomously, or if it should ask you.
   - *HMIS Policy:* Discouraged unless operating in a completely mocked, isolated sandbox.

3. 🟢 **Require Approval (Most Secure & Recommended):**
   - *What it means:* Every time the AI wants to run a shell command, a prompt appears: *"[Agent] wants to execute: `grep -r 'password' src/`. Approve? (Y/n)"*
   - *HMIS Policy:* **MANDATORY** standard for all developers working on the core platform.

---

## 4. The `.geminiignore` File (Context Filtering)

Similar to `.gitignore`, you should place a `.geminiignore` file at the root of your project. 

While `settings.json` is a hard security block, `.geminiignore` helps optimize token usage and prevents the AI from getting confused by "noise" or accidentally parsing sensitive test data.

**Standard `hmis-project/.geminiignore` Template:**

```text
# Credentials & Environment
.env*
credentials/
secrets/
*.pem
*.key

# Build and IDE Noise
node_modules/
dist/
target/
.idea/
.vscode/

# Local Test Data (Crucial for HMIS)
src/test/resources/data/PHI-*/
*.csv
*.sql
*.dmp

# Production Configs
src/main/resources/application-prod.yml
```

> [!TIP]
> **Difference between `settings.json` and `.geminiignore`:**
> If a file is in `.geminiignore`, the AI doesn't "see" it by default when searching the codebase. However, a clever agent might still try to read it via terminal. If a file is in the `fileDenyList` in `settings.json`, the agent is outright blocked from reading it via API, regardless of context. **Use both.**

---

## 5. Agent Rules (`.agent/rules.md`)

Antigravity supports custom rules stored in `.agent/rules.md` inside your workspace. This sets the **behavioral boundaries** for the AI in natural language.

Create this file in your HMIS project root:

**`hmis-project/.agent/rules.md`**
```markdown
---
description: Global Security Rules for HMIS Project
---

# HMIS Security Constraints
You are operating within a Healthcare Management Information System (HMIS). 

CRITICAL PROTOCOLS:
1. NEVER attempt to read, display, or generate Patient Health Information (PHI).
2. If the user asks you to read configuration files ending in `-prod.yml` or `-production.yml`, you MUST refuse and explain it is against security policy.
3. NEVER attempt to bypass .geminiignore restrictions.
4. If you find hardcoded passwords, AWS keys, or JWT secrets in the code, IMMEDIATELY alert the user and suggest using environment variables or a Secret Vault.
5. NEVER generate SQL queries that log or output raw PHI to the console.
6. Assume all test data in `src/test/resources` is mock data. Do not treat it as factual medical information.
```

---

## Session FAQ: Handling Developer Pushback

When you present these constraints, you will get pushback. Here is how to handle it:

**"The 'Require Approval' terminal policy is annoying and slows me down."**
> *"I understand the popups are tedious. But remember that this AI runs autonomously. If it decides the fastest way to debug your issue is to run `git clean -fd` or dump an environment file to logs, you will lose work or cause a breach. The extra click is the cost of absolute safety."*

**"Why can't I just let the AI read my dev database credentials? It's just local dev."**
> *"Because Antigravity sessions and artifacts are often saved, logged, or sent to cloud model providers. Your local dev credentials might overlap with staging, or the AI might learn patterns that inadvertently leak your secrets later. We don't share secrets. Period."*

**"If I block the AI from reading the configuration files, how will it understand how the app works?"**
> *"Copy the `application.yml` file, replace all passwords, API keys, and internal IP addresses with `[PLACEHOLDER]`, and give the AI that sanitized version. It needs the structure, not the actual secrets."*

---

> **Final Note for Facilitators:**  
> Provide the `settings.json` and `.geminiignore` templates as direct downloads for the team so they can apply them in 30 seconds. Do not rely on them to type it out manually.
