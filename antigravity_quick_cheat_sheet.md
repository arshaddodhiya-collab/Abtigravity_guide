# ⚡ Antigravity 1-Page Cheat Sheet

Pin this to your second monitor or print it for your desk. 

## 🚨 The 5 Security Rules (Non-Negotiable)
1. **NO Patient Data (PHI)** — Never paste real names, MRNs, Aadhaar, or medical records.
2. **NO Credentials** — Never paste DB passwords, JWT secrets, or API keys (`.env` files).
3. **NO Prod Configs** — Never share `application-prod.yml` or production IP addresses.
4. **ALWAYS Sanitize** — Strip internal package names and replace real IDs with `12345`.
5. **ALWAYS Review** — You are responsible for the code, not the AI. Test everything.

---

## 🧠 The CRISP Prompt Framework
To get good code, your prompt must be CRISP:
* **C** - Context (Framework, version, DB)
* **R** - Role (Who act as?)
* **I** - Instruction (What exactly to do?)
* **S** - Scope/Constraints (What NOT to do?)
* **P** - Proof/Format (How to output?)

---

## 📋 Copy & Paste Templates

### 1. Fix a Bug / Explain Stack Trace
```text
Tech Stack: [Spring Boot 3.2 / Angular 17]
Error: [paste SANITIZED error or stack trace here]
Context: I was trying to [operation, e.g., save a patient record].
Tried: [what you've already attempted]
Task: Identify the root cause, provide the fix, and explain why it happened.
Constraint: Ensure the fix handles null values gracefully.
```

### 2. Generate Unit Tests (Highest ROI)
```text
Tech Stack: [JUnit 5 + Mockito / Jasmine + Karma]
Task: Write comprehensive unit tests for the following class/method.
Code: [paste code here]
Requirements:
1. Test the happy path.
2. Test error cases (null inputs, exceptions).
3. Test edge cases.
4. Use parameterized tests if applicable.
Do not use real patient data in test fixtures. Use generic names.
```

### 3. Refactor Messy Code
```text
Tech Stack: [Java 17 / TypeScript]
Task: Refactor this method to improve readability and reduce cognitive complexity.
Code: [paste code here]
Requirements:
1. Break down into smaller private methods if needed.
2. Ensure variable names are highly descriptive.
3. Keep the exact same inputs and outputs (do not break the contract).
4. Explain what you changed and why.
```

### 4. Explain Unfamiliar Code (For 60% Outsourced Team)
```text
Task: Act as a Senior Architect. Explain this code to me simply.
Code: [paste code here]
Provide:
1. A 2-sentence summary of what this does functionally.
2. What business rules it seems to be enforcing.
3. What could go wrong (edge cases it might be missing).
```

### 5. Generate Documentation / PR Description
```text
Task: Write a concise, professional Pull Request description based on this diff:
Diff: [paste git diff]
Format:
- **What changed**: (bullet points)
- **Why it changed**: (the core bug/feature)
- **What was tested**: (areas reviewers should focus on)
Keep it brief and exclude internal paths.
```

---

*Remember: Check your `settings.json` to ensure your file `fileDenyList` is active!*
