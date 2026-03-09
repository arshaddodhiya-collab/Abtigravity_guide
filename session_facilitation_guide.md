# 🎤 Antigravity Training Session — Facilitator's Playbook
## How to Conduct the Developer Training Session

> **Facilitator:** [Your Name]  
> **Audience:** ~40-50 Developers (60% Outsourced · 40% In-House)  
> **Phase:** HMIS Product — Bug Fixing & Final Feature Changes (BMC Mumbai)  
> **CTO Directive:** Add value, enhance team productivity, don't code — lead  
> **Date:** March 2026

---

## Table of Contents

1. [Understanding Your Audience](#1-understanding-your-audience)
2. [Session Strategy — What Will Actually Work](#2-session-strategy)
3. [Pre-Session Preparation Checklist](#3-pre-session-preparation-checklist)
4. [Session Schedule — Detailed Agenda](#4-session-schedule)
5. [Session 1: Introduction & Why This Matters NOW](#5-session-1-introduction)
6. [Session 2: Live Demo — Antigravity in Action](#6-session-2-live-demo)
7. [Session 3: Hands-On Workshop](#7-session-3-hands-on-workshop)
8. [Session 4: Security & Safe Usage](#8-session-4-security)
9. [Session 5: Q&A, Challenges & Wrap-Up](#9-session-5-wrap-up)
10. [Handling Difficult Situations](#10-handling-difficult-situations)
11. [Post-Session Follow-Up Plan](#11-post-session-follow-up-plan)
12. [Measuring Impact — Prove Your Value](#12-measuring-impact)
13. [Slide Deck Outline](#13-slide-deck-outline)
14. [Speaker Notes & Talking Points](#14-speaker-notes)
15. [Resource Kit for Developers](#15-resource-kit)

---

## 1. Understanding Your Audience

Before designing the session, understand who's in the room:

### Audience Profile

| Factor                      | Reality                                                           | Session Impact                                                                      |
| --------------------------- | ----------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **60% Outsourced**          | May not feel deeply invested in the company's long-term success   | Focus on **personal skill-building** — "This makes YOU more valuable in the market" |
| **40% In-House**            | More stable but may feel stretched with product delivery pressure | Focus on **efficiency** — "This helps you deliver faster with less stress"          |
| **Product near delivery**   | Bug-fix mode, change requests from BMC Mumbai                     | Content must be **immediately applicable** — no theory-only sessions                |
| **High attrition risk**     | People may leave after delivery                                   | Create **portable knowledge** — skills they carry everywhere                        |
| **Mixed experience levels** | Juniors, mid-level, seniors, leads                                | Layer the content — basics for juniors, advanced patterns for seniors               |
| **Time pressure**           | Sprint commitments, deadlines                                     | Keep it **tight and practical** — no 3-hour lectures                                |

### The 3 Types of People in Your Room

```
🟢 ENTHUSIASTS (20%)
   "Finally! I've been wanting to learn this."
   → Give them advanced tips, make them champions

🟡 SKEPTICS (50%)
   "Does this actually work? I'm too busy for this."
   → Show immediate ROI with live bugs from their actual work

🔴 RESISTORS (30%)
   "AI is hype" or "It'll replace us" or "I don't care, I'm leaving"
   → Don't argue. Let the demo speak. Show, don't tell.
```

### What They ACTUALLY Want to Hear

| What YOU want to say                    | What THEY want to hear                                                   |
| --------------------------------------- | ------------------------------------------------------------------------ |
| "AI is the future of development"       | "This will shave 2 hours off your daily work"                            |
| "Let me explain how LLMs work"          | "Let me show you how to fix that BMC bug in 5 minutes"                   |
| "Here are best practices for prompting" | "Copy this prompt, paste it, get working code"                           |
| "Security is critical"                  | "Here's exactly what NOT to paste so you don't get fired"                |
| "This enhances your career"             | "Developers who use this are 2x faster — and that shows in your reviews" |

---

## 2. Session Strategy

### The Golden Rule

> **Show. Don't Tell.**

Nobody cares about slides. They care about seeing you fix a real bug in 3 minutes that would normally take 30.

### Session Format: Workshop-First Approach

```
❌ DON'T DO THIS:
   2 hours of slides → 30 min demo → "Any questions?"
   (Audience lost after 20 minutes)

✅ DO THIS:
   15 min context → 30 min LIVE DEMO → 45 min HANDS-ON → 
   20 min security → 10 min wrap-up
   (Audience engaged throughout)
```

### Key Principles

1. **Start with a WOW moment** — Fix an actual open bug live in under 5 minutes
2. **Make it about THEM** — "This saves YOU time, makes YOUR life easier"
3. **Use THEIR code** — Pick real examples from the project (sanitized)
4. **Keep it practical** — Every minute of theory must earn its place
5. **Handle resistance with results** — Don't debate, demonstrate
6. **Create champions** — Identify 3-4 enthusiasts to be team mentors post-session
7. **Follow up** — One session won't change behavior; weekly tips will

---

## 3. Pre-Session Preparation Checklist

### 1 Week Before

- [ ] **Talk to the CTO** — Confirm objectives, get explicit support
- [ ] **Announce the session** — Email/Slack with subject: *"Finish your bugs 2x faster — Antigravity Training"* (not *"Mandatory AI Training Session"*)
- [ ] **Survey the team** (3 questions):
  - Have you used AI coding tools before? (Yes/No)
  - What takes most of your time daily? (Bug fixing / Writing tests / Understanding code / Other)
  - One thing you wish was faster in your workflow?
- [ ] **Collect real examples** — Get 3-4 actual bugs/tasks from the current sprint (sanitize them)
- [ ] **Prepare the demo environment** — Antigravity installed, project open, bugs ready
- [ ] **Create the resource kit** — printed/shared guides, cheat sheets, prompt templates

### 1 Day Before

- [ ] **Test the demo end-to-end** — Run through every live example to avoid live failures
- [ ] **Prepare backup examples** — If live demo fails, have screenshots/recordings ready
- [ ] **Check projector/screen sharing** — Test resolution, font size (minimum 16pt in IDE)
- [ ] **Prepare printed cheat sheets** — 1 per developer (prompt templates, security rules)
- [ ] **Set up feedback form** — Google Form with 5 questions (prepare link/QR code)

### Day Of

- [ ] **Arrive 15 min early** — Set up, test screen, open all tabs/files
- [ ] **Have water and energy** — You're performing, not presenting
- [ ] **Mindset check** — You're here to HELP them, not to show off

---

## 4. Session Schedule

### Option A: Single 2-Hour Session (Recommended)

```
TIME          SECTION                           FORMAT        MINUTES
──────────────────────────────────────────────────────────────────────
00:00-00:15   Opening & WOW Demo                Live Demo       15
00:15-00:25   What is Antigravity + Why Now      Talk            10
00:25-00:55   Live Demo — 4 Real Use Cases       Live Demo       30
00:55-01:05   ☕ BREAK                            Break           10
01:05-01:35   Hands-On: Developers Try It        Workshop        30
01:35-01:50   Security — What NEVER to Share     Talk + Demo     15
01:50-02:00   Wrap-Up, Resources, Q&A            Discussion      10
──────────────────────────────────────────────────────────────────────
              TOTAL                                            2 hours
```

### Option B: Two 1-Hour Sessions (If Team Can't Spare 2 Hours)

**Session 1 (1 Hour): "See It In Action"**
```
00:00-00:10   Opening WOW Demo (fix a real bug live)
00:10-00:15   Brief intro — what, why, how
00:15-00:45   Live Demo — 4 use cases from YOUR project
00:45-00:55   Security — The 5 Rules (quick version)
00:55-01:00   Preview of Session 2, Q&A
```

**Session 2 (1 Hour): "Do It Yourself"**
```
00:00-00:05   Recap & setup check
00:05-00:40   Hands-on workshop — developers try with their own bugs
00:40-00:50   Advanced tips & prompting techniques
00:50-01:00   Wrap-up, resources, Q&A
```

### Option C: Quick "Brown Bag" Lunch Sessions (30 min × 4 days)

If the team is deep in bug-fixing and can't spare 2 hours:

| Day       | Topic                              | Duration |
| --------- | ---------------------------------- | -------- |
| Monday    | WOW Demo + What is Antigravity     | 30 min   |
| Tuesday   | Bug Fixing with Antigravity (Live) | 30 min   |
| Wednesday | Writing Tests + Refactoring (Live) | 30 min   |
| Thursday  | Security Rules + Hands-On + Q&A    | 30 min   |

> [!TIP]
> **Recommendation:** Go with **Option A** if possible. A single 2-hour block has more impact than fragmented sessions. But if the team pushes back, Option C (lunch sessions) feels less disruptive and gets good attendance.

---

## 5. Session 1: Introduction & WOW Demo (15 min)

### Opening Script (First 2 Minutes)

> *"Good [morning/afternoon], everyone. I know you're busy with bug fixes and BMC changes, so I'll make this worth your time.*
>
> *In the next 2 hours, I'm going to show you how to do in 5 minutes what currently takes you 30-60 minutes. I'm not going to give you a lecture. I'm going to fix a REAL bug from our sprint board — live, in front of you — using Antigravity.*
>
> *If at the end you don't think this was useful, tell me. But give me 2 hours."*

### The WOW Demo (First 5-8 Minutes)

**This is the MOST IMPORTANT part of the session.** If you nail this, you have the room. If you don't, you've lost them.

**How to Prepare:**

1. Pick a **real, current bug** from the sprint board that developers have seen
2. Pick one that's **moderately complex** — not trivial, not impossible
3. **Practice solving it 3 times** before the session
4. Time yourself — aim for **under 5 minutes** live

**Live Demo Flow:**

```
Step 1: Show the bug ticket on screen (JIRA/sprint board)
        "Here's bug HMIS-3421 — you've all seen this."

Step 2: Open the relevant code file in IDE

Step 3: Open Antigravity, paste the sanitized error/stack trace

Step 4: Show how Antigravity analyzes it and suggests a fix

Step 5: Apply the fix

Step 6: Run the test to show it works

Step 7: Pause. Let it sink in.
        "That took 4 minutes. Without AI, that's a 30-minute debugging session."
```

**Backup Plan:** If the live demo fails (it can happen):
- Have a **screen recording** of the same demo ready
- Say: *"The live gods are not with us today, so let me show you the recording I made yesterday"*
- NEVER apologize excessively — just pivot smoothly

### Brief Context (5 Minutes)

After the wow demo, give brief context:

- **What Antigravity is** — AI coding assistant in your IDE (1 min)
- **Why NOW** — We're in bug-fix mode, this accelerates it (1 min)
- **What it's NOT** — Not a replacement, not magic, needs your brain (1 min)
- **What we'll cover today** — 4 use cases, hands-on, security rules (1 min)
- **Your role after this session** — "I'll be available as your go-to for AI-assisted dev" (1 min)

---

## 6. Session 2: Live Demo — 4 Real Use Cases (30 min)

### Use Case 1: Bug Fixing (8 min)

Pick a **different bug** from the WOW demo. Walk through step by step:

```
1. Show the bug ticket
2. Open the code
3. Show how to SANITIZE the code before pasting (remove PHI, secrets)
4. Write the prompt using CRISP framework
5. Show Antigravity's response
6. Review the suggestion critically — point out what's good and what to verify
7. Apply the fix
8. Run tests

KEY TEACHING POINT:
"Notice I didn't just copy-paste. I READ the suggestion, verified it 
makes sense, and THEN applied it. Always review before committing."
```

### Use Case 2: Writing Tests (8 min)

This is the **highest-ROI use case** for bug-fix phase:

```
1. Pick a service method that has NO tests
2. Show how to write a prompt for test generation
3. Show Antigravity generating JUnit 5 + Mockito tests
4. Review: "Look, it generated 6 test cases including 
   edge cases I might not have thought of"
5. Run the tests — show they pass
6. Point out: "It caught that null input case — 
   important for code coming from BMC"

KEY TEACHING POINT:
"Every bug you fix should have a test. Antigravity generates 
that test in 2 minutes instead of 20. No more excuses for 
untested code."
```

### Use Case 3: Understanding Unfamiliar Code (7 min)

Especially relevant for outsourced team members who didn't write the original code:

```
1. Open a complex module that someone wrote months ago
2. "Raise your hand if you've been assigned a bug in code 
   you didn't write." (Everyone raises hand)
3. Select a method and ask Antigravity: "Explain what this 
   method does, what business rule it implements, and what 
   could go wrong"
4. Show the clear explanation
5. "This just saved you 30 minutes of reading through 
   interconnected classes"

KEY TEACHING POINT:
"For outsourced team members who joined mid-project — 
this is your fastest way to understand the codebase."
```

### Use Case 4: Code Refactoring After Bug Fix (7 min)

Relevant for the feature changes from BMC:

```
1. Show a method that works but is messy (long, complex)
2. Ask Antigravity to refactor it
3. Show the cleaner version
4. Run existing tests to prove nothing broke
5. "When BMC asks for a change, modifying clean code takes 
   10 minutes. Modifying spaghetti takes 2 hours."

KEY TEACHING POINT:
"Antigravity doesn't just fix bugs — it improves code quality. 
Every PR should leave the code better than you found it."
```

---

## 7. Session 3: Hands-On Workshop (30 min)

### Setup (5 min)

```
"Now it's your turn. Open your IDE. I want everyone to try this 
with a REAL task from your current sprint."

Instructions:
1. Pick ONE bug or task from your sprint board
2. Open the relevant code file
3. Write a prompt following the CRISP template I'll share
4. Use Antigravity to get a solution
5. Review, test, and if it works — commit it

I'll walk around and help. Raise your hand if you're stuck.
```

### During the Workshop (20 min)

**Your job during this time:**

1. **Walk the room** — don't sit down, be visible and available
2. **Help the stuck ones** — especially juniors and outsourced members
3. **Celebrate wins** — when someone fixes a bug, say "That's it! How long would that have taken otherwise?"
4. **Correct bad prompts** — show them how to improve their prompt
5. **Watch for security mistakes** — if someone pastes secrets, gently correct them
6. **Identify champions** — note who picks it up fastest, they'll be your team mentors

### Debrief (5 min)

```
"Okay, show of hands:"
- "Who fixed or made progress on their bug?" (Celebrate)
- "Who found the AI suggestion useful but needed to modify it?" (GOOD — they're reviewing)
- "Who got a completely wrong answer?" 
  (Address: "This is normal. Let's see how to improve your prompt.")
- "Who saved time compared to their usual approach?" (This is your metric)
```

---

## 8. Session 4: Security — What NEVER to Share (15 min)

### Why This Matters (2 min)

> *"Everything I've shown you is powerful. But with power comes responsibility. We're building a hospital management system. We deal with patient data. One wrong paste into an AI tool could be a compliance violation that costs the company — and potentially your career."*

### The 5 Security Rules (8 min)

Present these as **non-negotiable rules**, not suggestions:

```
RULE 1: NEVER paste patient data
        (No names, MRNs, Aadhaar, diagnoses — not even "test" 
        data copied from production)

RULE 2: NEVER paste credentials
        (No passwords, API keys, JWT secrets, database URLs 
        with real credentials — ALWAYS use placeholders)

RULE 3: NEVER paste proprietary algorithms
        (Billing formulas, drug interaction logic, clinical 
        decision engines — ask about the PATTERN, not the CODE)

RULE 4: ALWAYS sanitize before pasting
        (Replace real values with generic ones, strip internal 
        paths, remove customer-specific names)

RULE 5: ALWAYS review before committing
        (AI code is a DRAFT — it must pass the same code review 
        as human-written code)
```

### Live Security Demo (5 min)

```
Show WRONG way (on screen, never do it for real):
   "Here is application-prod.yml with database credentials..."
   → "See how dangerous this is? These credentials are now
      potentially exposed."

Show RIGHT way:
   "I need help configuring PostgreSQL connection pooling.
   Here's my config with placeholder values:
   url: jdbc:postgresql://HOST:PORT/DB_NAME
   username: USERNAME
   password: PASSWORD"
   → "Antigravity can still help — it doesn't NEED real values."
```

---

## 9. Session 5: Wrap-Up (10 min)

### Summary (3 min)

```
"Let's recap what we covered:

1. ✅ Antigravity can fix bugs, write tests, explain code, 
   and refactor — saving you 30-60 minutes daily

2. ✅ The quality of your PROMPT determines the quality of 
   the OUTPUT — use the CRISP framework

3. ✅ ALWAYS review AI output — it's a starting point, 
   not production-ready code

4. ✅ NEVER share patient data, credentials, or proprietary 
   algorithms — 5 rules, no exceptions

5. ✅ This is a SKILL that makes you more valuable — 
   whether you're here or anywhere else"
```

### Resource Distribution (2 min)

Share these resources (email/Slack/shared drive):

```
📁 Antigravity Resources (shared folder):
├── antigravity_developer_guide.md      (General guide)
├── antigravity_prompting_guide.md      (Prompting techniques)
├── angular17_antigravity_guide.md      (Frontend-specific)
├── springboot_antigravity_guide.md     (Backend-specific)
├── documentation_guide.md             (Documentation practices)
├── prompt_cheat_sheet.pdf             (1-page printable)
└── security_rules_poster.pdf          (Print for every desk)
```

### Call to Action (2 min)

```
"Here's what I want from each of you this week:

1. Use Antigravity for AT LEAST 1 bug fix or test this week
2. If you get stuck, reach out to me — I'm your go-to person
3. Share your wins in the [#antigravity-tips] Slack channel

I'll be doing follow-up 1:1 drop-ins with each team next week 
to help with specific use cases."
```

### Q&A (3 min)

Keep it brief. If a question is deeply technical, say:
> *"Great question — let me address that with you after the session so we don't hold everyone up."*

---

## 10. Handling Difficult Situations

### "AI is going to replace us"

> *"I get that concern. Here's the reality: AI doesn't replace developers. Developers who use AI replace developers who don't. This tool makes you MORE valuable, not less. The developer who fixes 10 bugs a day with AI is more valuable than the one who fixes 3 without it."*

### "I'm too busy for this training"

> *"I hear you — we're all under sprint pressure. That's exactly WHY I'm showing you this. If this saves you 1 hour today on that bug you're stuck on, then this session has already paid for itself."*

### "I tried AI before, it gives wrong answers"

> *"You're right — it does sometimes. That's why I'm teaching you HOW to prompt it correctly. Bad prompt = bad answer. Good prompt = useful answer. Let me show you the difference."*  
> (Demonstrate with a bad prompt vs. a CRISP prompt)

### "This doesn't work with our codebase / domain"

> *"Let me show you right now. Give me a file from your current task."*  
> (This is bold but powerful — if you can help them live, you win the room)

### "I don't need AI, I'm fast enough"

> *"That's great — and I respect your skill. Think of this as an extra gear. Lewis Hamilton is already fast, but he still uses the best car. This is just a better tool in your toolkit."*

### Outsourced Team Members Not Engaged

> *"For those of you who joined this project recently and are still learning the codebase — this is especially for you. Ask Antigravity to explain any file or method and you'll understand it in 2 minutes instead of 20."*

### Live Demo Fails

- **Stay calm.** Don't panic or over-apologize
- Say: *"Live demos are unpredictable — let me show you the backup I prepared"*
- Switch to your screen recording or prepared screenshots
- Move on quickly

---

## 11. Post-Session Follow-Up Plan

The session is only **20% of the impact**. The follow-up is **80%**.

### Week 1: Immediate Follow-Up

| Day              | Action                                                     | Format           |
| ---------------- | ---------------------------------------------------------- | ---------------- |
| Day 1 (Same Day) | Send all resources via email/Slack                         | Email with links |
| Day 2            | Share a "Prompt of the Day" in team channel                | Slack message    |
| Day 3            | Do 10-minute "desk drop-ins" with 2-3 teams                | In-person help   |
| Day 4            | Share a "Before vs After" example from someone who used it | Slack message    |
| Day 5            | Quick poll: "Have you used Antigravity this week?"         | Slack poll       |

### Week 2-4: Build the Habit

| Activity                  | Frequency                      | Purpose                          |
| ------------------------- | ------------------------------ | -------------------------------- |
| **Prompt of the Day**     | Daily for 2 weeks, then weekly | Keeps it top-of-mind             |
| **Desk Drop-Ins**         | 2-3 teams per week             | Hands-on help, builds trust      |
| **"Win of the Week"**     | Weekly Slack post              | Social proof, celebrate adopters |
| **FAQ Document**          | Update weekly                  | Address common issues            |
| **Mini Session** (15 min) | Bi-weekly                      | Cover advanced tips              |
| **1:1 with Team Leads**   | Week 2                         | Get their buy-in as multipliers  |

### Month 2: Measure & Report

- Collect metrics (see Section 12)
- Present results to CTO
- Identify next areas to drive productivity

---

## 12. Measuring Impact — Prove Your Value

### What to Track

| Metric                         | How to Measure                                     | Target               |
| ------------------------------ | -------------------------------------------------- | -------------------- |
| **Adoption Rate**              | Survey: "Did you use Antigravity this week?"       | 70%+ by Week 4       |
| **Time Saved (Self-Reported)** | Quick poll: "How much time did AI save you today?" | 30+ min/day average  |
| **Bugs Fixed Per Sprint**      | Compare sprint velocity before vs after            | 15-20% increase      |
| **Test Coverage**              | SonarQube metrics                                  | 10%+ improvement     |
| **PR Review Feedback**         | Track AI-related PR comments                       | Decreasing over time |
| **Developer Satisfaction**     | Anonymous survey at Week 4                         | Positive trend       |

### How to Present to CTO

```
Subject: Antigravity Training Impact — 4-Week Report

1. ADOPTION
   - 35/50 developers actively using Antigravity (70%)
   - 8 developers using it daily (16% — champions)

2. PRODUCTIVITY
   - Self-reported: average 45 min/day saved per developer
   - Estimated team impact: ~25 hours/day saved across team
   - Bug closure rate: up 18% compared to pre-training sprint

3. QUALITY
   - Test coverage: improved from 52% to 61%
   - AI-generated tests caught 4 edge-case bugs before release

4. NEXT STEPS
   - Advanced session for top adopters
   - Integrate prompt templates into team wiki
   - Weekly "AI tip" in standup
```

---

## 13. Slide Deck Outline

If you need slides (keep them minimal — max 15 slides):

```
Slide 1:  Title — "Work Smarter: Antigravity for HMIS Developers"
Slide 2:  The moment — "What if you could fix bugs 3x faster?"
Slide 3:  What is Antigravity (1 sentence + screenshot)
Slide 4:  What it CAN do (5 bullet points)
Slide 5:  What it CANNOT do (manage expectations)
Slide 6:  LIVE DEMO → (Switch to IDE - WOW demo)
Slide 7:  Use Case 1 — Bug Fixing (screenshot of result)
Slide 8:  Use Case 2 — Writing Tests (screenshot of result)
Slide 9:  Use Case 3 — Understanding Code (screenshot)
Slide 10: Use Case 4 — Refactoring (screenshot)
Slide 11: CRISP Framework — How to write prompts
Slide 12: ⚠️ Security — 5 Rules (bold, unmissable)
Slide 13: HANDS-ON → (Switch to workshop)
Slide 14: Resources & Cheat Sheet (QR code to shared folder)
Slide 15: "Your challenge: Use it for 1 task this week"
```

> [!TIP]
> **Design rule:** Maximum 5 bullet points per slide. Big fonts. More screenshots than text. Slides support YOU — they don't replace you.

---

## 14. Speaker Notes & Talking Points

### Energy & Delivery

| Principle              | How                                                                        |
| ---------------------- | -------------------------------------------------------------------------- |
| **Start strong**       | First 60 seconds sets the tone — be energetic, confident                   |
| **Eye contact**        | Look at people, not the screen (you know the content)                      |
| **Move around**        | Don't stand at the podium — walk, engage, point at screens                 |
| **Use names**          | "Rahul, can you share your screen for a moment?" — makes it personal       |
| **Pause often**        | After making a key point, pause 3 seconds — let it land                    |
| **Read the room**      | If eyes are glazing, skip to the demo or hands-on immediately              |
| **Be honest**          | If AI gives a wrong answer during demo: "See? This is why we REVIEW"       |
| **Show vulnerability** | "I also got terrible AI answers when I started — then I learned prompting" |

### Language Tips

| Instead of...                      | Say...                                                                  |
| ---------------------------------- | ----------------------------------------------------------------------- |
| "You should use AI"                | "Here's something that might save you an hour today"                    |
| "This is mandatory"                | "This is a skill that makes you stand out"                              |
| "AI is better than manual coding"  | "AI handles the boring parts so you can focus on the interesting logic" |
| "Everyone must follow these rules" | "These 5 rules protect you AND the company"                             |
| "You're doing it wrong"            | "Here's a way to get better results from the same prompt"               |
| "Any questions?" (at the end)      | "What's ONE thing you're going to try this week?"                       |

---

## 15. Resource Kit for Developers

### What to Distribute After the Session

**1. Prompt Cheat Sheet (1 Page — Printable)**

```
CHEAT SHEET: Antigravity Prompts for HMIS Developers

BUG FIX:
"Spring Boot 3.2, Java 17. Error: [sanitized trace]. 
Context: [what happened]. Tried: [your attempts]. Fix it."

WRITE TEST:
"Generate JUnit 5 + Mockito tests for [method name]. 
Behavior: [describe]. Include: happy path, error cases, edge cases."

UNDERSTAND CODE:
"Explain what this method does, what business rule it implements, 
and what could go wrong: [paste sanitized code]"

REFACTOR:
"Refactor this to reduce complexity. Apply [pattern]. 
Keep tests passing. Show before/after."

⚠️ SECURITY RULES:
❌ NEVER paste: patient data, credentials, prod configs, proprietary algorithms
✅ ALWAYS: sanitize code, use placeholders, review AI output, run tests
```

**2. Shared Drive / Repository Structure**

```
📁 team-resources/antigravity/
├── guides/
│   ├── developer_guide.md
│   ├── prompting_guide.md
│   ├── angular17_guide.md
│   ├── springboot_guide.md
│   └── documentation_guide.md
├── cheat-sheets/
│   ├── prompt_cheat_sheet.pdf
│   └── security_rules.pdf
├── examples/
│   ├── bug-fix-prompts.md
│   ├── test-generation-prompts.md
│   └── refactoring-prompts.md
└── faq.md
```

**3. Slack Channel Setup**

Create **#antigravity-tips** channel:
- Post daily prompts for first 2 weeks
- Developers share wins
- You answer questions
- Pin the cheat sheet and security rules

---

## One Final Note — Your Role Going Forward

Your CTO said: *"Don't code. Add value."*

This session is your **proof of concept**. If you:

1. ✅ Train developers effectively
2. ✅ Follow up consistently
3. ✅ Measure and report impact
4. ✅ Help the team deliver faster with fewer bugs

...you've proven that **one person driving productivity** is more valuable than one person writing code. That's leadership. That's what CTOs look for.

You're not just teaching a tool. You're **changing how the team works**. Own it.

---

> *"Tell me and I forget. Teach me and I remember. Involve me and I learn."*  
> — Benjamin Franklin

---

*Good luck with the session. You've got this.* 🚀
