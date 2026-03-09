# 🎯 Antigravity — Mastering Prompts
## The Developer's Complete Guide to Effective Prompting

> **Prepared for:** Development Team — HMIS Product Division  
> **Tech Stack:** Java Spring Boot · Angular · PostgreSQL  
> **Classification:** Internal — Training Material  
> **Date:** March 2026

---

## Table of Contents

1. [Why Prompting Matters](#1-why-prompting-matters)
2. [The CRISP Framework](#2-the-crisp-framework)
3. [Prompt Anatomy — What Makes a Great Prompt](#3-prompt-anatomy--what-makes-a-great-prompt)
4. [Golden Rules of Prompting](#4-golden-rules-of-prompting)
5. [Prompt Patterns for Daily Development](#5-prompt-patterns-for-daily-development)
6. [Spring Boot Prompt Cookbook](#6-spring-boot-prompt-cookbook)
7. [Angular Prompt Cookbook](#7-angular-prompt-cookbook)
8. [Database & SQL Prompt Cookbook](#8-database--sql-prompt-cookbook)
9. [DevOps & Infrastructure Prompts](#9-devops--infrastructure-prompts)
10. [Debugging & Troubleshooting Prompts](#10-debugging--troubleshooting-prompts)
11. [Code Review & Refactoring Prompts](#11-code-review--refactoring-prompts)
12. [Testing Prompts](#12-testing-prompts)
13. [Documentation Prompts](#13-documentation-prompts)
14. [Anti-Patterns — What NOT to Do](#14-anti-patterns--what-not-to-do)
15. [Prompt Chaining — Multi-Step Workflows](#15-prompt-chaining--multi-step-workflows)
16. [Quick Reference Cheat Sheet](#16-quick-reference-cheat-sheet)

---

## 1. Why Prompting Matters

The same AI model can give you a **brilliant, production-ready answer** or a **vague, incorrect mess** — the only difference is **how you ask**.

| Prompt Quality          | Result Quality           | Time Spent            |
| ----------------------- | ------------------------ | --------------------- |
| Vague, one-liner        | Generic, often wrong     | 30+ min fixing output |
| Moderate detail         | Usable but needs editing | 10-15 min adjusting   |
| Well-structured (CRISP) | Near production-ready    | 2-5 min review        |

> [!TIP]
> Investing **2 extra minutes** crafting a good prompt saves **20+ minutes** of back-and-forth corrections.

---

## 2. The CRISP Framework

Use **CRISP** as your mental model for every Antigravity prompt:

```
C — Context       → Tech stack, versions, project setup
R — Role           → What expertise should the AI assume?
I — Instruction    → Precisely what you want done
S — Scope          → Constraints, limitations, conventions
P — Proof          → Ask for explanation or reasoning
```

### CRISP in Action

**❌ Without CRISP:**
```
Create a login API
```

**✅ With CRISP:**
```
Context: Spring Boot 3.2, Java 17, Spring Security 6, PostgreSQL, JWT authentication
Role: Act as a senior backend engineer specializing in Spring Security
Instruction: Create a login endpoint that accepts email/password, 
validates credentials against the database, and returns a JWT access 
token + refresh token pair
Scope: 
- Use BCrypt for password hashing
- JWT expiry: 15 min access, 7 days refresh
- Return proper HTTP status codes (200, 401, 400)
- Use record classes for request/response DTOs
- No deprecated WebSecurityConfigurerAdapter
Proof: Explain why you chose this token expiry strategy
```

---

## 3. Prompt Anatomy — What Makes a Great Prompt

### The 6 Components

```
┌───────────────────────────────────────────────────────┐
│                    GREAT PROMPT                       │
├───────────────────────────────────────────────────────┤
│  1. CONTEXT     │ "Spring Boot 3.2, Java 17..."      │
│  2. OBJECTIVE   │ "Create / Fix / Explain / Review.." │
│  3. INPUT       │ Sanitized code, error, or spec      │
│  4. CONSTRAINTS │ "Use X, don't use Y, follow Z..."   │
│  5. OUTPUT      │ "Return code with comments..."      │
│  6. FOLLOW-UP   │ "Also explain trade-offs..."        │
└───────────────────────────────────────────────────────┘
```

### Specificity Scale

| Level          | Example                                                                                                                                      | AI Response Quality    |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| 🔴 **Vague**    | "Fix the bug"                                                                                                                                | Guesses randomly       |
| 🟡 **General**  | "Fix the NullPointer in my service"                                                                                                          | Gives generic advice   |
| 🟢 **Specific** | "Fix NPE in findById() — entity returns null when ID doesn't exist in PostgreSQL table, using Spring Data JPA"                               | Targeted, accurate fix |
| 💎 **Expert**   | Same as above + "I need it to return Optional, use @Query with LEFT JOIN FETCH, handle the empty case with a custom exception mapped to 404" | Production-ready code  |

---

## 4. Golden Rules of Prompting

### Rule 1: Be Explicit, Not Implicit

```
❌ "Make it better"
✅ "Refactor this method to reduce cyclomatic complexity from 12 to 
   under 5 by extracting validation logic into a separate class"
```

### Rule 2: Specify Versions

```
❌ "How to configure Spring Security?"
✅ "How to configure Spring Security 6.2 with Spring Boot 3.2 
   using the new SecurityFilterChain bean approach?"
```

> [!WARNING]
> Without version numbers, AI often generates code for older versions. Spring Security alone has had **3 major configuration style changes** — specifying the version avoids deprecated patterns.

### Rule 3: One Task Per Prompt

```
❌ "Create a user module with entity, repository, service, controller, 
   DTOs, mapper, tests, and API documentation"

✅ Break it down:
   Prompt 1: "Create the User JPA entity with [fields]..."
   Prompt 2: "Create the repository with custom queries for..."
   Prompt 3: "Create the service layer with [business rules]..."
   Prompt 4: "Create the controller with [endpoints]..."
```

### Rule 4: Provide Examples of Desired Output

```
"Generate a DTO for Patient. Follow this style:

public record PatientResponseDTO(
    Long id,
    String name,
    String status,
    LocalDateTime createdAt
) {}

Now create similar DTOs for: Appointment, Prescription, Invoice"
```

### Rule 5: Tell It What NOT to Do

```
"Create a REST controller.
- Do NOT use @Autowired field injection
- Do NOT return entity objects directly (use DTOs)
- Do NOT use ResponseEntity.ok() without proper error handling
- Do NOT hardcode any values"
```

### Rule 6: Ask for Alternatives

```
"Show me 3 different ways to implement caching for this query. 
Compare them by: performance, memory usage, and complexity. 
Recommend the best one for a healthcare application with 
10,000 concurrent users."
```

### Rule 7: Set the Output Format

```
"Return your answer in this format:
1. Code solution (with inline comments)
2. Explanation (2-3 sentences)  
3. Potential pitfalls (bullet list)
4. Production readiness score (1-10 with justification)"
```

---

## 5. Prompt Patterns for Daily Development

### Pattern 1: The Explainer

**Use when:** You need to understand code or concepts.

```
Template:
"Explain [concept/code] as if I'm a [level] developer.
Include: 
- How it works internally
- When to use it vs alternatives
- Common mistakes
- A simple example"

Example:
"Explain Spring Boot's @Transactional propagation levels as if 
I'm a mid-level developer. Include how REQUIRED vs REQUIRES_NEW 
behave when one @Transactional method calls another. Show what 
happens to the database if the inner method throws an exception."
```

### Pattern 2: The Generator

**Use when:** You need code written from scratch.

```
Template:
"Generate a [component type] for [purpose].
Tech: [stack and versions]
Requirements:
  1. [Specific requirement]
  2. [Specific requirement]
Constraints: [what to avoid]
Include: [tests/docs/error handling]"

Example:
"Generate a Spring Boot global exception handler using 
@ControllerAdvice. 
Tech: Spring Boot 3.2, Java 17
Requirements:
  1. Handle ResourceNotFoundException → 404
  2. Handle ValidationException → 400 with field-level errors
  3. Handle AccessDeniedException → 403
  4. Handle all other exceptions → 500 with generic message
  5. Log full stack trace for 500s, skip for 4xx
Constraints: Never expose internal error details to clients
Include: Unit tests with MockMvc"
```

### Pattern 3: The Reviewer

**Use when:** You want code reviewed or improved.

```
Template:
"Review the following [code type] for:
1. Security vulnerabilities
2. Performance issues  
3. Best practice violations
4. Missing error handling
5. [Domain-specific concern]

Rate each area (Good / Needs Improvement / Critical).
Provide fixed code for any Critical issues.

[Paste sanitized code]"
```

### Pattern 4: The Debugger

**Use when:** You're stuck on an error.

```
Template:
"Framework: [name + version]
Error message: [sanitized error]
Code context: [relevant sanitized snippet]
What I've tried:
  1. [Attempt 1]
  2. [Attempt 2]
Expected behavior: [what should happen]
Actual behavior: [what happens instead]
Environment: [OS, JDK version, DB, etc.]"
```

### Pattern 5: The Comparator

**Use when:** You need to choose between approaches.

```
Template:
"Compare [Option A] vs [Option B] for [use case].
Evaluation criteria:
  1. Performance
  2. Maintainability
  3. Scalability
  4. Learning curve
  5. [Custom criterion]
Present as a comparison table and give your recommendation 
for a [describe system type] system."

Example:
"Compare MapStruct vs ModelMapper vs manual mapping for 
Entity-to-DTO conversion.
In context of: healthcare application with 200+ entities, 
team of 15 developers, need for compile-time safety.
Present as a table and recommend one."
```

### Pattern 6: The Migrator

**Use when:** Upgrading or converting code.

```
Template:
"Convert this [old pattern/version] code to [new pattern/version].
Preserve the same behavior.
Highlight breaking changes.
Show before/after comparison.

[Paste sanitized old code]"

Example:
"Convert this class-based Angular component to use:
- Standalone component (no NgModule)
- Angular Signals instead of BehaviorSubject
- New control flow syntax (@if, @for) instead of *ngIf, *ngFor
- inject() function instead of constructor injection
Highlight all behavioral differences."
```

---

## 6. Spring Boot Prompt Cookbook

### 6.1 Entity & Repository

```
"Create a JPA @Entity for [EntityName] with the following fields:
- id: Long, auto-generated (IDENTITY strategy)
- [field]: [Type], [constraints]
- [field]: [Type], [constraints]
- Audit fields: createdAt, updatedAt (auto-populated)
- Soft delete support (isDeleted flag)

Include:
- Proper Lombok annotations (@Getter, @Setter, @NoArgsConstructor, @Builder)
- @Table with proper naming
- @Column constraints matching the field requirements
- equals/hashCode based on id only
- toString excluding lazy collections

Then create the Spring Data JPA repository with:
- Custom query: findAllByStatusAndCreatedAtBetween
- @Query with JPQL for [specific search]
- Specification support (extend JpaSpecificationExecutor)"
```

### 6.2 Service Layer

```
"Create a service class for [Entity]Service with:
- CRUD operations returning DTOs (not entities)
- Input validation using a separate validator
- @Transactional on write operations
- Logging with SLF4J at appropriate levels
- Proper exception handling:
  • ResourceNotFoundException for missing records
  • DuplicateResourceException for unique constraint violations
  • BusinessRuleException for domain rule violations
- Pagination support for list method
- Mapping using [MapStruct / manual / ModelMapper]

Use constructor injection. Do NOT use @Autowired."
```

### 6.3 REST Controller

```
"Create a REST controller for /api/v1/[resource] with:

Endpoints:
- GET /          → List with pagination (page, size, sort params)
- GET /{id}      → Get by ID
- POST /         → Create (validate request body)
- PUT /{id}      → Full update
- PATCH /{id}    → Partial update
- DELETE /{id}   → Soft delete

Include:
- @Valid on request bodies
- ResponseEntity with proper status codes per endpoint
- Swagger @Operation + @ApiResponse annotations
- @PreAuthorize for role-based access (ADMIN, DOCTOR, NURSE)
- Constructor injection of service
- No business logic in controller (delegate to service)"
```

### 6.4 Security Configuration

```
"Create a Spring Security 6.x configuration for a REST API:
- JWT-based stateless authentication
- SecurityFilterChain bean (not deprecated configure method)
- Public endpoints: /api/auth/**, /api/public/**, /actuator/health
- Role-based authorization:
  • ADMIN: full access
  • DOCTOR: read/write on patient, appointment
  • NURSE: read-only on patient, read/write on vitals
  • RECEPTIONIST: read/write on appointment, registration
- CORS configuration for Angular frontend on localhost:4200
- CSRF disabled (stateless API)
- Custom AuthenticationEntryPoint for 401 responses
- Password encoder: BCrypt"
```

### 6.5 Exception Handling

```
"Create a comprehensive @ControllerAdvice exception handler:

Map these exceptions:
- ResourceNotFoundException → 404
- DuplicateResourceException → 409
- BusinessRuleException → 422
- MethodArgumentNotValidException → 400 (field-level errors)
- ConstraintViolationException → 400
- AccessDeniedException → 403
- AuthenticationException → 401
- HttpRequestMethodNotSupportedException → 405
- DataIntegrityViolationException → 409
- Generic Exception → 500

Response format (as a record):
{
  'timestamp': '...',
  'status': 404,
  'error': 'Not Found',
  'message': 'Patient with id 123 not found',
  'path': '/api/v1/patients/123',
  'fieldErrors': [] // only for validation errors
}

Log 5xx errors with full stack trace, 4xx with warn level only."
```

---

## 7. Angular Prompt Cookbook

### 7.1 Component Generation

```
"Create an Angular 17 standalone component for a [purpose].
Structure:
- [component-name].component.ts (logic)
- [component-name].component.html (template)
- [component-name].component.scss (styles)

Requirements:
- Use standalone: true (no NgModule)
- Use Angular Signals for state management
- Use new control flow (@if, @for, @switch)
- inject() function instead of constructor injection
- OnPush change detection strategy
- Smart/Dumb component pattern: [specify which]

Include:
- Input/Output decorators (or signal-based inputs)
- Loading and error states
- Responsive layout (mobile-first)
- Accessibility (ARIA labels, keyboard navigation)"
```

### 7.2 Service with HTTP

```
"Create an Angular 17 service for [Resource]Service:
- Base URL: environment.apiUrl + '/api/v1/[resource]'
- Methods:
  • getAll(params: SearchParams): Observable<Page<ResourceDTO>>
  • getById(id: number): Observable<ResourceDTO>
  • create(dto: CreateResourceDTO): Observable<ResourceDTO>
  • update(id: number, dto: UpdateResourceDTO): Observable<ResourceDTO>
  • delete(id: number): Observable<void>
- Use HttpClient with typed responses
- Proper error handling with catchError
- Transform API errors into user-friendly messages
- Use providedIn: 'root'"
```

### 7.3 Reactive Forms

```
"Create a reactive form for [purpose]:
- FormGroup with these controls:
  • [field]: [type] — Validators: [required, minLength, etc.]
  • [field]: [type] — Validators: [pattern, custom, etc.]
  • [nestedGroup]: FormGroup with [sub-fields]
  • [arrayField]: FormArray for dynamic items
  
- Custom validators:
  • [describe custom validation logic]
  • Cross-field validation: [describe]

- Features:
  • Inline error messages (show only after touch)
  • Form-level error summary
  • Submit with loading state
  • Reset functionality
  • Dirty form guard (confirm before leaving)"
```

### 7.4 State Management

```
"Implement state management for [feature] using:
[Choose: NgRx / Angular Signals / RxJS BehaviorSubject]

State shape:
{
  items: Item[],
  selectedItem: Item | null,
  loading: boolean,
  error: string | null,
  filters: FilterParams
}

Actions/Operations:
- Load items (with pagination)
- Select item
- Create/Update/Delete item
- Apply filters
- Clear state

Include: selectors/computed signals, effects/subscriptions 
for side effects, optimistic updates for better UX."
```

### 7.5 Route Guards & Resolvers

```
"Create Angular 17 functional route guards:
1. AuthGuard — redirect to /login if not authenticated
2. RoleGuard — check user role against route data 
   (e.g., route.data['roles'] = ['ADMIN', 'DOCTOR'])
3. UnsavedChangesGuard — confirm dialog if form is dirty
4. Resolver — pre-fetch entity data before route activation

Use the new functional approach (CanActivateFn, etc.), 
NOT class-based guards. Use inject() for dependencies."
```

---

## 8. Database & SQL Prompt Cookbook

### 8.1 Schema Design

```
"Design a PostgreSQL database schema for a [module name] module:

Entities:
- [Entity1]: [describe key fields and relationships]
- [Entity2]: [describe key fields and relationships]

Requirements:
- Use proper data types (VARCHAR limits, TIMESTAMP WITH TIME ZONE)
- Define indexes for frequently queried columns
- Add unique constraints where appropriate
- Foreign keys with proper ON DELETE behavior
- Audit columns: created_at, updated_at, created_by, updated_by
- Soft delete support (deleted_at column)

Generate:
1. CREATE TABLE statements
2. Index definitions
3. Flyway migration script (V[number]__description.sql)"
```

### 8.2 Query Optimization

```
"Optimize this query for PostgreSQL:
[Paste sanitized query with generic table/column names]

Context:
- Table has approximately [N] rows
- Query runs [frequency]
- Current execution time: [X]ms
- Target: under [Y]ms

Provide:
1. EXPLAIN ANALYZE interpretation
2. Index recommendations
3. Query rewrite suggestions
4. JPA @Query or Specification equivalent"
```

---

## 9. DevOps & Infrastructure Prompts

### 9.1 Docker

```
"Create a multi-stage Dockerfile for a Spring Boot 3.2 application:
- Build stage: Maven build with test skip option
- Runtime stage: Eclipse Temurin JRE 17 slim
- Non-root user for security
- Health check endpoint: /actuator/health
- Proper ENTRYPOINT with JVM tuning flags
- Labels for metadata
- .dockerignore file

Also create a docker-compose.yml with:
- App service (referencing the Dockerfile)
- PostgreSQL 15 service with volume
- Environment variable substitution for secrets
- Network isolation"
```

### 9.2 CI/CD Pipeline

```
"Create a [GitHub Actions / GitLab CI / Jenkins] pipeline for 
a Spring Boot + Angular monorepo:

Stages:
1. Build — compile both projects
2. Test — unit tests (JUnit + Karma) with coverage
3. Code Quality — SonarQube analysis
4. Security Scan — OWASP dependency check
5. Docker Build — build and push image
6. Deploy — deploy to [staging/production]

Requirements:
- Cache Maven and npm dependencies
- Fail on test coverage below 80%
- Parallel execution where possible
- Environment-specific secrets handling
- Manual approval gate before production deploy"
```

---

## 10. Debugging & Troubleshooting Prompts

### 10.1 Stack Trace Analysis Template

```
"Analyze this sanitized error:

Framework: [Spring Boot 3.2 / Angular 17 / etc.]
JDK: [17 / 21]
Error Type: [Exception class name]
Message: [Sanitized error message]

Stack Trace (sanitized):
[Paste with generic package/class names]

What was happening: [Operation being performed]
When it occurs: [Always / Intermittently / Under load]
Recent changes: [What changed recently]

Provide:
1. Root cause explanation
2. Step-by-step fix
3. How to prevent this in the future"
```

### 10.2 Performance Troubleshooting

```
"My [endpoint/feature] is slow:

Observed: [current response time]
Expected: [target response time]
Load: [concurrent users / request rate]

Architecture:
- [Describe the flow: controller → service → repo → DB]
- [Caching: yes/no, type]
- [Connection pooling: HikariCP settings]

I suspect: [your hypothesis]
I've checked: [what you've already investigated]

Help me:
1. Identify the bottleneck
2. Suggest profiling/monitoring approach
3. Provide optimization options ranked by impact"
```

### 10.3 Angular-Specific Debugging

```
"My Angular component has a [describe issue]:

Setup:
- Change detection: [Default / OnPush]
- State source: [Observable / Signal / @Input]
- Template binding: [async pipe / manual subscribe / direct]
- Parent-child relationship: [describe]

Behavior:
- Expected: [what should happen]
- Actual: [what actually happens]
- Frequency: [always / sometimes / on specific action]

I've tried:
1. [Attempt 1]
2. [Attempt 2]

Explain why this happens and the correct solution."
```

---

## 11. Code Review & Refactoring Prompts

### 11.1 Automated Code Review

```
"Review this [service/controller/component] code for:

1. **Security** — injection vulnerabilities, auth issues, 
   data exposure
2. **Performance** — N+1 queries, unnecessary allocations, 
   missing pagination
3. **SOLID Principles** — violations of Single Responsibility, 
   Open/Closed, etc.
4. **Error Handling** — missing catches, swallowed exceptions, 
   generic handlers
5. **Concurrency** — race conditions, thread safety issues
6. **Healthcare Compliance** — PHI in logs, missing audit trail

For each issue found:
- Severity: Critical / Major / Minor
- Line reference
- Explanation of risk
- Suggested fix with code

[Paste sanitized code]"
```

### 11.2 Refactoring Prompts

```
"Refactor this code to apply [specific pattern]:

Current state: [Describe what's wrong — too long, too complex, 
violates X principle]

Target:
- Pattern to apply: [Strategy / Builder / Observer / etc.]
- Max method length: [N lines]
- Max cyclomatic complexity: [N]
- Must maintain backward compatibility

Constraints:
- Don't change public API signatures
- Keep all existing tests passing
- Follow project conventions: [list conventions]

Return:
1. Refactored code
2. List of all structural changes made
3. Before/after complexity metrics"
```

---

## 12. Testing Prompts

### 12.1 Unit Test Generation

```
"Generate JUnit 5 + Mockito tests for [ClassName].[methodName]:

Method signature: [paste sanitized signature]
Method behavior:
1. [Step 1 of the logic]
2. [Step 2 of the logic]
3. [Step 3 — error case]

Generate tests for:
- ✅ Happy path
- ❌ Each error case ([list them])
- 🔲 Boundary conditions ([list them])
- 🔄 Edge cases: null inputs, empty collections, max values
- 🔍 Verify mock interactions (verify calls, argument matchers)

Use:
- @DisplayName with descriptive test names
- @Nested classes for grouping
- @ParameterizedTest where applicable
- AssertJ assertions (not JUnit assertions)
- Arrange-Act-Assert structure with comments"
```

### 12.2 Integration Test Generation

```
"Generate a Spring Boot integration test for [endpoint]:

Endpoint: [HTTP method] [URL path]
Required setup:
- Test database: H2 / Testcontainers PostgreSQL
- Pre-loaded data: [describe test data needed]
- Authentication: [JWT token / @WithMockUser]

Test scenarios:
1. Success case — valid request → expected response + status
2. Validation failure — invalid input → 400 with field errors
3. Not found — missing resource → 404
4. Unauthorized — no token → 401
5. Forbidden — wrong role → 403

Use:
- @SpringBootTest with @AutoConfigureMockMvc
- MockMvc with content type application/json
- JSONPath assertions for response body
- @Sql for test data setup (or @BeforeEach)
- @Transactional for test isolation"
```

### 12.3 Angular Test Generation

```
"Generate Jasmine + TestBed tests for [ComponentName]:

Component type: [Smart / Presentational]
Dependencies to mock: [list services]
Template bindings: [list key bindings]

Test scenarios:
1. Component creation
2. Initial state rendering
3. User interaction: [describe click/input actions]
4. Service call verification
5. Loading state display
6. Error state display
7. @Input change handling
8. @Output event emission

Use:
- ComponentFixture with detectChanges()
- jasmine.createSpyObj for service mocks
- fakeAsync + tick for async operations
- By.css for DOM queries + nativeElement
- DebugElement for component testing"
```

---

## 13. Documentation Prompts

### 13.1 API Documentation

```
"Generate Swagger/OpenAPI 3.0 annotations for this controller:

[Paste sanitized controller]

For each endpoint include:
- @Operation with summary and description
- @ApiResponse for every possible HTTP status
- @Parameter descriptions for path/query params
- @Schema for request/response DTOs with examples
- @Tag for grouping

Also generate a standalone OpenAPI YAML spec for these endpoints."
```

### 13.2 Code Documentation

```
"Generate documentation for this [class/module]:

1. Class-level Javadoc:
   - Purpose and responsibility
   - Usage examples
   - Thread safety notes
   - Author and since tags

2. Method-level Javadoc:
   - @param for all parameters
   - @return description
   - @throws for all exceptions
   - Pre/post conditions

3. Inline comments for complex logic blocks

Style: professional, concise, avoid stating the obvious."
```

### 13.3 Architecture Decision Record

```
"Create an ADR (Architecture Decision Record) for:

Decision: [What was decided]
Context: [Why was this decision needed]
Options considered:
1. [Option A] — [brief description]
2. [Option B] — [brief description]
3. [Option C] — [brief description]

Format:
- Title
- Status (Proposed / Accepted / Deprecated)
- Context
- Decision
- Consequences (positive and negative)
- Alternatives considered with trade-off analysis"
```

---

## 14. Anti-Patterns — What NOT to Do

### ❌ The Lazy Prompt
```
"Write code for patient module"
```
**Why it fails:** Zero context. AI will guess your stack, patterns, and requirements.

### ❌ The Over-Dump
```
"Here's my entire 500-line file, fix it"
```
**Why it fails:** Too much noise. AI loses focus. Also risks exposing sensitive code.

### ❌ The Moving Target
```
"Create a service... also add caching... actually make it async... 
oh and add retry logic... and also events..."
```
**Why it fails:** Constant additions in one prompt create confusion. Use separate prompts.

### ❌ The Assumption Prompt
```
"You know our project structure, generate the next service"
```
**Why it fails:** AI has no memory of your project unless you provide context each time.

### ❌ The Trust Fall
```
[Copy-pastes AI output directly into production without review]
```
**Why it fails:** AI can generate plausible but incorrect code, especially for business logic.

### ❌ The Secret Sharer
```
"Here's my application.properties with all database credentials, 
why isn't it connecting?"
```
**Why it fails:** Credentials exposed. Always use placeholders.

---

## 15. Prompt Chaining — Multi-Step Workflows

For complex tasks, break work into a **chain of prompts** where each builds on the previous:

### Example: Building a Complete Feature

```
Chain Step 1 — Design:
"Design the database schema for an Appointment Scheduling 
module. Include entities, relationships, and constraints."
    ↓ [Review output, then proceed]

Chain Step 2 — Entity:
"Based on this schema, create the JPA entities with proper 
annotations, relationships, and audit fields:
[Paste schema from Step 1]"
    ↓ [Review output, then proceed]

Chain Step 3 — Repository:
"Create Spring Data JPA repositories for these entities. 
Include custom queries for: [list queries needed]"
    ↓ [Review output, then proceed]

Chain Step 4 — Service:
"Create the service layer. Business rules:
1. [Rule 1]
2. [Rule 2]
Use the repositories from the previous step."
    ↓ [Review output, then proceed]

Chain Step 5 — Controller:
"Create REST controllers exposing these services. 
Follow RESTful conventions."
    ↓ [Review output, then proceed]

Chain Step 6 — Tests:
"Generate unit tests for the service layer.
Generate integration tests for the controller layer."
    ↓ [Review output, then proceed]

Chain Step 7 — Documentation:
"Generate Swagger annotations and API documentation 
for all endpoints."
```

> [!TIP]
> Each step has a clear, focused objective. Review and adjust before moving to the next step. This avoids compounding errors across the chain.

---

## 16. Quick Reference Cheat Sheet

### Prompt Starters by Task

| Task              | Prompt Starter                                                               |
| ----------------- | ---------------------------------------------------------------------------- |
| **Generate Code** | "Create a [component] for [purpose] using [tech stack]..."                   |
| **Debug**         | "Analyze this error in [framework version]. Context: ..."                    |
| **Explain**       | "Explain [concept] with examples relevant to [our context]..."               |
| **Review**        | "Review this code for security, performance, and best practices..."          |
| **Refactor**      | "Refactor this to apply [pattern], reducing complexity from X to Y..."       |
| **Test**          | "Generate [JUnit/Jasmine] tests covering happy path + [N] error cases..."    |
| **Compare**       | "Compare [A] vs [B] for [use case]. Present as a table..."                   |
| **Convert**       | "Convert this [old pattern] to [new pattern]. Highlight breaking changes..." |
| **Document**      | "Generate [Javadoc/Swagger/ADR] for this [component]..."                     |
| **Optimize**      | "This [query/method] takes [X]ms, target [Y]ms. Profile and optimize..."     |

### Power Phrases to Improve Output

| Add This Phrase                                       | Effect                              |
| ----------------------------------------------------- | ----------------------------------- |
| "Act as a senior [role]"                              | Higher-quality, opinionated answers |
| "Explain your reasoning"                              | Gets the *why*, not just the *what* |
| "Show trade-offs"                                     | Balanced view of alternatives       |
| "Include edge cases"                                  | More thorough coverage              |
| "Follow [specific standard]"                          | Aligns to your conventions          |
| "What could go wrong?"                                | Surfaces risks proactively          |
| "Is this production-ready?"                           | Triggers self-assessment            |
| "Show before/after"                                   | Clear comparison of changes         |
| "Rate the complexity 1-10"                            | Quick quality assessment            |
| "What would you change if this system had 10x users?" | Scalability perspective             |

### The 30-Second Prompt Checklist

Before hitting Enter, verify:

- [ ] **Context** specified? (framework, version, module)
- [ ] **Objective** clear? (generate, fix, explain, review)
- [ ] **Constraints** defined? (style, patterns, what to avoid)
- [ ] **Sensitive data** removed? (credentials, PHI, proprietary logic)
- [ ] **Output format** requested? (code + comments, table, comparison)
- [ ] **One task** per prompt? (not multiple unrelated requests)

---

> **Remember:** A well-crafted prompt is an investment. The 2 minutes you spend writing a great prompt will save you 20 minutes of fixing a mediocre answer.

---

*This guide should be revisited as the team's AI prompting skills mature and new patterns emerge.*
