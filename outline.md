# Stage 2 — the outline

Read `<slug>-brief.md` and the sources it lists, write `<slug>-outline.md`, show it to the person and wait for their agreement. The draft writes nothing the outline does not hold.

If `<slug>-brief.md` is missing, offer to run the brief first, or ask the person to paste its content. If `<slug>-outline.md` already exists, ask whether to replace it or write under another name.

## 1. Choose the sections

When the request prescribes sections, their order or their titles, use those. Otherwise start from the kind:

| Kind | Sections |
|---|---|
| Quote or offer | Premise · Scope by area · Amounts by period · Conditions · Validity · Why us |
| Proposal | The need · What we propose · Plan and timeline · Team · Investment · Why us · Next step |
| Report | Summary with the conclusion · Context · Findings · Figures · Decisions asked or recommendations |
| Letter | One subject: the facts, the request or the answer, the next step; one page |

Add a section only for content the brief requires, and drop one only when the brief gives it nothing to say.

## 2. Write each section's sentence

Under each heading, write the one sentence the section establishes for the reader, in full: what it argues, not its topic. `Scope: the three areas` is a topic. `We run the three areas with the same team of four, and each area has its own weekly report` is a sentence. A section whose sentence you cannot write has nothing to say: merge it into its neighbour or cut it now.

`Why us` gets one line per reason. Each reason is a fact about the organisation from the brief's argument list, tied to a criterion or a need of the reader. An adjective is not a reason. When the brief holds no fact for the argument, ask the person for one before going on.

## 3. Compute every figure now

List every figure the document will carry, in the order it appears. Compute each one now with the calculator in `SKILL.md` from the values in the sources, and write down the call and its answer. The draft copies these values and never computes.

- A single value from a source: its file and place.
- A product, such as days × daily rate: `product` on the two source values.
- A sum, such as an area over its years or the grand total over the areas: `sum` on the values it adds.
- A percentage of something: `calculate` with the rate as a decimal.
- A rounded amount: `round`, only where the source or the convention of the document asks for rounding.

Then check the structure of the amounts with the calculator: every area's periods sum to the area's total, every period's areas sum to the period's total, and both sets sum to the same grand total. When the sources' own totals disagree with the calculator, the figure is not drafted: tell the person which figure, what the sources say and what the calculator gives, and ask which holds.

Every element listed under `Use` in the brief appears in a section: a split by period appears as amounts by period, a premium or an option as its own row or condition.

## 4. The file

```markdown
# Outline — <slug>

## <Section heading>
Sentence: <what this section establishes, in full>
Figures: <F1, F2>
Sources: <the brief's source lines this section draws on>

## Why us
- <reason> — <fact and its source> — <the reader's criterion or need it answers>

# Figures

| Id | Figure | Value | Printed as | Source or call |
|---|---|---:|---:|---|
| F1 | Area A, days in year 1 | 36 | 36 | price sheet, tab Years, row 4 |
| F2 | Area A, daily rate | 680 | 680 | price sheet, tab Rates, row 2 |
| F3 | Area A, year 1 amount | 24480 | 24.480 | product(F1, F2) |

# Checks
- <each sum that must hold, with the calculator's answer>

# Terms
- <validity, payment rhythm, …> — <the brief's source or the person's answer> | assumed — <the earlier document it was seen in>

# Missing
- <datum> — <who can give it>
```

`Value` is the calculator's `value`, `Printed as` the form the document prints, which for an Italian document is `value_it`.

## 5. Agree it with the person

Show the outline in the chat, in the person's language: each section with its sentence, the grand total with its split by area and by period, each term taken only from an earlier document with the question that would settle it, and what is missing. Ask whether it holds or what to change. Update the file with their changes, and start the draft only after they agree.
