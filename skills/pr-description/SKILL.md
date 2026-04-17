---
name: pr-description
description: This skill should be used when the user asks to "PR 설명 작성해줘", "PR description 써줘", "풀리퀘 설명 만들어줘", "write a PR description", "PR 내용 정리해줘", or any request to generate a pull request description.
version: 1.0.0
---

Generate a pull request description based on the current branch changes.

**Always respond in Korean.**

## Process

1. Run `git log main..HEAD --oneline` (or `git log origin/main..HEAD --oneline`) to see commits.
2. Run `git diff main...HEAD --stat` to see changed files.
3. Run `git diff main...HEAD` for detailed changes if needed.
4. Generate the PR description.

## PR Description Format

```markdown
## 개요
<!-- What this PR does in 1-2 sentences -->

## 변경 사항
- 
- 

## 스크린샷 (UI 변경 시)
<!-- Before / After -->

## 테스트 방법
1. 
2. 

## 체크리스트
- [ ] 테스트 작성/수정
- [ ] 문서 업데이트
- [ ] Breaking change 없음
```

## Rules

- Focus the overview on "why", not just "what changed"
- Describe changes as features/behaviors, not file lists
- Help the reviewer know where to start reading
- Remove sections that don't apply

$ARGUMENTS
