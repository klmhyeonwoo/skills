---
name: performance-review
description: This skill should be used when the user asks to "성능 리뷰해줘", "성능 문제 찾아줘", "performance review", "렌더링 최적화해줘", "느린 이유 찾아줘", "퍼포먼스 개선", or any request to review code for performance issues.
version: 1.0.0
---

Review the given code for performance issues.

**Always respond in Korean.**

## Review Areas

### React / Frontend
- Unnecessary re-renders (missing `useMemo`, `useCallback`, `React.memo`)
- Heavy computation during render (needs memoization)
- Large lists without virtualization (react-window, react-virtual)
- Images without lazy loading or proper format
- Bundle size issues (unnecessary imports, non-tree-shakable patterns)
- `useEffect` with too many dependencies causing excessive calls

### Network
- Unnecessary API calls (missing caching or deduplication)
- Waterfall requests (sequential calls that could be parallel)
- Loading all data without pagination or infinite scroll
- Over-fetching (not requesting only needed fields)

### JavaScript
- Loops with O(n²) or worse complexity
- Heavy operations called repeatedly without caching
- Unnecessary array/object creation (memory pressure)
- Synchronous blocking operations

## Output Format

For each issue:

**[Category] Issue Title**
- Problem: (what code is problematic and why)
- Impact: (actual performance effect)
- Fix: (concrete improved code)

$ARGUMENTS
