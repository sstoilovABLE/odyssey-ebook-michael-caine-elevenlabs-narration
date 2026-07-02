# 📋 Project Task Tracker

- [x] Update LICENSE.md
- [x] Add .gitignore
- [x] Create script to extract Roman name occurrences from the original WCB translation epub files
- [x] Add README.md
- [x] Create script to substitute Roman names with Greek ones
- [x] Create substitution table JSON with Roman names and Greek equivalents
- [x] Substitute Roman names with Greek ones, insofar as needed to match the Michael Caine narration
- [x] Create/update CLAUDE.md
- [x] Reorganize project directory to be cleaner
- [x] Create Chapter 0 from the Michael Caine narration
- [x] Write Editor's Note for the front and move WCB Preface to the end
    - [x] Rewrite colophon.xhtml (de-brand, factual lineage, record modifications, name editor)
    - [x] Update content.opf metadata (editor contributor, de-brand publisher/VCS, source, descriptions)
- [x] Write an endnote for the bridgehead section at the beginning of each book - explain it is not read out by Michael Caine but is kept for context and authenticity (added as note-1 on Book 1's bridgehead only; existing name-notes renumbered 2–20)
- [x] Renamed "Book 0" to a front-matter "Introduction" (`introduction.xhtml`, placed after the editor's note and before the half-title page; dropped the `se:label`/ordinal and `p` title; updated content.opf, toc.xhtml, colophon, README, CLAUDE.md)
- [x] Write an endnote for the Introduction - explain it is not in the original Odyssey but added to match the ElevenLabs narration
- [x] Fix Book 1 bridgehead: Bryant's argument said Athena appeared "in the shape of Mentor," but Book 1's own text has her as Mentes (Mentor is a distinct character, impersonated by Athena only later, in Books 2, 22, and 24) — corrected the argument to "Mentes" and added an explanatory endnote (new note-2; all subsequent notes renumbered up by one, now 1–22). This is an editorial correction of a Bryant slip, unrelated to the Greek/Roman deity-name substitution project — not run through `substitute.py`.
- [ ] Create new book cover; remove Standard Ebooks branding/wordmark from it
- [ ] De-brand the title page (titlepage.svg) and add an editor credit
- [ ] De-brand the imprint (imprint.xhtml): remove the SE logo, or drop the imprint page entirely
- [ ] Remove images/logo.svg from the manifest and delete it once nothing references it
- [ ] Revisit colophon cover-art/typeface credits after the cover/title-page redesign
- [ ] Decide whether to mint a new dc:identifier and update dc:date for this fork edition
- [ ] Review the "Standard Ebooks makes no representations" line in uncopyright.xhtml
- [ ] Run se lint; fix all lint warnings and errors
- [ ] Regenerate manifest/spine/TOC with se tooling and verify landmarks
- [ ] Build EPUB
- [ ] Test on Google Play Books and Calibre ebook reader
- [ ] Compile final v1.0 EPUB and upload it to Releases


# Actions to be done after every task

- Update README.md and CLAUDE.md only after significant tasks that concern the whole project — not after small or narrowly-scoped fixes
- Update TASKS.md to reflect tasks completed and to potentially add new tasks that may need to be done
