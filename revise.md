# Stage 4 — the revision

Read `<slug>.md` as its reader will, run the checks below, write what they find in `<slug>-revision.md`, and correct `<slug>.md`. A document is not rendered for delivery before this stage has closed.

## Why the author cannot do this alone

The author knows what each line meant and what each figure was supposed to be, so on re-reading they see the intended value instead of the printed one. A reader with the sources and without the reasoning finds in minutes an amount that does not multiply out, a total that does not match, or a detail nobody gave.

## Inputs

| What | Where | Used for |
|---|---|---|
| The document | `<slug>.md` | the text under review, and where the corrections go |
| The figures | the `Figures` and `Checks` blocks of `<slug>-outline.md` | what each figure should be and where it comes from |
| The sources | the files and places the brief's `Sources` block lists | tracing every figure and claim |
| The reader | the `Reader`, `Required content`, `Use` and `The organisation, for the argument` blocks of `<slug>-brief.md` | who reads it, what must be there, which facts are given |

## Who runs the checks

Run them through a sub-agent: start one with your task tool, of type `general`, and give it the paths above, this file's path, and the instruction to run the checks, write `<slug>-revision.md` in the format below and apply the corrections to `<slug>.md`. Give it nothing else: no chat, no notes, no reason why a section is there.

If you cannot start a sub-agent, run the checks yourself and write in the revision file that the author ran them.

## The checks

Run all of them, section by section.

### (a) Every figure, recomputed

List every number in `<slug>.md`: amounts, quantities, rates, percentages, dates, durations. For each one:

1. Find its source: a value read from a file and place, or a calculation on such values.
2. Recompute every calculated figure now with the calculator in `SKILL.md`, from the source values and not from the draft's: `product` for days × rate, `sum` for every total, `calculate` for a percentage, `round` where the document rounds.
3. Compare the printed figure with the calculator's answer, character by character in the document's printed form.

Every figure this stage changes or carries is recomputed here, in this stage: a value the outline already computed is computed again now, and the revision file lists each figure with the call that recomputed it. A figure this stage did not recompute is marked «not checked» in the revision file, and the report to the person names it.

Then the structure: every row and every column of each table sums to its total, the split by period sums to the grand total, and every total in the text equals the one in its table.

A figure with no source and no calculation is a finding: it comes out, or the person supplies it. **A total that does not add up stops the stage**: correct it from the sources, or, when the sources disagree, tell the person which figure, what each source says and what the calculator gives, and wait for their answer.

### (b) Nothing invented

Read the document for each of these by name: discounts, deadlines and dates, names of people, companies or products, guarantees and service levels, references and past clients, certifications, promised results. Each one traces to a source or to something the person said; whatever does not comes out, even when it reads as normal for this kind of document.

### (c) Every claim, sourced or cut

Every statement about the organisation, the reader, the market or a third party has its source in the brief or in a document the person gave. A claim with no source comes out. In a report, an estimate or an inference of ours is marked as ours inside its sentence.

### (d) The sources, used

Every element under `Use` in the brief appears in the document. A split by period, an option or a premium the sources carry and the document lacks is a finding.

### (e) Required content

Every item under `Required content` in the brief is in the document, in the place and under the title the request prescribes when it prescribes one.

### (f) The reader's test

For each sentence, ask who it is about. About the subject the reader acts on, it stays. About the author, the method, the sources consulted, a check run or a correction made, it comes out. A figure carrying a warning is a finding: the figure is either made sound or removed, and the warning goes with it.

### (g) The argument

`Why us` and every other reason given to the reader is a sourced fact tied to a need or a criterion of the reader. An adjective standing where a fact should be is a finding. A section that only repeats the price sheet's labels is a finding.

### (h) The writing

- Each sentence passes the delete test: deleted, the reader would lose information.
- No slogans: triads, antithesis, chiasmus, fragments for emphasis, aphorisms, wordplay. Read the title, the subtitle and every section's first and last sentence again: that is where they hide.
- Every table header and row label passes the label test.
- Every term on the reader's look-up list carries its meaning the first time it appears.
- No placeholder is left: no `<...>`, no `[...]`, no `XX`, no field the template expected and nobody filled.

## The revision file

```markdown
# Revision — <slug> — <date>

Run by: <a sub-agent | the author, no sub-agent available>

## Findings

| Section | Check | Line or figure | What is wrong | Correction applied |
|---|---|---|---|---|
| Amounts by period | a | Area B, year 2 | 20 × 680 printed as 14.600; the calculator gives 13.600 | corrected, and the totals after it |
| Why us | b | "response within 4 hours" | no source gives this service level | removed |

## Figures

| Figure | Printed as | The call that recomputed it |
|---|---:|---|
| Area B, year 2 | 13.600 | product(20, 680) |
| Grand total | 38.080 | sum(24480, 13600) |
| Premium, year 1 | 1.468,80 | not checked |

## Sections with no finding
<their headings>

## Not corrected, and why
<what is left and the reason; the section stays even when empty>
```

## Closing the stage

1. After the corrections, run check (a) once more on every figure the corrections touched and on every total.
2. Tell the person, in their language, how many figures this stage recomputed and which it did not, the findings in full, and what is left open. Never "it looks fine".
3. A finding left open is the person's to accept or not. While one is open, or while a total does not add up, the document is not rendered for delivery.
