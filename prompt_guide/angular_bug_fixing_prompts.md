# 🅰️ Angular 17 Bug Fixing Prompt Dictionary
## HMIS Frontend Developer Guide to AI-Assisted Debugging

> **Context:** Product-Based Company (HMIS) | Final Delivery / Bug Fix Phase
> **Tech Stack:** Angular 17, TypeScript, RxJS, NgRx/Signals, Angular Material

---

### Introduction
During the bug-fixing phase, reproducing and diagnosing frontend issues can be time-consuming, especially with asynchronous data streams (RxJS) and complex UI state. Use these specialized prompt templates to let Antigravity diagnose the issue instantly.

> ⚠️ **SECURITY REMINDER:** NEVER paste actual patient data (names, IDs, health records) or API URLs into your prompts.

---

## 1. UI & Rendering Bugs

### 🐛 Change Detection / View Not Updating
```markdown
[Role:] Expert Angular 17 UI Architect
[Task:] Diagnose why my Angular component view is not updating when the data changes.

[Component Code:]
{paste sanitized component class and HTML template here}

[Issue:] The `patientList` array is updating in the console, but the HTML table is not reflecting the new data.
[Context:] We are using `ChangeDetectionStrategy.OnPush`. The data is being updated inside a `.subscribe()` block.

[Constraints:]
- Explain why OnPush is blocking the render.
- Provide the exact code fix (e.g., using `ChangeDetectorRef.markForCheck()`, switching to an `async` pipe, or using an Angular 17 Signal).
- Maintain existing architecture as much as possible.
```

### 🐛 Angular 17 Control Flow (@if / @for) Migration or Logic Error
```markdown
[Role:] Angular 17 Expert
[Task:] I have a rendering issue with the new Angular 17 control flow syntax.

[Code:]
{paste HTML template with @if / @for and relevant component logic}

[Issue:] The `@for` loop is rendering duplicates / The `@if` condition is flashing before the data loads.
[Context:] I migrated this from `*ngFor` / `*ngIf`. 

[Constraints:]
- Ensure the `track` expression in the `@for` loop is correct for performance.
- Provide the corrected HTML.
- Explain the logic flaw in 1 sentence.
```

---

## 2. Asynchronous & Data Flow Bugs

### 🐛 RxJS Memory Leak / Multiple Subscriptions
```markdown
[Role:] Senior RxJS Developer
[Task:] Analyze this component for potential RxJS memory leaks and fix them.

[Component Code:]
{paste component class here}

[Issue:] When navigating away from this component and returning, the API calls are duplicating, suggesting a memory leak.
[Context:] The component subscribes to `PatientService.getUpdates()` in `ngOnInit`.

[Constraints:]
- Refactor the code to properly unsubscribe.
- Use the modern Angular 16+ `takeUntilDestroyed()` operator if applicable, or the `async` pipe.
- Do NOT change the business logic of what happens inside the subscribe block.
```

### 🐛 Race Conditions in API Calls
```markdown
[Role:] Angular Systems Integrator
[Task:] Fix a race condition in my RxJS HTTP calls.

[Code:]
{paste service or component doing the HTTP calls}

[Issue:] When the user types quickly in the search box, older API responses overwrite newer ones.
[Context:] We are using `valueChanges` on a FormControl to trigger patient search.

[Constraints:]
- Refactor the pipeline to cancel previous pending requests.
- Use the appropriate flattening operator (`switchMap`, `concatMap`, `exhaustMap`) and explain WHY it is the correct choice here.
- Include a `debounceTime` to reduce API load.
```

---

## 3. Form & Validation Bugs

### 🐛 Reactive Form Validation Not Triggering
```markdown
[Role:] Angular Forms Expert
[Task:] Find out why my Reactive Form validation state is incorrect.

[Code:]
{paste component class building the form and the HTML template}

[Issue:] The "Submit" button remains disabled even when all visible fields are filled out, OR the custom validator is not firing.
[Context:] This is physical exam form for the HMIS. The fields are added dynamically via a `FormArray`.

[Constraints:]
- Identify which control is remaining `INVALID` or `PENDING`.
- If it's an async validator issue, ensure it's completing correctly.
- Provide the fixed code for both the TS and HTML.
```

---

## 4. State Management Bugs

### 🐛 Signal State Out of Sync
```markdown
[Role:] Angular Signals Expert
[Task:] Debug my Angular 17 Signals implementation.

[Code:]
{paste component or service code using Signals}

[Issue:] A `computed()` signal is not updating when the underlying `WritableSignal` changes.
[Context:] I am trying to recalculate the total patient bill when a new service is added.

[Constraints:]
- Explain why the dependency tracking inside the `computed()` might be failing (e.g., mutating an array instead of creating a new reference).
- Provide the corrected `.set()` or `.update()` logic.
```

### 🐛 NgRx Action / Reducer Issue (For Legacy/Complex Modules)
```markdown
[Role:] NgRx Architect
[Task:] Find out why my NgRx state is not updating after an action is dispatched.

[Code:]
{paste Action, Reducer, and Effect files}

[Issue:] The `[Patient] Update Success` action fires in Redux DevTools, but the UI component selecting the state does not re-render.
[Context:] The state interface contains a nested object.

[Constraints:]
- Check for state mutation inside the reducer.
- Provide the corrected reducer code using the spread operator (`...`) properly.
```

---

## 5. Build & Routing Bugs

### 🐛 Circular Dependency Warning
```markdown
[Role:] Angular Build Expert
[Task:] Fix a circular dependency warning during the Angular build.

[Warning Output:]
{paste the specific warning from the CLI}

[Files Involved:]
{paste the imports section of the 2-3 files involved}

[Issue:] File A imports File B, which imports File A.
[Context:] This usually happens between our Models/Interfaces and Services.

[Constraints:]
- Recommend an architectural fix (e.g., refactoring interfaces into a shared file).
- Provide the steps to reorganize the code safely.
```

### 🐛 Lazy Loaded Route Failing
```markdown
[Role:] Angular Router Expert
[Task:] Diagnose why a lazy-loaded route is failing to load or throwing an error in Angular 17.

[Code:]
{paste app.routes.ts and the lazy-loaded route file}

[Issue:] Clicking the link to the Dashboard throws an error in the console and fails to navigate.
[Context:] We are using Angular 17 default `loadComponent` or `loadChildren`.

[Constraints:]
- Check for standalone component import conflicts.
- Check functional guard (`canActivateFn`) logic that might be silently rejecting the route without a redirect.
- Provide the fixed routing configuration.
```
