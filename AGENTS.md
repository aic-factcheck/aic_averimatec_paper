# AGENTS.md

## TODO (complete before using this file)
- [x] Define the role and scope of the agent for this repository.
- [x] Summarize the repository structure and primary artifacts.
- [x] Specify editing, formatting, and citation expectations for LaTeX/BibTeX.
- [x] Record build/compile commands and where outputs land.
- [x] Note figure/data handling conventions.
- [x] Add safety checks and review expectations before finalizing changes.

## Agent profile
- **Role:** Assist with editing, organizing, and validating the LaTeX paper and its supporting artifacts.
- **Scope:** Work within this repository only; avoid modifying external configs or global tooling unless explicitly requested.
- **Priorities:** Correctness of content, consistent formatting, and reproducible builds.

## Repository map (high level)
- `emnlp2023.tex`: Main LaTeX source.
- `emnlp2023.sty`, `acl_natbib.bst`: Style and bibliography formatting.
- `custom.bib`, `reduced.bib`, `anthology.bib`: Bibliography databases.
- `figures/`: Figures and plots.
- `src/`: Scripts or auxiliary sources (inspect before use).

## Editing guidelines
- **LaTeX:** Preserve the existing structure and macro conventions; keep edits minimal and localized.
- **Citations:** Use existing citation keys; add new entries only to the appropriate `.bib` file.
- **Formatting:** Follow the style file constraints; avoid manual spacing tweaks unless unavoidable.
- **Comments:** Keep concise; remove temporary comments before final output.

## Figures and data
- Prefer vector formats where possible.
- Do not overwrite source figure files without confirming the generation pipeline.
- If a figure is updated, verify references in the LaTeX source.

## Build/compile
- Primary compile target: `emnlp2023.tex`.
- If needed, run a standard LaTeX build (e.g., `latexmk`), then check for warnings and missing references.

## Review checklist before final response
- Ensure references compile without missing citations.
- Check for LaTeX warnings introduced by edits.
- Confirm that changes are limited to the requested scope.
- Summarize what changed and where.
