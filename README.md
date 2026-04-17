# skills

Claude Code 커맨드와 스킬 모음입니다.

## 구조

```
skills/
├── commands/   # 슬래시 커맨드
└── skills/     # 스킬
```

## 스킬 목록

| 스킬                          | 설명                                |
| ----------------------------- | ----------------------------------- |
| `commit-message`              | 변경사항 보고 커밋 메시지 자동 작성 |
| `pr-description`              | PR 설명 자동 생성                   |
| `test-writer`                 | 코드 보고 테스트 자동 작성          |
| `performance-review`          | 성능 이슈 분석                      |
| `accessibility-review`        | 웹 접근성 검토 (WCAG 2.1)           |
| `refactor`                    | 리팩토링 제안                       |
| `jsdoc`                       | JSDoc 주석 자동 생성                |
| `readme`                      | README.md 작성                      |
| `prd`                         | PRD.md 생성 (제품 요구사항 문서)    |
| `wrd`                         | WRD.md 생성 (작업 요구사항 문서)    |
| `frontend-fundamental-review` | 프론트엔드 원칙 기준 코드 리뷰      |

## 커맨드 목록

| 커맨드                        | 설명               |
| ----------------------------- | ------------------ |
| `/write-markdown-article`     | 블로그 글 작성     |
| `/toss-tech-design-knowledge` | 디자인 아티클 검색 |

---

## 서브모듈로 사용하기

### 1. 새 프로젝트에 추가

```bash
git submodule add https://github.com/klmhyeonwoo/skills.git .claude
```

`.claude/` 자체가 이 레포가 되므로 `commands/`와 `skills/`를 Claude Code가 바로 인식합니다.

### 2. 서브모듈이 포함된 레포 클론

```bash
git clone --recurse-submodules git@github.com:your/project.git
```

이미 클론한 경우:

```bash
git submodule update --init --recursive
```

### 3. 스킬/커맨드 업데이트

```bash
git submodule update --remote .claude
```

또는 서브모듈 안에서:

```bash
cd .claude && git pull
```

### 4. 서브모듈 제거

```bash
git submodule deinit .claude
git rm .claude
git commit -m "chore: remove ai submodule"
```

---

## 주의사항

- `.claude/`가 서브모듈이므로 프로젝트별 설정은 루트의 `CLAUDE.md`에 작성
- 스킬/커맨드 수정은 이 레포에서 하고 PR 후 각 프로젝트에서 `submodule update`
