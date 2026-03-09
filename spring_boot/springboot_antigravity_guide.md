# ☕ Antigravity for Spring Boot Backend Developers
## The Complete Guide to Efficient AI-Assisted Java Development

> **Prepared for:** Backend Development Team — HMIS Product Division  
> **Tech Stack:** Java 17 · Spring Boot 3.2 · Spring Security 6 · Spring Data JPA · PostgreSQL  
> **Audience:** Junior to Senior Backend Developers  
> **Classification:** Internal — Training Material  
> **Date:** March 2026

---

## Table of Contents

1. [Introduction — Antigravity for Backend Developers](#1-introduction)
2. [Java 17 + Spring Boot 3.2 — What's New](#2-java-17--spring-boot-32--whats-new)
3. [Project Setup & Architecture](#3-project-setup--architecture)
4. [Entity & Data Modeling](#4-entity--data-modeling)
5. [Repository Layer](#5-repository-layer)
6. [Service Layer & Business Logic](#6-service-layer--business-logic)
7. [REST Controller Layer](#7-rest-controller-layer)
8. [DTOs, Mappers & Validation](#8-dtos-mappers--validation)
9. [Exception Handling](#9-exception-handling)
10. [Spring Security & Authentication](#10-spring-security--authentication)
11. [Database & Migrations](#11-database--migrations)
12. [Caching & Performance](#12-caching--performance)
13. [Async Processing & Events](#13-async-processing--events)
14. [Scheduling & Background Jobs](#14-scheduling--background-jobs)
15. [File Handling & Document Management](#15-file-handling--document-management)
16. [Logging & Monitoring](#16-logging--monitoring)
17. [Testing — Unit, Integration & Contract](#17-testing--unit-integration--contract)
18. [API Documentation (OpenAPI/Swagger)](#18-api-documentation)
19. [Integration Patterns (HL7/FHIR/ABDM)](#19-integration-patterns)
20. [Docker & Deployment](#20-docker--deployment)
21. [Debugging with Antigravity](#21-debugging-with-antigravity)
22. [Code Review & Refactoring](#22-code-review--refactoring)
23. [HMIS-Specific Backend Patterns](#23-hmis-specific-backend-patterns)
24. [Security Guidelines for Antigravity Usage](#24-security-guidelines-for-antigravity-usage)
25. [Prompt Templates — The Spring Boot Cookbook](#25-prompt-templates)
26. [Anti-Patterns & Common Mistakes](#26-anti-patterns--common-mistakes)
27. [Quick Reference Cheat Sheet](#27-quick-reference-cheat-sheet)

---

## 1. Introduction

### What Antigravity Can Do for Spring Boot Developers

| Task                                  | Time Without AI | Time With AI | Savings |
| ------------------------------------- | --------------- | ------------ | ------- |
| JPA Entity with relationships         | 20-30 min       | 3-5 min      | ~80%    |
| CRUD Service + Controller             | 40-60 min       | 8-12 min     | ~75%    |
| JUnit 5 + Mockito test class          | 45-60 min       | 10-15 min    | ~75%    |
| Spring Security configuration         | 30-45 min       | 5-10 min     | ~75%    |
| Exception handler (@ControllerAdvice) | 25-30 min       | 5 min        | ~80%    |
| Flyway migration scripts              | 15-20 min       | 3-5 min      | ~75%    |
| Debugging complex stack traces        | 30-60 min       | 5-10 min     | ~80%    |
| MapStruct mapper with nested objects  | 15-20 min       | 3-5 min      | ~75%    |

> [!IMPORTANT]
> AI-generated code is a **starting point**. You must review, test, and verify every line before committing — especially in healthcare software where bugs can affect patient safety, billing accuracy, and regulatory compliance.

---

## 2. Java 17 + Spring Boot 3.2 — What's New

### Java 17 Features to Use

| Feature                           | How Antigravity Helps                          |
| --------------------------------- | ---------------------------------------------- |
| **Records**                       | Generates DTO records with proper constructors |
| **Sealed Classes**                | Creates sealed hierarchies for domain models   |
| **Pattern Matching (instanceof)** | Refactors legacy instanceof + cast patterns    |
| **Text Blocks**                   | Converts string concatenation to text blocks   |
| **Switch Expressions**            | Modernizes if-else chains                      |
| **Optional Improvements**         | Teaches idiomatic Optional usage               |
| **Stream.toList()**               | Replaces Collectors.toList()                   |

### Spring Boot 3.2 Changes

| Feature               | What Changed                                                                   |
| --------------------- | ------------------------------------------------------------------------------ |
| **Jakarta EE 10**     | `javax.*` → `jakarta.*` package migration                                      |
| **Spring Security 6** | New `SecurityFilterChain` bean config (no more `WebSecurityConfigurerAdapter`) |
| **Observability**     | Micrometer + OpenTelemetry built-in                                            |
| **Virtual Threads**   | Project Loom support (`spring.threads.virtual.enabled=true`)                   |
| **RestClient**        | New declarative HTTP client replacing RestTemplate                             |
| **Problem Details**   | RFC 7807 error responses built-in                                              |
| **GraalVM Native**    | Improved native image support                                                  |

### Migration Prompt

```
Prompt: "Migrate this Spring Boot 2.x code to Spring Boot 3.2:
1. Change javax.* imports to jakarta.*
2. Replace WebSecurityConfigurerAdapter with SecurityFilterChain bean
3. Replace deprecated methods with Spring Boot 3.2 alternatives
4. Use Java 17 features: records for DTOs, pattern matching, text blocks
5. Replace RestTemplate with RestClient
6. Show before/after comparison

[Paste sanitized code]"
```

---

## 3. Project Setup & Architecture

### 3.1 Project Structure

```
Prompt: "Suggest a Spring Boot 3.2 multi-module project structure 
for a large-scale HMIS application with these modules:
- Patient Management
- Appointment Scheduling
- OPD/IPD Management
- Billing & Invoicing
- Laboratory
- Pharmacy
- Radiology
- Reports & Analytics
- User & Role Management
- Notification (Email/SMS/Push)
- Integration (HL7/FHIR)
- Audit & Logging

Requirements:
- Maven multi-module setup
- Clean/Hexagonal architecture per module
- Shared commons module (DTOs, utils, exceptions)
- API Gateway module
- Scalable for 25+ developers working in parallel
- Follow Spring Boot best practices"
```

**Recommended Structure:**
```
hmis-platform/
├── pom.xml                          # Parent POM
│
├── hmis-commons/                    # Shared across all modules
│   ├── src/main/java/
│   │   └── com/company/hmis/commons/
│   │       ├── dto/                 # Common DTOs (PagedResponse, ApiError)
│   │       ├── exception/           # Base exceptions
│   │       ├── util/                # Utility classes
│   │       ├── audit/               # Audit base entity & config
│   │       ├── security/            # Security annotations & utils
│   │       └── constants/           # System-wide constants
│   └── pom.xml
│
├── hmis-patient/
│   ├── src/main/java/
│   │   └── com/company/hmis/patient/
│   │       ├── controller/          # REST controllers
│   │       ├── service/             # Business logic interfaces
│   │       │   └── impl/            # Business logic implementations
│   │       ├── repository/          # Spring Data JPA repositories
│   │       ├── entity/              # JPA entities
│   │       ├── dto/                 # Request/Response DTOs
│   │       │   ├── request/
│   │       │   └── response/
│   │       ├── mapper/              # MapStruct mappers
│   │       ├── validator/           # Custom validators
│   │       ├── event/               # Domain events
│   │       ├── config/              # Module-specific config
│   │       └── spec/                # JPA Specifications for search
│   ├── src/main/resources/
│   │   └── db/migration/            # Flyway migrations for this module
│   ├── src/test/
│   └── pom.xml
│
├── hmis-appointment/                # Same structure as patient
├── hmis-billing/
├── hmis-lab/
├── hmis-pharmacy/
├── hmis-notification/
├── hmis-integration/                # HL7/FHIR/ABDM integrations
├── hmis-audit/                      # Audit trail service
│
├── hmis-api-gateway/                # API Gateway (Spring Cloud Gateway)
│   └── pom.xml
│
└── hmis-app/                        # Main application bootstrapper
    ├── src/main/java/
    │   └── com/company/hmis/
    │       └── HmisApplication.java
    ├── src/main/resources/
    │   ├── application.yml
    │   ├── application-dev.yml
    │   ├── application-staging.yml
    │   └── application-prod.yml
    └── pom.xml
```

### 3.2 Base Configuration

```
Prompt: "Generate the application.yml for a Spring Boot 3.2 
HMIS application with:
- PostgreSQL datasource with HikariCP pool (min 5, max 20)
- JPA/Hibernate config (ddl-auto: validate, show-sql: false, 
  physical naming strategy)
- Flyway migration enabled
- Spring Security defaults
- Jackson config (date format ISO, null handling, 
  snake_case to camelCase)
- Actuator endpoints (health, info, metrics, prometheus)
- Logging config (SLF4J with Logback)
- File upload limits (10MB per file, 50MB total)
- Pagination defaults (page=0, size=20, max-size=100)
- CORS config for Angular frontend (localhost:4200)
- Server compression enabled

Use PLACEHOLDER values for all secrets.
Show separate profiles for dev, staging, prod."
```

---

## 4. Entity & Data Modeling

### 4.1 Base Audit Entity

```
Prompt: "Create a JPA base entity (MappedSuperclass) for our 
HMIS application with:

Audit fields:
- id: Long, auto-generated (IDENTITY strategy)
- createdAt: LocalDateTime, auto-populated, non-updatable
- updatedAt: LocalDateTime, auto-updated
- createdBy: String, auto-populated from SecurityContext
- updatedBy: String, auto-updated from SecurityContext
- version: Long (@Version for optimistic locking)
- deleted: boolean (soft delete, default false)

Include:
- @EntityListeners(AuditingEntityListener.class)
- @PrePersist and @PreUpdate callbacks
- equals/hashCode using ID only (Hibernate-safe)
- toString using only non-lazy fields
- @Where(clause = 'deleted = false') for soft delete

Also create:
- JpaAuditingConfig with @EnableJpaAuditing
- AuditorAware implementation reading from Spring Security
- Use Java 17 features where applicable"
```

### 4.2 Complex Entity with Relationships

```
Prompt: "Create JPA entities for a Patient module in an HMIS system:

Entities:
1. Patient (extends BaseAuditEntity)
   - mrn: String (unique, auto-generated format: MRN-YYYYMMDD-XXXX)
   - firstName, lastName: String (not blank)
   - dateOfBirth: LocalDate
   - gender: Gender (enum: MALE, FEMALE, OTHER)
   - bloodGroup: BloodGroup (enum)
   - maritalStatus: MaritalStatus (enum)
   - nationality: String (default 'Indian')
   - photo: byte[] (@Lob, lazy fetched)
   - status: PatientStatus (enum: ACTIVE, INACTIVE, DECEASED)

2. PatientContact (OneToOne with Patient)
   - mobile, alternateMobile, email
   - address: embedded Address object

3. Address (@Embeddable)
   - line1, line2, city, state, pincode, country

4. PatientIdentity (OneToMany with Patient)
   - type: IdentityType (enum: AADHAAR, PAN, PASSPORT, DL)
   - number: String (encrypted at rest)
   - documentPath: String

5. EmergencyContact (OneToOne with Patient)
   - name, relation, phone

6. PatientInsurance (OneToMany with Patient)
   - provider, policyNumber, validUntil, coverageAmount

Requirements:
- Proper cascade types (no CascadeType.ALL blindly)
- Lazy loading for collections
- Indexed columns for search (name, mrn, mobile)
- @NaturalId for MRN
- Column constraints matching validation rules
- Proper Lombok annotations
- Enums as @Enumerated(STRING)

DO NOT include real patient data in examples."
```

### 4.3 Enum Best Practices

```
Prompt: "Create best-practice enums for an HMIS application in Java 17:

1. Gender — with display name and HL7 code mapping
2. BloodGroup — with display name and compatibility mapping
3. PatientStatus — with allowed transitions (state machine)
4. AppointmentStatus — SCHEDULED, CHECKED_IN, IN_PROGRESS, 
   COMPLETED, CANCELLED, NO_SHOW — with transition validation
5. BillStatus — DRAFT, FINALIZED, PARTIALLY_PAID, PAID, CANCELLED

For each enum include:
- Display name field (for UI)
- Description field
- Static factory fromCode(String) method
- @JsonCreator for deserialization
- Transition validation (e.g., CANCELLED cannot go to COMPLETED)
- Unit tests for transition logic"
```

---

## 5. Repository Layer

### 5.1 Repository with Custom Queries

```
Prompt: "Create a Spring Data JPA repository for Patient entity:

Standard Queries (derived query methods):
- findByMrn(String mrn): Optional<Patient>
- findByMobileNumber(String mobile): Optional<Patient>
- findByFirstNameContainingIgnoreCaseOrLastNameContainingIgnoreCase
- existsByMrn(String mrn): boolean
- countByStatus(PatientStatus status): long

JPQL Queries (@Query):
- Find patients with upcoming appointments in next 7 days
- Find patients by department with pagination
- Search patients by name, MRN, or mobile (combined OR query)
- Find patients registered between dates with status filter

Native Queries:
- Full-text search using PostgreSQL tsvector
- Complex reporting query (patient count by department by month)

Specifications (JpaSpecificationExecutor):
- Dynamic search with any combination of: 
  name, MRN, mobile, gender, status, age range, 
  blood group, registration date range, department

Include:
- @EntityGraph for eager loading specific relations
- Projections (interface-based) for list views
- Pageable support on all list queries
- @Modifying for bulk update queries
- @QueryHints for read-only optimization"
```

### 5.2 Specifications for Dynamic Search

```
Prompt: "Create a comprehensive JPA Specification builder for 
Patient search in Spring Boot 3.2:

Search criteria:
- name: partial match, case-insensitive (firstName OR lastName)
- mrn: exact match
- mobile: exact match
- gender: exact match from enum
- status: exact match or in-list
- ageRange: min-max (calculated from dateOfBirth)
- bloodGroup: exact match
- registrationDateRange: from-to on createdAt
- department: join with Encounter entity
- doctor: join with Encounter → Doctor entity
- hasInsurance: boolean (exists sub-query)

Create:
1. PatientSearchCriteria record (Java 17 record)
2. PatientSpecification class with static builder methods
3. Combine methods using Specification.where().and().or()
4. Handle null criteria gracefully (skip null filters)
5. Example usage in service layer
6. Unit tests for each specification"
```

---

## 6. Service Layer & Business Logic

### 6.1 CRUD Service

```
Prompt: "Create a PatientService interface and implementation in 
Spring Boot 3.2 with clean architecture:

Interface: PatientService
- create(CreatePatientRequest): PatientDetailResponse
- update(Long id, UpdatePatientRequest): PatientDetailResponse
- getById(Long id): PatientDetailResponse
- getAll(PatientSearchCriteria, Pageable): Page<PatientListResponse>
- softDelete(Long id): void
- activate(Long id): void
- deactivate(Long id): void
- findByMrn(String mrn): PatientDetailResponse
- search(String query): List<PatientListResponse>
- uploadPhoto(Long id, MultipartFile): void

Implementation: PatientServiceImpl
Requirements:
- @Service with constructor injection
- @Transactional on all write operations
- @Transactional(readOnly = true) on read operations
- Input validation in a separate PatientValidator class
- Business rule validation:
  • MRN must be unique
  • Mobile must be unique
  • Age must be > 0 (calculated from DOB)
  • Cannot delete a patient with active encounters
- MapStruct for entity ↔ DTO mapping
- Proper exception handling:
  • ResourceNotFoundException (404)
  • DuplicateResourceException (409)
  • BusinessRuleException (422)
- Logging with SLF4J at appropriate levels
- Domain events: PatientCreatedEvent, PatientUpdatedEvent
- Audit: log all state changes

Use Java 17 features (records, pattern matching, Optional).
NO real patient data in code or examples."
```

### 6.2 Complex Business Logic

```
Prompt: "Show me how to implement complex business rules in 
Spring Boot following SOLID principles:

Scenario: Appointment Booking
Business Rules (implement as a chain):
1. Doctor must be active and not on leave for the date
2. Slot must be available (no existing booking)
3. Buffer of 15 min between appointments
4. Patient cannot have 2 appointments with same doctor on same day
5. Emergency appointments bypass rules 2 and 3
6. Walk-in appointments bypass rule 2 time check
7. Telemedicine has separate slot pool

Design with:
- Strategy pattern for different appointment types 
  (Regular, Emergency, Walk-in, Telemedicine)
- Chain of Responsibility for validation rules
- Domain events for post-booking actions (notifications, billing)
- Pessimistic locking to prevent double-booking

Show:
1. Interface and rule classes
2. Service orchestrating the chain
3. Unit tests for each rule
4. Integration test for the full flow"
```

---

## 7. REST Controller Layer

### 7.1 CRUD Controller with Best Practices

```
Prompt: "Create a Spring Boot 3.2 REST controller for /api/v1/patients:

Endpoints:
- GET /                 → Page<PatientListResponse> with pagination, sort, search
- GET /{id}             → PatientDetailResponse
- GET /mrn/{mrn}        → PatientDetailResponse
- POST /                → PatientDetailResponse (201 Created)
- PUT /{id}             → PatientDetailResponse (200 OK)
- PATCH /{id}/status    → void (change status: activate/deactivate)
- DELETE /{id}          → void (204 No Content, soft delete)
- POST /{id}/photo      → void (upload photo)
- GET /{id}/photo       → byte[] (download photo)
- GET /search           → List<PatientListResponse> (quick search)
- GET /export/csv       → CSV file download

Requirements:
- @RestController with constructor injection
- @Valid on all request bodies
- @PreAuthorize for role-based access:
  • GET: DOCTOR, NURSE, ADMIN, RECEPTIONIST
  • POST/PUT: DOCTOR, ADMIN, RECEPTIONIST
  • DELETE: ADMIN only
  • PATCH status: ADMIN only
- Swagger @Operation, @ApiResponse, @Parameter on every endpoint
- ResponseEntity with proper HTTP status codes
- No business logic in controller (delegate to service)
- RequestParam for pagination: page, size, sort (with defaults)
- PathVariable validation (@Positive, @NotBlank)
- Custom @PageableDefault(size = 20, sort = 'createdAt', 
  direction = DESC)
- Log request/response using AOP (no PHI in logs)
- HATEOAS links for navigation (optional)"
```

### 7.2 API Versioning

```
Prompt: "Show me how to implement API versioning in Spring Boot 3.2 
for an HMIS application:

Compare these approaches:
1. URI versioning: /api/v1/patients, /api/v2/patients
2. Header versioning: X-API-Version: 1
3. Media type versioning: Accept: application/vnd.hmis.v1+json

For each approach:
- Implementation code
- Pros and cons
- How to maintain backward compatibility
- How to deprecate old versions

Recommend the best approach for:
- Multiple hospital clients on different API versions
- Mobile app consumers
- Third-party integrators (HL7/FHIR)

Show how to run v1 and v2 side by side with shared service layer."
```

---

## 8. DTOs, Mappers & Validation

### 8.1 DTO Design

```
Prompt: "Create a comprehensive DTO design for Patient module 
using Java 17 records in Spring Boot 3.2:

Request DTOs:
1. CreatePatientRequest — all fields for new patient
2. UpdatePatientRequest — updatable fields only
3. PatientSearchRequest — search/filter parameters

Response DTOs:
1. PatientListResponse — for list/table views (minimal fields)
2. PatientDetailResponse — for detail view (all fields + relations)
3. PatientSummaryResponse — for autocomplete/dropdown (id, name, mrn)

For each DTO:
- Use Java 17 record class
- Jakarta Bean Validation annotations on request DTOs:
  • @NotBlank, @NotNull, @Size, @Pattern, @Email
  • @Past for dateOfBirth
  • Custom @ValidMobile annotation
  • @Valid for nested objects
- @Schema annotations for Swagger documentation
- @JsonFormat for date fields
- Nested records for related data (address, contact)
- Builder pattern where records need flexibility

Show validation error response format matching our API standard."
```

### 8.2 MapStruct Mappers

```
Prompt: "Create MapStruct mappers for Patient module in Spring Boot 3.2:

Mappers needed:
1. PatientMapper:
   - Entity → PatientDetailResponse (include all relations)
   - Entity → PatientListResponse (minimal fields, computed age)
   - Entity → PatientSummaryResponse (for dropdowns)
   - CreatePatientRequest → Entity (ignore id, audit fields)
   - UpdatePatientRequest → update existing Entity (@MappingTarget)

2. AddressMapper:
   - Address entity ↔ AddressDTO (embedded mapping)

3. PatientInsuranceMapper:
   - List<Insurance> → List<InsuranceDTO>

Requirements:
- Use @Mapper(componentModel = 'spring') for DI
- Handle null safety with nullValuePropertyMappingStrategy
- Custom mapping for computed fields (age from DOB)
- Ignore audit fields (@Mapping(target='createdAt', ignore=true))
- Map enums to display strings
- Handle nested object mapping
- Handle collection mapping with null checks
- Unit tests for each mapping method"
```

### 8.3 Custom Validation

```
Prompt: "Create custom Bean Validation annotations and validators 
for an HMIS application in Spring Boot 3.2:

Annotations:
1. @ValidMobile — Indian mobile number (10 digits, starts with 6-9)
2. @ValidAadhaar — 12 digits with Verhoeff checksum
3. @ValidPAN — Indian PAN format (ABCDE1234F)
4. @ValidGST — Indian GST format
5. @ValidPincode — Indian 6-digit pincode
6. @NotFutureDate — date must not be in the future
7. @AgeRange(min, max) — age calculated from date of birth
8. @UniqueField(entity, field) — database uniqueness check
9. @ValidEnum(enumClass) — value must be valid enum constant
10. @FieldsNotEqual(field1, field2) — cross-field: two fields must differ

For each:
- Annotation definition with @Constraint
- ConstraintValidator implementation
- Error message in messages.properties
- Unit test
- Usage example on a DTO"
```

---

## 9. Exception Handling

```
Prompt: "Create a production-grade exception handling system for 
Spring Boot 3.2 HMIS application:

1. Custom Exception Hierarchy:
   - HmisBaseException (abstract, with error code)
     ├── ResourceNotFoundException → 404
     ├── DuplicateResourceException → 409
     ├── BusinessRuleException → 422
     ├── AccessDeniedException → 403
     ├── AuthenticationException → 401
     ├── RateLimitException → 429
     └── IntegrationException → 502

2. Global @ControllerAdvice Handler:
   Map everything to RFC 7807 Problem Detail format:
   {
     'type': '/errors/resource-not-found',
     'title': 'Resource Not Found',
     'status': 404,
     'detail': 'Patient with ID 123 not found',
     'instance': '/api/v1/patients/123',
     'timestamp': '2026-03-07T12:00:00Z',
     'errorCode': 'PATIENT_NOT_FOUND',
     'fieldErrors': []  // only for validation
   }

   Handle:
   - MethodArgumentNotValidException → 400 (field-level errors)
   - ConstraintViolationException → 400
   - HttpRequestMethodNotSupportedException → 405
   - DataIntegrityViolationException → 409
   - HttpMessageNotReadableException → 400
   - MissingServletRequestParameterException → 400
   - MaxUploadSizeExceededException → 413
   - All other exceptions → 500

3. Logging Rules:
   - 4xx → WARN level, no stack trace
   - 5xx → ERROR level, full stack trace
   - NEVER log PHI in error messages

4. Use Spring Boot 3.2's ProblemDetail support

Include unit tests for the handler."
```

---

## 10. Spring Security & Authentication

### 10.1 JWT Authentication

```
Prompt: "Implement complete JWT authentication for Spring Boot 3.2 
+ Spring Security 6 in an HMIS application:

1. SecurityConfig:
   - SecurityFilterChain bean (NOT WebSecurityConfigurerAdapter)
   - Stateless session (STATELESS)
   - Public endpoints: /api/auth/**, /actuator/health, 
     /swagger-ui/**, /v3/api-docs/**
   - All other endpoints authenticated
   - CORS for Angular frontend (localhost:4200)
   - CSRF disabled (stateless)
   - Custom JwtAuthenticationFilter before UsernamePasswordFilter
   - Custom AuthenticationEntryPoint (401 JSON response)
   - Custom AccessDeniedHandler (403 JSON response)
   - Password encoder: BCrypt

2. JwtService:
   - generateAccessToken(user): 15-minute expiry
   - generateRefreshToken(user): 7-day expiry
   - validateToken(token): boolean
   - extractUsername(token): String
   - extractRoles(token): List<String>
   - isTokenExpired(token): boolean
   - Use jjwt library with HS256 or RS256

3. AuthController (/api/auth):
   - POST /login → {accessToken, refreshToken, expiresIn}
   - POST /refresh → {accessToken, newRefreshToken}
   - POST /logout → invalidate refresh token
   - POST /change-password → validate old, set new
   - GET /me → current user profile

4. JwtAuthenticationFilter (OncePerRequestFilter):
   - Extract token from Authorization: Bearer header
   - Validate and parse token
   - Set SecurityContext
   - Handle expired/invalid tokens gracefully

Use placeholder values for JWT secret.
NEVER include real secrets in code."
```

### 10.2 Role-Based Access Control (RBAC)

```
Prompt: "Implement RBAC for an HMIS application in Spring Boot 3.2:

HMIS Roles:
- SUPER_ADMIN: Full system access
- ADMIN: User management, configuration
- DOCTOR: Patient read/write, appointments, prescriptions
- NURSE: Patient read, vitals write, medication administration
- RECEPTIONIST: Registration, appointments
- BILLING: Billing, invoicing, payment
- LAB_TECH: Lab orders, results
- PHARMACIST: Pharmacy, drug dispensing
- RADIOLOGIST: Radiology orders, results

Implementation:
1. User, Role, Permission entities (many-to-many)
2. @PreAuthorize annotations on service methods
3. Custom @RequiresPermission annotation
4. Method-level security configuration
5. Dynamic permission checking service
6. Department-based access (doctor can only see own department)
7. Hierarchy: SUPER_ADMIN inherits all permissions

Show examples:
- @PreAuthorize('hasRole(''DOCTOR'') or hasRole(''ADMIN'')')
- @PreAuthorize('@permissionService.canAccessPatient(#patientId)')
- Custom security expression"
```

---

## 11. Database & Migrations

### 11.1 Flyway Migrations

```
Prompt: "Create Flyway migration scripts for HMIS Patient module 
in PostgreSQL:

V1__create_patient_tables.sql:
- patients table with all columns, constraints, indexes
- patient_contacts table
- patient_identities table
- patient_insurance table
- emergency_contacts table
- Proper foreign keys with ON DELETE behavior
- Indexes on: mrn, mobile, name (for search)
- GIN index for full-text search on patient name
- CHECK constraints for enums
- DEFAULT values
- COMMENT on each column

V2__create_audit_trigger.sql:
- Audit trigger function that logs all changes to audit_log table
- Apply to patients table

V3__seed_master_data.sql:
- Reference data: departments, designations, roles

Naming convention: V{version}__{description}.sql
Include rollback scripts where possible.
Use PostgreSQL-specific features (UUID, JSONB, tsvector)."
```

### 11.2 Query Optimization

```
Prompt: "Help me optimize these database queries for PostgreSQL 
in a Spring Boot HMIS application:

Scenario 1: Patient List with Search
- Table: 500,000+ patients
- Search by: name (partial), MRN (exact), mobile (exact)
- Paginated with sort (default: recently registered)
- Current time: 3.2 seconds
- Target: under 200ms

Scenario 2: Dashboard Statistics
- Active patients today
- Appointments today (by status)
- Bed occupancy by ward
- Revenue today
- Currently running: 12 separate queries, total 5 seconds
- Target: Single optimized query or materialized view

Scenario 3: N+1 Problem
- Loading patient list, each patient has contacts, insurance, 
  and last appointment
- Currently: 1 + 20*3 = 61 queries per page
- Target: 1-3 queries per page

For each scenario:
1. Explain the problem
2. EXPLAIN ANALYZE interpretation
3. Index recommendations
4. Query rewrite
5. Spring Data JPA implementation
6. Caching strategy if applicable"
```

---

## 12. Caching & Performance

```
Prompt: "Implement a comprehensive caching strategy for Spring Boot 3.2 
HMIS application:

1. Spring Cache Setup with Redis:
   - @EnableCaching configuration
   - RedisCacheManager with custom TTL per cache
   - JSON serialization (not Java serialization)
   - Cache key generation strategy
   - Cache error handler (degrade gracefully)

2. Cache Usage Patterns:
   - @Cacheable: Master data (departments, roles, tariffs)
     TTL: 1 hour, evict on update
   - @Cacheable: Patient detail (by ID)
     TTL: 5 minutes, evict on update
   - @CachePut: Update cache on data change
   - @CacheEvict: Clear cache on delete
   - Custom cache key with SpEL

3. What NOT to cache:
   - Real-time vitals data
   - Appointment availability (changes per second)
   - Billing in-progress (consistency critical)
   - Anything with PHI in cache keys

4. Second-Level Cache (Hibernate):
   - Enable for read-heavy entities (master data)
   - Configuration for EhCache or Redis
   - Region-based cache management

5. API Response Caching:
   - HTTP caching headers (ETag, Last-Modified)
   - Cache-Control for static-ish endpoints

Include:
- Performance benchmarks (before vs after)
- Monitoring cache hit/miss ratios
- Cache warming strategy on startup"
```

---

## 13. Async Processing & Events

```
Prompt: "Implement async processing and domain events in 
Spring Boot 3.2 for HMIS:

1. Spring Domain Events:
   - PatientCreatedEvent → trigger: create MRN, send SMS
   - AppointmentBookedEvent → trigger: send notification
   - LabResultFinalizedEvent → trigger: notify doctor, update billing
   - PrescriptionCreatedEvent → trigger: check drug interactions
   - DischargeEvent → trigger: generate summary, update bed

   Implementation:
   - AbstractAggregateRoot for entity event publishing
   - @EventListener methods in separate service classes
   - @Async on event listeners (non-blocking)
   - @TransactionalEventListener(phase = AFTER_COMMIT)
   - Error handling for failed event processing
   - Retry mechanism (Spring Retry)

2. Async Configuration:
   - @EnableAsync with custom ThreadPoolTaskExecutor
   - Pool config: core=5, max=20, queue=100
   - Custom thread name prefix for debugging
   - Async exception handler
   - Virtual threads configuration (Java 21 / Spring Boot 3.2)

3. Message Queue (Kafka/RabbitMQ):
   - When to use sync events vs message queue
   - Producer/Consumer pattern for cross-module communication
   - Dead letter queue for failed messages
   - Idempotent consumers
   - Message ordering guarantees

Include examples for each with unit tests."
```

---

## 14. Scheduling & Background Jobs

```
Prompt: "Implement scheduled tasks for Spring Boot 3.2 HMIS:

1. @Scheduled Tasks:
   - Daily: Generate MIS reports (2 AM)
   - Hourly: Check appointment no-shows (mark after 30 min)
   - Every 15 min: Sync data with external lab system
   - Daily: Clean up expired sessions and temp files
   - Weekly: Generate billing summaries
   - Monthly: Archive old records to cold storage

2. Configuration:
   - @EnableScheduling with custom TaskScheduler
   - Clustered scheduling (ShedLock) — prevent duplicate execution
   - Configurable cron expressions from application.yml
   - Disable scheduling in test profile

3. Job Monitoring:
   - Log job start/end/duration
   - Alert on job failure (email/Slack notification)
   - Job execution history table
   - Health check for long-running jobs

4. Error Handling:
   - Retry policy per job
   - Dead letter logging
   - Circuit breaker for external integrations

Show ShedLock configuration with PostgreSQL for distributed lock."
```

---

## 15. File Handling & Document Management

```
Prompt: "Implement file upload/download for Spring Boot 3.2 HMIS:

Use cases:
- Patient photo upload
- ID document upload (Aadhaar, PAN scans)
- Lab report PDF upload/download
- Discharge summary export
- X-ray/scan image viewing
- Prescription file generation

Implementation:
1. FileStorageService:
   - Upload: validate type, size, scan for malware hints
   - Download: serve with proper Content-Type and Content-Disposition
   - Delete: soft delete with archival
   - Storage: local filesystem (dev) / AWS S3 (prod)
   - Path structure: /patients/{id}/documents/{type}/{uuid}.{ext}

2. Security:
   - File type whitelist (PDF, JPG, PNG, DICOM)
   - Max file size: 10MB (configurable)
   - Virus/malware scanning hook
   - Prevent directory traversal (sanitize filenames)
   - Access control: only authorized roles can access

3. Controller:
   - POST /api/v1/patients/{id}/documents → upload
   - GET /api/v1/patients/{id}/documents → list
   - GET /api/v1/patients/{id}/documents/{docId} → download
   - DELETE /api/v1/patients/{id}/documents/{docId} → soft delete

4. Database:
   - Document metadata entity (not the file itself)
   - Link to patient, type, original name, stored path, size, mime

Include error handling for corrupt files, max size exceeded."
```

---

## 16. Logging & Monitoring

```
Prompt: "Create a production-grade logging and monitoring setup for 
Spring Boot 3.2 HMIS application:

1. Logging Configuration (Logback):
   - JSON log format for production (ELK-compatible)
   - Human-readable for development
   - Log levels: ERROR for prod, DEBUG for dev
   - Separate log files: application, audit, error, security
   - Log rotation: 30 days retention, 100MB per file
   - Async appender for performance

2. PHI-Safe Logging:
   - Custom LogSanitizer utility
   - Mask patient name: 'John Doe' → 'J*** D**'
   - Mask Aadhaar: '123456789012' → 'XXXX-XXXX-9012'
   - Mask MRN: 'MRN-20260101-0001' → 'MRN-****-****'
   - Remove PHI from exception messages before logging
   - @MaskPHI annotation for method parameters

3. Request/Response Logging (AOP):
   - Log: method, URL, params, user, duration, status code
   - Mask request body PHI fields
   - Don't log file upload bodies
   - MDC: correlationId, userId, sessionId for request tracing

4. Audit Logging:
   - All data modifications (who, what, when, before/after)
   - Login/logout events
   - Access to sensitive data
   - Failed authorization attempts
   - Stored in database for compliance

5. Monitoring (Actuator + Micrometer):
   - Custom health indicators (DB, Redis, Kafka, external APIs)
   - Custom metrics (active patients, appointments today)
   - Prometheus endpoint for Grafana dashboards
   - Alert rules for critical thresholds"
```

---

## 17. Testing — Unit, Integration & Contract

### 17.1 Unit Testing

```
Prompt: "Generate comprehensive JUnit 5 + Mockito tests for 
PatientServiceImpl in Spring Boot 3.2:

Test Class Structure:
@ExtendWith(MockitoExtension.class)
- @Mock PatientRepository, PatientMapper, PatientValidator
- @InjectMocks PatientServiceImpl

Test Categories with @Nested:

1. @Nested CreatePatientTests:
   - create_WithValidData_ReturnsPatientResponse
   - create_WithDuplicateMrn_ThrowsDuplicateException
   - create_WithDuplicateMobile_ThrowsDuplicateException
   - create_WithNullRequest_ThrowsIllegalArgument
   - create_VerifiesRepositorySave
   - create_VerifiesEventPublished

2. @Nested GetByIdTests:
   - getById_WithExistingId_ReturnsPatient
   - getById_WithNonExistingId_ThrowsNotFoundException
   - getById_VerifiesRepositoryCall

3. @Nested UpdateTests:
   - update_WithValidData_ReturnsUpdatedPatient
   - update_WithNonExistingId_ThrowsNotFoundException
   - update_WithDuplicateMobile_ThrowsDuplicateException
   - update_DoesNotChangeMrn

4. @Nested DeleteTests:
   - delete_WithExistingId_SoftDeletes
   - delete_WithActiveEncounters_ThrowsBusinessRuleException
   - delete_WithNonExistingId_ThrowsNotFoundException

5. @Nested SearchTests:
   - search_WithCriteria_ReturnsFilteredResults
   - search_WithPagination_ReturnsPage
   - search_WithNoCriteria_ReturnsAll

Use:
- @DisplayName for readable test names
- @ParameterizedTest where applicable
- AssertJ fluent assertions
- ArgumentCaptor for verifying saved entities
- BDDMockito (given/when/then style)
- No real patient data in test fixtures"
```

### 17.2 Integration Testing

```
Prompt: "Generate Spring Boot 3.2 integration tests for 
PatientController using @SpringBootTest + MockMvc:

Setup:
- @SpringBootTest with @AutoConfigureMockMvc
- @Transactional for test isolation
- Testcontainers for PostgreSQL
- @WithMockUser for security context
- Test data factory: PatientTestDataFactory

Test Cases:

1. POST /api/v1/patients:
   - 201: valid creation with full response verification
   - 400: missing required fields (verify field error messages)
   - 400: invalid email format
   - 400: future date of birth
   - 409: duplicate MRN
   - 401: unauthenticated request
   - 403: insufficient role (NURSE trying to create)

2. GET /api/v1/patients/{id}:
   - 200: existing patient with full response verification
   - 404: non-existing ID
   - 401: unauthenticated

3. GET /api/v1/patients?search=&page=&size=:
   - 200: returns paginated results
   - 200: search filters work correctly
   - 200: default pagination (page=0, size=20)
   - 200: empty results

4. PUT /api/v1/patients/{id}:
   - 200: successful update
   - 404: non-existing ID
   - 400: validation errors
   - 403: unauthorized role

5. DELETE /api/v1/patients/{id}:
   - 204: successful soft delete
   - 404: non-existing ID
   - 403: only ADMIN can delete
   - 422: patient has active encounters

Use:
- MockMvcResultMatchers for status, JSON path assertions
- @Sql for test data setup where needed
- @TestPropertySource for test configs
- Verify database state after write operations"
```

---

## 18. API Documentation

```
Prompt: "Set up comprehensive API documentation for Spring Boot 3.2 
HMIS application using Springdoc OpenAPI 3:

1. Configuration:
   - springdoc-openapi-starter-webmvc-ui dependency
   - OpenAPIConfig class with API info, contact, license
   - Security scheme (Bearer JWT)
   - Server URLs (dev, staging, prod)
   - Group APIs by module/tag
   - Customize Swagger UI theme

2. Controller Annotations:
   - @Tag for controller grouping
   - @Operation with summary and description
   - @ApiResponse for each HTTP status code
   - @Parameter for path/query params
   - @RequestBody with @Schema examples
   - @Schema on all DTOs with description and example

3. DTO Documentation:
   Show how to annotate record DTOs with:
   - @Schema(description, example, required)
   - @ArraySchema for collections
   - Enum documentation
   - Nested object documentation

4. Generate:
   - Swagger UI at /swagger-ui.html
   - OpenAPI spec at /v3/api-docs
   - Postman collection export

Show example with Patient endpoints fully documented."
```

---

## 19. Integration Patterns (HL7/FHIR/ABDM)

```
Prompt: "Design integration patterns for an HMIS backend in 
Spring Boot 3.2:

1. HL7 v2 Integration (Lab systems):
   - HAPI library for HL7 message parsing
   - ORM^O01 (lab order), ORU^R01 (lab result) message handling
   - TCP/MLLP listener for incoming messages
   - Message acknowledgment (ACK/NAK)
   - Error handling and retry

2. FHIR R4 Integration:
   - HAPI FHIR library setup
   - Map internal Patient to FHIR Patient resource
   - RESTful FHIR server endpoint
   - FHIR resource validation
   - Bulk data export

3. ABDM (Ayushman Bharat Digital Mission):
   - ABHA ID verification
   - Health record linking
   - Consent management flow
   - Data push/pull patterns

4. General Integration Best Practices:
   - Circuit breaker pattern (Resilience4j)
   - Retry with exponential backoff
   - Timeout configuration
   - Fallback responses
   - Integration health checks
   - Message queue for async integration
   - Idempotency for duplicate messages"
```

---

## 20. Docker & Deployment

```
Prompt: "Create production-ready Docker setup for Spring Boot 3.2 
HMIS application:

1. Multi-stage Dockerfile:
   - Build stage: Maven + JDK 17, skip tests option
   - Runtime: Eclipse Temurin JRE 17 slim
   - Non-root user (appuser:appgroup)
   - Health check: curl /actuator/health
   - JVM flags: -XX:+UseContainerSupport, MaxRAMPercentage
   - ENTRYPOINT with exec form
   - Labels for metadata

2. docker-compose.yml:
   - Application service
   - PostgreSQL 15 with volume, init scripts
   - Redis 7 for caching
   - Kafka + Zookeeper (optional)
   - Nginx reverse proxy
   - Network isolation
   - Environment variables from .env file
   - Health checks for dependencies

3. .dockerignore file

4. Kubernetes manifests (basic):
   - Deployment with resource limits
   - Service (ClusterIP)
   - Ingress
   - ConfigMap and Secret
   - HorizontalPodAutoscaler
   - Liveness and readiness probes

Use PLACEHOLDER values for all secrets and environment specifics."
```

---

## 21. Debugging with Antigravity

### 21.1 Stack Trace Analysis

```
Template:
"Analyze this Spring Boot error:

Framework: Spring Boot 3.2, Java 17
Error Type: [Exception class]
Message: [Sanitized error message]

Sanitized Stack Trace:
[Paste with generic package/class names]

Context:
- What operation was being performed
- What changed recently
- Is it reproducible?

Provide:
1. Root cause explanation
2. Step-by-step fix
3. How to prevent recurrence"
```

### 21.2 Performance Debugging

```
Template:
"My Spring Boot API is slow:

Endpoint: [HTTP method] [URL pattern]
Current response time: [Xms]
Target: [Yms]
Load: [concurrent users]
Database: PostgreSQL [version]

What I know:
- [Any observations from logs/metrics]
- [Hibernate query count if known]
- [HikariCP pool stats if known]

Help me:
1. Identify the bottleneck
2. Add diagnostic logging
3. Optimize the critical path"
```

### 21.3 Common Spring Boot Issues

```
Prompt: "Explain and fix these common Spring Boot issues:

1. LazyInitializationException — accessing lazy collection 
   outside transaction
2. N+1 query problem — detected via Hibernate statistics
3. Circular dependency — bean creation fails
4. @Transactional not working — called from same class
5. @Cacheable not caching — proxy bypass issue
6. @Async not async — called from same bean
7. @Scheduled running twice — multiple instances
8. CORS errors with Angular frontend
9. Jackson serialization infinite recursion — bidirectional JPA
10. Connection pool exhaustion — HikariCP max reached

For each: cause, fix, prevention."
```

---

## 22. Code Review & Refactoring

```
Prompt: "Review this Spring Boot code for:

1. Security: SQL injection, missing auth, data exposure
2. Performance: N+1, missing indexes, no pagination
3. SOLID: SRP violation, tight coupling
4. Error Handling: swallowed exceptions, generic catches
5. Transaction: missing @Transactional, wrong propagation
6. Thread Safety: shared mutable state in singleton beans
7. Healthcare Compliance: PHI in logs, missing audit trail

For each issue:
- Severity: 🔴 Critical / 🟡 Major / 🟢 Minor
- Explanation
- Suggested fix with code

[Paste sanitized code]"
```

---

## 23. HMIS-Specific Backend Patterns

### 23.1 MRN Generation

```
Prompt: "Implement a thread-safe MRN (Medical Record Number) 
generator in Spring Boot 3.2:

Format: MRN-YYYYMMDD-XXXX (e.g., MRN-20260307-0001)
- XXXX resets daily (first patient of each day = 0001)
- Must be unique across the system
- Must be thread-safe (concurrent registrations)
- Must be sequential within a day
- Must handle server restarts (persist last value)

Options to implement and compare:
1. Database sequence
2. Redis atomic increment
3. Pessimistic locking
4. UUID-based alternative

Recommend the best for an HMIS with 500+ registrations/day."
```

### 23.2 Drug Interaction Check

```
Prompt: "Design a drug interaction checking Service in Spring Boot:

Note: I'm asking about the DESIGN PATTERN, not the medical rules.
Use generic/fake drug data for examples.

Service Design:
1. DrugInteractionService interface
2. Rule engine pattern for interaction rules
3. Severity levels: CONTRAINDICATED, MAJOR, MODERATE, MINOR
4. Data source: interaction matrix in database table
5. Cache strategy (drug master data changes infrequently)
6. Response DTO with interactions list and severity
7. Integration point: called before prescription save

Show the pattern — NOT actual medical interaction data."
```

### 23.3 Audit Trail

```
Prompt: "Implement comprehensive audit trail for an HMIS backend 
in Spring Boot 3.2:

What to audit:
- All CRUD operations on clinical entities
- Login/logout events
- Access to sensitive patient data
- Configuration changes
- Role/permission changes
- Failed authentication attempts

Implementation:
1. AuditLog entity:
   - id, timestamp, userId, userName, userRole
   - action (CREATE, UPDATE, DELETE, VIEW, LOGIN, LOGOUT)
   - entityType, entityId
   - oldValue (JSON), newValue (JSON)
   - ipAddress, userAgent, sessionId
   - correlationId (trace ID)

2. AOP-based auditing:
   - @Auditable annotation for service methods
   - Aspect that captures before/after state
   - Async persistence (don't slow down main operation)

3. Query & reporting:
   - Search audit logs by: user, entity, date range, action
   - Compliance report: who accessed what patient data
   - Security report: failed login attempts

4. Retention:
   - Hot storage: 90 days (PostgreSQL)
   - Cold storage: 7 years (archive, compliance)"
```

---

## 24. Security Guidelines for Antigravity Usage

> [!CAUTION]
> As backend developers handling database access, APIs, and business logic, you are the **last line of defense** for data security.

### 🔴 NEVER Share with Antigravity

| Category                   | Examples                                            |
| -------------------------- | --------------------------------------------------- |
| **Database credentials**   | `spring.datasource.url`, username, password         |
| **JWT secrets**            | `jwt.secret`, signing keys                          |
| **API keys**               | Third-party service keys, ABDM credentials          |
| **Production configs**     | `application-prod.yml` with real values             |
| **Patient data**           | Any SQL output, log entries, or test data from prod |
| **Encryption keys**        | Keys for Aadhaar/PAN encryption                     |
| **Infrastructure**         | Server IPs, internal domains, VPN configs           |
| **Proprietary algorithms** | Billing formulas, clinical decision engines         |

### ✅ Safe to Share (After Sanitization)

| Category        | How to Sanitize                                                                          |
| --------------- | ---------------------------------------------------------------------------------------- |
| Entity classes  | Remove `@Table(name)` if it reveals schema, use generic field names for sensitive fields |
| Service code    | Remove business-specific logic, share the pattern                                        |
| Controller code | Replace endpoint paths if they reveal business                                           |
| Configuration   | Replace ALL values with `PLACEHOLDER`                                                    |
| SQL queries     | Replace table/column names if revealing                                                  |
| Stack traces    | Remove internal package names and paths                                                  |
| Test code       | Use synthetic data: `new Patient("TEST", "MRN-000")`                                     |

### Pre-Prompt Checklist

```
Before pasting Spring Boot code into Antigravity:
□ Removed database credentials and connection strings
□ Removed JWT/encryption secrets
□ Removed API keys for external services
□ Replaced production URLs with placeholders
□ Removed patient/PHI data from any examples
□ Stripped internal package names if revealing
□ Removed customer-specific business logic
□ Sanitized log outputs that may contain patient data
```

---

## 25. Prompt Templates

### Quick-Copy Templates

**New Entity:**
```
Create a JPA entity [Name] extending BaseAuditEntity:
Fields: [list fields with types and constraints]
Relationships: [describe OneToMany, ManyToOne, etc.]
Indexes: [columns to index]
Use: Lombok, Java 17, Jakarta validation, soft delete
```

**New Service:**
```
Create a Spring Boot 3.2 service for [Entity]:
Operations: [list CRUD + custom operations]
Business rules: [list validation rules]
Use: @Transactional, MapStruct, constructor injection
Exceptions: ResourceNotFound, Duplicate, BusinessRule
```

**New Controller:**
```
Create a REST controller for /api/v1/[resource]:
Endpoints: [list with HTTP methods]
Roles: [list @PreAuthorize per endpoint]
Include: @Valid, pagination, Swagger annotations
```

**Debug Template:**
```
Spring Boot 3.2, Java 17, PostgreSQL
Error: [sanitized exception + message]
Context: [what operation triggered it]
Tried: [your attempts]
Expected vs Actual: [describe gap]
```

**Test Template:**
```
Generate JUnit 5 + Mockito tests for [Class.method]:
Behavior: [describe what the method does]
Test cases: happy path, [list error cases], edge cases
Use: @ExtendWith, @Nested, @DisplayName, AssertJ, BDDMockito
```

---

## 26. Anti-Patterns & Common Mistakes

| Anti-Pattern                                    | Problem                             | Correct Pattern                                     |
| ----------------------------------------------- | ----------------------------------- | --------------------------------------------------- |
| `@Autowired` field injection                    | Untestable, hidden dependencies     | Constructor injection or `@RequiredArgsConstructor` |
| Business logic in controller                    | Violates SRP, untestable            | Delegate to service layer                           |
| Returning entities from controller              | Exposes DB schema, lazy load issues | Use DTOs mapped via MapStruct                       |
| `CascadeType.ALL` everywhere                    | Unintended deletes, performance     | Choose specific cascade types                       |
| No `@Transactional(readOnly=true)` on reads     | Missed Hibernate optimization       | Add to all read methods                             |
| `@Transactional` on private methods             | Spring proxy can't intercept        | Must be public                                      |
| Calling `@Transactional` method from same class | Bypasses proxy                      | Extract to separate bean                            |
| Catching `Exception` generically                | Swallows important errors           | Catch specific exceptions                           |
| PHI in log statements                           | Compliance violation                | Use `LogSanitizer` utility                          |
| Hardcoded secrets in code                       | Security breach risk                | Use environment variables / Vault                   |
| No pagination on list endpoints                 | Memory explosion with large data    | Always return `Page<T>`                             |
| `findAll()` without filters                     | Full table scan                     | Always accept search criteria                       |
| Missing `@Version` for optimistic locking       | Lost updates in concurrent edits    | Add version field                                   |
| `new Date()` in entity                          | Not timezone-safe                   | Use `LocalDateTime` or `Instant`                    |
| Raw SQL with string concatenation               | SQL injection                       | Use parameterized queries / Specifications          |
| `@Modifying` without `@Transactional`           | No transaction context              | Always pair them                                    |
| No index on foreign key columns                 | Slow joins                          | Add `@Index` on FK columns                          |

---

## 27. Quick Reference Cheat Sheet

### Spring Boot 3.2 + Java 17 Syntax

```java
// ── Entity ──
@Entity
@Table(name = "patients", indexes = {
    @Index(name = "idx_patient_mrn", columnList = "mrn", unique = true)
})
@Where(clause = "deleted = false")
@Getter @Setter @NoArgsConstructor @AllArgsConstructor @Builder
public class Patient extends BaseAuditEntity {
    @Column(nullable = false, unique = true, length = 20)
    private String mrn;
    
    @Enumerated(EnumType.STRING)
    private PatientStatus status;
    
    @OneToMany(mappedBy = "patient", cascade = {PERSIST, MERGE}, 
               orphanRemoval = true)
    private List<PatientInsurance> insurances = new ArrayList<>();
}

// ── Record DTO (Java 17) ──
public record CreatePatientRequest(
    @NotBlank @Size(max = 50) String firstName,
    @NotBlank @Size(max = 50) String lastName,
    @NotNull @Past LocalDate dateOfBirth,
    @NotNull Gender gender
) {}

// ── Service ──
@Service
@RequiredArgsConstructor
@Transactional(readOnly = true)
public class PatientServiceImpl implements PatientService {
    private final PatientRepository repository;
    private final PatientMapper mapper;
    
    @Override
    @Transactional
    public PatientDetailResponse create(CreatePatientRequest request) {
        // validate → map → save → map → return
    }
}

// ── Controller ──
@RestController
@RequestMapping("/api/v1/patients")
@RequiredArgsConstructor
@Tag(name = "Patient", description = "Patient Management APIs")
public class PatientController {
    private final PatientService service;
    
    @PostMapping
    @PreAuthorize("hasAnyRole('ADMIN', 'DOCTOR', 'RECEPTIONIST')")
    @Operation(summary = "Create a new patient")
    public ResponseEntity<PatientDetailResponse> create(
            @Valid @RequestBody CreatePatientRequest request) {
        return ResponseEntity.status(CREATED).body(service.create(request));
    }
}

// ── Security (Spring Security 6) ──
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    return http
        .csrf(AbstractHttpConfigurer::disable)
        .sessionManagement(s -> s.sessionCreationPolicy(STATELESS))
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/api/auth/**").permitAll()
            .anyRequest().authenticated())
        .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)
        .build();
}
```

### When to Ask Antigravity — Decision Guide

| Situation                 | Ask?                     | Notes                       |
| ------------------------- | ------------------------ | --------------------------- |
| Generate CRUD boilerplate | ✅ Yes                    | High-value, low-risk        |
| Write unit tests          | ✅ Yes                    | Sanitize class under test   |
| Debug stack trace         | ✅ Yes                    | Remove internal paths       |
| Design patterns question  | ✅ Yes                    | Pure knowledge, no risk     |
| Optimize SQL query        | ✅ Yes                    | Use generic table names     |
| Spring Security config    | ✅ Yes                    | Use placeholder secrets     |
| Code review               | ✅ Yes                    | Sanitize first              |
| Billing algorithm logic   | ❌ No                     | Proprietary                 |
| Drug interaction rules    | ❌ No                     | Clinical IP                 |
| Production config fixes   | ❌ No                     | Contains secrets            |
| Patient data issues       | ❌ No                     | PHI violation               |
| Encryption implementation | ⚠️ Ask about pattern only | Don't share keys/algorithms |

---

> **Remember:** Antigravity makes you a **faster** Java developer, but as a backend engineer you are the **guardian** of data integrity, security, and compliance. Sanitize, review, test, and never compromise.

---

*This guide should be updated with each Spring Boot major version release and as new Antigravity capabilities emerge.*
