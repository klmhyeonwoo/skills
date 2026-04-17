---
name: prd
description: This skill should be used when the user asks to "PRD 작성해줘", "PRD 만들어줘", "기획서 작성해줘", "제품 요구사항 문서 만들어줘", "product requirements document 써줘", or any request to create a Product Requirements Document.
version: 1.0.0
---

Generate a PRD (Product Requirements Document) and save it as `PRD.md` in the current directory.

**Always respond in Korean.**

## What is a PRD

A PRD answers "why does this product exist?" It focuses on business goals and user needs. Implementation details belong in the WRD.

## Process

1. Ask the user for any missing information:
   - Core purpose of the product/feature
   - Target users
   - Problem being solved
   - High-level feature list
   - Success criteria
2. Write `PRD.md` based on the answers
3. Save to the current directory

## PRD.md Format

```markdown
# PRD: [제품/기능명]

## 개요
<!-- 이 제품이 존재하는 이유를 한 문단으로 -->

## 문제 정의
<!-- 현재 어떤 문제가 있는가, 왜 지금 해결해야 하는가 -->

## 목표
- 
- 

## 비목표 (Out of Scope)
- 

## 타깃 사용자
<!-- 누가, 어떤 상황에서 쓰는가 -->

## 주요 기능
<!-- User-facing behavior only. No implementation details. -->

### [기능 1]
- 사용자는 ~할 수 있다

### [기능 2]
...

## 성공 지표
| 지표 | 현재 | 목표 |
|------|------|------|
|      |      |      |

## 제약사항
- 

## 참고자료
```

## Rules

- No implementation details (tech stack, API design) — those go in WRD
- Describe features as user actions ("사용자는 ~할 수 있다")
- No vague expressions — use measurable criteria instead of "빠르게", "쉽게"
- Keep it under ~1,000 tokens

$ARGUMENTS
