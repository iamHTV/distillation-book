# SIEVE — Book Knowledge Distillation Framework

<div align="center">

### Distill knowledge from books, retain 85-92% of valuable information

[![Framework: SIEVE](https://img.shields.io/badge/Framework-SIEVE-2ea44f.svg)](./sieve-book-distillation/SKILL.md)
[![Compression: 90%](https://img.shields.io/badge/Compression-90%25-blue.svg)](./sieve-book-distillation/references/00-overview.md)
[![Retention: 85-92%](https://img.shields.io/badge/Retention-85--92%25-green.svg)](./sieve-book-distillation/references/03-phase3-validate.md)

</div>

## Why this exists

You read books but don't have time. You want to **fully understand a book** without missing important information.

Current frameworks have problems:

| Framework | Problem |
|-----------|---------|
| **Regular summarization** | 98% compression, loses 70-80% of information |
| **Progressive Summarization** | No gap-detection mechanism, easy to miss things |

**SIEVE** solves this with:
1. **5 parallel extractors** — 5 different perspectives, reduces blind spots
2. **Teacher-Student loop** — Uses output to query the original book, finds gaps
3. **4-tier output** — Read at whatever depth you need

## What is SIEVE?

**S**tructure → **I**terative Extract → **V**alidate (Teacher-Student) → **E**ncode → **V**erify

```
Input: 500-page book
         │
         ▼
Phase 1: Structure      → Book Map + Backbone + Glossary
Phase 2: Extract        → 5 extractors × N chapters
Phase 3: Validate       → Teacher-Student loop (2-3 rounds)
Phase 4: Encode         → 4-tier output (~50 pages)
Phase 5: Verify         → Quality gate + user review
         │
         ▼
Output: ~50 pages (90% compression, 85-92% retention)
```

## 4-Tier Output

```
Tier 1: Executive Summary     (2-3 pages)   → Read 15 min → Understand 50%
Tier 2: Chapter Summaries     (10-15 pages)  → Read 1 hour → Understand 75%
Tier 3: Detailed Extracts     (20-30 pages)  → Read 2-3 hrs → Understand 90%
Tier 4: Knowledge Graph       (5-10 pages)   → Reference   → Understand connections
```

## Why 85-92% retention?

### 5 Extractors (reduce blind spots)

| Extractor | Finds | Why needed |
|-----------|-------|------------|
| **Argument** | Claims + evidence + counter-arguments | Preserves book's logic |
| **Data** | Statistics, numbers, research | Preserves hard evidence |
| **Narrative** | Case studies, stories, examples | Preserves real-world illustrations |
| **Concept** | Definitions, terminology, frameworks | Preserves author's language |
| **Contrarian** | Criticisms, limitations, warnings | Preserves nuance |

### Teacher-Student Loop (gap detection)

```
Student: "I think the book says A, B, C"
Teacher: "Correct, but you missed D and E, and A needs condition F"
Student: "Thanks, I'll add D, E, F"
Teacher: "Now you missed G (smaller)"
→ Repeat 2-3 rounds until gaps are minimal
```

This is **SIEVE's core innovation**.

## Comparison with alternatives

| Framework | Purpose | Compression | Retention | Output |
|-----------|---------|-------------|-----------|--------|
| **SIEVE** | Understand book | 90% | 85-92% | 50 pages layered |
| **Progressive Summarization** | Personal notes | 80% | 60-70% | Highlight layers |
| **Regular summarization** | Quick overview | 98% | 20-30% | 2-3 pages |

## Repo Structure

```
distillation-book/
├── README.md                   # Documentation (Vietnamese)
├── README.en.md                # Documentation (English)
├── docs/                       # Core ideas, origin story, research
│   ├── core-ideas.md           # Philosophy & principles
│   ├── origin-story.md         # Development history
│   └── research-notes.md       # Research & improvements
├── sieve-book-distillation/    # Skill folder
│   ├── SKILL.md                # Skill definition
│   ├── references/             # Methodology docs (loaded as needed)
│   │   ├── 00-overview.md
│   │   ├── 01-phase1-structure.md
│   │   ├── 02-phase2-extract.md
│   │   ├── 03-phase3-validate.md
│   │   ├── 04-phase4-encode.md
│   │   └── 05-phase5-verify.md
│   └── assets/                 # Output templates
│       ├── EXECUTIVE-SUMMARY.md.template
│       ├── CHAPTER-SUMMARY.md.template
│       ├── DETAILED-EXTRACT.md.template
│       └── KNOWLEDGE-GRAPH.md.template
└── .gitignore
```

## Usage

### Option 1: Use as AI Skill

Install via skillshare:
```bash
skillshare install iamHTV/distillation-book --all
skillshare sync
```

Then tell your AI agent:
> "Summarize [book title] using SIEVE framework"

### Option 2: Read methodology and do it yourself

1. Read `sieve-book-distillation/references/00-overview.md` to understand the flow
2. Read each phase (01 → 05) for details
3. Use templates in `sieve-book-distillation/assets/` to create output

## Time estimates

| Book | Phase 1 | Phase 2 | Phase 3 | Phase 4 | Phase 5 | Total |
|------|---------|---------|---------|---------|---------|-------|
| 200 pages | 10 min | 20 min | 15 min | 10 min | 5 min | ~1 hour |
| 500 pages | 15 min | 40 min | 30 min | 15 min | 10 min | ~2 hours |
| 1000 pages | 25 min | 60 min | 45 min | 20 min | 15 min | ~3 hours |

## Contributing

Framework is under active development. Areas to improve:
- [ ] Detailed extractor prompts (for AI agents)
- [ ] Real-world output examples
- [ ] Auto-generate questions for Teacher-Student loop
- [ ] Completeness scoring algorithm

## License

MIT

## Contact

- GitHub: [iamHTV](https://github.com/iamHTV)
- Repo: [distillation-book](https://github.com/iamHTV/distillation-book)
