# Agentic AI Quick Guide

This file is for humans.

If you want to lead the agent efficiently, just tell it clearly:
- what you want
- where
- which track if needed

---

## Main agent: orchestrator

This is the default main agent.

What it does:
- understand your request: detect what you want to do
- choose the correct folder: map topic to the right path
- call subagent automatically for Q&A generation/review: delegate to `interviewer` without requiring special delegation wording
- update docs / files / repo structure directly when needed: handle non-Q&A repo tasks

Best user input style:

```text
<action> + <topic or file path> + <track if needed> + <focus if needed>
```

Examples:

```text
Generate Q&A for Event-Driven Architecture in message-queue/EDA
Generate Q&A for Agile methodology in methodologies/agile
Generate pitfalls folder for backend/nodejs
Add 3 Level 2 questions to backend/C#/foundation/QnA.md about LINQ
Review and improve frameworks/ASP.NET/pitfalls/QnA.md
Create TOPIC.md for message-queue/EDA
Update README.md to mention pitfalls folders
```

---

## Subagent: interviewer

This subagent is used for Q&A work.

Abilities:
- generate new Q&A topics: create a new topic set from scratch
- generate `foundation`: create Level 1-3 core questions
- generate `advance`: create Level 4-5 deeper questions
- generate `pitfalls`: create common mistakes / anti-pattern questions
- add more questions to existing `QnA.md`: append new entries without replacing the file
- improve existing Q&A: rewrite weak or unclear content
- review Q&A quality: check overlap, gaps, and formatting consistency

Notes:
- full new topic generation now means:
  - `foundation/`
  - `advance/`
  - `pitfalls/`
- if you ask only one track, it only generates that track

Example user input:

```text
Generate Q&A for CQRS in backend/common/CQRS
Generate only pitfalls Q&A for backend/nodejs
Generate advance Q&A for testing/TDD
Add 5 Level 2 questions to backend/C#/foundation/QnA.md about delegates
Add 1 question to backend/C#/foundation/QnA.md. Question is: distinguishing IQueryable vs IEnumerable vs List
Review and improve backend/nodejs/foundation/QnA.md
Generate pitfalls Q&A for frameworks/ASP.NET focus on DI lifetime, async, EF Core, middleware ordering
```

---

## Skill: self-feedback

Use this when you want to change agent behavior or prompt rules.

Abilities:
- update orchestrator behavior: change how the main agent routes and handles requests
- update subagent behavior: change how a subagent generates or edits content
- sync behavior with new repo structure: keep prompts aligned with folder changes
- add new generation rules: enforce new defaults or conventions

Example user input:

```text
New feedback, pitfalls folder is MUST generated along with foundation and advance folders
Update interviewer subagent so pitfalls means common mistakes even senior developers make
Update orchestrator prompt so if user asks for pitfalls it should target pitfalls/QnA.md by default
```

---

## Simple command templates

Generate full topic:

```text
Generate Q&A for <Topic> in <path>
```

Generate only one track:

```text
Generate only <foundation|advance|pitfalls> Q&A for <path>
```

Add more questions:

```text
Add <count> Level <N> questions to <file path> about <topic>
```

Add one exact question:

```text
Add 1 question to <file path>. Question is: <your question>
```

Improve existing file:

```text
Review and improve <file path>
```

Change agent behavior:

```text
New feedback: <new rule>
```

---

## Best examples

```text
Generate Q&A for Event-Driven Architecture in message-queue/EDA
Generate Q&A for Agile methodology in methodologies/agile
Generate only pitfalls Q&A for backend/nodejs
Add 3 Level 2 questions to backend/C#/foundation/QnA.md about async/await
Add 1 question to backend/C#/foundation/QnA.md. Question is: distinguishing IQueryable vs IEnumerable vs List
Review and improve frameworks/ASP.NET/pitfalls/QnA.md
New feedback, full topic generation must always create foundation, advance, and pitfalls
```

---

## Short rule

Best user input:

```text
action + exact path/topic + track + focus
```

Example:

```text
Add 3 Level 2 pitfalls questions to backend/nodejs/pitfalls/QnA.md about event loop blocking, memory leaks, and graceful shutdown
```
