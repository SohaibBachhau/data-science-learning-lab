# Repository Instructions

## Purpose

This repository is a long-term learning system for mathematics, probability, statistics, econometrics, programming, data science, machine learning, deep learning and artificial intelligence.

## Organization

- Store official course-specific materials under `courses/`.
- Store permanent explanations by subject under `knowledge/`.
- Store long mathematical proofs under `derivations/` when they would interrupt a concept note.
- Store simulations and coding experiments under `labs/`.
- Store practice material under `exercises/` and retrieval material under `review/`.
- Store bibliographic notes under `references/`.
- Avoid duplicating complete explanations across folders. Link to the permanent note instead.

## Knowledge notes

Each permanent concept note should contain, when relevant:

- a central question;
- a concise answer;
- intuition;
- a formal definition;
- notation;
- assumptions and existence conditions;
- main properties;
- a derivation or proof outline;
- an example;
- a counterexample or failure case;
- common mistakes;
- retrieval questions;
- links to related notes;
- sources and a review log.

Use these status values:

- `seed`: an initial rough note;
- `developing`: substantially written but still being checked or expanded;
- `stable`: reviewed, accurate and well connected to the repository.

Do not mark a note as `stable` merely because it is long or complete in appearance.

## Mathematical notation

- Use `$...$` for inline mathematics.
- Use `$$...$$` for display mathematics.
- Put opening and closing display delimiters on separate lines.
- Do not use `\(`, `\)`, `\[` or `\]` as Markdown delimiters.
- Define each symbol before or immediately after its first use.
- Distinguish scalars, vectors, matrices, random variables, realizations, parameters, estimators and estimates.
- State whether a result is exact, conditional, unconditional or asymptotic.
- State the assumptions used at the step where they matter.

## Sources

- Preserve course terminology when writing course-specific notes.
- Distinguish source-derived material, personal interpretation and additional explanation.
- Record books, slides, lectures or papers in the `Sources` section.
- Do not upload copyrighted books, lecture slides, solution manuals or restricted course materials unless redistribution is permitted.
- Keep locally stored source PDFs excluded through `.gitignore`.

## Writing style

- Explain intuition before introducing dense notation.
- Prefer clear prose over compressed formula lists.
- Explain why each important mathematical step is valid.
- Avoid claiming an assumption is necessary when it is only sufficient.
- Record common misunderstandings explicitly.
- Link to an existing explanation instead of repeating it.

## Git workflow

- Review rendered Markdown mathematics before committing.
- Check for unmatched code fences and math delimiters.
- Use focused, descriptive commit messages.
- Do not commit secrets, private data, copyrighted PDFs or generated system files.
