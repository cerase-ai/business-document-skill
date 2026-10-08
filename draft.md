# Stage 3 — the draft

Write `<slug>.md` in the workspace from the agreed outline. This Markdown is the original: every format is rendered from it, and every later correction is made in it.

If `<slug>-outline.md` is missing or the person has not agreed it, go back to stage 2. If `<slug>.md` already exists, ask whether to replace it or write under another name.

## 1. The file's shape

The renderer reads this shape:

```markdown
---
title: Office cleaning service, 2027 to 2029
subtitle: Economic and technical offer
author: <name and role, as the brief gives them>
date: <date>
recipient: <the reader's organisation and office>
reference: <the request's reference, if it has one>
---

# Premise

...
```

- The YAML block starts on line 1. Each field comes from the brief's title block; a field the brief does not give is left out, never filled. Put a value containing a colon in double quotes.
- `#` for a section, `##` for a sub-section, `###` at most.
- Pipe tables with a header row; a numeric column right-aligned with `|---:|`; a total row last, in bold.
- `- ` for bullets, at most seven to a group; `1. ` for steps in order.
- Every paragraph and every bullet on one line.

## 2. Writing each section

Each section opens with the sentence the outline gave it, and the rest of the section backs it up.

- **Premise.** Who asked for what, with the request's reference and date, in two to four sentences. No praise of the client.
- **Scope by area.** For each area, what we do and what the reader gets from it, in the reader's terms: the activities, how often, who does them, what they produce. A line of the price sheet names a cost item and says nothing about the work: never copy its labels as the scope. The effort per area comes from the outline's figures.
- **Amounts by period.** A table with the areas as rows and the periods as columns, as the sources split them, with a total for each row and each column and the grand total. Then the unit and the basis: days and daily rate, the currency, and whether tax is included, as the source states it. Premiums, options and penalties the sources carry each get their own row or line.
- **Conditions.** Payment terms, what is included and excluded, premiums and penalties: only those the sources or the person state.
- **Validity.** The period the brief gives. Without one, ask; a customary default is still an invented term.
- **Why us.** The reasons from the outline, each a fact about the organisation tied to what the reader needs or scores: comparable work done, a figure, a certification, the people on the job and their roles, with names only as given. Words like leading, excellent or tailored give the reader nothing to check: write the fact that would justify them instead.
- **Report.** The conclusion first, in the summary; then the evidence for it, section by section. A report built on several searches or sources names any that failed and what that leaves out, because it limits what the reader may conclude.
- **Letter.** One subject, the facts it rests on, what is asked or answered, and the next step, on one page.

## 3. Figures

Every figure is copied from the outline's `Printed as` column, never typed from memory or worked out here. A figure the outline does not hold goes back to stage 2. The amounts in the text and in the tables are the same values, in the same form.

## 4. Sentences

- Each sentence tells the reader something they can act on. Delete it in your head: if nothing is lost, it stays deleted.
- No slogans: no triads, no antithesis or chiasmus, no fragment for emphasis, no aphorism, no wordplay, no line that announces instead of saying. A document for a board or a tender commission is held to the same rule.
- A number instead of an adjective: `four people on site every working day`, not `a dedicated team`.
- Every table header and row label passes the label test: shown one value under it, a reader can say what the value asserts.
- A term the reader would have to look up, per the brief's two vocabulary lists, carries its meaning the first time it appears.
- In a report, an estimate or an inference of ours is marked as ours inside the sentence that carries it.
- Name who acts: we, the client, the evaluator. The passive hides the party who carries an obligation.
- Do not explain the readers their own trade.
- Nothing about how the document was made: no sources searched, no checks run, no corrections, no assurances of diligence.

## 5. Check before declaring the draft done

- [ ] Every section of the outline is there, opening with its sentence.
- [ ] Every element under `Use` in the brief appears.
- [ ] Every figure is in the outline's figures table, printed as it says.
- [ ] Every claim about the organisation, the reader or a third party has a source in the brief.
- [ ] No discount, deadline, date, name, guarantee, reference or promised result that nobody gave.
- [ ] `Why us` holds facts, each tied to the reader.
- [ ] No slogan, no filler, no sentence about the making of the document.
- [ ] Every label passes the label test.

Then hand over to stage 4.
