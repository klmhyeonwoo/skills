# Write a Blog Article

Write a blog article on the following topic: $ARGUMENTS

The article must be written in **Korean**. Follow the style guide below strictly.

---

## Style Guide

### Tone & Voice
- Personal and narrative — feels like someone sharing what they figured out, not a tutorial
- Short sentences with rhythm. No rambling.
- Use natural connectors like "사실", "근데", "결국", "예전만 해도", "막상"
- Self-reflective tone throughout — "~이었다", "~이지 않았다", "~를 깨닫게 됐다"
- Technically accurate, but told from personal experience — not dry or lecture-like
- Occasional informal exclamations or casual endings ("^,^", "..") are fine at the very end

### Structure
1. **Intro**: Follow this 4-beat pattern the writer uses:
   ① 해당 기술/기능을 "당연하게" 쓰던 익숙한 경험 서술 ("~는 그냥 당연한 것처럼 느껴졌다")
   ② 그 기능이 속한 더 넓은 맥락이나 철학 언급 — Vue가 많은 걸 자동으로 해준다는 식의 배경
   ③ "근데 문제가 생겼을 때 모른다면?" 이라는 의문으로 좁혀짐 — 동작을 모르면 사이드 이펙트를 이해하기 어렵다는 인식
   ④ 결국 내부를 직접 들여다보게 된 계기로 자연스럽게 연결
   Use first-person narrative ("~했다", "~이었다"). Don't address the reader with "해봤을 것이다" or similar.
2. **Background**: Brief timeline of why this exists and how it evolved — told as a story, not a bullet list
3. **Core Concept**: Explain internal mechanics in depth — how it works under the hood, what happens step by step at runtime or parse time, why it behaves the way it does. Use code and ASCII diagrams actively. The reader should finish this section feeling like they truly understand the internals, not just the surface API.
4. **Comparison**: Objective comparison using a table
5. **Practical Guide**: Concrete scenario-based recommendations for "what to use when"
6. **Closing**: End the last section naturally — no dedicated "마무리" section. Close with a personal reflection or commitment ("~야겠다", "~이 보이기 시작한다"), optionally recommending a related resource the writer found valuable.

### Formatting Rules
- Separate sections with `---` horizontal rules
- **Bold** key concepts
- Add `← comment` annotations inside code blocks
- Use tables only for essential comparisons, not excessively
- Use `###` for subheadings; avoid deep nesting

### Code Block Style
```
# Commands like this
npm install react     # explanation

# Structure diagrams as ASCII art
node_modules/
  package-a/          ← annotation like this
  package-b/
```

### Writing Principles
- Concrete examples before abstract explanations
- Personal experience woven throughout — not just the intro, but also mid-article ("이 부분에서 처음에 헷갈렸던 건 ~이었다")
- Balanced pros/cons, but state personal opinion clearly and without hedging
- **No ambiguous expressions**: never use vague phrases like "생각보다 복잡하다", "꽤 정교하다", "내부가 복잡하게 얽혀 있다". Always state exactly what is complex or how it works. Bad: "구조가 생각보다 정교하다" → Good: "ReactiveEffect, dep, _dirty 세 가지가 맞물려 동작하는 구조다"
- **Term annotations with `*`**: when a technical term appears for the first time, mark it with `*` in the text and add a one-line definition immediately after the paragraph using the format `*term: definition`. Example:
  > 이 전역 변수가 `activeEffect`*다.
  >
  > *activeEffect: 현재 실행 중인 ReactiveEffect 인스턴스를 가리키는 전역 변수. getter가 실행되는 동안 어떤 effect가 값을 읽고 있는지 추적하는 데 사용된다.
- Write so the reader thinks "ah, now I get it — and I can see how you got confused too"
- End with a personal reflection or commitment the writer genuinely feels, not a CTA directed at the reader
- **No metaphors or personification**: avoid expressions like "범인", "영리하다", "계획을 망쳤다". State facts directly.
- **No imperative titles**: don't use `~하라` form in titles (main or section). Use question form like `~해야 할까?` instead. Also avoid `~란` — use `~는 무엇일까?` instead.
- **No commanding tone in body**: avoid `~하라`, `~마라`, `~니까` endings. Use descriptive forms like `~하는 것이 좋다`, `~때문이다`, `~하면 된다`.
- Section subheadings can be casual, natural language phrases — not always question form. Examples: "같은 결과인데 신기하게도 다르게 표현된다", "런타임에서 실제로 무슨 일이 일어날까?"

### Korean Expression Rules
- Keep English technical terms as-is (npm, pnpm, hoisting, etc.)
- Use Korean only when the translation feels natural (e.g., "심볼릭 링크", "하드링크")
- Avoid overly formal expressions (use "~한다", "~이다" instead of "~합니다")

---

Follow the style above. Adjust structure flexibly to fit the topic.
Depth matters — the reader should feel like this one article covers everything they need.
Go deep on internal workings: execution order, how the runtime or browser processes things step by step, what's happening behind the syntax. Surface-level explanation is not enough.

---

When done, save to `~/blog/YYYY-MM-DD-{topic-in-kebab-case}.md`.
Create `~/blog/` directory first if it doesn't exist.
