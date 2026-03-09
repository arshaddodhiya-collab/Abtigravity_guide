# 🚀 Antigravity — Developer Training Guide
## Safe & Effective Use of AI Coding Assistant in HMIS Development

> **Prepared for:** Development Team — HMIS Product Division  
> **Audience:** Java Spring Boot & Angular Developers  
> **Classification:** Internal — Training Material  
> **Date:** March 2026

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Use Cases for Developers](#2-use-cases-for-developers)
3. [Safe Usage Guidelines ⚠️](#3-safe-usage-guidelines)
4. [Company-Level Best Practices](#4-company-level-best-practices)
5. [Developer Workflow with Antigravity](#5-developer-workflow-with-antigravity)
6. [Risks and Limitations](#6-risks-and-limitations)
7. [Recommended Prompting Techniques](#7-recommended-prompting-techniques)
8. [Realistic Examples](#8-realistic-examples)
9. [Conclusion](#9-conclusion)

---

## 1. Introduction

### 1.1 What is Antigravity?

Antigravity is an **AI-powered coding assistant** that integrates directly into your development environment. It leverages large language models to understand code, answer technical questions, generate snippets, debug issues, and accelerate your day-to-day development workflow.

Think of it as a highly knowledgeable **pair programmer** that is available 24/7 — but one that requires careful guidance, especially in security-sensitive environments like healthcare.

### 1.2 Why Developers Use AI Coding Tools

| Pain Point                     | How AI Helps                                         |
| ------------------------------ | ---------------------------------------------------- |
| Writing repetitive boilerplate | Generates DTOs, controllers, services in seconds     |
| Debugging cryptic errors       | Explains stack traces, suggests fixes                |
| Learning new APIs/frameworks   | Provides contextual examples and explanations        |
| Writing tests                  | Scaffolds unit and integration tests with edge cases |
| Documentation fatigue          | Generates Javadoc, README, API docs automatically    |
| Code reviews                   | Spots anti-patterns, suggests improvements           |

### 1.3 Productivity Benefits

- **30-50% faster** boilerplate and test code generation
- **Reduced context-switching** — get answers without leaving your IDE
- **Consistent code quality** — AI follows patterns you define
- **Faster onboarding** — new developers learn the stack faster with AI assistance
- **Focus on business logic** — let AI handle the mechanical parts

> [!IMPORTANT]
> AI tools are **amplifiers**, not replacements. They amplify both good and bad practices. The quality of output depends heavily on the quality of input and the developer's ability to review it critically.

---

## 2. Use Cases for Developers

### 2.1 Writing Boilerplate Code

AI excels at generating repetitive structural code, freeing you to focus on business logic.

**Examples:**
- JPA entity classes with annotations
- Spring Boot REST controller scaffolding
- Angular component/service/module boilerplate
- DTO and Mapper classes
- Configuration classes (`@Configuration`, `@Bean`)

```
Prompt: "Generate a Spring Boot REST controller for Patient entity 
with CRUD endpoints. Use ResponseEntity, proper HTTP status codes, 
and follow RESTful naming conventions."
```

### 2.2 Debugging and Error Analysis

Paste a stack trace or error message and ask for analysis. AI can:

- Identify the **root cause** of exceptions
- Suggest **configuration fixes** (e.g., missing beans, wrong properties)
- Explain **obscure framework errors** (Hibernate lazy loading, Angular change detection)
- Recommend **debugging strategies** step-by-step

```
Prompt: "I'm getting a LazyInitializationException when accessing 
patient.getAppointments() outside a transaction. Explain why this 
happens and give me 3 different solutions with trade-offs."
```

### 2.3 Writing Unit and Integration Tests

This is one of the **highest-value** use cases. AI can generate:

- **JUnit 5** test cases with `@ParameterizedTest`
- **Mockito** mock setups for service layers
- **MockMvc** tests for controller endpoints
- **Jasmine/Karma** tests for Angular components
- Edge cases and boundary conditions you might miss

```
Prompt: "Write JUnit 5 tests for a PatientService.findById() method. 
Include: happy path, patient not found (should throw ResourceNotFoundException), 
null ID input, and verify repository interaction using Mockito."
```

### 2.4 Code Refactoring

AI helps identify and apply refactoring patterns:

- Extracting methods from long functions
- Applying **design patterns** (Strategy, Builder, Factory)
- Converting legacy code to modern Java (streams, optionals, records)
- Improving Angular code (RxJS operators, reactive patterns)
- Reducing cyclomatic complexity

```
Prompt: "Refactor this method to reduce cyclomatic complexity. 
Extract validation logic into a separate validator class using 
the Strategy pattern. Keep the original method as a coordinator."
```

### 2.5 Documentation Generation

- Javadoc for classes and methods
- Swagger/OpenAPI annotations
- Angular component documentation
- README files and architecture decision records
- API endpoint documentation

```
Prompt: "Generate Javadoc for this service class. Include @param, 
@return, @throws annotations. Also add Swagger @Operation and 
@ApiResponse annotations for the controller methods."
```

### 2.6 Learning New Frameworks & Libraries

- Ask about **Spring Security** configurations
- Understand **Angular Signals** or **Standalone Components**
- Explore **RxJS** operator chains
- Learn **Hibernate** query optimization
- Understand **Docker/Kubernetes** configurations

```
Prompt: "Explain how Spring Security's filter chain works in 
Spring Boot 3.x. Show me how to configure JWT-based authentication 
with role-based access control for a REST API."
```

---

## 3. Safe Usage Guidelines ⚠️

> [!CAUTION]
> This is the **MOST CRITICAL** section. As an HMIS product company, we handle **Protected Health Information (PHI)**, proprietary business logic, and sensitive infrastructure details. Violating data security can lead to **regulatory penalties, data breaches, and loss of customer trust**.

### 3.1 What Code Should NEVER Be Shared with AI

🔴 **Absolute No-Go — Never paste these into any AI tool:**

| Category                     | Examples                                                                                             |
| ---------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Patient/PHI Data**         | Patient names, IDs, medical records, diagnoses, prescriptions, insurance details — even in test data |
| **API Keys & Secrets**       | AWS keys, database credentials, JWT secrets, OAuth client secrets, encryption keys                   |
| **Production Configs**       | `application-prod.yml`, production database URLs, server IPs, SSL certificates                       |
| **Proprietary Algorithms**   | Billing calculation engines, drug interaction checkers, clinical decision support logic              |
| **Security Implementations** | Authentication flows with real logic, encryption/decryption routines, access control matrices        |
| **Customer-Specific Code**   | Tenant-specific customizations, customer names, SLA details, deployment configs                      |
| **Internal Infrastructure**  | Network topologies, CI/CD pipeline secrets, internal domain names, VPN configurations                |

### 3.2 Handling Proprietary Business Logic

When you need AI help with business logic:

✅ **Do This:**
```
"I have a billing calculation that applies a discount based on 
patient category (A, B, C). Show me a design pattern to make 
this extensible for new categories."
```

❌ **Not This:**
```
"Here is our complete billing algorithm that calculates insurance 
claims using [actual proprietary formula]. Fix the bug on line 45."
```

**Guidelines:**
- **Abstract the problem** — describe the pattern, not the implementation
- **Use generic domain terms** — "entity," "category," "calculation" instead of specific business terms
- **Strip context** — remove variable names that reveal business intent
- **Ask about patterns** — "How should I design X?" instead of "Fix my proprietary X"

### 3.3 Handling Healthcare / Patient Data

As an HMIS company, we must comply with:

- **HIPAA** (Health Insurance Portability and Accountability Act)
- **HITECH** (Health Information Technology for Economic and Clinical Health Act)
- **Local data protection regulations**

**Rules for Developers:**

1. **Never paste real patient data** into any AI tool — not even "test" records that were copied from production
2. **Use synthetic data** — generate fake patient records using libraries like **JavaFaker** or **Mockaroo**
3. **Anonymize before sharing** — if you must share a data structure, replace all real values:
   ```java
   // ❌ NEVER
   Patient patient = new Patient("John Doe", "MRN-12345", "Diabetes Type 2");
   
   // ✅ SAFE
   Patient patient = new Patient("REDACTED", "MRN-XXXXX", "CONDITION_A");
   ```
4. **Database queries** — never share queries containing actual table names tied to sensitive modules if they reveal PHI schema design
5. **Log outputs** — never paste application logs that may contain patient info

### 3.4 Protecting API Keys, Secrets, and Credentials

- **Never paste** `.env` files, `application-prod.properties`, or any credential files
- **Audit your clipboard** before pasting — accidental credential exposure is the #1 risk
- **Use placeholders** when asking about configuration:
  ```yaml
  # ✅ SAFE
  spring:
    datasource:
      url: jdbc:postgresql://HOST:PORT/DB_NAME
      username: USERNAME
      password: PASSWORD
  ```
- If you accidentally paste a secret, **rotate it immediately** — assume it is compromised

### 3.5 Secure Prompting Practices

| Practice                             | Description                                                                                   |
| ------------------------------------ | --------------------------------------------------------------------------------------------- |
| **Strip before paste**               | Remove all sensitive values before sharing code                                               |
| **Minimize context**                 | Share only the relevant 10-20 lines, not the entire file                                      |
| **Use pseudocode**                   | Describe logic in pseudocode for sensitive algorithms                                         |
| **Generic naming**                   | Use generic names: `EntityA`, `ServiceX`, `calculateValue()`                                  |
| **Review output**                    | Always review AI output before committing — it may hallucinate credentials or unsafe patterns |
| **No screenshots of sensitive data** | Screenshots of production dashboards, database tables, or admin panels are equally risky      |

---

## 4. Company-Level Best Practices

### 4.1 Using AI with Sanitized Code Snippets

Create a **sanitization checklist** before every AI interaction:

```
Pre-Prompt Sanitization Checklist:
□ Removed all hardcoded credentials
□ Replaced real entity names with generic ones
□ Removed any patient/PHI references
□ Stripped company-specific naming conventions
□ Removed internal service URLs and endpoints
□ Verified no production data in examples
```

### 4.2 Using Internal Documentation Instead of Raw Code

Instead of sharing production code, consider:

- **Share interface definitions** — share the `interface`, not the implementation
- **Share DTOs/models** — these are structural, not logic-bearing
- **Use architecture diagrams** — describe the pattern, not the code
- **Reference framework docs** — "I'm using Spring Data JPA's `@Query`" instead of pasting the query
- **Create sanitized reference examples** — maintain a library of safe example snippets

### 4.3 Code Review After AI-Generated Code

> [!WARNING]
> **All AI-generated code MUST go through the same code review process as human-written code.** AI-generated code is a starting point — not production-ready output.

**Review Focus Areas:**

| Area                 | What to Check                                                                 |
| -------------------- | ----------------------------------------------------------------------------- |
| **Security**         | SQL injection, XSS, insecure deserialization, missing auth checks             |
| **Performance**      | N+1 queries, unnecessary object creation, missing pagination                  |
| **Error Handling**   | Proper exception handling, no swallowed exceptions, meaningful error messages |
| **Compliance**       | PHI logging, audit trail requirements, access control                         |
| **Coding Standards** | Adherence to team conventions, naming standards, project structure            |
| **Dependencies**     | No unknown/vulnerable libraries introduced                                    |
| **Test Coverage**    | AI tests may miss edge cases — verify boundary conditions                     |

### 4.4 Security Review Checklist for AI-Generated Code

Before merging any AI-assisted code:

- [ ] **No hardcoded secrets** — credentials, keys, tokens
- [ ] **Input validation** — all user inputs are validated and sanitized
- [ ] **Authentication/Authorization** — proper `@PreAuthorize` or security annotations
- [ ] **SQL injection safe** — parameterized queries, no string concatenation in queries
- [ ] **XSS protection** — Angular's built-in sanitization is preserved, no `bypassSecurityTrust*`
- [ ] **Logging compliance** — no PHI in log statements
- [ ] **Error messages** — don't expose internal details to end users
- [ ] **Dependency check** — run OWASP dependency check if new libraries are added
- [ ] **CORS configuration** — no wildcard (`*`) origins in production
- [ ] **Data exposure** — API responses don't include unnecessary sensitive fields

---

## 5. Developer Workflow with Antigravity

### 5.1 Bug-Fixing Workflow

```
┌─────────────────────────────────────────────────┐
│           Bug-Fixing with Antigravity           │
├─────────────────────────────────────────────────┤
│                                                 │
│  1. 🐛 Reproduce the bug locally                  │
│          ↓                                      │
│  2. 📋 Isolate the error (stack trace/log)      │
│          ↓                                      │
│  3. 🧹 Sanitize the error output                │
│     • Remove patient data from logs             │
│     • Replace real service names                 │
│     • Strip production URLs                      │
│          ↓                                      │
│  4. 🤖 Ask Antigravity for analysis             │
│     "Here's a NullPointerException in a         │
│      service layer. The entity has lazy-loaded   │
│      collections. What are possible causes?"     │
│          ↓                                      │
│  5. 🔍 Review the suggestion critically          │
│          ↓                                      │
│  6. 🧪 Apply fix and write a test               │
│          ↓                                      │
│  7. 👥 Submit for code review                    │
│                                                 │
└─────────────────────────────────────────────────┘
```

**Example Interaction:**

```
Developer: "I have a Spring Boot service method that fetches an entity 
by ID and accesses its one-to-many relationship. I'm getting a 
LazyInitializationException when the method is called from a 
scheduled task (outside HTTP request context). How can I fix this?"

Antigravity: [Provides solutions: @Transactional, JOIN FETCH, 
EntityGraph, DTO projection — with trade-offs for each]

Developer: [Reviews options, selects JOIN FETCH based on use case, 
writes test, submits PR]
```

### 5.2 Test Generation Workflow

```
Step 1: Identify the class/method to test
Step 2: Determine test type (Unit / Integration / E2E)
Step 3: Prepare a SANITIZED version of the method signature + behavior description
Step 4: Prompt Antigravity

    "Generate JUnit 5 + Mockito tests for a service method with this signature:
     
     public Optional<EntityDTO> findById(Long id)
     
     Behavior:
     - Calls repository.findById(id)
     - If found, maps to DTO and returns
     - If not found, throws ResourceNotFoundException
     - If id is null, throws IllegalArgumentException
     
     Include: happy path, not found, null input, verify mock interactions."

Step 5: Review generated tests for:
    □ Correct assertions
    □ Edge cases covered
    □ No hardcoded sensitive data
    □ Follows project test conventions

Step 6: Add project-specific edge cases the AI missed
Step 7: Run tests, verify they pass, submit PR
```

### 5.3 Refactoring Workflow

```
Step 1: Identify the code smell (long method, duplicate code, etc.)
Step 2: Create a GENERIC description of the problem

    "I have a 200-line method that handles:
     1. Input validation (30 lines)
     2. Business rule evaluation with 8 if-else branches (100 lines) 
     3. Entity mapping (30 lines)
     4. Persistence and notification (40 lines)
     
     Suggest a refactoring approach using design patterns."

Step 3: Review AI's suggested patterns (Strategy, Chain of Responsibility, etc.)
Step 4: Apply refactoring incrementally:
    - Extract validation → separate Validator class
    - Extract business rules → Strategy/Chain pattern
    - Extract mapping → MapStruct/dedicated mapper
Step 5: Ensure all existing tests still pass
Step 6: Add new tests for extracted classes
Step 7: Code review and merge
```

---

## 6. Risks and Limitations

### 6.1 Incorrect Code Generation

> [!WARNING]
> AI models generate **plausible-looking** code that may be **subtly wrong**. This is especially dangerous in healthcare software where bugs can have real-world consequences.

**Common Issues:**

| Risk                          | Example                                                                      |
| ----------------------------- | ---------------------------------------------------------------------------- |
| **Outdated APIs**             | Generates deprecated Spring Security config (`WebSecurityConfigurerAdapter`) |
| **Wrong annotations**         | Confuses JPA annotations (`@OneToMany` mappings with wrong cascade types)    |
| **Incomplete error handling** | Misses critical exception cases                                              |
| **Incorrect logic**           | Subtle off-by-one errors, wrong comparison operators                         |
| **Security vulnerabilities**  | Generates code without proper input validation or auth checks                |
| **Hallucinated methods**      | References methods or classes that don't exist                               |
| **Wrong dependency versions** | Suggests incompatible library versions                                       |

**Mitigation:**
- Always **compile and run** AI-generated code
- **Write tests first** (TDD) and then use AI to implement — the tests catch errors
- **Cross-reference** with official documentation
- Never deploy AI code **without code review**

### 6.2 Data Leakage Risks

| Scenario                                       | Risk Level | Mitigation                   |
| ---------------------------------------------- | ---------- | ---------------------------- |
| Pasting production logs                        | 🔴 Critical | Use synthetic/sanitized logs |
| Sharing database schemas with real table names | 🟡 Medium   | Rename tables generically    |
| Copying stack traces with file paths           | 🟡 Medium   | Redact internal paths        |
| Sharing `.properties` files                    | 🔴 Critical | Use placeholder values       |
| Pasting entire source files                    | 🟠 High     | Share only relevant snippets |
| Sharing API contracts with real endpoints      | 🟡 Medium   | Anonymize URLs               |

### 6.3 Over-Reliance on AI

**Symptoms of Over-Reliance:**
- Accepting AI output without understanding it
- Not being able to code without AI assistance
- Skipping documentation reading — "just ask AI"
- Copy-pasting without reviewing
- Declining problem-solving and debugging skills

**Healthy Balance:**
- Use AI for **acceleration**, not **substitution**
- Always **understand** the code before committing
- **Learn the fundamentals** — AI is a tool, not a teacher replacement
- **Challenge AI output** — ask "why?" and verify the reasoning
- Spend time doing **manual coding** to keep skills sharp

---

## 7. Recommended Prompting Techniques

### 7.1 How to Ask Better Questions

**❌ Vague Prompt:**
```
"Fix my code"
```

**✅ Structured Prompt:**
```
"I have a Spring Boot 3.2 REST API using Spring Data JPA with 
PostgreSQL. My PatientService.findAll() method returns a Page<PatientDTO>.

Problem: When I add a @Cacheable annotation, I get a 
SerializationException because Page is not serializable.

What I've tried:
1. Making DTO implement Serializable
2. Using PageImpl directly

Expected: Cached paginated results
Actual: SerializationException on second call

How can I properly cache paginated results?"
```

### 7.2 The CRISP Framework for Development Prompts

Use this structure for every prompt:

| Letter | Meaning     | Description                                                   |
| ------ | ----------- | ------------------------------------------------------------- |
| **C**  | Context     | Tech stack, framework version, module type                    |
| **R**  | Role        | "Act as a Spring Boot expert" / "Act as an Angular architect" |
| **I**  | Instruction | Exactly what you want — be specific                           |
| **S**  | Scope       | Constraints — "no deprecated APIs," "Java 17+," "use records" |
| **P**  | Proof       | Ask for explanation — "explain why this approach is better"   |

**Example using CRISP:**
```
Context: Spring Boot 3.2, Java 17, Spring Data JPA, MapStruct
Role: Act as a senior Java backend developer
Instruction: Create a mapper that converts between Patient entity 
and PatientResponseDTO. The entity has an Address embedded object 
and a List<Appointment> relationship.
Scope: Use MapStruct annotations, handle null safety, 
exclude sensitive fields (SSN, insuranceId)
Proof: Explain the mapping strategy for nested objects
```

### 7.3 Prompt Templates for Common Tasks

**For Bug Analysis:**
```
Framework: [Spring Boot / Angular / etc.]
Version: [X.Y.Z]
Error: [Paste sanitized error message]
Context: [What were you doing when this occurred?]
What I tried: [List attempts]
Expected vs Actual: [Describe gap]
```

**For Code Generation:**
```
Generate a [component type] for [purpose].
Tech stack: [specific versions]
Requirements:
1. [Requirement 1]
2. [Requirement 2]
Constraints: [security, performance, style]
Include: [tests, docs, error handling]
```

**For Code Review:**
```
Review this [code type] for:
1. Security vulnerabilities
2. Performance issues
3. Best practice violations
4. Missing error handling
Suggest improvements with explanations.
```

---

## 8. Realistic Examples

### 8.1 Spring Boot Examples

#### Example 1: Generating a REST Controller

```
Prompt: "Generate a Spring Boot 3.2 REST controller for an 
Appointment resource. Include:
- CRUD endpoints with proper HTTP methods and status codes
- Request validation using @Valid and Jakarta Bean Validation
- Pagination support for the list endpoint
- Exception handling with @ControllerAdvice pattern
- ResponseEntity wrapper for all responses
- Swagger annotations for API documentation
Use constructor injection, not @Autowired."
```

#### Example 2: Creating a Specification for Dynamic Queries

```
Prompt: "Show me how to implement Spring Data JPA Specifications 
for dynamic search/filtering. The entity has fields: 
name (String), status (Enum: ACTIVE, INACTIVE), 
createdDate (LocalDateTime), category (String).

Requirements:
- Support partial text search on name
- Filter by status
- Date range filtering on createdDate
- Combine multiple filters dynamically
- Use Criteria API under the hood
- Compatible with Pageable"
```

#### Example 3: Implementing an Audit Trail

```
Prompt: "Design a JPA audit mechanism using Spring Data's 
@EntityListeners and AuditingEntityListener. I need:
- Automatic createdBy, createdDate, lastModifiedBy, lastModifiedDate
- A base entity class that other entities extend
- Integration with Spring Security to capture the current user
- Envers-based history table for a specific entity
Show the full configuration including @EnableJpaAuditing."
```

### 8.2 Angular Examples

#### Example 1: Creating a Reactive Form

```
Prompt: "Create an Angular 17 reactive form component for 
patient registration. Include:
- Fields: name, email, phone, date of birth, gender (dropdown), 
  address (nested FormGroup)
- Validations: required, email format, phone pattern, 
  age must be > 0
- Custom validator: date of birth cannot be in the future
- Show validation error messages inline
- Use standalone component with Signal-based state
- Submit handler that calls a service method"
```

#### Example 2: Building an HTTP Interceptor

```
Prompt: "Create an Angular 17 HTTP interceptor that:
1. Adds JWT token from localStorage to Authorization header
2. Handles 401 responses by redirecting to login
3. Handles 403 with a toast notification
4. Shows a global loading spinner during HTTP calls
5. Implements retry logic (max 2 retries) for 5xx errors
Use the new functional interceptor pattern (HttpInterceptorFn), 
not class-based."
```

#### Example 3: Creating a Data Table with Features

```
Prompt: "Create an Angular 17 standalone component for a data table 
that supports:
- Server-side pagination
- Column sorting (single and multi)
- Search/filter input with debounce (300ms)
- Row selection (single and multi-select)
- Loading skeleton state
- Empty state message
- Responsive design
Use Angular Material or PrimeNG (specify which). 
Include the service call pattern using RxJS."
```

### 8.3 Debugging Examples

#### Example 1: Analyzing a Stack Trace

```
Prompt: "Analyze this Spring Boot error:

org.springframework.beans.factory.BeanCreationException: 
Error creating bean with name 'entityManagerFactory': 
Invocation of init method failed; nested exception is 
org.hibernate.AnnotationException: 
No identifier specified for entity: com.example.model.AuditLog

I have an @Entity class that extends a @MappedSuperclass. 
The superclass has a field annotated with @Id. 
Why isn't Hibernate detecting the ID field?"
```

#### Example 2: Angular Change Detection Issue

```
Prompt: "My Angular component is not updating the view when data 
changes. Setup:
- Component uses OnPush change detection
- Data comes from an Observable via async pipe
- Parent passes an object via @Input
- When I mutate a property on the input object, the view 
  doesn't update

Explain why this happens with OnPush and give me the proper 
solution using immutable patterns."
```

#### Example 3: Performance Debugging

```
Prompt: "My Spring Boot API endpoint returns 200 records but 
takes 8 seconds. I suspect N+1 query issues. I have:
- An entity with 3 @OneToMany lazy relationships
- A service that calls findAll() and then accesses each relationship
- Using Spring Data JPA

How can I:
1. Confirm if this is an N+1 problem
2. Fix it using EntityGraph or JOIN FETCH
3. Add query logging to monitor SQL statements
Show the before/after comparison."
```

---

## 9. Conclusion

### Key Takeaways

1. **Antigravity is a productivity multiplier** — it accelerates boilerplate, debugging, testing, and learning
2. **Security is non-negotiable** — never share PHI, credentials, or proprietary algorithms
3. **Sanitize everything** — strip sensitive data before every interaction
4. **Review everything** — AI-generated code is a draft, not a final product
5. **Use structured prompts** — the CRISP framework ensures better AI responses
6. **Maintain your skills** — use AI as an accelerator, not a crutch
7. **Follow the checklist** — use the security review checklist for every AI-assisted PR

### Developer Pledge

> *"I will use AI coding tools responsibly. I will never share patient data, production secrets, or proprietary business logic with any AI system. I will review all AI-generated code with the same rigor as human-written code. I will prioritize security and compliance in every interaction."*

### Quick Reference Card

| ✅ DO                               | ❌ DON'T                        |
| ---------------------------------- | ------------------------------ |
| Sanitize code before sharing       | Paste production configs       |
| Use generic names and placeholders | Share real patient data        |
| Review all AI-generated code       | Blindly copy-paste AI output   |
| Ask about patterns and approaches  | Share proprietary algorithms   |
| Use structured prompts (CRISP)     | Ask vague, one-line questions  |
| Write tests for AI code            | Skip testing AI-generated code |
| Report security concerns           | Ignore potential data exposure |
| Keep learning fundamentals         | Become dependent on AI         |

---

> **Questions?** Reach out to the Engineering Leads or the Security Team.  
> **Report a security incident:** [Your internal security reporting channel]

---

*This document should be reviewed and updated quarterly to reflect new features, policies, and best practices.*
