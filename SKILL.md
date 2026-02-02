---
name: added-typos
description: Add authentic human typing errors to text documents. Simulates natural typo patterns including sticky keys, adjacent key misses, letter transpositions, and optionally dyslexic spelling or punctuation habits. Triggers on phrases like "using added-typos skill", "add typos to", "amend with added-typos", "simulate typing errors", or when user wants to make text appear naturally human-typed rather than AI-generated. Accepts any text file (.md, .txt, .docx, .html) as input.
---

# Added-Typos Skill

Transforms sterile text into authentically human-typed output by introducing controlled, natural error patterns.

## Configuration Parsing

Extract from user prompt (use defaults when unspecified):

| Parameter | Values | Default |
|-----------|--------|---------|
| `intensity` | `light` (1-2%), `moderate` (3-5%), `heavy` (7-10%), or percentage | `moderate` |
| `profile` | `keyboard-hardware`, `speed-typist`, `fatigue`, `balanced` | `balanced` |
| `dyslexic` | `true`/`false` | `false` |
| `punctuation` | `true`/`false` | `false` |

**Example triggers:**
- "add typos to draft.md" → all defaults
- "amend report.txt with added-typos, heavy intensity" → heavy + balanced
- "simulate typing errors, speed-typist profile with punctuation habits" → moderate + speed-typist + punctuation enabled

## Preservation Rules (Always Active)

Never introduce errors into:
- URLs: `https?://\S+`
- Emails: `\S+@\S+\.\S+`
- Code blocks: fenced ``` blocks and inline `code`
- Numbers and dates: `\d+` patterns, date formats
- Markdown syntax: `#`, `**`, `*`, `_`, `[]()`, `>`, `-` list markers

## Core Error Patterns

### 1. Sticky Keys (Repetition/Omission)

High-frequency letters may double or drop. See `references/qwerty-mapping.md` for frequency weights.

| Letter | Sticky Weight | Example (double) | Example (drop) |
|--------|---------------|------------------|----------------|
| e | 0.15 | "thee" | "th" |
| t | 0.12 | "thatt" | "tha" |
| a | 0.10 | "thaat" | "tht" |
| o | 0.09 | "tooo" | "to" (for "too") |
| i | 0.09 | "thinkiing" | "thnking" |
| n | 0.08 | "thinkinng" | "thikig" |

Probability: 60% double, 40% drop (when sticky triggers).

### 2. Adjacent Key Errors

Finger misses target key, hits neighbor. See `references/qwerty-mapping.md` for full adjacency map.

**Error types:**
- **Substitution**: wrong key replaces correct → "thr" for "the" (e→r)
- **Insertion**: extra key added → "thew" for "the" (w inserted)

Probability: 70% substitution, 30% insertion.

### 3. Transposition

Adjacent letters swap positions within word.

Examples: "teh" for "the", "freind" for "friend", "recieve" for "receive"

Probability weight: higher for common letter pairs (th, ie, ei, er).

## Intensity Calculation

Calculate target error count per 100 words:

| Intensity | Errors per 100 words |
|-----------|---------------------|
| light | 1-2 |
| moderate | 3-5 |
| heavy | 7-10 |

Distribute errors across pattern types based on active profile.

## Workflow

1. **Parse configuration** from user prompt
2. **Load profile** from `references/pattern-profiles.md`
3. **If dyslexic enabled**: load `references/dyslexic-patterns.md`
4. **If punctuation enabled**: load `references/punctuation-habits.md`
5. **Tokenize** input text, marking preservation zones
6. **Calculate** error budget based on intensity and word count
7. **Distribute** errors across patterns per profile weights
8. **Apply** errors randomly across eligible tokens
9. **For fatigue profile**: weight errors toward document end
10. **Output** modified text

## Profile Selection Guide

| Profile | Best For | Dominant Patterns |
|---------|----------|-------------------|
| `balanced` | General authenticity | Even mix of all patterns |
| `keyboard-hardware` | Simulating worn keyboards | Sticky keys (60%), adjacent (30%), transposition (10%) |
| `speed-typist` | Fast typing simulation | Adjacent (50%), dropped letters (30%), transposition (20%) |
| `fatigue` | Long documents, tired writer | Progressive: clean start → heavy errors at end |

See `references/pattern-profiles.md` for detailed weights.

## Output

Return the modified text with errors applied. Do not annotate or highlight the errors—output should read as natural human-typed text.
