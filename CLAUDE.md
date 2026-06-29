# Odyssey Ebook — Michael Caine / ElevenLabs Edition

## Project Purpose
This is a fork of the Standard Ebooks William Cullen Bryant translation of Homer's Odyssey. The goal is to substitute Latinised/Roman character names with their Greek equivalents, to match the naming conventions used consistently in the ElevenLabs AI audiobook narrated via Michael Caine's voice clone (released June 2026).

## Directory Layout

```
epub-src/    ← SE project root; pass this to se lint / se build
scripts/     ← name-substitution Python scripts and data
new-cover/   ← working folder for new cover design
```

SE commands are run from the repo root with `epub-src/` as the project path:

```bash
se lint epub-src/
se build epub-src/
```

## Source Files
All content lives in `epub-src/src/epub/text/` as `book-1.xhtml` … `book-24.xhtml`, plus `book-0.xhtml` (the prose introduction — an Eleven Productions original transcribed from the audiobook), `preface.xhtml`, `colophon.xhtml`, etc. These are UTF-8 XHTML files containing typographic characters (`’`, `—`, curly quotes) — edits must preserve valid XHTML markup. Only modify metadata files like `content.opf` or `toc.xhtml` insofar as needed to reflect edits to `book-x.xhtml` files.

Verse is marked up cleanly: each poetic line is its own `<span>…</span>` separated by `<br/>`. Each book opens with a prose "argument" `<p>` that also contains names. The sole exception is `book-0.xhtml`, which is plain prose (ordinary `<p>` paragraphs, `epub:type="chapter"` *without* `z3998:poem`) and has no argument.

## Name Substitution Map
The final, audio-verified swap list is documented in `README.md`. The mapping itself lives in `scripts/substitutions.json` and is applied by `scripts/substitute.py`; `scripts/extract_names.py` re-scans the books to confirm no Bryant forms remain.

- `scripts/substitute.py` is word-boundary-safe and **text-node-only** (tags, attributes, and whitespace pass through byte-for-byte). Dry-run by default; `--apply` writes in place as UTF-8 with original line endings preserved.
- `scripts/extract_names.py epub-src/src/epub/text` extracts proper-noun candidates into `scripts/names_report.md` / `scripts/names_raw_forms.csv` (gitignored). Dependency: `lxml`.

## Critical Traps
- **Bryant already mixes Greek and Roman.** Forms like `Hermes` and `Apollo` already appear in the source, so **never do a loose global replace** — substitute specific forms with word boundaries, longest / compound / possessive form first (e.g. `Pallas Athene` before bare `Pallas`, `Jove’s` before `Jove`).
- **The ElevenLabs narration only replaces the names of the 7 core deities** rather than all Roman names. Always ask for a human verification against the audio before doing a substitution. 
- **Encoding:** on Windows, always pass `encoding="utf-8"` to every `open()` for read AND write, or the `’`/`—` characters throw `charmap` errors and corrupt the typography. `PYTHONUTF8=1` is a safe global fallback.

## Completion status (as of 2026-06-29)

All substitution work is **complete**:
- All 24 book XHTML files have been updated (commit 5026a71).
- `toc.xhtml` entries mirror each book's `<p epub:type="title">` (Athena/Odysseus).
- `se:long-description` blurb in `content.opf` reads Odysseus/Poseidon. Upstream identifiers, dates, and source/VCS URLs in `content.opf` are intentionally left as-is.
- `epub-src/src/epub/text/endnotes.xhtml` was added explaining every name change and every name deliberately kept as Bryant wrote it.

Do not re-run substitutions — the books are already in their final Greek-names state.

### Book 0 added (2026-06-30)
- `epub-src/src/epub/text/book-0.xhtml` adds the audiobook's framing introduction (opening "This is an Eleven Productions original."), transcribed from the Michael Caine narration. It is **prose, not verse** — the only such chapter — and is titled "Book 0: Introduction".
- Registered in `content.opf` (manifest + spine, immediately before `book-1.xhtml`) and `toc.xhtml` (first entry under "The Odyssey"); the `bodymatter` landmark now points to `book-0.xhtml`.
- It is new content that already uses the Greek names (Odysseus), not a Bryant passage, so it is **exempt from the substitution scripts** — `extract_names.py` may surface its forms, but do not run `substitute.py` against it.

These files still contain Bryant forms **on purpose** — do not "fix" them:
- `preface.xhtml` — Bryant's 1871 preface arguing *for* keeping the Latin names; swapping would make it self-contradictory.
- `endnotes.xhtml` — quotes the Bryant forms to explain each change.
- `colophon.xhtml` — "Ulysses and the Sirens" is the actual title of the Waterhouse painting.

## Critical Caveat — Metre
Bryant wrote in blank verse (iambic pentameter). Roman and Greek names are often NOT syllable-equivalent. Substitutions WILL break metre in many lines. This is accepted and intentional for this edition — the goal is name consistency with the audio, not metrical perfection. Do NOT attempt to repair metre.

## Approach
- Preserve all XHTML tags exactly
- Preserve capitalisation (e.g. "Ulysses" → "Odysseus", "ULYSSES" → "ODYSSEUS")
- Handle possessives (e.g. "Ulysses'" → "Odysseus'")
- Do NOT substitute inside XML attributes, only inside text nodes