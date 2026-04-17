---
name: test-writer
description: This skill should be used when the user asks to "테스트 작성해줘", "테스트 코드 만들어줘", "write tests", "unit test 써줘", "테스트 케이스 추가해줘", "이 함수 테스트해줘", or any request to generate test code.
version: 1.0.0
---

Write tests for the given code.

**Always respond in Korean for explanations. Test descriptions (`it`, `test`) should be written in Korean.**

## Process

1. Read the target file to understand the code structure.
2. Check `package.json` to identify the testing framework (vitest, jest, testing-library, etc.).
3. Identify what needs to be tested: functions, components, hooks, API calls.
4. Write comprehensive tests.

## Coverage Targets

### Functions / Utilities
- Happy path
- Edge cases (empty values, null, undefined, boundary values)
- Error cases (exceptions)

### React Components
- Renders correctly
- User interactions (click, input, submit)
- Behavior on prop changes
- Async states (loading, error, success)

### Custom Hooks
- Initial state
- State transitions
- Side effects

### API / Async
- Success response handling
- Error response handling
- Loading state

## Rules

- Use `describe` blocks for grouping
- Follow AAA pattern (Arrange - Act - Assert)
- Test behavior, not implementation details
- Minimize mocks — only use when necessary

$ARGUMENTS
