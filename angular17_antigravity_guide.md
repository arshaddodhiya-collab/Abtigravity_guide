# 🅰️ Antigravity for Angular 17 Frontend Developers
## The Complete Guide to Efficient AI-Assisted Angular Development

> **Prepared for:** Frontend Development Team — HMIS Product Division  
> **Framework:** Angular 17 (Standalone APIs, Signals, New Control Flow)  
> **Audience:** Junior to Senior Angular Developers  
> **Classification:** Internal — Training Material  
> **Date:** March 2026

---

## Table of Contents

1. [Introduction — Antigravity for Angular Developers](#1-introduction)
2. [Angular 17 — What's New & How Antigravity Helps](#2-angular-17--whats-new--how-antigravity-helps)
3. [Project Setup & Architecture with Antigravity](#3-project-setup--architecture-with-antigravity)
4. [Component Development](#4-component-development)
5. [Services & Dependency Injection](#5-services--dependency-injection)
6. [Reactive Forms & Validation](#6-reactive-forms--validation)
7. [State Management](#7-state-management)
8. [Routing & Navigation](#8-routing--navigation)
9. [HTTP Communication & API Integration](#9-http-communication--api-integration)
10. [RxJS — Mastering Reactive Patterns](#10-rxjs--mastering-reactive-patterns)
11. [Angular Signals](#11-angular-signals)
12. [UI Components & Design Systems](#12-ui-components--design-systems)
13. [Testing — Unit, Integration & E2E](#13-testing--unit-integration--e2e)
14. [Performance Optimization](#14-performance-optimization)
15. [Security Best Practices](#15-security-best-practices)
16. [Error Handling & Logging](#16-error-handling--logging)
17. [Internationalization (i18n)](#17-internationalization-i18n)
18. [Debugging with Antigravity](#18-debugging-with-antigravity)
19. [Code Review & Refactoring](#19-code-review--refactoring)
20. [Angular + HMIS Specific Patterns](#20-angular--hmis-specific-patterns)
21. [Security Guidelines for Antigravity Usage](#21-security-guidelines-for-antigravity-usage)
22. [Prompt Templates — The Angular Cookbook](#22-prompt-templates--the-angular-cookbook)
23. [Anti-Patterns & Common Mistakes](#23-anti-patterns--common-mistakes)
24. [Quick Reference Cheat Sheet](#24-quick-reference-cheat-sheet)

---

## 1. Introduction

### Why This Guide Exists

As Angular frontend developers in an HMIS product company, you work with:

- **Complex healthcare UIs** — patient registration, clinical dashboards, billing screens
- **Sensitive data** — patient details, medical records, prescriptions
- **Strict compliance** — HIPAA, NABH, ABDM data handling rules
- **Evolving framework** — Angular 17 introduces signals, new control flow, deferrable views

Antigravity can **dramatically accelerate** your Angular development — but it must be used **correctly and securely**.

### What Antigravity Can Do for Angular Developers

| Task                                | Time Without AI         | Time With AI | Savings |
| ----------------------------------- | ----------------------- | ------------ | ------- |
| New component scaffolding           | 20-30 min               | 3-5 min      | ~80%    |
| Writing unit tests (full component) | 45-60 min               | 10-15 min    | ~75%    |
| Reactive form with validation       | 30-40 min               | 5-10 min     | ~75%    |
| RxJS operator chains                | 15-20 min (+ debugging) | 3-5 min      | ~70%    |
| Migration (NgModule → Standalone)   | 10-15 min/component     | 2-3 min      | ~80%    |
| CSS/SCSS for responsive layout      | 20-30 min               | 5-8 min      | ~70%    |
| Debugging change detection          | 30-60 min               | 5-10 min     | ~80%    |

---

## 2. Angular 17 — What's New & How Antigravity Helps

### Key Angular 17 Features

| Feature                            | What Changed                                       | How Antigravity Helps                    |
| ---------------------------------- | -------------------------------------------------- | ---------------------------------------- |
| **Standalone Components**          | Default — no NgModules needed                      | Generates standalone-first code          |
| **New Control Flow**               | `@if`, `@for`, `@switch` replace `*ngIf`, `*ngFor` | Converts legacy templates instantly      |
| **Signals**                        | Reactive primitive replacing many RxJS patterns    | Explains signal vs observable trade-offs |
| **Deferrable Views**               | `@defer` for lazy-loading template blocks          | Generates defer patterns with triggers   |
| **View Transitions API**           | Smooth page transitions                            | Creates animation configs                |
| **SSR Hydration**                  | Improved server-side rendering                     | Configures SSR with hydration            |
| **esbuild**                        | Faster builds replacing Webpack                    | Troubleshoots build config               |
| **Functional Guards/Interceptors** | Replace class-based patterns                       | Generates modern functional patterns     |

### Migration Prompt — Legacy to Angular 17

```
Prompt: "Convert this Angular component to Angular 17 standards:

1. Remove NgModule, make standalone with imports array
2. Replace *ngIf with @if, *ngFor with @for (include track)
3. Replace constructor DI with inject() function
4. Replace BehaviorSubject state with Angular Signals
5. Use new @defer for heavy child components
6. Replace class-based guard with functional CanActivateFn

Here is my component:
[Paste sanitized component]"
```

---

## 3. Project Setup & Architecture with Antigravity

### 3.1 Project Structure

```
Prompt: "Suggest an Angular 17 project structure for a large-scale 
HMIS application with the following modules:
- Patient Registration
- Appointment Scheduling
- OPD/IPD Management
- Billing & Invoice
- Lab & Radiology
- Pharmacy
- Reports & Analytics
- User & Role Management

Requirements:
- Standalone components (no NgModules)
- Lazy-loaded feature routes
- Shared component library
- Core services (auth, http, error handling)
- Environment-based configuration
- Follow Angular style guide
- Scalable for 20+ developers working in parallel"
```

**Recommended Structure:**
```
src/
├── app/
│   ├── core/                    # Singleton services, guards, interceptors
│   │   ├── auth/
│   │   │   ├── auth.service.ts
│   │   │   ├── auth.guard.ts
│   │   │   └── auth.interceptor.ts
│   │   ├── http/
│   │   │   ├── api.service.ts
│   │   │   ├── error.interceptor.ts
│   │   │   └── loading.interceptor.ts
│   │   ├── services/
│   │   │   ├── notification.service.ts
│   │   │   ├── storage.service.ts
│   │   │   └── logger.service.ts
│   │   └── models/
│   │       ├── user.model.ts
│   │       └── api-response.model.ts
│   │
│   ├── shared/                  # Reusable components, directives, pipes
│   │   ├── components/
│   │   │   ├── data-table/
│   │   │   ├── confirm-dialog/
│   │   │   ├── search-bar/
│   │   │   ├── patient-card/
│   │   │   └── loading-spinner/
│   │   ├── directives/
│   │   │   ├── permission.directive.ts
│   │   │   └── auto-focus.directive.ts
│   │   ├── pipes/
│   │   │   ├── date-format.pipe.ts
│   │   │   └── currency-inr.pipe.ts
│   │   └── validators/
│   │       ├── phone.validator.ts
│   │       └── date-range.validator.ts
│   │
│   ├── features/                # Feature modules (lazy-loaded)
│   │   ├── patient/
│   │   │   ├── patient-list/
│   │   │   ├── patient-registration/
│   │   │   ├── patient-detail/
│   │   │   ├── services/
│   │   │   ├── models/
│   │   │   └── patient.routes.ts
│   │   ├── appointment/
│   │   ├── billing/
│   │   ├── lab/
│   │   ├── pharmacy/
│   │   └── reports/
│   │
│   ├── layout/                  # Shell components
│   │   ├── header/
│   │   ├── sidebar/
│   │   ├── footer/
│   │   └── main-layout.component.ts
│   │
│   ├── app.component.ts
│   ├── app.config.ts
│   └── app.routes.ts
│
├── assets/
├── environments/
└── styles/
    ├── _variables.scss
    ├── _mixins.scss
    ├── _typography.scss
    └── styles.scss
```

### 3.2 Initial Configuration

```
Prompt: "Generate the app.config.ts for an Angular 17 standalone 
application with:
- provideRouter with lazy-loaded routes and preloading strategy
- provideHttpClient with:
  • withInterceptors([authInterceptor, errorInterceptor, loadingInterceptor])
  • withFetch() for modern HTTP
- provideAnimations()
- Custom providers for environment config
- Error handler provider (custom global ErrorHandler)"
```

---

## 4. Component Development

### 4.1 Smart vs Dumb Component Pattern

```
Prompt: "Create a patient list feature using Smart/Dumb component pattern 
in Angular 17:

SMART (Container) Component — patient-list-page.component.ts:
- Injects PatientService
- Manages state with Signals (patients, loading, error, filters)
- Handles all business logic and side effects
- Passes data DOWN to dumb components via inputs
- Receives events UP from dumb components via outputs

DUMB (Presentational) Components:
1. patient-filter.component.ts — search/filter inputs
   - Input: current filter values
   - Output: filterChange event
2. patient-table.component.ts — displays patient list
   - Input: patients array, loading state
   - Output: select, edit, delete events
3. patient-card.component.ts — single patient card view
   - Input: patient data
   - Output: action events

All components must be:
- Standalone with OnPush change detection
- Use new @if/@for control flow
- Use signal-based inputs (Angular 17.1+)
- Have proper TypeScript interfaces for all data"
```

### 4.2 Component with All Angular 17 Features

```
Prompt: "Create an Angular 17 component for [purpose] that demonstrates:

1. Standalone component (no NgModule)
2. Signal-based state:
   - writable signals for local state
   - computed signals for derived state
   - effect() for side effects
3. New control flow in template:
   - @if / @else for conditionals
   - @for with track for lists
   - @switch for multi-branch
   - @empty for empty state in @for
4. @defer for lazy sections:
   - @defer (on viewport) for below-fold content
   - @loading and @placeholder blocks
5. inject() instead of constructor injection
6. OnPush change detection
7. Signal inputs (input()) and model inputs (model())
8. output() function for event emission

Include the .ts, .html, and .scss files separately."
```

### 4.3 Lifecycle & Change Detection

```
Prompt: "Explain Angular 17's component lifecycle hooks with Signals:

1. Which lifecycle hooks still exist in Angular 17?
2. How do Signals change the way we handle data updates 
   vs the traditional ngOnChanges approach?
3. When to use effect() vs ngOnChanges vs computed()
4. How does OnPush work with Signals vs Input properties 
   vs Observables with async pipe?
5. How does afterNextRender() and afterRender() work?

Provide a comparison table and code examples for each scenario.
Show which approach to use for our HMIS use cases:
- Patient vitals updating in real-time
- Dashboard widgets refreshing on filter change
- Form fields reacting to selections"
```

---

## 5. Services & Dependency Injection

### 5.1 Service Creation

```
Prompt: "Create an Angular 17 service for PatientService:

Base URL: environment.apiUrl + '/api/v1/patients'

Methods with full TypeScript typing:
1. getAll(params: PatientSearchParams): Observable<PagedResponse<PatientListDTO>>
2. getById(id: number): Observable<PatientDetailDTO>
3. create(dto: CreatePatientDTO): Observable<PatientDetailDTO>
4. update(id: number, dto: UpdatePatientDTO): Observable<PatientDetailDTO>
5. delete(id: number): Observable<void>
6. search(query: string): Observable<PatientListDTO[]>
7. getVitals(patientId: number): Observable<VitalSign[]>
8. uploadDocument(patientId: number, file: File): Observable<UploadResponse>

Requirements:
- Use inject(HttpClient) — not constructor injection
- providedIn: 'root'
- Proper error handling using catchError
- Transform API errors into user-friendly messages
- Use generics for the HTTP call wrapper
- Create all TypeScript interfaces/types used

DO NOT include any real patient data in examples."
```

### 5.2 Dependency Injection — Modern Patterns

```
Prompt: "Show me all the modern DI patterns in Angular 17:

1. inject() function — when and how to use
2. InjectionToken — for configuration values
3. providedIn: 'root' vs providedIn: 'any' vs component-level
4. Functional providers with factory functions
5. Multi-providers for plugin architectures
6. inject() with options: { optional: true, self: true, skipSelf: true }
7. makeEnvironmentProviders() for feature providers

For each pattern, show:
- When to use in an HMIS application
- Code example with Angular 17 syntax
- Common mistakes to avoid"
```

---

## 6. Reactive Forms & Validation

### 6.1 Complex Registration Form

```
Prompt: "Create a Patient Registration reactive form in Angular 17:

Form Structure:
├── Personal Info (FormGroup)
│   ├── firstName: required, minLength(2), maxLength(50), namePattern
│   ├── lastName: required, minLength(2), maxLength(50)
│   ├── dateOfBirth: required, notFutureDate (custom validator)
│   ├── gender: required, enum(MALE, FEMALE, OTHER)
│   ├── bloodGroup: optional, enum(A+, A-, B+, B-, O+, O-, AB+, AB-)
│   ├── maritalStatus: optional
│   └── nationality: required, default 'Indian'
│
├── Contact Info (FormGroup)
│   ├── mobile: required, pattern(10-digit Indian mobile)
│   ├── alternateMobile: optional, pattern, notSameAs('mobile')
│   ├── email: optional, email format
│   └── address (FormGroup)
│       ├── line1: required
│       ├── line2: optional
│       ├── city: required
│       ├── state: required (dropdown, cascading from country)
│       ├── pincode: required, pattern(6-digit)
│       └── country: required, default 'India'
│
├── Identity Documents (FormArray)
│   └── Each item:
│       ├── type: required (Aadhaar, PAN, Passport, Driving License)
│       ├── number: required, pattern based on type (dynamic)
│       └── file: optional (upload)
│
├── Emergency Contact (FormGroup)
│   ├── name: required
│   ├── relation: required
│   └── phone: required, pattern
│
└── Insurance Info (FormGroup) — shown only if hasInsurance toggle
    ├── provider: required
    ├── policyNumber: required
    ├── validUntil: required, notPastDate
    └── coverageAmount: required, min(0)

Features:
- Standalone component with inject()
- Custom validators in separate file
- Cross-field validation (alternate mobile ≠ primary mobile)
- Dynamic validation (ID number pattern changes by document type)
- Conditional sections (insurance shown on toggle)
- FormArray: add/remove identity documents
- Form-level error summary
- Dirty check guard (warn on unsaved navigation)
- Submit with loading state
- Reset functionality
- Auto-save draft to localStorage

Use @if/@for in the template.
Use Angular Material or PrimeNG for form controls.

DO NOT use any real patient data — use placeholder labels only."
```

### 6.2 Custom Validators

```
Prompt: "Create a comprehensive custom validators library for 
Angular 17 reactive forms in an HMIS application:

Sync Validators:
1. notFutureDate — date must not be in the future
2. notPastDate — date must not be in the past
3. minAge(years) — DOB check for minimum age
4. maxAge(years) — DOB check for maximum age
5. indianMobile — 10-digit Indian mobile pattern
6. indianPincode — 6-digit pincode
7. aadhaarNumber — 12-digit with Verhoeff checksum
8. panNumber — Indian PAN format (ABCDE1234F)
9. gstNumber — Indian GST format
10. noWhitespace — no leading/trailing spaces
11. matchField(fieldName) — confirm field matches another field
12. uniqueInArray(controlName) — value unique within a FormArray

Async Validators:
1. uniqueEmail(service) — check if email already exists via API
2. uniqueMRN(service) — check if MRN already exists
3. uniqueMobile(service) — check if mobile already registered

For each validator:
- Use ValidatorFn or AsyncValidatorFn factory functions
- Return proper error keys and messages
- Include usage example
- Write unit tests"
```

---

## 7. State Management

### 7.1 Signal-Based State Management

```
Prompt: "Implement a lightweight state management solution using 
Angular 17 Signals for a Patient module:

State Shape:
{
  patients: PatientListDTO[],
  selectedPatient: PatientDetailDTO | null,
  loading: boolean,
  error: string | null,
  filters: {
    searchQuery: string,
    status: 'ALL' | 'ACTIVE' | 'INACTIVE' | 'DISCHARGED',
    department: string | null,
    dateRange: { from: Date, to: Date } | null
  },
  pagination: {
    page: number,
    size: number,
    totalElements: number,
    totalPages: number
  }
}

Create a PatientStore (injectable service) with:
- Private writable signals for each state property
- Public readonly signals (computed where applicable)
- Computed signals:
  • filteredCount: computed from patients + filters
  • hasNextPage: computed from pagination
  • isFirstLoad: computed from patients + loading
- Methods:
  • loadPatients(filters, pagination)
  • selectPatient(id)
  • clearSelection()
  • updateFilters(partial filters)
  • resetFilters()
  • refreshCurrentPage()
- effect() for:
  • Auto-reload when filters change (with debounce)
  • Log state changes in development mode

Compare this approach with NgRx and explain when to use each 
in a large HMIS application."
```

### 7.2 NgRx (for Complex Modules)

```
Prompt: "Implement NgRx state management for the Appointment 
Scheduling module in Angular 17:

1. State interface with:
   - appointments, loading, error, selectedDate, 
     selectedDoctor, viewMode (day/week/month)

2. Actions (use createActionGroup):
   - loadAppointments, loadAppointmentsSuccess, loadAppointmentsFailure
   - createAppointment, updateAppointment, cancelAppointment
   - selectDate, selectDoctor, changeViewMode

3. Reducer using createReducer with on() handlers

4. Effects using createEffect with functional API:
   - Load appointments on date/doctor change
   - Show notification on success/failure
   - Navigate after creation

5. Selectors using createFeatureSelector + createSelector:
   - selectAllAppointments
   - selectAppointmentsByStatus
   - selectAppointmentsForCurrentView (filtered by date range)
   - selectIsLoading
   - selectError

6. Feature registration using provideState and provideEffects

Use standalone APIs only (no StoreModule.forFeature)."
```

---

## 8. Routing & Navigation

### 8.1 Lazy-Loaded Route Configuration

```
Prompt: "Create the complete route configuration for an Angular 17 
HMIS application:

Route Structure:
/login                          — Public
/forgot-password                — Public
/dashboard                      — Protected (all roles)
/patients                       — Protected (DOCTOR, NURSE, ADMIN, RECEPTIONIST)
/patients/:id                   — Protected
/patients/:id/vitals            — Protected (DOCTOR, NURSE)
/patients/:id/prescriptions     — Protected (DOCTOR)
/patients/:id/billing           — Protected (BILLING, ADMIN)
/appointments                   — Protected (all clinical roles)
/appointments/calendar          — Protected
/appointments/:id               — Protected
/billing                        — Protected (BILLING, ADMIN)
/billing/invoices               — Protected
/billing/invoices/:id           — Protected
/lab                            — Protected (LAB_TECH, DOCTOR)
/lab/orders                     — Protected
/lab/results/:id                — Protected
/pharmacy                       — Protected (PHARMACIST, DOCTOR)
/admin/users                    — Protected (ADMIN only)
/admin/roles                    — Protected (ADMIN only)
/admin/settings                 — Protected (ADMIN only)

Requirements:
- All feature routes lazy-loaded with loadChildren
- Functional guards: authGuard, roleGuard(roles[])
- Route resolvers for patient-detail (pre-fetch data)
- Route data for: title, breadcrumb, required roles
- Wildcard route → 404 page
- Error routing for unauthorized (403)
- Layout route (shared header/sidebar wrapping protected routes)
- canDeactivate guard for forms with unsaved changes"
```

### 8.2 Functional Guards

```
Prompt: "Create all route guards for our Angular 17 HMIS application 
using the new FUNCTIONAL guard pattern (not class-based):

1. authGuard: CanActivateFn
   - Check if JWT token exists and is not expired
   - Redirect to /login if not authenticated
   - Store attempted URL for post-login redirect

2. roleGuard: (roles: string[]) => CanActivateFn
   - Check if user has at least one of the required roles
   - Redirect to /403 (forbidden page) if unauthorized
   - Log unauthorized access attempts

3. unsavedChangesGuard: CanDeactivateFn
   - Check if component has unsaved form changes
   - Show confirmation dialog using Angular Material or PrimeNG
   - Allow/block navigation based on user choice

4. patientAccessGuard: CanActivateFn
   - Check if user has access to this specific patient
   - Doctor: only assigned patients
   - Nurse: department-based access
   - Admin: all patients

Use inject() inside guard functions.
Show how to apply guards in route configuration."
```

---

## 9. HTTP Communication & API Integration

### 9.1 HTTP Interceptors

```
Prompt: "Create 4 HTTP interceptors for Angular 17 using the new 
FUNCTIONAL interceptor pattern (HttpInterceptorFn):

1. authInterceptor:
   - Add Bearer token from AuthService to all API requests
   - Skip token for public endpoints (/api/auth/**)
   - Handle token refresh on 401 (using refresh token)
   - Queue concurrent requests during refresh
   - Redirect to login if refresh fails

2. errorInterceptor:
   - Handle HTTP errors globally:
     • 400: Parse validation errors, show toast
     • 401: Handled by authInterceptor
     • 403: Show 'Access Denied' notification
     • 404: Show 'Resource not found' notification
     • 409: Show 'Conflict' notification (duplicate data)
     • 422: Show business rule violation message
     • 500: Show generic error, log full error
     • 0 (network error): Show 'No network' toast
   - Don't show toast if request has 'skipErrorHandling' header

3. loadingInterceptor:
   - Show global loading spinner for requests > 300ms
   - Track concurrent requests (show spinner until ALL complete)
   - Skip loading for requests with 'skipLoading' header
   - Use a LoadingService with Signals

4. loggingInterceptor (dev only):
   - Log request method, URL, duration
   - Log response status and size
   - Highlight slow requests (> 2s) in console
   - Only active in development environment

Show how to register all interceptors in app.config.ts 
using withInterceptors()."
```

### 9.2 API Service Base Class

```
Prompt: "Create a generic base API service class for Angular 17 
that all feature services can extend:

Features:
- Generic CRUD methods: getAll<T>, getById<T>, create<T>, update<T>, delete
- Pagination support with PagedResponse<T> type
- Query parameter builder from filter objects
- File upload with progress tracking
- Request cancellation support (AbortController or takeUntil)
- Retry logic for idempotent requests (GET, PUT)
- Cache support for frequently accessed data (with TTL)
- Custom headers per request

Types to create:
- PagedResponse<T> { content: T[], page, size, totalElements, totalPages }
- ApiError { status, message, fieldErrors?, timestamp }
- SortParams { field, direction }
- FilterParams (generic dictionary)

Example usage:
export class PatientService extends BaseApiService<PatientDTO> {
  constructor() {
    super('/api/v1/patients');
  }
  // Additional custom methods...
}"
```

---

## 10. RxJS — Mastering Reactive Patterns

### 10.1 Essential Operators for HMIS

```
Prompt: "Show me the most important RxJS patterns for an Angular 17 
HMIS application with practical healthcare examples:

1. Search with debounce (patient search):
   - debounceTime(300) + distinctUntilChanged + switchMap
   - Cancel previous request on new input
   - Show loading state during search

2. Auto-refresh (vitals monitor dashboard):
   - timer/interval + switchMap to poll API
   - Pause when tab is not visible
   - Resume on tab focus

3. Concurrent requests (patient detail page):
   - forkJoin to load patient + vitals + appointments together
   - Handle partial failures
   - Show loading until ALL complete

4. Sequential requests (create admission flow):
   - concatMap for ordered operations
   - Create patient → Create encounter → Create bed assignment
   - Rollback on failure

5. Race condition prevention (appointment slot selection):
   - exhaustMap to ignore duplicate clicks
   - Prevent double-booking

6. WebSocket (real-time lab results):
   - webSocket + retry + reconnect
   - Share connection across components

7. Form value changes (cascading dropdowns):
   - valueChanges + switchMap
   - State → City dropdown cascade
   - Department → Doctor dropdown cascade

For each pattern, provide:
- Complete code example
- Why this operator (not an alternative)
- Error handling approach
- Unsubscribe/cleanup strategy"
```

### 10.2 Memory Leak Prevention

```
Prompt: "Create a comprehensive guide for preventing RxJS memory leaks 
in Angular 17:

Show all cleanup strategies with examples:
1. async pipe (preferred for template bindings)
2. takeUntilDestroyed() from @angular/core/rxjs-interop
3. DestroyRef + takeUntilDestroyed(destroyRef) in non-injection contexts
4. Signals replacing observables (no cleanup needed)
5. toSignal() for converting observables to signals
6. take(1) for one-time subscriptions
7. Manual unsubscribe with Subscription (last resort)

For each strategy:
- When to use it
- When NOT to use it
- Code example
- Common mistakes

Also show how to DETECT memory leaks using:
- Angular DevTools
- Chrome DevTools Performance tab
- Console logging of subscription counts"
```

---

## 11. Angular Signals

### 11.1 Complete Signals Guide

```
Prompt: "Create a comprehensive Angular 17 Signals tutorial for 
HMIS frontend development:

Cover these topics with healthcare examples:

1. signal() — basic writable signals
   Example: Patient form editing state

2. computed() — derived signals
   Example: BMI calculated from height + weight signals

3. effect() — side effects
   Example: Auto-save patient notes when content changes

4. input() — signal-based inputs (Angular 17.1+)
   Example: Patient card component receiving patient data

5. output() — signal-based outputs (Angular 17.3+)
   Example: Emitting appointment selection events

6. model() — two-way binding signals
   Example: Toggle switches in settings

7. toSignal() — convert Observable to Signal
   Example: Converting HTTP response to signal

8. toObservable() — convert Signal to Observable
   Example: Feeding signal changes into RxJS pipe

9. linkedSignal() — signal derived from another with reset capability
   Example: Selected tab resets when patient changes

10. resource() — async data fetching with signals
    Example: Loading patient data when ID signal changes

For each:
- Code example with component + template
- When to use vs RxJS alternative
- Pitfalls and gotchas
- Performance implications"
```

### 11.2 Signal vs Observable Decision Guide

```
Prompt: "Create a decision guide: When to use Signals vs Observables 
in Angular 17 for an HMIS application.

Create a comparison table for these scenarios:
1. Simple component state (loading, error, toggles)
2. Form field values
3. HTTP request responses
4. WebSocket streams (real-time vitals)
5. Complex transformations (multiple operators)
6. Shared state across components
7. Event streams (button clicks, keyboard)
8. Timer/interval (auto-refresh)
9. Route params
10. User interactions (drag, scroll)

For each: Signal ✅/❌, Observable ✅/❌, Recommended approach, Why.

Rule of thumb summary at the end."
```

---

## 12. UI Components & Design Systems

### 12.1 Reusable Data Table

```
Prompt: "Create a reusable Angular 17 data table component for 
HMIS applications using [Angular Material / PrimeNG]:

Features:
- Server-side pagination (page, size params sent to API)
- Column sorting (single and multi-column)
- Global search with debounce
- Column-level filters (text, dropdown, date range)
- Row selection (single, multi-select with checkboxes)
- Row actions menu (view, edit, delete, custom actions)
- Expandable rows (for detail view)
- Column show/hide toggle
- Column reordering
- Export to Excel/CSV
- Loading skeleton state while fetching
- Empty state with custom message
- Responsive (horizontal scroll on mobile)
- Keyboard navigation (accessibility)

Inputs:
- columns: ColumnConfig[] (field, header, sortable, filterable, type, width)
- dataSource: Signal<T[]> or Observable<PagedResponse<T>>
- selectable: boolean
- actions: ActionConfig[]
- loading: Signal<boolean>

Outputs:
- pageChange: PageEvent
- sortChange: SortEvent
- filterChange: FilterEvent
- rowSelect: T
- rowAction: { action: string, row: T }

Make it standalone with OnPush change detection."
```

### 12.2 Clinical Dashboard Widgets

```
Prompt: "Create a set of Angular 17 dashboard widget components 
for an HMIS clinical dashboard:

1. StatCard Component
   - Displays: icon, label, value, trend (up/down/neutral)
   - Input: statConfig signal
   - Responsive, animated counter on load
   - Example: 'Active Patients: 245 ↑12%'

2. VitalsChart Component
   - Line chart for patient vitals over time
   - Input: vitals data array, vital type
   - Use Chart.js or ngx-charts
   - Shows normal range bands (green zones)
   - Highlights out-of-range readings in red

3. AppointmentTimeline Component
   - Vertical timeline of today's appointments
   - Color-coded by status (scheduled, in-progress, completed, no-show)
   - Click to view details
   - Current time indicator

4. BedOccupancy Component
   - Ward-wise bed occupancy graphic
   - Shows: total, occupied, available, maintenance
   - Color-coded grid or bar chart
   - Click ward for detail view

All components must:
- Be standalone with OnPush
- Use Signals for state
- Have @defer for lazy rendering
- Include loading skeletons
- Be responsive
- NO real patient data in examples"
```

---

## 13. Testing — Unit, Integration & E2E

### 13.1 Component Testing

```
Prompt: "Write comprehensive Angular 17 tests for a 
PatientListComponent using Jasmine + TestBed:

Component characteristics:
- Standalone component with OnPush
- Injects PatientService (to mock)
- Uses Signals: patients, loading, error, searchQuery
- Template uses @if, @for with track
- Has child components: search-bar, data-table, pagination

Test categories:

1. CREATION TESTS
   - Component creates successfully
   - Default signal values are correct

2. DATA LOADING TESTS
   - Shows loading skeleton when loading signal is true
   - Renders patient list when data arrives
   - Shows empty state when no patients
   - Shows error message on API failure

3. SEARCH TESTS
   - Calls service when search query changes
   - Debounces search input
   - Clears results when search is emptied

4. INTERACTION TESTS
   - Clicking a row navigates to patient detail
   - Pagination change triggers data reload
   - Sort change triggers data reload

5. CHILD COMPONENT INTEGRATION
   - Search bar emits query to parent
   - Data table receives correct inputs
   - Pagination shows correct page info

Use:
- jasmine.createSpyObj for service mocks
- ComponentFixture with detectChanges()
- fakeAsync + tick for async operations
- By.css for DOM queries
- Signal testing patterns (set signal, check DOM)"
```

### 13.2 Service Testing

```
Prompt: "Write unit tests for a PatientService in Angular 17:

Test with HttpClientTestingModule (or provideHttpClientTesting):

1. getAll():
   - Makes GET request to correct URL with params
   - Returns typed PagedResponse<PatientDTO>
   - Handles empty results
   - Handles HTTP error (4xx, 5xx)

2. getById(id):
   - Makes GET request to /patients/{id}
   - Returns typed PatientDetailDTO
   - Handles 404 error
   - Handles null/undefined ID

3. create(dto):
   - Makes POST request with correct body
   - Returns created patient
   - Handles validation error (400)
   - Handles duplicate error (409)

4. search(query):
   - Sends query as URL parameter
   - Returns array of results
   - Handles empty search term

For each test:
- Use HttpTestingController to mock HTTP
- Verify request method, URL, body, headers
- Use flush() to simulate response
- Test error handling with flush(errorBody, errorOptions)
- Use expectOne() for request verification"
```

### 13.3 E2E Testing

```
Prompt: "Create Cypress or Playwright E2E tests for the Patient 
Registration flow in Angular 17:

Flow:
1. Navigate to /patients/register
2. Fill personal info form section
3. Fill contact info with address
4. Add 2 identity documents (use FormArray add)
5. Fill emergency contact
6. Toggle insurance ON, fill insurance details
7. Submit form
8. Verify success notification
9. Verify redirect to patient detail page

Tests:
1. Happy path — complete registration
2. Validation — check all field validations trigger
3. Required fields — submit without filling shows errors
4. Duplicate check — submit existing patient shows error
5. Navigation guard — fill partial form, try to navigate away, 
   confirm dialog appears
6. FormArray — add 3 documents, remove 1, verify 2 remain

Use Page Object pattern for selectors.
Use test data fixtures (NO real patient data).
Include accessibility checks (axe-core)."
```

---

## 14. Performance Optimization

```
Prompt: "Create a comprehensive Angular 17 performance optimization 
guide for our HMIS application:

1. CHANGE DETECTION
   - OnPush everywhere with Signals
   - Avoid function calls in templates
   - Use @defer for heavy components below the fold

2. LAZY LOADING
   - Route-level lazy loading (loadComponent)
   - @defer for template-level lazy loading
   - Virtual scrolling for long lists (patient lists, lab results)
   - Infinite scroll vs pagination trade-offs

3. BUNDLE SIZE
   - Tree-shaking large libraries (lodash, moment → date-fns)
   - Analyze bundle with source-map-explorer
   - Code splitting strategy for HMIS modules
   - Lazy-load Angular Material modules

4. RENDERING
   - trackBy function in @for (and why it matters)
   - Avoid unnecessary DOM elements
   - Use content projection over dynamic components
   - Image optimization (lazy loading, srcset, WebP)

5. NETWORK
   - HTTP caching strategy (ETag, Cache-Control)
   - Request deduplication
   - Preloading strategy for routes: PreloadAllModules vs 
     custom strategy (preload critical modules only)
   - Compress API payloads (pagination, field selection)

6. MEMORY
   - Subscription cleanup (takeUntilDestroyed)
   - Signals reduce subscription overhead
   - Avoid storing large datasets in memory
   - Web Workers for heavy computation (report generation)

For each optimization:
- Before/after code comparison
- Measurable impact
- How to verify the improvement"
```

---

## 15. Security Best Practices

> [!CAUTION]
> This section is **CRITICAL** for HMIS applications handling Protected Health Information (PHI).

### 15.1 Frontend Security Fundamentals

```
Prompt: "Create a security best practices guide for Angular 17 
frontend in an HMIS application:

1. XSS PREVENTION
   - How Angular's built-in sanitization works
   - When bypassSecurityTrustHtml is needed (and when it's DANGEROUS)
   - innerHTML sanitization in templates
   - DomSanitizer proper usage
   - Content Security Policy (CSP) headers

2. AUTHENTICATION
   - JWT storage: localStorage vs sessionStorage vs HttpOnly cookie
   - Token refresh flow (auto-refresh before expiry)
   - Idle timeout (auto-logout after 15 min inactivity)
   - Multi-tab session synchronization
   - Login session on only one device (optional)

3. AUTHORIZATION
   - Route guards for role-based access
   - UI element hiding based on permissions
   - *appHasPermission directive (structural directive)
   - Never rely on frontend-only authorization

4. SENSITIVE DATA HANDLING
   - Never store PHI in localStorage/sessionStorage
   - Clear sensitive data on logout
   - Mask sensitive fields in UI (partial Aadhaar display)
   - Prevent browser auto-fill for sensitive fields
   - Disable copy/paste on critical fields (optional)

5. SECURE COMMUNICATION
   - HTTPS only (redirect HTTP)
   - Certificate pinning considerations
   - CORS configuration
   - CSRF token handling

6. INPUT VALIDATION
   - Always validate on frontend AND backend
   - Sanitize file uploads (type, size, virus scan)
   - Prevent directory traversal in file paths
   - Rate limiting on sensitive operations"
```

### 15.2 Authentication Implementation

```
Prompt: "Implement a complete authentication system for Angular 17:

1. AuthService:
   - login(credentials): store tokens securely
   - logout(): clear ALL sensitive data
   - refreshToken(): auto-refresh before expiry
   - isAuthenticated(): signal returning boolean
   - getCurrentUser(): signal returning UserProfile
   - hasRole(role): computed signal
   - hasPermission(permission): computed signal

2. Idle Timeout Service:
   - Track user activity (mouse, keyboard, touch)
   - Show warning dialog at 13 minutes of inactivity
   - Auto-logout at 15 minutes
   - Reset timer on any user interaction
   - Configurable timeout duration

3. Session Sync across Browser Tabs:
   - Listen to storage events
   - If one tab logs out, all tabs logout
   - If one tab refreshes token, all tabs get new token

4. Login Component:
   - Email/password form with validation
   - Show/hide password toggle
   - Remember me (email only, NOT password)
   - Max login attempts display
   - Redirect to originally requested URL after login

Use Signals for all reactive state.
No class-based guards — use functional guards."
```

### 15.3 Permission Directive

```
Prompt: "Create an Angular 17 structural directive for 
permission-based UI rendering:

Usage examples:
<button *appHasPermission=\"'PATIENT_CREATE'\">Add Patient</button>
<div *appHasRole=\"'DOCTOR'\">Doctor-only content</div>
<menu-item *appHasAnyRole=\"['ADMIN', 'BILLING']\">Billing</menu-item>

Create 3 directives:
1. HasPermissionDirective — show element if user has specific permission
2. HasRoleDirective — show element if user has specific role
3. HasAnyRoleDirective — show element if user has any of the listed roles

Requirements:
- Standalone directives
- Inject AuthService to check permissions
- Reactively update when user role changes (signal-based)
- TemplateRef + ViewContainerRef approach
- Optional 'else' template support
- Log unauthorized access attempts in development mode

Also create a HasPermission pipe for inline usage:
{{ 'PATIENT_EDIT' | hasPermission }}"
```

---

## 16. Error Handling & Logging

```
Prompt: "Create a comprehensive error handling system for Angular 17:

1. GlobalErrorHandler (implements ErrorHandler):
   - Catch all unhandled errors
   - Categorize: HTTP vs JavaScript vs Angular-specific
   - Log to console in dev, send to error tracking service in prod
   - Show user-friendly notification
   - Never expose technical details to users

2. ErrorTrackingService:
   - Buffer errors (don't send every error immediately)
   - Batch send to backend every 30 seconds
   - Include context: URL, user role, component, browser info
   - Rate limit (max 50 errors per minute)
   - Ignore known/benign errors

3. UserNotificationService (Signals-based):
   - success(message): green toast, auto-dismiss 3s
   - error(message): red toast, manual dismiss
   - warning(message): yellow toast, auto-dismiss 5s
   - info(message): blue toast, auto-dismiss 3s
   - confirm(message): dialog with Yes/No
   - Queue multiple notifications
   - Position: top-right
   - Accessible (ARIA live regions)

4. Component-Level Error Boundaries:
   - ErrorBoundary component wrapping feature sections
   - Catches child component errors
   - Shows fallback UI instead of blank screen
   - Retry button to reinitialize the component

IMPORTANT: Error messages must NEVER contain:
- Patient identifiers or data
- Internal system paths or URLs
- Stack traces (in production)
- Database error details"
```

---

## 17. Internationalization (i18n)

```
Prompt: "Set up internationalization for Angular 17 HMIS application:

Requirements:
- Support languages: English, Hindi, Tamil, Telugu, Kannada
- Use Angular built-in i18n OR ngx-translate (compare both, 
  recommend one for our use case)
- Date formatting by locale (Indian format: DD/MM/YYYY)
- Currency formatting: INR with ₹ symbol
- Number formatting: Indian numbering system (12,34,567)
- RTL support (for potential Arabic/Urdu)

Implementation:
1. Translation file structure
2. Language switcher component
3. Pipe for dynamic translations
4. Date/time locale-aware pipe
5. Currency pipe with INR formatting
6. Storing user's language preference
7. Lazy-loading translation files per language

Include example translations for:
- Patient registration form labels
- Dashboard headings
- Error messages
- Button labels"
```

---

## 18. Debugging with Antigravity

### 18.1 Change Detection Issues

```
Prompt: "My Angular 17 component is not updating the UI:

Setup:
- Component uses OnPush change detection
- Data source: [signal / observable / @Input]
- Template uses: [@if / async pipe / direct binding]
- Parent passes [new reference / mutated object]

Behavior:
- Expected: [what should render]
- Actual: [what actually renders]
- Works when I: [any workaround you found]

Explain:
1. Why this happens with OnPush
2. How Angular 17 signals change the equation
3. The correct fix (not just markForCheck hack)
4. How to prevent this in the future"
```

### 18.2 RxJS Debugging

```
Prompt: "Debug this RxJS pipe — it's not emitting values as expected:

[Paste sanitized RxJS pipe chain]

Expected behavior: [describe]
Actual behavior: [describe]
I've verified the source observable emits using tap()

Questions:
1. Walk me through how data flows through each operator
2. Which operator is likely filtering/blocking the emission?
3. Show me how to add debugging tap() operators between steps
4. What operator should I use instead?"
```

### 18.3 Build and Compilation Issues

```
Prompt: "I'm getting this Angular build error:

Error: [sanitized error message]
Angular version: 17.x
Node version: [version]
npm version: [version]

Recent changes:
- [What you changed before the error]

I've tried:
- [Attempt 1]
- [Attempt 2]

Explain the error and give me the fix."
```

---

## 19. Code Review & Refactoring

### 19.1 Code Review with Antigravity

```
Prompt: "Review this Angular 17 component for:

1. Angular best practices (standalone, signals, new control flow)
2. Performance issues (change detection, memory leaks, unnecessary renders)
3. Security concerns (XSS, data exposure, unsafe pipes)
4. Accessibility violations (ARIA, keyboard, screen reader)
5. Responsive design issues
6. Error handling gaps
7. Testing gaps

For each issue:
- Severity: 🔴 Critical / 🟡 Major / 🟢 Minor
- Explanation of the problem
- Suggested fix with code

[Paste sanitized component]"
```

### 19.2 Refactoring Patterns

```
Prompt: "Refactor this Angular component:

Current problems:
1. 300+ lines in one component
2. Mixes business logic with presentation
3. Uses deprecated patterns (NgModule, *ngIf, constructor DI)
4. Has subscriptions without cleanup
5. No error handling
6. Not using OnPush

Refactor to:
1. Smart/Dumb component split
2. Extract service for business logic
3. Angular 17 standalone + signals
4. New control flow syntax
5. Proper error boundaries
6. Full OnPush + signal reactivity

Show the refactored components with explanations."
```

---

## 20. Angular + HMIS Specific Patterns

### 20.1 Patient Search Autocomplete

```
Prompt: "Create a patient search autocomplete component for Angular 17:

Features:
- Searches by: name, MRN, mobile number, Aadhaar (last 4 digits)
- Debounce: 300ms
- Minimum 3 characters to trigger search
- Shows patient photo, name, age/gender, MRN in dropdown
- Recent searches stored in memory (not localStorage — PHI concern)
- Keyboard navigation (arrow keys, enter to select)
- Loading indicator while searching
- 'No results' state with option to register new patient
- Accessible (ARIA combobox pattern)

Security:
- Mask Aadhaar in display (XXXX-XXXX-1234)
- Don't store patient data in browser storage
- Sanitize search input
- Limit results to 20

Use standalone component, signals, and OnPush.
DO NOT include any real patient data."
```

### 20.2 Clinical Form with Auto-Save

```
Prompt: "Create an Angular 17 clinical notes form with auto-save:

Features:
- Rich text editor for clinical notes (use Quill or TipTap)
- Auto-save every 30 seconds (only if content changed)
- Manual save button
- Draft/Final status toggle
- Template selection (pre-fill from templates)
- Version history sidebar (last 5 saves)
- Character count and word count
- Unsaved changes indicator in header
- Conflict detection (if another user edited the same note)

Technical:
- Use Angular Signals for form state
- RxJS for debounced auto-save
- IndexedDB for offline draft storage
- Optimistic UI updates
- Error recovery (retry failed saves)

Security:
- Clinical notes may contain PHI — never cache unencrypted
- Auto-logout must clear draft from memory
- No PHI in console logs"
```

---

## 21. Security Guidelines for Antigravity Usage

> [!CAUTION]
> As frontend developers working on HMIS, you handle patient-facing screens. Follow these rules strictly when using Antigravity.

### 🔴 NEVER Share with Antigravity

| Category                           | Examples                                                                                 |
| ---------------------------------- | ---------------------------------------------------------------------------------------- |
| **Patient Data**                   | Names, MRNs, addresses, diagnoses, prescriptions — even mock data copied from production |
| **Screenshots of Patient Screens** | Any screenshot showing patient information                                               |
| **Environment Files**              | `.env`, `environment.prod.ts` with real API URLs, keys                                   |
| **Auth Tokens**                    | JWT tokens, refresh tokens, OAuth secrets                                                |
| **API Endpoints**                  | Full production API URLs with domain names                                               |
| **Internal Component Names**       | If they reveal business secrets (e.g., `DrugInteractionEngine`)                          |
| **Customer-Specific Configs**      | Tenant IDs, hospital names, deployment configs                                           |

### ✅ Safe to Share (After Sanitization)

| Category                  | How to Sanitize                                                |
| ------------------------- | -------------------------------------------------------------- |
| **Component Code**        | Replace specific entity names with generic ones                |
| **Service Code**          | Replace API URLs with `environment.apiUrl + '/api/v1/...'`     |
| **HTML Templates**        | Remove any hardcoded text that reveals business logic          |
| **SCSS/CSS**              | Generally safe — no secrets in styles                          |
| **TypeScript Interfaces** | Rename sensitive fields: `aadhaarNumber` → `idNumber`          |
| **Error Messages**        | Remove internal references                                     |
| **Test Code**             | Use synthetic data: `{ name: 'Test Patient', mrn: 'MRN-000' }` |

### Sanitization Template

Before pasting Angular code into Antigravity:

```
Pre-Prompt Sanitization Checklist:
□ Removed all hardcoded patient/PHI data
□ Replaced real API URLs with placeholders
□ Removed environment secrets
□ Replaced business-specific entity names if sensitive
□ Removed internal comments referencing clients or deployments
□ Removed console.log statements that might show data
□ Verified no screenshots contain patient information
```

---

## 22. Prompt Templates — The Angular Cookbook

### Quick-Copy Prompt Templates

#### New Component
```
Create an Angular 17 standalone component for [PURPOSE].
- OnPush change detection
- Signals for state: [list state variables]
- Inputs: [list @input/@input signals]
- Outputs: [list events emitted]
- Template: use @if, @for, @defer
- Style: SCSS, responsive, [Angular Material / PrimeNG]
- Include: loading state, error state, empty state
```

#### New Service
```
Create an Angular 17 service for [RESOURCE]:
- Base URL: environment.apiUrl + '/api/v1/[resource]'
- Methods: [list CRUD + custom methods]
- Use inject(HttpClient), providedIn: 'root'
- Return typed Observables
- Error handling with catchError
- Create all required interfaces/types
```

#### Debug Template
```
Angular 17 component issue:
- Component: [type and purpose]
- Change detection: [Default/OnPush]
- State: [signals/observables/inputs]
- Expected: [what should happen]
- Actual: [what happens]
- Tried: [your attempts]
```

#### Test Template
```
Write tests for Angular 17 [component/service/pipe/directive]:
- Test framework: Jasmine + TestBed
- Mock: [list dependencies]
- Test cases:
  1. [Scenario 1]
  2. [Scenario 2]
  3. [Error scenario]
- Use fakeAsync for async, signal testing patterns
```

#### Migration Template
```
Convert this Angular [old version] code to Angular 17:
- Replace NgModule with standalone
- Replace *ngIf/*ngFor with @if/@for
- Replace constructor DI with inject()
- Replace BehaviorSubject with signals where appropriate
- Replace class-based guard with functional guard
- Show before/after comparison
```

---

## 23. Anti-Patterns & Common Mistakes

### ❌ Don't Do This in Angular 17

| Anti-Pattern                                     | Problem                             | Correct Pattern                                        |
| ------------------------------------------------ | ----------------------------------- | ------------------------------------------------------ |
| `subscribe()` in component without cleanup       | Memory leak                         | `takeUntilDestroyed()` or `async` pipe or `toSignal()` |
| Function calls in template: `{{ getTotal() }}`   | Called every change detection cycle | Use `computed()` signal                                |
| `*ngIf` and `*ngFor`                             | Deprecated structural directives    | `@if` and `@for` with `track`                          |
| `constructor(private svc: Service)`              | Old DI pattern                      | `svc = inject(Service)`                                |
| `NgModule` for new components                    | Unnecessary boilerplate             | `standalone: true`                                     |
| Storing PHI in `localStorage`                    | Security violation                  | Memory only, clear on logout                           |
| `bypassSecurityTrustHtml()` without sanitization | XSS vulnerability                   | Use Angular's built-in sanitization                    |
| Business logic in components                     | Violates SRP, untestable            | Extract to services                                    |
| Giant components (500+ lines)                    | Unmaintainable                      | Smart/Dumb split                                       |
| `any` type for API responses                     | No type safety                      | Create proper interfaces                               |
| `console.log` with patient data                  | PHI in browser console              | Use LoggerService with PHI filter                      |
| Hard-coded API URLs                              | Environment mismatch                | Use `environment.apiUrl`                               |
| Missing `trackBy` in `@for`                      | Poor list rendering performance     | Always use `track item.id`                             |
| Manual `ChangeDetectorRef.detectChanges()`       | Fighting the framework              | Fix the root cause (signals, immutability)             |

---

## 24. Quick Reference Cheat Sheet

### Angular 17 Syntax Quick Reference

```typescript
// ── Component ──
@Component({
  selector: 'app-example',
  standalone: true,
  imports: [CommonModule, RouterModule, FormsModule],
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: `...`,
  styleUrl: './example.component.scss'
})
export class ExampleComponent {
  // ── Dependency Injection ──
  private svc = inject(MyService);
  private router = inject(Router);
  private destroyRef = inject(DestroyRef);

  // ── Signals ──
  count = signal(0);
  items = signal<Item[]>([]);
  loading = signal(false);
  
  // ── Computed ──
  total = computed(() => this.items().length);
  isEmpty = computed(() => this.items().length === 0);
  
  // ── Signal Inputs ──
  patientId = input.required<number>();
  showHeader = input(true); // with default
  
  // ── Outputs ──
  selected = output<Item>();
  
  // ── Effects ──
  logEffect = effect(() => {
    console.log('Count changed:', this.count());
  });
}
```

```html
<!-- ── New Control Flow ── -->

<!-- If/Else -->
@if (loading()) {
  <app-spinner />
} @else if (error()) {
  <app-error [message]="error()" />
} @else {
  <app-content [data]="items()" />
}

<!-- For with track and empty -->
@for (item of items(); track item.id) {
  <app-card [data]="item" />
} @empty {
  <p>No items found</p>
}

<!-- Switch -->
@switch (status()) {
  @case ('active') { <span class="badge-green">Active</span> }
  @case ('inactive') { <span class="badge-red">Inactive</span> }
  @default { <span class="badge-grey">Unknown</span> }
}

<!-- Defer -->
@defer (on viewport) {
  <app-heavy-chart [data]="chartData()" />
} @placeholder {
  <div class="chart-placeholder"></div>
} @loading (minimum 500ms) {
  <app-skeleton-chart />
}
```

### When to Ask Antigravity — Decision Guide

| Situation                                 | Ask Antigravity? | Why                              |
| ----------------------------------------- | ---------------- | -------------------------------- |
| "How does `@defer` work?"                 | ✅ Yes            | General framework knowledge      |
| "Generate CRUD service for Patient"       | ✅ Yes            | Boilerplate with sanitized names |
| "Why is my component not rendering?"      | ✅ Yes            | Debugging with sanitized code    |
| "Write tests for my component"            | ✅ Yes            | High-value task for AI           |
| "Review my code for security"             | ✅ Yes            | With sanitized code              |
| "Fix this error: [stack trace]"           | ✅ Yes            | After removing internal paths    |
| "Here's my patient detail page, fix it"   | ⚠️ Sanitize first | Remove all PHI references        |
| "Here's our drug interaction algorithm"   | ❌ Never          | Proprietary business logic       |
| "Use this JWT to test my API"             | ❌ Never          | Credential exposure              |
| "Here's a screenshot of a patient record" | ❌ Never          | PHI in image                     |

---

> **Remember:** Antigravity makes you a **faster** Angular developer — but you must remain a **responsible** one. Sanitize, review, test, and never compromise on security.

---

*This guide should be updated with each Angular major version release and as new Antigravity capabilities emerge.*
