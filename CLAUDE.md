# Claude.md - AIC AVeriTeC Paper Repository Guide

## Project Overview
This repository contains the LaTeX source for the paper **"AIC CTU@AVerImaTeC: dual-retriever RAG for image-text fact checking"** describing the 3rd place system in the AVerImaTeC shared task at EMNLP 2023.

**Authors:** Herbert Ullrich and Jan Drchal (AI Center @ CTU FEE, Prague)

**Key Contribution:** A simple yet competitive RAG pipeline combining textual retrieval with reverse image search, achieving competitive performance at ~$0.013 per fact-check using GPT-4o via OpenAI batch API.

## Repository Structure

```
.
├── emnlp2023.tex           # Main paper file (entry point)
├── emnlp2023.sty           # EMNLP 2023 style file (DO NOT EDIT)
├── acl_natbib.bst          # Bibliography style (DO NOT EDIT)
├── custom.bib              # Custom bibliography entries (28KB)
├── reduced.bib             # Reduced bibliography subset (11KB)
├── anthology.bib           # ACL anthology entries (81MB - LARGE!)
├── figures/                # All figures and plots
├── src/                    # LaTeX input files
│   ├── introduction.tex
│   ├── system_description.tex
│   ├── results.tex
│   ├── conclusions.tex
│   └── appendix_a_llms.tex
├── aux/                    # Build artifacts (LaTeX aux files)
└── .vscode/                # VSCode settings
```

## Key Files

### Main LaTeX File
- **[emnlp2023.tex](emnlp2023.tex)**: Entry point, includes all sections via `\input{}` commands
  - Lines 109-114: Section includes (some commented out)
  - Lines 118-130: Limitations, ethics, acknowledgements
  - Line 134: Bibliography includes anthology + custom
  - Lines 137-142: Appendix includes

### Content Sections (in src/)
- **[src/introduction.tex](src/introduction.tex)**: Paper introduction
- **[src/system_description.tex](src/system_description.tex)**: System architecture and methodology
- **[src/results.tex](src/results.tex)**: Experimental results and analysis
- **[src/conclusions.tex](src/conclusions.tex)**: Conclusions and future work
- **[src/appendix_a_llms.tex](src/appendix_a_llms.tex)**: LLM prompts and details

### Bibliography Files
- **[custom.bib](custom.bib)**: Custom references (primary editing target for new citations)
- **[reduced.bib](reduced.bib)**: Reduced citation set
- **[anthology.bib](anthology.bib)**: Full ACL anthology (81MB - avoid editing directly)

## Custom LaTeX Commands

Defined in [emnlp2023.tex:44-58](emnlp2023.tex#L44-L58):

```latex
\averitec        → AVerImaTeC (task name)
\evr             → Ev²R (notation)
\supp            → Supported (label)
\reff            → Refuted (label)
\nei             → Not enough evidence (label)
\conf            → Conflicting evidence/Cherrypicking (label)
\todo{text}      → Red/yellow highlighted TODO
\review{text}    → Black text (review mode macro)
\footnoteref{#}  → Reference existing footnote
```

**IMPORTANT:** Always use these macros instead of literal text for consistency.

## Build & Compile

### Primary Build Command
```bash
pdflatex emnlp2023.tex
bibtex emnlp2023
pdflatex emnlp2023.tex
pdflatex emnlp2023.tex
```

Or use `latexmk` for automatic builds:
```bash
latexmk -pdf emnlp2023.tex
```

### Review vs Final Mode
- **Review mode** (current): Line 8 `\usepackage[review]{EMNLP2023}`
- **Final mode**: Remove `[review]` option before submission

### Build Output Location
- PDF output: `emnlp2023.pdf`
- Auxiliary files: `aux/` directory

## Editing Guidelines

### General Principles
1. **Preserve structure**: Keep existing section organization and macro conventions
2. **Minimal changes**: Only edit what's necessary for the requested task
3. **No over-engineering**: Avoid "improvements" beyond the scope
4. **Consistency**: Follow existing formatting patterns
5. **LaTeX best practices**: Use semantic markup, avoid manual spacing

### Content Editing
- Edit section files in `src/`, not the main [emnlp2023.tex](emnlp2023.tex)
- Use custom commands (`\averitec`, `\evr`, etc.) consistently
- Keep paragraph structure aligned with ACL formatting guidelines
- Avoid manual line breaks unless required by formatting

### Citation Management
1. **Adding citations:**
   - Add new entries to [custom.bib](custom.bib) (preferred)
   - Use consistent BibTeX formatting
   - Cite in text with `\cite{key}` or `\citep{key}`

2. **Citation styles:**
   - Narrative: `\citet{key}` → "Author (Year)"
   - Parenthetical: `\citep{key}` → "(Author, Year)"

3. **Verification:**
   - Check all `\cite{}` commands resolve
   - Run BibTeX after adding citations
   - Verify no "?" in PDF output

### Figures and Tables
- Store all figures in [figures/](figures/) directory
- Prefer vector formats (PDF, SVG → PDF) over raster (PNG, JPG)
- Reference figures: `\ref{fig:label}`
- Include figures:
  ```latex
  \begin{figure}[t]
    \centering
    \includegraphics[width=\columnwidth]{figures/filename.pdf}
    \caption{Caption text.}
    \label{fig:label}
  \end{figure}
  ```

### DO NOT Edit
- [emnlp2023.sty](emnlp2023.sty): Conference style file
- [acl_natbib.bst](acl_natbib.bst): Bibliography style
- [anthology.bib](anthology.bib): ACL anthology (too large, use as read-only)

## Common Workflows

### Adding a New Section
1. Create file in `src/new_section.tex`
2. Add `\input{src/new_section}` to [emnlp2023.tex](emnlp2023.tex)
3. Rebuild to verify

### Adding a Figure
1. Place file in `figures/`
2. Add `\includegraphics` in appropriate section
3. Add `\label{fig:name}` for cross-referencing
4. Verify with rebuild

### Adding a Citation
1. Add entry to [custom.bib](custom.bib)
2. Use `\cite{key}` in text
3. Run full build cycle (pdflatex → bibtex → pdflatex × 2)
4. Check for warnings in output

### Updating Results/Tables
1. Edit [src/results.tex](src/results.tex)
2. Preserve table formatting (use `booktabs` package)
3. Rebuild and verify alignment

## Quality Checks Before Finalizing

Run through this checklist before completing any task:

- [ ] **Build succeeds**: No LaTeX errors
- [ ] **No warnings**: Check for undefined references, overfull boxes
- [ ] **Citations resolve**: No "?" for citations
- [ ] **Figures display**: All `\includegraphics` work
- [ ] **Cross-references work**: All `\ref{}` resolve
- [ ] **Custom macros used**: Not literal text where macros exist
- [ ] **Consistent formatting**: Follows existing patterns
- [ ] **Only requested changes**: No scope creep
- [ ] **Git status clean**: Understand what changed

## Important Constraints

### Paper Limits
- Conference format: EMNLP 2023
- Page limit: Check conference guidelines
- Currently in review mode with line numbers

### Technical Details
- Uses `pdflatex` (required, see [emnlp2023.tex:1-2](emnlp2023.tex#L1-L2))
- UTF-8 encoding
- Font: Times (11pt)
- Bibliography: natbib with ACL style

### Dataset & System Details
- **Dataset:** AVerImaTeC (image-text fact verification)
- **Task:** Multi-modal fact checking with evidence retrieval
- **System:** Dual-retriever RAG (text similarity + reverse image search)
- **Model:** GPT-4o (referred to as GPT5.1 in text - verify this nomenclature)
- **Cost:** ~$0.013 per fact-check via OpenAI batch API
- **Result:** 3rd place in shared task

### Label Classes
Use macros for consistency:
- Supported: `\supp`
- Refuted: `\reff`
- Not enough evidence: `\nei`
- Conflicting evidence/Cherrypicking: `\conf`

## Known Issues & Notes

1. **GPT nomenclature:** Paper uses "GPT5.1" - verify this refers to GPT-4o
2. **Class imbalance:** 95% refuted in train, 78% in test (mentioned in limitations)
3. **Large anthology.bib:** 81MB file - avoid opening/editing directly
4. **Commented sections:** Some inputs commented out in main file (classification, software, appendices B-C)

## GitHub Repository
Code available at: `https://github.com/heruberuto/AVerImaTec_Shared_Task`

## When Working on This Repository

1. **Always read before editing**: Don't propose changes to files you haven't read
2. **Use custom commands**: Leverage `\averitec`, `\evr`, etc.
3. **Preserve formatting**: Follow ACL/EMNLP guidelines
4. **Test builds**: Rebuild after changes
5. **Check references**: Ensure citations and cross-refs work
6. **Stay focused**: Only make requested changes
7. **Document changes**: Summarize what changed and where

## Contact & Attribution
- Herbert Ullrich: ullriher@fel.cvut.cz
- Jan Drchal: drchajan@fel.cvut.cz
- AI Center @ CTU FEE, Prague, Czech Republic

---

**Last Updated:** 2026-01-31
**Repository:** aic_averimatec_paper
**Purpose:** System description paper for AVerImaTeC shared task @ EMNLP 2023