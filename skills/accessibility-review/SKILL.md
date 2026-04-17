---
name: accessibility-review
description: This skill should be used when the user asks to "접근성 리뷰해줘", "a11y 검토해줘", "accessibility review", "웹 접근성 확인해줘", "스크린리더 지원 확인해줘", or any request to review code for accessibility issues.
version: 1.0.0
---

Review the given code for accessibility issues based on WCAG 2.1 guidelines.

**Always respond in Korean.**

## Review Checklist

### Semantic Markup
- Appropriate HTML elements (`button` vs `div`, `nav`, `main`, `section`, etc.)
- Correct heading hierarchy (`h1` → `h2` → `h3`)
- Lists using `ul`/`ol`

### Keyboard Accessibility
- All interactive elements reachable by keyboard
- No unnecessary `tabIndex` usage
- Focus trap implemented where needed (modals)
- Focus order matches visual order

### ARIA
- `aria-label`, `aria-labelledby`, `aria-describedby` used appropriately
- `role` attribute used correctly
- State attributes updated on change (`aria-live`, `aria-expanded`, `aria-selected`)
- Icon buttons have text alternatives

### Visual
- Information not conveyed by color alone
- Text contrast ratio met (normal text 4.5:1, large text 3:1)
- Focus indicator visible (if `outline` removed, alternative provided)

### Images / Media
- `img` has `alt` attribute (decorative images use `alt=""`)
- Complex images have descriptions

## Output Format

For each issue:

**[WCAG Criterion] Issue Title**
- Problem: (what code is problematic and why)
- Impact: (which users are affected and how)
- Fix: (concrete improved code)

$ARGUMENTS
