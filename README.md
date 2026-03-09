# 🚀 Antigravity HMIS Developer Toolkit
## Master Index & Learning Path

Welcome to the **Antigravity Developer Toolkit** for the HMIS Product Division. 

This repository contains everything your team needs to adopt AI coding assistance safely, effectively, and responsibly while building our healthcare platform.

---

## 📂 What's In This Folder?

We have structured these guides by role and purpose. Start with the core guides, then move to your specific stack.

### 🌟 Core Guides (Read These First)
1. **[General Developer Guide](./antigravity_developer_guide.md)**
   - Start here. Covers what Antigravity is, how it saves time, standard workflows (bug fixing, tests, refactoring), and company best practices.
2. **[Security Constraints Guide](./antigravity_security_constraints_guide.md)**
   - **MANDATORY READING.** The visual guide on how to configure your IDE (`settings.json`, `.geminiignore`) to prevent PHI leaks and secure our codebase.
3. **[Prompting Mastery Guide](./antigravity_prompting_guide.md)**
   - The "CRISP" framework for writing prompts that actually work, plus dozens of templates for daily tasks.
4. **[Documentation Guide](./documentation_guide_for_developers.md)**
   - How to use Antigravity to write ADRs, PR descriptions, and code documentation in a healthcare context.

### 💻 Stack-Specific Guides (Choose Your Path)
5. **[Angular 17 Frontend Guide](./angular17_antigravity_guide.md)**
   - For UI developers. Covers Signals, Standalone Components, Reactive Forms, RxJS, state management, and frontend security prompts.
6. **[Spring Boot 17 Backend Guide](./springboot_antigravity_guide.md)**
   - For backend developers. Covers JPA Entities, MapStruct, complex SQL/query optimization, Spring Security, and REST APIs.

### 🎤 For Team Leads & Facilitators
7. **[Session Facilitation Guide](./session_facilitation_guide.md)**
   - The step-by-step playbook for conducting the rollout training session, including live demo scripts and how to handle pushback from the team.

### ⚡ Quick Reference
8. **[1-Page Cheat Sheet](./antigravity_quick_cheat_sheet.md)** *(New!)*
   - A highly condensed reference of the 5 Security Rules and the most common copy-paste prompts. Pin this to your second monitor.

---

## 🎯 Recommended Learning Paths

### For a Junior Developer Just Joining:
1. Setup IDE using **Security Constraints Guide**
2. Read the **Core Developer Guide**
3. Keep the **Cheat Sheet** open while working
4. Review the relevant Stack Guide (Frontend or Backend)

### For a Senior Developer / Tech Lead:
1. Read the **Prompting Mastery Guide** for advanced chaining techniques.
2. Review the **Documentation Guide** to standardise PRs.
3. Help enforce the **Security Constraints**.

### For the Session Facilitator:
1. Read the **Session Facilitation Guide** cover to cover.
2. Practice the "WOW Demo" using bugs from your current sprint.

---

> **The Golden Rule for HMIS Development with AI:**
> Never paste PHI, Credentials, or Production Configs. ALWAYS sanitize your inputs. ALWAYS review the AI's output before committing.
