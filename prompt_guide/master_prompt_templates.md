# 📚 The Master Prompt Template Dictionary
## Complete "Plug and Play" Prompts for Spring Boot & Angular 17

> **Audience:** HMIS Frontend & Backend Developers  
> **Purpose:** 100+ raw, copy-paste ready prompt templates for daily development tasks.  
> **Tech Stack:** Java 17, Spring Boot 3.2, PostgreSQL, Angular 17, TypeScript  

---

<details>
<summary><strong>⚠️ READ FIRST: THE 3 RULES OF COPY-PASTING THESE PROMPTS</strong></summary>

1. **REPLACE THE BRACKETS:** Anything inside `[brackets]` needs to be replaced with your actual context.
2. **SANITIZE CODE:** NEVER paste code containing PHI, real patient data, passwords, or production DB strings.
3. **PROVIDE CONTEXT:** If the template says "Context:", explain what you're trying to achieve mathematically or functionally.

</details>

---

## Table of Contents
1. [Universal Developer Prompts](#1-universal-developer-prompts) (Debugging, git, explanations)
2. [☕ Spring Boot 3.2 Backend Prompts](#2-☕-spring-boot-32-backend-prompts) (Entities, Services, Controllers, Security)
3. [🅰️ Angular 17 Frontend Prompts](#3-🅰️-angular-17-frontend-prompts) (Signals, Components, Forms, Http, Routing)
4. [🧪 Testing & QA Prompts](#4-🧪-testing--qa-prompts) (JUnit 5, Mockito, Cypress, Jasmine/Karma)
5. [📄 Documentation & Code Review](#5-📄-documentation--code-review) (PRs, Javadoc, README)

---

## 1. Universal Developer Prompts

### 🐞 Debugging Stack Traces & Errors
```markdown
[Role:] Java 17/Spring Boot 3.2 (or Angular 17/TypeScript) Expert
[Task:] Analyze this error and provide an immediate fix.
[Error Message/Stack Trace:] 
{paste sanitized stack trace}

[Context:] I was trying to {describe what you were doing, e.g., fetch data from API, save to DB}.
[Attempted Solutions:] I already tried {what you tried}.

[Constraints:] 
- Do not explain the history of the framework. Just tell me the root cause.
- Provide the exact code block to fix it.
- Explain "Why" it broke in 1-2 bullet points.
```

### 🧠 Explaining Legacy / Complex Code
```markdown
[Role:] Senior Archtiect Reviewer
[Task:] Break down this code block so a junior developer could understand it.
[Code:]
{paste sanitized code}

[Format output as:]
1. **The Goal:** A 1-sentence summary of what this functionally does.
2. **The Flow:** Step-by-step logic map.
3. **The Danger Zones:** Point out edge cases (null pointers, race conditions, memory leaks) this code might not be handling.
4. **Suggestions:** 1-2 ways to make it cleaner.
```

### 🚀 Refactoring Spaghetti Code
```markdown
[Role:] Clean Code / SOLID Principles Expert
[Task:] Refactor this method to drastically reduce cognitive complexity.
[Code:]
{paste messy code}

[Constraints:]
- You MUST maintain the exact same input parameters and return type.
- Do not change the business logic. 
- Break large chunks into private helper methods with descriptive names.
- Ensure all variables are properly typed and named clearly.
- Follow Java 17 / TS best practices.
```

### � Fixing a Specific Logical Bug
```markdown
[Role:] Senior Developer
[Task:] I have a logical bug in this method. It is not behaving as expected.
[Code:]
{paste your method/class here}

[Expected Behavior:] {What it should do, e.g., "It should calculate the discount as 10% if the patient is a senior citizen, otherwise 0%."}
[Actual Behavior:] {What it is doing wrong, e.g., "It always returns 0% regardless of age."}

[Constraints:]
- Identify the exact line causing the issue.
- Provide the corrected code.
- Explain the flaw in 1-2 sentences.
- Ensure the fix doesn't break existing tests or introduce edge cases.
```

### 📝 Making a Minor Feature Change
```markdown
[Role:] Senior Developer
[Task:] Make a minor feature change to the provided code.
[Code:]
{paste your component, service, or method here}

[Change Request:] {Describe the change, e.g., "Add a 'middleName' field to the patient creation flow." or "Add a confirmation dialog before deleting."}

[Constraints:]
- Maintain the existing coding style and architecture.
- Do not refactor unrelated parts of portions of the code.
- Only change what is strictly necessary.
- Keep the diff as small and focused as possible.
```

### �🔀 Git Issue Resolver
```markdown
[Task:] Fix my git state. 
[Current Situation:] I am on branch {branch-name}. I accidentally {what you did, e.g., committed to master, merged the wrong branch, wiped my stash}.
[Goal:] I want my local state to be {desired state}. 

Provide exact terminal commands to fix this without losing my uncommitted work.
```

---

## 2. ☕ Spring Boot 3.2 Backend Prompts

### 🏛️ Database Entities & Auditing
```markdown
[Role:] Spring Data JPA Expert
[Task:] Generate a JPA Entity for a Healthcare module.
[Entity Name:] {e.g., PatientEncounter}
[Fields:] 
- {List fields, e.g., String mrn, LocalDate encounterDate, String symptoms}

[Relationships:]
- {e.g., ManyToOne with Patient}
- {e.g., OneToOne with VitalsRecord}

[Constraints:]
- Use Java 17 standards.
- Extend our `BaseAuditEntity` (contains id, createdAt, updatedAt).
- Generate Lombok annotations (`@Getter`, `@Setter`, `@NoArgsConstructor`, `@AllArgsConstructor`, `@Builder`).
- Do NOT use `@Data` on JPA entities.
- Ensure proper cascaded operations (`PERSIST`, `MERGE`).
- Add Jakarta Validation annotations (`@NotNull`, `@Size`, etc.).
- Prevent `LazyInitializationException` by configuring fetching correctly.
```

### 🗄️ Spring Data Repositories & Search
```markdown
[Role:] Database Optimization Expert
[Task:] Create a Spring Data Repository for `{EntityName}`.

[Required Queries:]
1. Find by {field1}
2. Check existence by {field2}
3. Complex query: {Describe the complex search, e.g., Find patients registered last week with status 'ACTIVE' and age > 60}.

[Constraints:]
- Paginate the complex query using `Pageable`.
- If the query is complex, use `@Query` with JPQL instead of derived method names.
- If it requires dynamic filtering (optional params), generate an accompanying `Specification` builder class.
- Avoid N+1 issues; use `@EntityGraph` for heavy relationships.
```

### ⚙️ Service Layer & Business Logic
```markdown
[Role:] Spring Boot Architect
[Task:] Create a Service Interface and Implementation for `{DomainName}`.

[Required Operations:]
1. Create (Takes `{CreateDTO}`)
2. Update (Takes `{UpdateDTO}`, throws ResourceNotFound if missing)
3. Soft Delete
4. Paginated List (Takes `{SearchDTO}`)

[Constraints:]
- Use constructor injection (`@RequiredArgsConstructor`).
- Add `@Transactional` to the class (readOnly=true), and override it for write methods.
- Validate business rules BEFORE database operations: {List business rules, e.g., "MRN must be unique"}.
- Use MapStruct to map between DTOs and Entities.
- Do not log any Patient Health Information (PHI).
```

### 🌐 REST Controllers & API Design
```markdown
[Role:] API Designer
[Task:] Generate a Spring Boot 3.2 REST Controller for `{ResourceName}`.

[Constraints:]
- Base Path: `/api/v1/{resources}`.
- Operations required: GET paginated, GET by ID, POST, PUT, DELETE.
- Use `ResponseEntity<?>`.
- Validate request bodies with `@Valid`.
- Set Swagger/OpenAPI annotations (`@Tag`, `@Operation`, `@ApiResponse`).
- Assign Role-Based Access Control using `@PreAuthorize("hasAnyRole('ADMIN', 'DOCTOR')")`.
- Handle pagination explicitly using `PageableDefault(size=20, sort="createdAt", direction=DESC)`.
```

### 🔒 Spring Security 6 Configuration
```markdown
[Role:] AppSec Engineer
[Task:] Generate a `SecurityFilterChain` bean for Spring Security 6.

[Requirements:]
- Stateless JWT authentication.
- Disable CSRF.
- Public Endpoints: `/api/auth/**`, `/swagger-ui/**`, `/actuator/health`.
- All other endpoints require authentication.
- Add a custom `JwtAuthenticationFilter` before `UsernamePasswordAuthenticationFilter`.
- Configure an AuthenticationEntryPoint to return a 401 JSON response instead of a redirect.
- Configure CORS for frontend: `http://localhost:4200`.

[Constraints:]
- Do NOT use the deprecated `WebSecurityConfigurerAdapter`.
- Write in Java 17 lambda-DSL style.
```

### 📦 MapStruct Mappers
```markdown
[Context:] I have an Entity `{Entity}` and a DTO `{DTO}`.
[Task:] Generate a MapStruct mapper interface mapping them both ways.

[Constraints:]
- Use componentModel = "spring".
- Ignore mapping the `id` and `audit` fields when mapping DTO -> Entity.
- Map the Enum field `{EntityEnum}` to String in DTO.
- Output the interface code.
```

### 📜 Flyway Database Migrations
```markdown
[Role:] PostgreSQL DBA
[Task:] Write a Flyway V1 migration script `.sql` file to create tables for the `{ModuleName}` module.

[Entities involved:]
- {Entity 1: fields...}
- {Entity 2: fields...}

[Constraints:]
- Use PostgreSQL-specific data types (`UUID`, `JSONB` where applicable, `TIMESTAMP WITH TIME ZONE`).
- Add appropriate constraints (`NOT NULL`, `UNIQUE`).
- Define the Foreign Keys with `ON DELETE RESTRICT`.
- Create indexes on frequently searched columns (e.g., `mrn`, `mobile`).
```

---

## 3. 🅰️ Angular 17 Frontend Prompts

### 🧱 Standalone Components (New Angular 17 Syntax)
```markdown
[Role:] Advanced Angular 17 Developer
[Task:] Create a standalone component for `{ComponentName}`.

[Requirements:]
- Use the `@Component` decorator with `standalone: true`.
- Import necessary CommonModule or required standalone modules/directives.
- The component takes an input named `{inputName}` (type: `{InputType}`). Must be required.
- The component emits an output event named `{eventName}` returning `{OutputType}`.
- Use the new Angular 17 Control Flow syntax (`@if`, `@for`, `@empty`) in the HTML, NOT `*ngIf` or `*ngFor`.

[Constraints:]
- Use Signals `input()` instead of `@Input` if possible.
- Use SCSS for styling.
- Keep the component "dumb/presentational" (no HTTP calls inside).
```

### 🚥 State Management with Signals
```markdown
[Role:] Angular Signals Expert
[Task:] Create a local State Service (Service-with-a-Subject pattern replaced by Signals) for managing `{ResourceName}` data.

[Requirements:]
- Define a private `WritableSignal` for the state (array of items, loading boolean, error string).
- Expose public computed, read-only Signals for components to consume.
- Create methods to: `loadData()`, `addItem()`, `updateItem()`, `deleteItem()`.
- Inject the `HttpClient` to do actual network operations before updating the Signal.

[Constraints:]
- Use functional DI (`inject(HttpClient)`).
- Handle HTTP errors gracefully and update the error Signal.
```

### 📝 Reactive Forms with Complex Validation
```markdown
[Role:] Angular Forms Architect
[Task:] Build a Reactive Form (`FormGroup`) for a `{FormPurpose, e.g., Patient Registration}`.

[Fields required:]
- {Field 1: Name, required}
- {Field 2: Mobile, required, must be 10 digits}
- {Field 3: Email, optional, valid email}
- {Field 4: Address, this should be a nested FormGroup}

[Constraints:]
- Use the `FormBuilder` (or `NonNullableFormBuilder`).
- Provide the TypeScript class code linking the form.
- Provide the HTML template using Angular Material (or Bootstrap) showing validation error messages.
- Create ONE custom async validator: {Describe validator, e.g., check if mobile exists in DB}.
```

### 🛡️ Functional Route Guards (v17 style)
```markdown
[Role:] Angular Security Expert
[Task:] Create a functional Route Guard `canActivateFn` for restricting route access.

[Requirements:]
- Inject the `AuthService` and `Router`.
- Check if the user is logged in.
- Check if the user has the role `{RequiredRole}`.
- If true, allow navigation.
- If false, redirect to `/login` with an unauthorized query parameter.

[Constraints:]
- Use the new Angular 14+ functional guard syntax (not class-based `CanActivate`).
```

### 🌐 HTTP Interceptors (Functional)
```markdown
[Role:] Angular Systems Integrator
[Task:] Create a functional HTTP Interceptor `HttpInterceptorFn`.

[Goal:] {State goal: e.g., Add Authorization Bearer Token, Handle 401 Global Errors, or Add a Loading Spinner}

[Constraints:]
- Use functional interceptor syntax. 
- Inject required services via `inject()`.
- For Global Errors: If status is 401, clear local storage and redirect to login, then throw error.
- Clone the request to modify headers safely.
```

### 🌊 RxJS Observables & Leak Prevention
```markdown
[Role:] RxJS Master
[Task:] Write an RxJS pipeline for a search box auto-complete feature.

[Requirements:]
- I have an `FormControl` called `searchControl`.
- Pipe the `valueChanges`.
- Apply `debounceTime` (300ms) and `distinctUntilChanged`.
- Ignore searches less than 3 characters.
- Use `switchMap` to call the `{Service.searchMethod()}` so previous requests are cancelled.
- Handle API errors inside the stream by catching them and returning an empty array `of([])`.

[Constraints:]
- Show how to subscribe in the template using the `async` pipe.
- Show how to unsubscribe properly if doing manual subscription (e.g., `takeUntilDestroyed()`).
```

---

## 4. 🧪 Testing & QA Prompts

### ♨️ Backend: JUnit 5 & Mockito (Spring Boot)
```markdown
[Role:] Java QA Engineer
[Task:] Write comprehensive JUnit 5 tests for this Service class method.
[Code/Method:] {Paste the specific method here}

[Requirements:]
- Use `@ExtendWith(MockitoExtension.class)`.
- Use BDD style commenting (`// Given`, `// When`, `// Then`).
- Write 3 test cases:
  1. Happy Path (successful operation).
  2. Exception Path (resource not found).
  3. Validation/Edge case (e.g., null input).
- Use `verify()` to ensure the repository was called exactly once.

[Constraints:]
- Generate mock objects. Do not hit a real database.
- Use AssertJ `assertThat()` for assertions.
```

### 📐 Frontend: Jasmine / Karma (Angular)
```markdown
[Role:] Angular QA Engineer
[Task:] Write a spec file (`.spec.ts`) for this Angular Component.
[Code:] {Paste component class here}

[Requirements:]
- Setup `TestBed` using `TestBed.configureTestingModule`.
- Provide mock implementations for any injected services using `jasmine.createSpyObj`.
- Write tests to verify:
  1. Component creates successfully (`toBeTruthy()`).
  2. That `{specific method}` updates the state properly.
  3. That an emitted `@Output()` actually fires when the method is called.
```

### 🕸️ E2E: Cypress
```markdown
[Role:] E2E Automation Expert
[Task:] Write a Cypress test script for the `{FeatureName}` flow.

[Scenario:]
1. User visits `/login`.
2. Types `{username}` and `{password}` into data-cy marked inputs.
3. Clicks login button.
4. Asserts the URL changes to `/dashboard`.
5. Asserts a success toast exists.

[Constraints:]
- Use Cypress standard syntax.
- Write custom commands if necessary.
- Intercept the network request to `/api/login` and mock a `200 OK` response with a dummy token.
```

---

## 5. 📄 Documentation & Code Review

### 📝 Write a Professional PR Description
```markdown
[Task:] Write a Pull Request description based on this Git Diff.
[Diff:] {Paste output of git diff}

[Format output as:]
**JIRA Ticket:** [Leave blank]
**Summary:** [1-sentence summary]
**Changes Made:**
- Bulleted list of technical changes.
**How to Test:**
- Step-by-step instructions for the QA/Reviewer.
**Security Considerations:**
- Did this touch authentication or patient data logic? (Yes/No answer based on diff).
```

### 📖 Generate Javadoc / TSdoc
```markdown
[Task:] Generate professional Javadoc (or TSDoc) for this class and its public methods.
[Code:] {Paste code}

[Constraints:]
- Detail the `@param`, `@return`, and `@throws`.
- Briefly explain the business logic the method handles, not just "returns the string".
- Output the code back to me with the comments inserted.
```

### 👁️ Be My Code Reviewer
```markdown
[Role:] Extremely Strict Senior Staff Engineer
[Task:] Perform a code review on this block. Be brutal.
[Code:] {Paste code}

[Review Criteria:]
1. **Security:** (SQL injection, XSS, PHI data exposure, unhandled auth).
2. **Performance:** (N+1 queries, memory leaks, missing indexes, unpaginated arrays).
3. **Clean Code:** (SOLID violations, bad naming, massive methods).

[Output:]
- Severity (Critical, Moderate, Minor)
- Line/Area of concern
- Why it is bad
- Proposed exact code fix
```

---

> **Note to Developers:** Bookmark this document or keep it open in a separate tab while coding. Taking 10 seconds to copy a well-structured prompt will save you 10 minutes of fighting with the AI over bad outputs. 🚀
