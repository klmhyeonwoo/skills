---
name: frontend-fundamental-review
description: This skill should be used when the user asks to "코드 리뷰해줘", "review this code", "코드 리뷰 부탁해", "이 코드 봐줘", "코드 검토해줘", "코드 리뷰해", "review my code", "check my code", or any other code review request. Reviews code against Toss Frontend Fundamentals guidelines across readability, cohesion, coupling, and predictability. Reports issues with concrete improvement suggestions.
version: 1.0.0
---

Review the following code against the Toss Frontend Fundamentals code quality guidelines.

**Always respond in Korean.**

For each issue found, report in this format:

**[Category] Rule Name**
- Problem: (what code is problematic and why)
- Improvement: (concrete improved code)

The review criteria are the 17 guidelines below:

---

## Readability

### 1. Read comparisons left to right (comparison-order)
Write range conditions in the same direction as math inequalities: `min <= value <= max`.
```typescript
// BAD
if (score >= 80 && score <= 100) { ... }
if (price >= minPrice && price <= maxPrice) { ... }

// GOOD
if (80 <= score && score <= 100) { ... }
if (minPrice <= price && price <= maxPrice) { ... }
```

### 2. Name complex conditions (condition-name)
Extract complex boolean expressions into named variables to reduce cognitive load.
```typescript
// BAD
const result = products.filter((product) =>
  product.categories.some(
    (category) =>
      category.id === targetCategory.id &&
      product.prices.some((price) => price >= minPrice && price <= maxPrice)
  )
);

// GOOD
const matchedProducts = products.filter((product) => {
  return product.categories.some((category) => {
    const isSameCategory = category.id === targetCategory.id;
    const isPriceInRange = product.prices.some(
      (price) => price >= minPrice && price <= maxPrice
    );
    return isSameCategory && isPriceInRange;
  });
});
```

### 3. Abstract implementation details (login-start-page)
Don't mix multiple concerns (auth, redirect, UI) in one component. Use wrapper components or HOCs to encapsulate cross-cutting concerns.
```tsx
// BAD: login page exposes auth check implementation
function LoginStartPage() {
  useCheckLogin({ onChecked: (status) => {
    if (status === "LOGGED_IN") { location.href = "/home"; }
  }});
  return <>{/* ... */}</>;
}

// GOOD: AuthGuard encapsulates auth logic
function App() {
  return <AuthGuard><LoginStartPage /></AuthGuard>;
}
```

### 4. Name magic numbers (magic-number-readability)
Extract numeric literals into named constants that express their meaning.
```typescript
// BAD
await delay(300); // animation? server sync? unknown

// GOOD
const ANIMATION_DELAY_MS = 300;
await delay(ANIMATION_DELAY_MS);
```

### 5. Separate code that never runs together (submit-button)
When code only runs under mutually exclusive conditions (e.g. viewer/admin), delegate to fully separate components at a single branch point.
```tsx
// BAD: viewer and admin code interleaved
function SubmitButton() {
  const isViewer = useRole() === "viewer";
  useEffect(() => {
    if (isViewer) return;
    showButtonAnimation();
  }, [isViewer]);
  return isViewer ? <TextButton disabled>Submit</TextButton> : <Button type="submit">Submit</Button>;
}

// GOOD: single branch, each component handles only its own case
function SubmitButton() {
  const isViewer = useRole() === "viewer";
  return isViewer ? <ViewerSubmitButton /> : <AdminSubmitButton />;
}
```

### 6. Simplify ternary operators (ternary-operator)
Replace nested ternaries with IIFE + if statements to make the flow explicit.
```typescript
// BAD
const status = A && B ? "BOTH" : A || B ? (A ? "A" : "B") : "NONE";

// GOOD
const status = (() => {
  if (A && B) return "BOTH";
  if (A) return "A";
  if (B) return "B";
  return "NONE";
})();
```

### 7. Split hooks by responsibility (use-page-state-readability)
A hook with an overly broad role (e.g. managing all query params) grows bloated and causes unnecessary re-renders. Split by responsibility.
```typescript
// BAD
export function usePageState() {
  const [query, setQuery] = useQueryParams({
    cardId: NumberParam, statementId: NumberParam,
    dateFrom: DateParam, dateTo: DateParam
  });
  return useMemo(() => ({ values: { ... }, controls: { ... } }), [query, setQuery]);
}

// GOOD: independent hook per param
export function useCardIdQueryParam() {
  const [cardId, _setCardId] = useQueryParam("cardId", NumberParam);
  const setCardId = useCallback((id: number) => {
    _setCardId({ cardId: id }, "replaceIn");
  }, []);
  return [cardId ?? undefined, setCardId] as const;
}
```

### 8. Reduce context switching (user-policy)
Minimize jumping between functions and variables to understand logic. Use inline objects or switch statements so everything is visible in one place.
```tsx
// BAD: understanding policy requires 3 hops (component → function → constant)
const policy = getPolicyByRole(user.role);
return <Button disabled={!policy.canInvite}>Invite</Button>;

// GOOD: inline object, no context switching
const policy = {
  admin:  { canInvite: true,  canView: true },
  viewer: { canInvite: false, canView: true }
}[user.role];
```

---

## Cohesion

### 9. Choose the right form cohesion level (form-fields)
- **Field-level cohesion**: use inline validation per field when fields need independent/async validation or reuse across forms
- **Form-level cohesion**: use a centralized schema (e.g. Zod) when all fields belong to a single business unit or have interdependencies

### 10. Eliminate magic numbers to improve cohesion (magic-number-cohesion)
Extract magic numbers so that related values change together when requirements change.
```typescript
// BAD: 300 is tied to animation but the relationship is invisible
await delay(300);

// GOOD: named constant reveals the relationship
const ANIMATION_DELAY_MS = 300;
await delay(ANIMATION_DELAY_MS);
```

### 11. Co-locate files that change together (code-directory)
Don't organize files only by technical type (components, hooks, utils). Group by domain so that related files live together.
```text
# BAD: organized by type — 100+ unrelated files per folder
src/
  components/
  hooks/
  utils/

# GOOD: organized by domain
src/
  components/   # truly global
  domains/
    Domain1/
      components/
      hooks/
    Domain2/
      components/
      hooks/
```
Cross-domain imports like `import { useFoo } from "../../../Domain2/hooks/useFoo"` immediately signal a boundary violation.

---

## Coupling

### 12. Eliminate props drilling (item-edit-modal)
When a middle component passes props it doesn't use, fix it with the Composition pattern or Context API.
```tsx
// BAD: ItemEditBody passes through items and onConfirm without using them
function ItemEditBody({ keyword, onKeywordChange, items, onConfirm, onClose }) {
  return <ItemEditList items={items} onConfirm={onConfirm} />;
}

// GOOD: Composition — parent composes children directly
function ItemEditModal({ items, onConfirm, onClose }) {
  const [keyword, setKeyword] = useState("");
  return (
    <ItemEditBody keyword={keyword} onKeywordChange={setKeyword} onClose={onClose}>
      <ItemEditList items={items} onConfirm={onConfirm} />
    </ItemEditBody>
  );
}
```

### 13. Allow duplication over wrong abstraction (use-bottom-sheet)
Extracting a shared hook just because code looks similar creates unnecessary coupling. If behavior might diverge per page, duplication is the better choice. **Only consolidate when behavior is identical now and will stay identical.**

### 14. Manage one responsibility per hook (use-page-state-coupling)
When every component depends on a single wide-scope hook, any change blows up the impact radius. Split into focused hooks so each component only depends on what it actually needs.

---

## Predictability

### 15. Expose hidden logic (hidden-logic)
Don't hide side effects (logging, analytics, etc.) inside functions whose name, parameters, or return type give no hint of them. Move side effects to the call site.
```typescript
// BAD: "fetch balance" secretly also logs
async function fetchBalance(): Promise<number> {
  const balance = await http.get<number>("...");
  logging.log("balance_fetched"); // unpredictable from signature
  return balance;
}

// GOOD: fetchBalance is pure; logging is explicit at call site
async function fetchBalance(): Promise<number> {
  return await http.get<number>("...");
}
const balance = await fetchBalance();
logging.log("balance_fetched");
```

### 16. Avoid name collisions with external libraries (http)
If a custom module shares a name with a well-known library, callers will misread its behavior. Give service-specific modules unique names that reflect what they actually do.
```typescript
// BAD: named http — looks like a plain HTTP client but secretly injects auth
export const http = { async get(url) { /* hidden token injection */ } };

// GOOD: name makes behavior obvious
export const httpService = {
  async getWithAuth(url: string) { /* clearly an authenticated request */ }
};
```

### 17. Unify return types within the same function family (use-user)
Functions of the same kind (API hooks, validation functions) should return the same shape so callers can rely on consistent behavior.
```typescript
// BAD: useUser returns Query object, useServerTime returns only data — inconsistent
function useServerTime() {
  const query = useQuery({ ... });
  return query.data;
}

// GOOD: both return Query object
function useServerTime() {
  return useQuery({ ... });
}

// Validation: use Discriminated Union for consistent shape
type ValidationResult = { ok: true } | { ok: false; reason: string };
function checkIsNameValid(name: string): ValidationResult { ... }
function checkIsAgeValid(age: number): ValidationResult { ... }
```

---

Code to review:

$ARGUMENTS
