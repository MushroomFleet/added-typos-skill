# Added-Typos Skill

A Claude skill for transforming sterile AI-generated text into authentically human-typed output by introducing controlled, natural typing error patterns.

## Overview

Perfect text is a tell. When you need documents, drafts, or content that reads like it was typed by a real human—complete with the minor imperfections that characterize natural typing—this skill introduces authentic error patterns based on observed human typing behaviors.

The skill simulates:
- **Sticky keys** — repeated or dropped high-frequency letters (worn keyboard simulation)
- **Adjacent key errors** — finger misses based on QWERTY layout and touch-typing zones
- **Transpositions** — swapped letter pairs from typing rhythm disruption
- **Dyslexic patterns** — optional letter reversals, phonetic spelling, syllable drops
- **Punctuation habits** — optional apostrophe omission, spacing issues, comma patterns

## Installation

Download `added-typos.skill` and add it to your Claude skills directory:
```
/mnt/skills/user/added-typos/
```

## Usage

### Basic Trigger

```
"amend my 'draft.md' with the added-typos skill"
```

or

```
"add typos to document.txt"
```

### With Configuration

```
"add typos to report.md, heavy intensity, speed-typist profile"
```

```
"simulate typing errors on notes.txt with dyslexic and punctuation enabled"
```

## Configuration Options

| Parameter | Values | Default | Description |
|-----------|--------|---------|-------------|
| `intensity` | `light`, `moderate`, `heavy`, or percentage | `moderate` | Error density (1-2%, 3-5%, 7-10%) |
| `profile` | `balanced`, `keyboard-hardware`, `speed-typist`, `fatigue` | `balanced` | Error pattern distribution |
| `dyslexic` | `true` / `false` | `false` | Enable dyslexic spelling patterns |
| `punctuation` | `true` / `false` | `false` | Enable punctuation degradation |

## Profiles

### `balanced` (default)
Even mix of all error patterns. Best for general-purpose authenticity.

### `keyboard-hardware`
Simulates worn or malfunctioning keyboard. Heavy emphasis on sticky keys (60%), with repeated letters and occasional drops.

**Example:** "thee problem withh this approaach"

### `speed-typist`
Simulates fast, careless typing. High adjacent key errors (50%), many dropped letters.

**Example:** "thr problen wirh this approaxh"

### `fatigue`
Progressive degradation throughout document. Clean start, errors accumulate toward the end.

**Example flow:**
- Start: "The proposal outlines our strategy."
- End: "In conclsuion, thiss appraoch wil deliever teh best rsults."

## Preservation Rules

The following elements are **never modified**:
- URLs (`https://...`)
- Email addresses
- Code blocks (fenced and inline)
- Numbers and dates
- Markdown syntax (`#`, `**`, `[]()`, etc.)

## Examples

### Input
```
The quick brown fox jumps over the lazy dog. This sentence contains every letter of the alphabet and demonstrates typical prose structure.
```

### Output (moderate, balanced)
```
The quikc brown fox jumps over teh lazy dog. This sentennce contains every letter of the alphabet and demonstraets typical prose struture.
```

### Output (heavy, speed-typist)
```
Thr qiuck brown fox jumsp over teh lazy dog. Tihs sentnce contians evry letter of the alphbet and demonstates typicl prose struture.
```

### Output (moderate, with punctuation enabled)
```
The quikc brown fox jumps over teh lazy dog. this sentence contians every letter of the alphabet and demonstraets typical prose struture.
```

## File Structure

```
added-typos/
├── SKILL.md                        # Core workflow & configuration
├── README.md                       # This file
└── references/
    ├── qwerty-mapping.md           # Adjacent keys, finger zones, sticky weights
    ├── pattern-profiles.md         # Profile definitions and weights
    ├── dyslexic-patterns.md        # Opt-in dyslexic simulation
    └── punctuation-habits.md       # Opt-in punctuation degradation
```

## Supported File Types

- Markdown (`.md`)
- Plain text (`.txt`)
- Word documents (`.docx`)
- HTML (`.html`)

## Use Cases

- **Creative writing** — Make AI-assisted drafts appear more naturally written
- **Testing** — Generate realistic user input for form validation or spell-check testing
- **Training data** — Create datasets with authentic human typing patterns
- **Authenticity** — Produce content that doesn't have the "AI polish" tell

## License

MIT License - See LICENSE file for details.

---

## 📚 Citation

### Academic Citation

If you use this codebase in your research or project, please cite:

```bibtex
@software{added_typos_skill,
  title = {Added-Typos Skill: Authentic Human Typing Error Simulation for Claude},
  author = {Drift Johnson},
  year = {2025},
  url = {https://github.com/MushroomFleet/added-typos-skill},
  version = {1.0.0}
}
```

### Donate

[![Ko-Fi](https://cdn.ko-fi.com/cdn/kofi3.png?v=3)](https://ko-fi.com/driftjohnson)

---

## Support This Project

If you found this useful, please **star the repo** — it helps others discover it!

[![Star on GitHub](https://img.shields.io/github/stars/MushroomFleet/added-typos-skill?style=social)](https://github.com/MushroomFleet/added-typos-skill)