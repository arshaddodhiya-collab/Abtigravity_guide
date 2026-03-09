# 📄 Documentation in Development — The Complete Guide
## Why Docs Matter, When to Write Them & How to Do It Right

> **Prepared for:** Development Team — HMIS Product Division  
> **Context:** Product-Based Company · Healthcare Domain  
> **Tech Stack:** Java Spring Boot · Angular · PostgreSQL  
> **Date:** March 2026

---

## Table of Contents

1. [Why Documentation Matters](#1-why-documentation-matters)
2. [The Real Cost of Missing Documentation](#2-the-real-cost-of-missing-documentation)
3. [Why It Matters Even MORE in HMIS / Healthcare](#3-why-it-matters-even-more-in-hmis--healthcare)
4. [Types of Documentation Every Developer Must Know](#4-types-of-documentation-every-developer-must-know)
5. [When to Write Documentation](#5-when-to-write-documentation)
6. [How to Write Good Documentation](#6-how-to-write-good-documentation)
7. [Documentation Standards for Our HMIS Product](#7-documentation-standards-for-our-hmis-product)
8. [Templates & Examples](#8-templates--examples)
9. [Documentation in the Developer Workflow](#9-documentation-in-the-developer-workflow)
10. [Tools & Automation](#10-tools--automation)
11. [Common Excuses & Why They Don't Hold Up](#11-common-excuses--why-they-dont-hold-up)
12. [Documentation Culture — Making It Stick](#12-documentation-culture--making-it-stick)

---

## 1. Why Documentation Matters

### The Hard Truth

> *"Code tells you **how**. Documentation tells you **why**."*

Every developer has experienced this: you open a 3-year-old module, see a complex piece of logic, and ask — *"Why is this written this way? What business rule does this serve? What happens if I change it?"*

Without documentation, you're left guessing. In an HMIS system, guessing can mean **wrong billing calculations, incorrect drug interactions, or broken patient workflows**.

### Documentation Is Not Optional — It's a Product Feature

| With Documentation                        | Without Documentation                             |
| ----------------------------------------- | ------------------------------------------------- |
| New developer productive in **1-2 weeks** | New developer struggles for **4-8 weeks**         |
| Bug fixes take **hours**                  | Bug fixes take **days** (tracing unknown logic)   |
| Feature changes are **predictable**       | Feature changes break **unexpected things**       |
| Knowledge survives **attrition**          | Knowledge leaves **with the developer**           |
| Compliance audits pass **smoothly**       | Compliance audits become **stressful firefights** |
| Client implementations are **consistent** | Every deployment is a **from-scratch effort**     |

### The Numbers

- Developers spend **~58% of their time understanding existing code**, not writing new code *(IEEE Study)*
- Poor documentation increases onboarding time by **3-5x**
- In product companies, **every undocumented decision becomes technical debt**
- HMIS compliance audits (HIPAA, NABH, HL7) **require documented processes** — not just working code

---

## 2. The Real Cost of Missing Documentation

### Scenario 1: The Developer Who Left

> Rajesh built the entire billing engine single-handedly over 2 years. He knew every edge case — waiver logic, insurance claim rules, GST exceptions, multi-payer splits. Then Rajesh left. No documentation. The team spent **6 months** reverse-engineering his code. Three production bugs slipped through because nobody understood the waiver priority logic.

**Cost:** 6 months × team of 3 = **18 person-months of lost productivity**

### Scenario 2: The "Quick Change" That Broke Everything

> A developer was asked to modify the appointment scheduling logic to add a 15-minute buffer between appointments. Simple, right? But the scheduling logic was undocumented and had hidden dependencies on the OPD queue, doctor allocation, and billing pre-authorization. The "quick change" broke billing for 2 days.

**Cost:** 2 days of downtime for a hospital client = **reputation damage + SLA penalty**

### Scenario 3: The Compliance Audit

> During a compliance audit, the auditor asked: *"How does your system ensure that only authorized personnel can access patient records? Show me the access control documentation."* The team scrambled to create documentation retroactively from code. The audit was delayed by 3 weeks.

**Cost:** Delayed certification = **delayed deal closures**

### The Message Is Clear

> [!CAUTION]
> In a product company, **undocumented code is a ticking time bomb**. It doesn't explode today — it explodes when someone leaves, when a client asks "why," or when an auditor says "show me."

---

## 3. Why It Matters Even MORE in HMIS / Healthcare

### Regulatory & Compliance Requirements

Healthcare software is **regulated**. Unlike a social media app, your code decisions can affect:

- **Patient safety** — wrong dosage calculations, drug allergy misses
- **Legal liability** — incorrect medical records, data breaches
- **Financial accuracy** — billing errors, insurance claim rejections
- **Regulatory compliance** — HIPAA, NABH, HL7/FHIR, ABDM

| Compliance Standard | Documentation Required                                                         |
| ------------------- | ------------------------------------------------------------------------------ |
| **HIPAA**           | Access control policies, audit trail documentation, data handling procedures   |
| **NABH**            | System workflow documentation, user role definitions, SOP documents            |
| **HL7/FHIR**        | Integration specifications, message format docs, data mapping guides           |
| **ABDM**            | API integration docs, consent flow documentation, data exchange specs          |
| **ISO 27001**       | Information security procedures, risk assessment docs, incident response plans |

### Healthcare-Specific Documentation Needs

| Area                       | Why Documentation Is Critical                                                                     |
| -------------------------- | ------------------------------------------------------------------------------------------------- |
| **Clinical Workflows**     | Doctors and nurses use the system differently — their flows must be documented to avoid ambiguity |
| **Drug Interaction Rules** | The logic behind drug-drug interaction alerts MUST be documented with clinical references         |
| **Billing & Insurance**    | Multi-payer logic, waiver rules, GST calculations — all require business rule documentation       |
| **Lab Integration**        | HL7 message mappings, LIS/LIMS interfaces — need integration specs                                |
| **Consent Management**     | Patient consent workflows must be documented for ABDM and HIPAA compliance                        |
| **Audit Trails**           | What is logged, when, and why — required for compliance and forensic analysis                     |

> [!IMPORTANT]
> In healthcare, documentation isn't just "nice to have" — it's **legally required**. If you can't document how your system handles patient data, you can't certify it.

---

## 4. Types of Documentation Every Developer Must Know

### Overview Map

```
┌─────────────────────────────────────────────────────────────┐
│                 DOCUMENTATION TYPES                         │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  📐 ARCHITECTURE DOCS     📝 CODE DOCUMENTATION            │
│  • System architecture    • Inline comments                 │
│  • Module design docs     • Javadoc / JSDoc                 │
│  • Data flow diagrams     • README files                    │
│  • ER diagrams            • CHANGELOG                       │
│                                                             │
│  📘 API DOCUMENTATION      🧪 TESTING DOCUMENTATION         │
│  • OpenAPI/Swagger specs  • Test plan documents             │
│  • Integration guides     • Test case specifications        │
│  • Postman collections    • QA handoff documents            │
│  • Webhook docs           • Coverage reports                │
│                                                             │
│  📋 PROCESS DOCUMENTATION  🏥 DOMAIN DOCUMENTATION          │
│  • ADRs (Architecture     • Business rule specs             │
│    Decision Records)      • Clinical workflow docs          │
│  • Sprint handoff docs    • Billing rule documentation      │
│  • Deployment runbooks    • Compliance matrices             │
│  • Incident playbooks     • User role & permission maps     │
│                                                             │
│  📦 PRODUCT DOCUMENTATION  🔧 OPERATIONAL DOCS              │
│  • Release notes          • Deployment guides               │
│  • Feature specs          • Monitoring & alerting setup     │
│  • Migration guides       • Troubleshooting runbooks        │
│  • Configuration guides   • Infrastructure docs             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### The 4 Layers — From Code to Customer

| Layer                      | Audience                               | Examples                                                  |
| -------------------------- | -------------------------------------- | --------------------------------------------------------- |
| **Layer 1: Code-Level**    | Developers on the same team            | Inline comments, Javadoc, README, method docs             |
| **Layer 2: System-Level**  | All developers, architects             | Architecture docs, API specs, data models, ADRs           |
| **Layer 3: Process-Level** | Dev team + QA + DevOps                 | Deployment runbooks, test plans, incident playbooks       |
| **Layer 4: Product-Level** | Implementation team, clients, auditors | User guides, feature docs, compliance docs, release notes |

---

## 5. When to Write Documentation

### The Golden Rule

> **Document at the moment of maximum context** — when you understand the *why* best.

### Documentation Trigger Points

```
┌────────────────────────────────────────────────────────────────────┐
│                    DEVELOPMENT LIFECYCLE                           │
│                                                                    │
│  📝 PLANNING          → Write: PRD, Technical Spec, ADR           │
│     ↓                                                              │
│  🔨 DEVELOPMENT       → Write: Code comments, Javadoc, README     │
│     ↓                                                              │
│  🔗 INTEGRATION       → Write: API docs, Integration specs        │
│     ↓                                                              │
│  🧪 TESTING           → Write: Test plans, QA handoff doc         │
│     ↓                                                              │
│  📦 PR / CODE REVIEW  → Write: PR description, Decision rationale │
│     ↓                                                              │
│  🚀 RELEASE           → Write: Release notes, Migration guide     │
│     ↓                                                              │
│  🏥 DEPLOYMENT        → Write: Deployment runbook, Config guide   │
│     ↓                                                              │
│  🐛 POST-INCIDENT     → Write: Incident report, Root cause doc    │
│     ↓                                                              │
│  🔄 FEATURE CHANGE    → Update: All affected docs above           │
└────────────────────────────────────────────────────────────────────┘
```

### Specific "When" Triggers

| Trigger                              | What to Document              | Why Now                                       |
| ------------------------------------ | ----------------------------- | --------------------------------------------- |
| **New module/feature**               | Architecture doc + API spec   | You understand the full picture during design |
| **Complex business rule**            | Business rule specification   | You have the requirements fresh in mind       |
| **Non-obvious code decision**        | Inline comment with "why"     | You'll forget the reason in 2 weeks           |
| **API creation/change**              | Swagger annotations + Postman | Consumers need this immediately               |
| **Bug fix for edge case**            | Comment explaining the fix    | Future devs will wonder why the code exists   |
| **Configuration addition**           | Config doc update             | Deployment will fail without context          |
| **Integration with external system** | Integration spec              | The mapping and flow are complex              |
| **Production incident**              | Post-mortem document          | Prevents repeat incidents                     |
| **Developer leaving the team**       | Knowledge transfer doc        | Last chance to capture expertise              |
| **Major refactoring**                | ADR + migration notes         | Team needs to understand what changed and why |
| **Client customization**             | Customization log             | Support team needs this for troubleshooting   |

### The "Tomorrow Test"

Before closing your IDE, ask yourself:

> *"If a new developer opens this code tomorrow with zero context, will they understand:*  
> *1. What does this do?*  
> *2. Why was it done this way?*  
> *3. What are the edge cases?*  
> *4. What depends on this?"*

If the answer is **no** to any of those — document it now.

---

## 6. How to Write Good Documentation

### The 5 Principles of Great Documentation

#### Principle 1: Write for the Reader, Not Yourself

```
❌ "Fixed the thing using the pattern we discussed"
✅ "Applied the Strategy pattern to the billing discount 
   calculator to support adding new discount types (e.g., 
   senior citizen, government scheme) without modifying 
   existing code. See ADR-047 for the design decision."
```

#### Principle 2: The Why > The What > The How

```
❌ Comment: "Adds 15 minutes to appointment time"
   (Tells WHAT — but we can read the code for that)

✅ Comment: "Buffer of 15 min is added between appointments 
   to allow for sanitization of OPD rooms as per NABH 
   infection control guidelines (Standard I.3.2)"
   (Tells WHY — something the code can never tell you)
```

**Priority of documentation content:**
1. **WHY** — the business reason, the design decision, the constraint
2. **WHAT** — the behavior, the expected outcomes, the edge cases
3. **HOW** — the implementation detail (only when non-obvious)

#### Principle 3: Keep It Close to the Code

| Distance from Code              | Likelihood of Being Updated             |
| ------------------------------- | --------------------------------------- |
| Inline comment                  | ✅ Very high — devs see it while editing |
| Javadoc on the method           | ✅ High — visible in IDE                 |
| README in the module folder     | 🟡 Medium — visible in git               |
| Wiki page                       | 🟡 Low-Medium — separate from workflow   |
| Confluence page nobody links to | 🔴 Very low — forgotten                  |
| Word document on a shared drive | 🔴 Practically zero                      |

> [!TIP]
> **The closer documentation is to the code, the more likely it is to stay updated.** Prefer Javadoc, README.md in module folders, and Swagger annotations over external wikis.

#### Principle 4: Use Diagrams Over Paragraphs

People understand visuals faster than text. Use diagrams for:

- **Architecture overviews** — C4 model diagrams
- **Data flows** — sequence diagrams for clinical workflows
- **Entity relationships** — ER diagrams for database modules
- **State machines** — patient journey states, appointment lifecycle
- **Decision trees** — billing rule logic, triage flows

**Tools to use:**
- **Mermaid** (in Markdown files — renders in GitHub/GitLab)
- **PlantUML** (integrates with IntelliJ)
- **draw.io** (free, exports to PNG/SVG)
- **dbdiagram.io** (for ER diagrams)

#### Principle 5: Maintain a Living Document

Documentation is not a one-time event. Build updates into your workflow:

- **PR checklist includes:** "Did you update related documentation?"
- **Sprint planning includes:** documentation tasks with story points
- **Quarterly reviews:** audit documentation freshness
- **Definition of Done includes:** documentation complete

---

## 7. Documentation Standards for Our HMIS Product

### 7.1 Code-Level Standards

#### Inline Comments — When and How

**DO comment:**
- Business rules that aren't obvious from the code
- Workarounds and hacks (with ticket reference)
- Regulatory or compliance reasons for specific logic
- Non-obvious performance decisions
- External system dependencies and assumptions

**DON'T comment:**
- What the code literally does (redundant)
- Every single line
- Commented-out code (delete it — git has history)

```java
// ❌ BAD — states the obvious
// Get patient by ID
Patient patient = patientRepository.findById(id);

// ✅ GOOD — explains the WHY
// Prefetching appointments with JOIN FETCH to avoid N+1 queries
// on the patient list screen where appointments count is displayed.
// See PERF-1242 for the original performance issue.
@Query("SELECT p FROM Patient p LEFT JOIN FETCH p.appointments WHERE p.id = :id")
Patient findWithAppointments(@Param("id") Long id);

// ✅ GOOD — documents a business rule
// Discharge summary must be finalized within 24 hours of discharge
// as per NABH Standard A.5.1. After 24 hours, the summary is 
// auto-locked and requires HOD approval to modify.
if (hoursSinceDischarge > 24) {
    summary.setLocked(true);
    summary.setRequiresApproval(true);
}
```

#### Javadoc Standards

Every public class and method MUST have Javadoc:

```java
/**
 * Calculates the total billable amount for an encounter.
 * 
 * <p>Applies the following business rules in order:
 * <ol>
 *   <li>Base charges from the tariff master for the facility</li>
 *   <li>Category-based discount (BPL, Senior Citizen, Staff)</li>
 *   <li>Scheme/Insurance coverage deduction</li>
 *   <li>GST calculation based on service category (SAC codes)</li>
 *   <li>Round-off to nearest rupee (as per company policy)</li>
 * </ol>
 * 
 * <p><b>Regulatory note:</b> GST exemption applies to healthcare
 * services under SAC 9993 as per CGST notification 12/2017.
 * 
 * @param encounterId the encounter to calculate billing for
 * @param applyDiscounts whether to apply applicable discounts
 * @return the calculated bill with itemized breakdown
 * @throws EncounterNotFoundException if the encounter does not exist
 * @throws BillingLockedException if the bill is already finalized
 * @see TariffMaster
 * @see DiscountPolicy
 * @since 3.4.0
 */
public BillSummary calculateBill(Long encounterId, boolean applyDiscounts) {
    // ...
}
```

#### README Standards for Each Module

Every module folder should have a `README.md`:

```
module-name/
├── README.md          ← Module documentation
├── src/
├── pom.xml
└── ...
```

README should include:
1. **Purpose** — what this module does (2-3 sentences)
2. **Key Components** — main classes/services and their responsibilities
3. **Business Rules** — key domain rules implemented here
4. **Dependencies** — what this module depends on and what depends on it
5. **Configuration** — module-specific configuration properties
6. **API Endpoints** — if applicable, list the endpoints
7. **How to Test** — how to run tests for this module
8. **Known Issues** — documented quirks or limitations

### 7.2 API Documentation Standards

Every REST API must have:

| Item                        | Format                                 | Tool                       |
| --------------------------- | -------------------------------------- | -------------------------- |
| Endpoint specification      | OpenAPI 3.0 YAML/JSON                  | Springdoc / Swagger        |
| Request/Response examples   | Annotated DTOs with `@Schema`          | Swagger UI                 |
| Authentication requirements | Documented per endpoint                | Swagger security schemes   |
| Error codes & messages      | Standardized error response format     | `@ApiResponse` annotations |
| Postman collection          | Importable `.json` collection          | Postman export             |
| Integration guide           | Step-by-step for third-party consumers | Markdown document          |

### 7.3 Business Rule Documentation

For every complex business rule in the HMIS, maintain a specification:

```markdown
## BR-042: Appointment Slot Availability

**Module:** Appointment Scheduling  
**Last Updated:** 2026-02-15  
**Owner:** Dr. Mehta / Dev: Priya  

### Rule Description
A doctor's appointment slot is considered available only when ALL 
of the following conditions are met:

### Conditions
1. The slot falls within the doctor's defined schedule for that day
2. No existing appointment exists for that slot  
   (status != CANCELLED)
3. The doctor has not marked leave for that date
4. The slot is at least 30 minutes in the future (configurable)
5. The buffer time (15 min) after the previous appointment has passed
6. The slot does not overlap with any blocked/reserved time 
   (e.g., surgery blocks, break time)

### Edge Cases
- Walk-in patients override condition 4 (front-desk role required)
- Emergency slots (marked with isEmergency=true) override conditions 
  4 and 5
- Telemedicine slots have a separate availability pool

### Regulatory Reference
- NABH Standard A.2.1 — Outpatient scheduling guidelines

### Implementation Reference
- Service: `AppointmentSlotService.checkAvailability()`
- Config: `appointment.buffer-minutes=15`
- Config: `appointment.advance-booking-minutes=30`
```

### 7.4 Architecture Decision Records (ADRs)

For every significant technical decision, create an ADR:

```markdown
# ADR-015: Use Event-Driven Architecture for Lab-Billing Integration

## Status: Accepted

## Date: 2026-01-20

## Context
When a lab test result is finalized, the billing module needs to 
be notified to update the invoice. Previously, this was a direct 
synchronous REST call from Lab module to Billing module.

Problems with synchronous approach:
- Tight coupling between modules
- Billing downtime blocks lab result finalization
- No retry mechanism for failed notifications

## Decision
We will use Apache Kafka for asynchronous event-driven communication 
between Lab and Billing modules.

- Lab module publishes `LabResultFinalizedEvent` to Kafka topic
- Billing module consumes the event and creates/updates invoice
- Dead letter queue for failed processing
- Idempotent consumer to handle duplicate events

## Consequences

### Positive
- Modules are decoupled — can be deployed independently
- Lab can finalize results even if Billing is down
- Built-in retry and dead letter handling
- Audit trail of all events

### Negative
- Added infrastructure complexity (Kafka cluster)
- Eventual consistency (billing update is not instant)
- Team needs Kafka expertise (training required)
- Additional monitoring for consumer lag

## Alternatives Considered
1. **RabbitMQ** — Rejected: Kafka better suits our event 
   streaming and replay needs
2. **Spring Events (in-process)** — Rejected: doesn't work 
   across microservice boundaries
3. **Scheduled polling** — Rejected: adds latency, wastes resources
```

---

## 8. Templates & Examples

### 8.1 Module README Template

```markdown
# [Module Name]

## Purpose
[2-3 sentence description of what this module does and why it exists]

## Architecture
[Link to architecture diagram or embed Mermaid diagram]

## Key Components

| Component       | Type       | Responsibility               |
| --------------- | ---------- | ---------------------------- |
| `XxxService`    | Service    | [Core business logic for...] |
| `XxxController` | Controller | [REST API for...]            |
| `XxxRepository` | Repository | [Data access for...]         |
| `XxxMapper`     | Mapper     | [Entity ↔ DTO mapping]       |

## Business Rules
- **BR-XXX:** [Brief description] → see `docs/business-rules/BR-XXX.md`
- **BR-YYY:** [Brief description] → see `docs/business-rules/BR-YYY.md`

## API Endpoints
| Method | Path               | Description          | Roles         |
| ------ | ------------------ | -------------------- | ------------- |
| GET    | `/api/v1/xxx`      | List with pagination | ALL           |
| POST   | `/api/v1/xxx`      | Create new record    | ADMIN, DOCTOR |
| PUT    | `/api/v1/xxx/{id}` | Update record        | ADMIN, DOCTOR |
| DELETE | `/api/v1/xxx/{id}` | Soft delete          | ADMIN         |

## Configuration
| Property              | Default | Description              |
| --------------------- | ------- | ------------------------ |
| `xxx.feature.enabled` | `true`  | Enable/disable feature X |
| `xxx.cache.ttl`       | `300`   | Cache TTL in seconds     |

## Dependencies
- **Depends on:** [Module A] (for X), [Module B] (for Y)
- **Depended by:** [Module C], [Module D]

## Testing
```bash
mvn test -pl module-name
mvn verify -pl module-name  # integration tests
```

## Known Issues
- [JIRA-123] Description of known limitation
```

### 8.2 PR Description Template

```markdown
## Summary
[1-2 sentence description of what this PR does]

## JIRA Ticket
[HMIS-XXXX](link-to-jira)

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Refactoring
- [ ] Documentation
- [ ] Configuration change

## Changes Made
- [File/Module] — [What changed and why]
- [File/Module] — [What changed and why]

## Business Rule Impact
- [ ] No business rules affected
- [ ] Modified: [BR-XXX — describe change]
- [ ] New: [BR-YYY — describe rule]

## Testing Done
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] Manual testing completed
- [ ] Test cases: [describe scenarios tested]

## Documentation Updated
- [ ] Javadoc updated
- [ ] README updated
- [ ] API docs (Swagger) updated
- [ ] Business rule doc updated
- [ ] No documentation changes needed

## Deployment Notes
- [ ] No special deployment steps
- [ ] Database migration required
- [ ] Configuration change required: [describe]
- [ ] Feature flag: [flag name] = [value]

## Screenshots (if UI change)
[Attach screenshots]
```

### 8.3 Release Notes Template

```markdown
# Release v3.5.0 — March 2026

## 🆕 New Features

### Teleconsultation Module
- Video consultation booking and scheduling
- Prescription generation during teleconsultation
- Automatic consultation recording consent flow
- Integration with payment gateway for online fees

### Lab Module Enhancements
- Batch result entry for common panels
- Auto-critical value alerts to treating doctor

## 🐛 Bug Fixes
- **HMIS-3421:** Bill amount mismatch when discount applied after 
  partial payment
- **HMIS-3398:** Duplicate appointment slots for concurrent bookings
- **HMIS-3445:** MLC report not generating for emergency patients

## ⚠️ Breaking Changes
- API `/api/v1/patients` response now wrapped in pagination object
  → Update Angular service calls (see migration guide)
- Minimum Java version upgraded from 11 to 17

## 🔧 Configuration Changes
| Property                     | Old Value | New Value | Action Required            |
| ---------------------------- | --------- | --------- | -------------------------- |
| `teleconsult.enabled`        | N/A       | `false`   | Set to `true` to enable    |
| `lab.critical.alert.enabled` | N/A       | `true`    | Configure alert thresholds |

## 📦 Migration Steps
1. Run Flyway migration: `V3.5.0__teleconsult_tables.sql`
2. Update `application.yml` with new properties
3. Restart application with `--spring.profiles.active=prod`

## 📋 Known Issues
- Teleconsultation recording does not work on Safari 16.x
  (WebRTC compatibility — fix planned for v3.5.1)
```

### 8.4 Incident Post-Mortem Template

```markdown
# Incident Post-Mortem: [Title]

**Date:** [When it happened]  
**Duration:** [How long it lasted]  
**Severity:** [P1/P2/P3/P4]  
**Affected:** [Which clients/modules]  
**Author:** [Who wrote this report]

## Summary
[2-3 sentence description of what happened]

## Timeline (IST)
| Time  | Event                                                |
| ----- | ---------------------------------------------------- |
| 10:30 | Alert triggered — billing API returning 500          |
| 10:35 | On-call engineer acknowledged                        |
| 10:45 | Root cause identified — DB connection pool exhausted |
| 10:50 | HikariCP max pool increased from 10 to 30            |
| 11:00 | Service restored, monitoring confirmed               |

## Root Cause
[Technical explanation of what went wrong]

## Impact
- [X] patients affected
- [X] bills delayed
- [X] minutes of downtime

## Resolution
[What was done to fix it]

## Action Items
| Action                             | Owner  | Deadline | Status  |
| ---------------------------------- | ------ | -------- | ------- |
| Add connection pool monitoring     | DevOps | March 15 | Pending |
| Set up PagerDuty for pool alerts   | SRE    | March 12 | Pending |
| Load test with 2x expected traffic | QA     | March 20 | Pending |

## Lessons Learned
- [What we learned and how to prevent recurrence]
```

---

## 9. Documentation in the Developer Workflow

### Integrating Docs into Daily Work

```
┌──────────────────────────────────────────────────────────┐
│              SPRINT WORKFLOW WITH DOCS                    │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  📋 SPRINT PLANNING                                      │
│     • Story includes documentation acceptance criteria   │
│     • Complex stories get a documentation sub-task       │
│     • Estimate includes documentation time               │
│                                                          │
│  💻 DEVELOPMENT                                          │
│     • Write code + Javadoc together (not after)          │
│     • Update README if module behavior changes           │
│     • Add Swagger annotations while building APIs        │
│     • Document business rules as you implement them      │
│                                                          │
│  🔍 CODE REVIEW                                          │
│     • Reviewer checks: "Is this documented?"             │
│     • PR template enforces documentation checklist       │
│     • Missing docs = PR revision requested               │
│                                                          │
│  🧪 TESTING                                              │
│     • Test cases reference business rule docs            │
│     • QA handoff includes documentation review           │
│                                                          │
│  🚀 RELEASE                                              │
│     • Release notes written before deployment            │
│     • Migration guide reviewed by DevOps                 │
│     • Client-facing docs updated                         │
│                                                          │
│  📊 RETROSPECTIVE                                        │
│     • "Did documentation help or hurt us this sprint?"   │
│     • Identify documentation gaps                        │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

### Definition of Done — Updated

A story is **not done** until:

- [ ] Code is written and reviewed
- [ ] Unit and integration tests pass
- [ ] **Javadoc/JSDoc is written for public APIs**
- [ ] **Swagger annotations are added for REST endpoints**
- [ ] **README is updated if module behavior changed**
- [ ] **Business rule doc is created/updated if applicable**
- [ ] **PR description follows the template**
- [ ] **Release notes entry is drafted**
- [ ] QA sign-off received

---

## 10. Tools & Automation

### Documentation Tools for Our Stack

| Purpose                   | Tool                                  | Integration                     |
| ------------------------- | ------------------------------------- | ------------------------------- |
| **Java Code Docs**        | Javadoc                               | Built into JDK, IDE preview     |
| **API Docs**              | Springdoc OpenAPI                     | Auto-generates from annotations |
| **Angular Docs**          | Compodoc                              | Auto-generates from components  |
| **Diagrams in Markdown**  | Mermaid.js                            | Renders in GitHub/GitLab        |
| **ER Diagrams**           | dbdiagram.io / SchemaSpy              | Reverse-engineers from DB       |
| **Architecture Diagrams** | draw.io / PlantUML                    | IntelliJ plugin available       |
| **Centralized Docs**      | Confluence / Notion / GitBook         | Linked to git repos             |
| **API Testing & Docs**    | Postman / Bruno                       | Export as collection            |
| **Changelog**             | Conventional Commits + auto-changelog | Git hooks                       |

### Automating Documentation

**1. Swagger UI — Auto-Generated API Docs**
```java
// Add Springdoc dependency and annotations → auto-generates interactive docs
// Access at: http://localhost:8080/swagger-ui.html
```

**2. Compodoc — Auto-Generated Angular Docs**
```bash
npx @compodoc/compodoc -p tsconfig.json -s
# Generates interactive component documentation
```

**3. Conventional Commits → Auto Changelog**
```
feat(billing): add multi-payer split support
fix(appointment): resolve concurrent booking race condition
docs(lab): update integration specification for LIS
```

**4. Pre-Commit Hooks — Documentation Enforcement**
```bash
# Reject commits with public methods missing Javadoc
# Reject PRs without description template
# Lint Markdown documentation files
```

**5. SchemaSpy — Auto-Generate DB Documentation**
```bash
# Connects to your database and generates HTML docs 
# with ER diagrams, table relationships, and column descriptions
```

---

## 11. Common Excuses & Why They Don't Hold Up

| Excuse                               | Reality                                                                                                                            |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| *"I don't have time to write docs"*  | You don't have time to NOT write docs. The time spent explaining, re-learning, and debugging undocumented code is 5x more          |
| *"Good code is self-documenting"*    | Code shows HOW. Only documentation explains WHY. Business rules, regulatory reasons, and design decisions can't live in code alone |
| *"The code changes too fast"*        | Then write docs close to the code (Javadoc, Swagger, READMEs) so they change together. External wikis go stale — inline docs don't |
| *"Nobody reads documentation"*       | Nobody reads BAD documentation. Good, concise, well-placed docs are used daily. If your docs aren't read, improve them             |
| *"We'll document it later"*          | "Later" never comes. You'll forget the context. Document at the moment of maximum understanding                                    |
| *"AI will generate docs for us"*     | AI can help draft docs, but only YOU know the WHY. AI doesn't know your business rules, compliance needs, or design trade-offs     |
| *"I'm the only one working on this"* | Until you go on leave, switch teams, or leave the company. The "bus factor" of undocumented code is 1                              |

---

## 12. Documentation Culture — Making It Stick

### For Individual Developers

1. **Adopt the 15-Minute Rule** — Spend the last 15 minutes of every task writing/updating docs
2. **Document while coding** — Write Javadoc before the implementation (like TDD for docs)
3. **Use templates** — Templates reduce the friction of starting
4. **Think of your future self** — You in 6 months is your biggest documentation consumer
5. **Make it a habit** — Like writing tests, documentation is a professional practice

### For Team Leads

1. **Include docs in Definition of Done** — no story is complete without docs
2. **Review docs in code reviews** — make it a checklist item
3. **Allocate story points for documentation** — don't treat it as "extra"
4. **Recognize good documentation** — call out well-documented PRs in retrospectives
5. **Run documentation sprints** — periodically dedicate time to doc debt

### For the Organization

1. **Set documentation standards** — this guide is a start
2. **Provide tools and training** — give teams the right tools
3. **Audit documentation quarterly** — identify gaps before auditors do
4. **Tie documentation to compliance** — make it a business requirement, not just engineering preference
5. **New hire feedback loop** — ask new joiners "what was hard to understand?" and fix those docs

### The Documentation Maturity Model

| Level                   | Description                                                                   | Your Target |
| ----------------------- | ----------------------------------------------------------------------------- | ----------- |
| **Level 0: Tribal**     | Knowledge lives in people's heads                                             | ❌           |
| **Level 1: Reactive**   | Docs written only when asked                                                  | ❌           |
| **Level 2: Basic**      | Key modules have READMEs, API has Swagger                                     | 🟡 Minimum   |
| **Level 3: Integrated** | Docs are part of Definition of Done, reviewed in PRs                          | ✅ Target    |
| **Level 4: Cultural**   | Team proactively finds and fills doc gaps, new hires are productive in Week 1 | 🌟 Goal      |

---

## Final Thought

> *"The palest ink is better than the best memory."*  
> — Chinese Proverb

In a healthcare product company, documentation isn't overhead — it's **infrastructure**. It protects patients, empowers developers, satisfies auditors, and ensures your product can outlive any individual on the team.

**Start today. Start small. But start.**

---

*This guide should be reviewed and updated quarterly. Track documentation improvements in sprint retrospectives.*
