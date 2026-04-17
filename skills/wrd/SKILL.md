---
name: wrd
description: This skill should be used when the user asks to "WRD 작성해줘", "WRD 만들어줘", "작업 요구사항 문서 만들어줘", "기술 스펙 문서 써줘", "work requirement document 써줘", "구현 명세 작성해줘", or any request to create a Work Requirement Document.
version: 1.0.0
---

Generate a WRD (Work Requirement Document) and save it as `WRD.md` in the current directory.

**Always respond in Korean.**

## What is a WRD

A WRD translates PRD goals into concrete implementation specs from a developer's perspective. It answers "how will we build it?" It is designed so that AI agents and developers don't need to re-explain the same context every session.

- Target length: 1,000–2,000 tokens for up to 10 features
- Split by domain if exceeding 2,000 tokens
- Update before requesting new features

## Process

1. Read `PRD.md` if it exists
2. If not, ask the user:
   - Feature list to implement
   - Tech stack (framework, DB, language, etc.)
   - Key constraints (API limits, performance requirements, etc.)
3. Write `WRD.md` and save to current directory

## WRD.md Format

```markdown
# WRD: [제품/기능명]

## 기술 스택
| 구분 | 기술 |
|------|------|
| Frontend | Next.js, TypeScript, Tanstack-Query |
| Backend | Node.js |
| DB | PostgreSQL |

## 기능 명세

### [기능명]
- 구현 방식:
- 입력:
- 출력:
- 제약사항:
- 엣지케이스:

## API 설계

| Method | Path | 설명 |
|--------|------|------|
| GET | /api/... | ... |

## 데이터 모델

\`\`\`
User {
  id: string
  email: string
}
\`\`\`

## 비기능 요구사항
- 성능:
- 보안:

## 구현 우선순위
| 우선순위 | 기능 | 이유 |
|----------|------|------|
| P0 | | 없으면 서비스 불가 |
| P1 | | 핵심 사용자 경험 |
| P2 | | 있으면 좋음 |
```

## Rules

- Keep each feature spec to 3–5 lines — no over-explaining
- Specify implementation approach clearly so AI generates consistent code
- Include only key API endpoints, not everything
- No "TBD" items — decide before writing
- Split into separate files for 10+ features (`WRD-auth.md`, `WRD-payment.md`, etc.)

$ARGUMENTS
