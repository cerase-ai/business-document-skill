# Stage 1 — the brief

Read the sources, interview the person, then write `<slug>-brief.md` in the workspace. The outline reads it to decide every section and every figure: who reads the document, what it must achieve, what it must contain, and where each fact comes from.

If `<slug>-brief.md` already exists, ask whether to replace it, add to it, or write a new file under another name. Never overwrite it silently.

## 1. Read the sources before asking

When the person names or attaches material, such as a price sheet, a call for tenders, a client's request, an earlier offer or a profile of the organisation, read all of it first, so the interview asks only what the sources do not say.

- A file in the workspace (PDF, Word, Excel, CSV): `call_recipe("cerase-docreader.read_document", {"path": "<file>"})`.
- A Google Doc: `call_recipe("google-workspace.readGoogleDoc", {"documentId": "<id>", "format": "markdown"})`.
- A Google Sheet: first its tabs with `call_recipe("google-workspace.getSpreadsheetInfo", {"spreadsheetId": "<id>"})`, then every tab that carries figures with `call_recipe("google-workspace.getGoogleSheetContent", {"spreadsheetId": "<id>", "range": "<tab>!A1:Z200"})`. A split by year, an option or a premium often sits on a tab of its own.

A document somebody else wrote that you cannot open is asked for, never rebuilt from memory or from a summary.

Then list every element the sources offer the document: each line of the price sheet with its quantity, unit and rate; every split by period, such as years, quarters or phases; every option, premium, penalty, discount and condition the sheet or the request states; every requirement of the request, with the criteria the reader will score it on when the request gives them. An element of the sources that does not reach the document is left out by a decision written in the brief, never by oversight.

## 2. The interview

Ask in this order, one or two questions at a time, in the person's language. When the person does not know, write `unknown` and move on; the outline asks again where it matters.

1. **Kind.** A quote or an offer, a proposal, a report, a letter, or another kind the person names.
2. **Reader.** Who reads it: role, organisation, what they decide. For a tender, who evaluates the bids and on which criteria. What they already know, which terms they use every day and which they would have to look up.
3. **Objective.** The one thing the document must achieve: be chosen, have a budget approved, inform a decision, answer a request. For a quote or an offer: what is offered, to whom, for which period.
4. **Required content.** The sections, figures, conditions, attachments and declarations the request, the client or the person require, with who requires each.
5. **Depth.** The length in pages or words, and the level of detail: by area, by activity, by month.
6. **Sources of the figures.** For every figure the document will carry, the file and the place in it. Where two sources disagree, ask which one holds.
7. **The organisation and the person.** The material for the argument: what the organisation does and for whom, comparable work, numbers, certifications, the people who will do the work and their roles, and the role of the person you are writing for. Take it from what you have, such as the organisation's instructions, the sources or a profile the person points to, and ask for what is missing. Prefer facts that answer the reader's criteria. A fact about the organisation that nobody gave you is not added.
8. **Form.** The format, PDF unless the person asks for Word or a Google Doc. Paper, A4 by default, and orientation, portrait by default. The brand: colours, fonts or CSS, or `default`. The title block: title, subtitle, author, date, recipient, reference, each only as given. Whether the text goes into a document that already exists, which `existing-document.md` then covers.
9. **Language and tone.** The document's language, by default the person's, and the register: formal, neutral or direct.
10. **Confirm, then write.** Summarise the brief in five to ten lines, ask the person to confirm, then write the file.

## Check before writing

- The reader is concrete: a role in an organisation, not "the client".
- The objective is one sentence.
- Every figure the document will carry has a named source, or is listed under `Missing`.
- Every fact for the argument has a source.
- Every element of the sources is either in `Use` or in `Leave out` with its reason.

If one of these is empty after the interview, ask one more targeted question before writing.

## The file

Write `<slug>-brief.md` with these headings exactly, in short bullets:

```markdown
# Document brief — <slug>

## Kind
- <quote | offer | proposal | report | letter | other: ...>

## Reader
- Who: ...
- What they decide: ...
- Evaluation criteria: ...
- Terms they use every day: ...
- Terms they would have to look up: ...

## Objective
- ...

## Required content
- <item> — required by <the request | the client | the person>

## Depth
- Length: ...
- Detail: ...

## Sources
- <file and place> — <what it carries>

### Use
- <element of the sources> — <the section it goes to>

### Leave out
- <element of the sources> — <the reason, and who decided>

## The organisation, for the argument
- <fact> — <source>

## Form
- Format: <PDF | Word | Google Doc>
- Paper and orientation: ...
- Brand: <default | colours, fonts or CSS as given>
- Title block: <title, subtitle, author, date, recipient, reference, as given>
- Existing document: <none | its name and id>

## Language and tone
- Language: ...
- Register: ...

## Missing
- <datum> — <who can give it>
```

Then tell the person the brief is written and that the next stage is the outline.
