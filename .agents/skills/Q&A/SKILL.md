---
name: Q&A
description: Short guidance for generating bilingual interview Q&A content based on the subagent-interviewer rules.
---

## Role

Use this skill to create or improve technical interview Q&A content.

## Delegation Rule

- This skill must delegate Q&A generation or review work to the `interviewer` subagent.
- Use `spawn_agent` to call the `subagent-interviewer` agent for execution.
- Pass the target topic path, difficulty, Bloom levels, question count, sub-topics, code language, and whether content already exists.
- The main agent should verify the result and summarize the changed files after the subagent finishes.

## Core Rules

- Write bilingual content for every entry:
  - `en:` English
  - `vi:` Vietnamese
- Structure questions by Bloom's Taxonomy.
- Use `C#` for code examples unless the caller says otherwise.
- Keep `pitfalls/` focused on mistakes, failure modes, warning signs, and safer alternatives.

## Difficulty Split

- `foundation`: Levels 1-3
- `advance`: Levels 4-5
- `pitfalls`: compact, high-signal mistake-focused set

Default full generation:
- `foundation/QnA.md`: 40 questions
- `advance/QnA.md`: 10 questions
- `pitfalls/QnA.md`: concise pitfalls set

## Bloom Levels

- Level 1: Remembering
- Level 2: Understanding
- Level 3: Applying
- Level 4: Analyzing
- Level 5: Evaluating

## Required QnA Format

```md
# {Topic} {Difficulty} Q&A

---

### Level {N}: {Level Name}

#### Q_LEVEL{N}_{DIGITS}: {Short Title}

**Question:**
en: ...
vi: ...

**Answer:**
en: ...
vi: ...
```

For Level 3+ add a code block when useful:

```csharp
// Example in C#
```

For long explanations, add:

```md
**DETAILS =>** {relative_path}/{Q_ID}.md
```

## Writing Standard

- Explain `why`, not only `what`.
- Vietnamese should read naturally, not as a literal translation.
- Keep English technical terms in Vietnamese when needed.
