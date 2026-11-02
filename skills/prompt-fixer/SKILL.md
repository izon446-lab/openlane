---
name: prompt-fixer
description: Load this skill when the user's message is messy, scattered, typo-heavy, mixed-language, stream-of-consciousness, or unclear — or when they explicitly ask to fix, improve, rewrite, or structure a prompt ("prompt düzelt", "bunu düzgün yaz"). Interprets vague intent, fills gaps with sensible defaults, runs an advisor critique pass on the corrected prompt, and either shows the clean structured prompt or silently executes the task. On first load, read references/interpretation-rules.md. Worked examples in examples/demo-run.md.
---

# Prompt Fixer

Turn messy, incomplete, or stream-of-consciousness requests into a clean, workable
prompt — and then act on it. The user of this skill writes fast and scattered: typos,
missing letters, mixed Turkish/English, half sentences, and thought-dumps are normal.
The goal is to catch the intent, never to judge the writing.

## Step 1 — Extract the intent (read the meaning, not the syntax)

Re-read the message and extract:

1. **Goal** — what does the user actually want? Fix typos mentally as you read
   ("araştır" → "araştır", "benm" → "benim", "yapver" → "yapıver"); identify the
   dominant language if the message mixes languages. Common patterns are listed in
   `references/interpretation-rules.md`.
2. **Context** — which person, project, tool, file, or event is being referenced?
   Complete it from prior messages, personal knowledge folders, and the filesystem.
3. **Scope** — how much detail, which format, which audience? Note if unspecified.
4. **Implicit expectation** — what the user expects but didn't write. "Fix this report"
   usually means "same content, more professional tone", not a rewrite from scratch.

## Step 2 — Close the gaps

- For small ambiguities, **assume and proceed** (tone, length, language). State your
  assumptions in one line at the end ("Kept the tone professional — can simplify on request").
- Ask ONLY when a critical gap materially changes the result. Maximum 2-3 questions,
  via `ask_user_question`, with options. Critical gaps: which file/source to work from,
  where the output goes, hard limits like budget/deadline.
- If the user is clearly in "just do it" mode, don't ask anything: take the best
  interpretation and go. The spirit of this skill: ask little, solve much.

## Step 3 — Write the corrected prompt (in the user's language)

```
GÖREV / TASK: [single-sentence precise goal]
BAĞLAM / CONTEXT: [known background, sources, files]
KAPSAM / SCOPE: [what's included, what's excluded]
KISITLAR / CONSTRAINTS: [tone, length, format, language, deadline]
ÇIKTI / OUTPUT: [expected deliverable — report, table, canvas, code, etc.]
BAŞARI ÖLÇÜTÜ / SUCCESS CRITERIA: [what makes the result "good"]
```

- Preserve every concrete detail from the original message (numbers, names, dates,
  special requests). If the user asked for two things, both stay in the prompt.
- Mark uncertain parts as `[not sure: tell me if you meant X]`.
- Write the prompt in a language the user understands, at a precision a model can execute.

## Step 4 — Advisor Pass (before executing)

Like Perplexity's advisor step: after writing the corrected prompt, review it through
the eyes of a skeptical senior consultant BEFORE running it.

1. **Critique**: Is the goal actually precise? Does the output format match the goal?
   Is the success criterion measurable? Any scope bloat or critical missing piece?
   Any risky assumption?
2. **Comment**: max 3 bullets, most critical first. Skip nitpicks.
3. **Fix**: apply each comment to the prompt and update it. If an advisor comment
   requires no change, leave the prompt untouched.
4. **Report**: summarize the advisor note and the fixes to the user in 1-2 lines.
   If the user objects, the user wins.

## Step 5 — Execute

- User asked **"fix this prompt"**: show the corrected prompt, explain briefly, and
  offer to run it.
- User **gave a messy task** without asking for a fix: build the prompt silently and
  **execute the task directly**. Don't show the prompt unless needed; summarize what
  you understood in one sentence, then do the work.
- If the corrected prompt targets another skill (deep research, report, code), load
  that skill and run the chain.

## Hard Rules

- Never mock or lecture the user about their writing. Just do the work.
- The prompt fixer works like a hidden translator: remove noise, keep signal.
- When multiple interpretations are plausible, pick the most likely one, mark it,
  and proceed. Don't drown the user in options.
