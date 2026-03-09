# ☕ Spring Boot 3.2 Bug Fixing Prompt Dictionary
## HMIS Backend Developer Guide to AI-Assisted Debugging

> **Context:** Product-Based Company (HMIS) | Final Delivery / Bug Fix Phase
> **Tech Stack:** Java 17, Spring Boot 3.2, Spring Security 6, Hibernate/JPA, PostgreSQL

---

### Introduction
Backend bugs in an HMIS application are often related to data persistence, transaction boundaries, or complex security rules. Use these specialized prompt templates to let Antigravity diagnose the issue instantly.

> ⚠️ **SECURITY REMINDER:** NEVER paste actual database credentials, JWT secrets, or production environment variables into your prompts.

---

## 1. Database & Hibernate/JPA Bugs

### 🐛 LazyInitializationException
```markdown
[Role:] Spring Data JPA Expert
[Task:] Fix a `LazyInitializationException` in my Spring Boot application.

[Stack Trace:]
{paste sanitized stack trace}

[Code:]
{paste the Entity class showing the relationships, and the Service/Controller method where the error occurs}

[Issue:] The code crashes when trying to access `patient.getInsurances()` inside the controller or mapper.
[Context:] The `insurances` list is mapped as `@OneToMany(fetch = FetchType.LAZY)`.

[Constraints:]
- Do NOT simply change the fetch type to `EAGER` (this degrades performance).
- Provide the architectural fix: either moving the operation inside the `@Transactional` boundary OR using `@EntityGraph` / `JOIN FETCH` in the repository query.
- Provide the exact corrected code.
```

### 🐛 N+1 Query Problem (Performance Bug)
```markdown
[Role:] Database Optimization Expert
[Task:] Resolve an N+1 query issue detected by Hibernate statistics.

[Code:]
{paste the Repository and the Service method doing the iteration}

[Issue:] When fetching a list of 50 patients, Hibernate executes 1 query for the patients, and 50 additional queries to fetch their emergency contacts.
[Context:] We are paginating the `Patient` list.

[Constraints:]
- Write the correct optimized Spring Data `@Query` using `JOIN FETCH` or configure an `@EntityGraph`.
- Ensure pagination (`Pageable`) still works correctly in memory without throwing the "firstResult/maxResults specified with collection fetch" warning.
```

### 🐛 Transaction Rollback Failure
```markdown
[Role:] Spring Transaction Architect
[Task:] Figure out why my database transaction is not rolling back on an error.

[Code:]
{paste the Service class with transaction annotations}

[Issue:] If step 3 of this method throws a checked exception, the database changes from step 1 are STILL being committed.
[Context:] The method is annotated with `@Transactional`.

[Constraints:]
- Explain how Spring handles checked vs. unchecked exceptions for rollbacks.
- Correct the `@Transactional` annotation (e.g., `rollbackFor = Exception.class`).
- Ensure the fix adheres to clean architecture.
```

---

## 2. Security & Authentication Bugs

### 🐛 403 Forbidden on Valid Token (Spring Security 6)
```markdown
[Role:] Spring Security 6 Expert
[Task:] Debug why an authenticated user is getting a 403 Forbidden error.

[Code:]
{paste your SecurityFilterChain configuration bean and the relevant Controller method with @PreAuthorize}

[Issue:] The user logs in successfully, receives a JWT, passes the filter, but the `@PreAuthorize("hasRole('DOCTOR')")` endpoint returns 403.
[Context:] My JWT filter parses roles as "ROLE_DOCTOR". Spring Security 6 is being used.

[Constraints:]
- Check if Spring Security is double-prefixing "ROLE_" automatically.
- Check if `@EnableMethodSecurity` is present.
- Provide the configuration change required to fix the role mismatch.
```

### 🐛 CORS Preflight Error
```markdown
[Role:] AppSec Integrator
[Task:] Fix a CORS (Cross-Origin Resource Sharing) blocked error.

[Browser Error:]
{paste CORS error from browser console}

[Code:]
{paste your WebMvcConfigurer or SecurityFilterChain CORS configuration}

[Issue:] GET requests work, but POST/PUT requests from the Angular frontend running on localhost:4200 are blocked by CORS policy.
[Context:] The frontend is sending an `Authorization` header.

[Constraints:]
- Provide the exact Spring Boot configuration to explicitly allow CORS for the required methods and headers.
- Explain why the preflight `OPTIONS` request was failing.
```

---

## 3. Business Logic & Data Flow Bugs

### 🐛 Null Pointer Exception (NPE) in Deeply Nested Object
```markdown
[Role:] Senior Java 17 Developer
[Task:] Fix a `NullPointerException` elegantly using modern Java features.

[Stack Trace:]
{paste sanitized NPE trace}

[Code:]
{paste the method causing the issue}

[Issue:] We are trying to access `patient.getAddress().getCity().getName()`, but sometimes `Address` or `City` is null.
[Context:] This data comes from an external HL7/FHIR integration, so data quality varies.

[Constraints:]
- Do not write massive `if(x != null)` blocks.
- Refactor the code using Java `Optional` chaining (`Optional.ofNullable().map()`) to handle the nulls safely.
- Provide the updated method.
```

### 🐛 Optimistic Locking Exception
```markdown
[Role:] Enterprise Application Architect
[Task:] Handle an `ObjectOptimisticLockingFailureException`.

[Code:]
{paste the Entity and the Service update method}

[Issue:] When two receptionists try to update the same appointment slot simultaneously, one gets a 500 server error stack trace.
[Context:] The entity has an `@Version` field.

[Constraints:]
- Explain to the user what happened in a friendly, user-facing error message.
- Provide a `@ControllerAdvice` global exception handler specifically for this error that returns a 409 Conflict with a clear message.
- How can we optionally implement retry logic here?
```

---

## 4. Build, Serialization, & Configuration Bugs

### 🐛 Jackson Infinite Recursion (StackOverflowError)
```markdown
[Role:] API Serialization Expert
[Task:] Fix an infinite recursion error during JSON serialization.

[Code:]
{paste the two Entities causing the loop, e.g., Patient and PatientEncounter}

[Issue:] When returning a `Patient` object from the REST controller, Jackson gets stuck in an infinite loop parsing Patient -> Encounter -> Patient -> Encounter until memory runs out.
[Context:] They have a bidirectional `@OneToMany` / `@ManyToOne` relationship.

[Constraints:]
- Provide the cleanest fix (e.g., `@JsonManagedReference` / `@JsonBackReference`, or better yet, mapping it to a `DTO` instead of returning the raw entity).
- Highly recommend the DTO approach and show how MapStruct handles this.
```

### 🐛 Circular Dependency in Beans
```markdown
[Role:] Spring Boot Context Expert
[Task:] Resolve a circular dependency preventing the application from starting.

[Error:]
`The dependencies of some of the beans in the application context form a cycle:`
{paste the cycle graph from the console}

[Context:] `BillingService` needs `NotificationService` to send a receipt, but `NotificationService` needs `BillingService` to check the balance.

[Constraints:]
- Do NOT use `@Lazy` unless absolutely necessary (it masks bad design).
- Recommend an architectural refactor: extract the shared logic into a third service, or use Spring Application Events (`@EventListener`) to decouple them.
- Provide the modified code structure for the Event-driven approach.
```
