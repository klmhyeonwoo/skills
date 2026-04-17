---
name: readme
description: This skill should be used when the user asks to "README 작성해줘", "리드미 만들어줘", "프로젝트 문서 작성해줘", "write a README", "README.md 만들어줘", or any request to generate project documentation.
version: 1.0.0
---

Generate a README.md for the given project.

**Always respond in Korean.**

## Process

1. Read the project root structure (`package.json`, `src/` directory, etc.)
2. Check `package.json` for project name, description, scripts, and dependencies
3. Explore key files and directories
4. Generate the README

## README Format

```markdown
# 프로젝트명

> 한 줄 설명

## 시작하기

### 요구사항
- Node.js 18+
- ...

### 설치

\`\`\`bash
npm install
\`\`\`

### 실행

\`\`\`bash
npm run dev
\`\`\`

## 프로젝트 구조

\`\`\`
src/
├── components/
├── hooks/
└── ...
\`\`\`

## 주요 기능

- 기능 1
- 기능 2

## 환경변수

| 변수명 | 설명 | 필수 |
|--------|------|------|
| `API_URL` | API 서버 주소 | O |

## 스크립트

| 명령어 | 설명 |
|--------|------|
| `npm run dev` | 개발 서버 실행 |
| `npm run build` | 프로덕션 빌드 |
| `npm run test` | 테스트 실행 |
```

## Rules

- Only write accurate information based on the actual code — never guess
- Installation/run commands must actually work
- Reference `.env.example` for environment variables if it exists

$ARGUMENTS
