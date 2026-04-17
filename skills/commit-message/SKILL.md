---
name: commit-message
description: This skill should be used when the user asks to "커밋 메시지 작성해줘", "commit message 써줘", "커밋 메시지 만들어줘", "write a commit message", "git commit 메시지", or any request to generate a git commit message based on code changes.
version: 1.0.0
---

Generate a git commit message based on the current changes.

**Always respond in Korean (body), but keep the subject line in English following Conventional Commits.**

## Process

1. Run `git diff --staged`. If nothing staged, run `git diff HEAD`.
2. Analyze the changes and determine the appropriate type and scope.
3. Generate the commit message.

## Conventional Commits Format

```
<type>(<scope>): <subject>

<body>
```

### Types
- `feat`: new feature
- `fix`: bug fix
- `refactor`: refactoring without behavior change
- `style`: formatting, semicolons (no logic change)
- `test`: add or update tests
- `docs`: documentation only
- `chore`: build config, package updates
- `perf`: performance improvement
- `ci`: CI/CD related

### Rules
- Subject: under 50 chars, present tense, no period
- Body: explain why, not what (wrap at 72 chars)
- Breaking change: add `BREAKING CHANGE:` in footer

## Output Format

Output the commit message in a code block, ready to copy.

```
feat(auth): add OAuth2 login support

소셜 로그인 기능 추가 (Google, GitHub)
기존 이메일 로그인과 병행 사용 가능
```

$ARGUMENTS
