---
name: refactor
description: This skill should be used when the user asks to "리팩토링해줘", "코드 개선해줘", "refactor this", "코드 정리해줘", "더 좋은 구조로 바꿔줘", "클린하게 만들어줘", or any request to refactor or improve code structure.
version: 1.0.0
---

Refactor the given code to improve readability, maintainability, and structure.

**Always respond in Korean for explanations.**

## Refactoring Principles

### Readability
- Function/variable names clearly reveal intent
- Extract complex conditions into named variables
- Flatten deeply nested code using early return
- Extract magic numbers/strings into named constants

### Function Separation
- Each function does exactly one thing
- Split functions that are too long
- Extract repeated logic

### Duplication Removal
- Consolidate similar code patterns
- But distinguish accidental similarity from true shared logic — avoid premature abstraction

### Type Safety (TypeScript)
- Remove `any` types
- Use union types and type guards
- Choose interface vs type appropriately

### React Patterns
- Separate concerns (UI logic vs business logic)
- Extract logic into custom hooks
- Split components that are too large

## Output Format

1. **Summary of current problems**
2. **Full refactored code**
3. **Explanation of each change**

Keep behavior identical. Do not add features or fix bugs.

$ARGUMENTS
