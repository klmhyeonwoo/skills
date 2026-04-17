---
name: jsdoc
description: This skill should be used when the user asks to "JSDoc 작성해줘", "주석 달아줘", "jsdoc comment 추가해줘", "함수 문서화해줘", "타입 주석 추가해줘", or any request to add JSDoc comments to code.
version: 1.0.0
---

Add JSDoc comments to the given code.

**Always respond in Korean for descriptions inside JSDoc.**

## JSDoc Format

### Functions
```javascript
/**
 * 사용자 목록을 페이지네이션하여 조회한다.
 *
 * @param {Object} options - 조회 옵션
 * @param {number} options.page - 페이지 번호 (1부터 시작)
 * @param {number} options.limit - 페이지당 항목 수
 * @param {string} [options.search] - 검색어 (선택)
 * @returns {Promise<{users: User[], total: number}>} 사용자 목록과 전체 수
 * @throws {ValidationError} page 또는 limit이 유효하지 않을 때
 *
 * @example
 * const result = await getUsers({ page: 1, limit: 20 });
 */
```

### React Components (TSDoc style)
```typescript
/**
 * 사용자 프로필 카드 컴포넌트.
 *
 * @param props.user - 표시할 사용자 정보
 * @param props.onEdit - 편집 버튼 클릭 시 콜백
 * @param props.isLoading - 로딩 상태 여부
 *
 * @example
 * <UserCard user={user} onEdit={handleEdit} />
 */
```

### Types / Interfaces
```typescript
/**
 * 사용자 엔티티
 */
interface User {
  /** 고유 식별자 */
  id: string;
  /** 사용자 이름 */
  name: string;
  /** 이메일 주소 */
  email: string;
  /** 계정 생성 일시 */
  createdAt: Date;
}
```

## Rules

- Don't add comments to self-evident code
- Explain "why" and "how", not "what"
- Use `@param`, `@returns`, `@throws`, `@example` actively
- In TypeScript, skip type annotations already clear from the type signature
- When using `@deprecated`, always mention the alternative

$ARGUMENTS
