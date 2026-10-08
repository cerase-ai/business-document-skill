# business-document-skill

A Cerase skill that has the assistant write a quote, an offer, a bid for a
tender, a proposal, a report, a business letter or another document for a
client or for management, and write text into a document that already exists,
such as a Google Doc or a letterhead. A slide deck is the `deck` skill, and the
text of an email is the `email-drafting` skill.

## What the assistant does

The document is built in five stages. Each one writes a file in the workspace
that the next one reads, named after a slug of the document's title chosen in
the brief, and the assistant tells the person which stage it is on. There is no
draft before the person agrees the outline, and no delivery before the
revision has closed.

1. **Brief** (`brief.md`). Reads every source the person names or attaches
   before asking anything: files in the workspace with
   `cerase-docreader.read_document`, Google Docs with
   `google-workspace.readGoogleDoc`, and every tab of a Google Sheet with
   `google-workspace.getSpreadsheetInfo` and
   `google-workspace.getGoogleSheetContent`. It lists every element the sources
   offer: each price line with its quantity, unit and rate, each split by
   period, each option, premium, penalty and condition, each requirement of
   the request with the criteria it will be scored on. Then it interviews the
   person one or two questions at a time: the kind of document, the reader, the
   objective, the required content, the depth, the source of every figure, the
   facts about the organisation for the argument, the form (format, paper,
   brand, title block), the language and the tone. It writes
   `<slug>-brief.md` once the person confirms a summary of it.
2. **Outline** (`outline.md`). Takes the sections from the request, or from
   the kind of document: a quote has premise, scope by area, amounts by
   period, conditions, validity and why us, and a proposal, a report and a
   letter each have their own set. Under each heading it writes the one
   sentence that section establishes for the reader. It computes every figure
   with the calculator now, and checks that every area's periods and every
   period's areas sum to the same grand total. It shows the outline with the
   grand total and what is missing, and waits for the person to agree it.
3. **Draft** (`draft.md`). Writes `<slug>.md` in Markdown with a YAML title
   block, one section per heading of the outline, each opening with its
   sentence. Every figure is copied from the outline's figures table. The
   writing rules: a number instead of an adjective, no slogans, every table
   header and row label passing the label test, and nothing about how the
   document was made.
4. **Revision** (`revise.md`). A sub-agent given only the document, the
   outline's figures, the sources and the brief's description of the reader
   runs eight checks: every figure recomputed with the calculator and every
   table summed by row and by column; nothing invented (discounts, dates,
   names, guarantees, references, certifications, promised results); every
   claim sourced or cut; every element of the sources used; the required
   content present; every sentence about the subject rather than about how it
   was made; reasons given as facts tied to the reader's criteria; the
   writing. It writes `<slug>-revision.md` and corrects `<slug>.md`. Without a
   sub-agent the assistant runs the checks itself and records that in the
   file. A total that does not add up, or a finding the person has not
   settled, stops the delivery.
5. **Render and deliver.** Renders `<slug>.md` to PDF with
   `cerase-office-converter.render_document`, on A4 portrait unless the brief
   says otherwise and with the brand as `template_css` when the brief records
   one. It reads the PDF back with `cerase-docreader.read_document` to check
   the title block, the sections and the totals, attaches it with
   `[[attach: outputs/<slug>.pdf]]`, and tells the person what the document
   contains and what is missing. Word or a Google Doc only when the person
   asks, through the `docx` skill.

**Text for a document that already exists** (`existing-document.md`). In a
Google Doc the assistant reads the document's tabs, its sections and the style
of the paragraphs around the place the text goes, and asks whether to change
the original or a copy. It inserts the text at that place with the
neighbours' paragraph style, font, size, colour and bullets, replaces a
template's placeholders in place after a dry run that counts the matches, and
reads the area back. A letterhead in Google Docs is copied for each letter; a
letterhead in Word is the `docx` skill's template. A PDF of a Google Doc is the
one Google exports. Stages 1, 2 and 4 apply to this text too.

Every figure comes from a source or from the calculator, never from the
assistant's own arithmetic. A detail nobody gave (a discount, a deadline, a
name, a guarantee) does not enter the document, and a missing figure is named
to the person rather than estimated. Chat follows the person's language; the
brief, the outline, the revision and the document follow the document's
language, by default the person's.

## Requirements

- The `cerase-calc` connector, for every figure: `calculate`, `sum`,
  `product` and `round`.
- The `cerase-office-converter` connector: `render_document`, for the PDF or
  an HTML page.
- The `cerase-docreader` connector: `read_document`, for the sources in the
  workspace and for reading the rendered PDF back.
- The `google-workspace` connector, for Google Docs and Sheets as sources and
  for writing into an existing Google Doc: `readGoogleDoc`,
  `getSpreadsheetInfo`, `getGoogleSheetContent`, `getDocumentInfo`,
  `listDocumentTabs`, `getGoogleDocContent`, `getGoogleDocContentPaginated`,
  `copyFile`, `insertText`, `applyParagraphStyle`, `applyTextStyle`,
  `createParagraphBullets`, `findAndReplaceInDoc`, `downloadFile`. Without it
  the assistant says the organisation's administrator assigns it, and offers
  the document as a PDF.
- The `docx` skill, for Word or a Google Doc as the output format.

## Files

| File | Purpose |
|---|---|
| `SKILL.md` | The instructions the assistant loads: the five stages, the rules that hold in every stage, the calculator calls, the render and the delivery. |
| `brief.md` | Stage 1: reading the sources, the interview, the checks before writing, and the brief's template. |
| `outline.md` | Stage 2: sections by kind of document, one sentence per section, every figure computed, and the outline's template. |
| `draft.md` | Stage 3: the Markdown shape the renderer reads, how each section is written, figures and sentences, and the check before the draft is done. |
| `revise.md` | Stage 4: who runs the checks, the eight checks, and the revision file. |
| `existing-document.md` | Writing into an existing Google Doc or letterhead, reading it back, and a Google Doc's PDF. |
| `cerase.json` | Marketplace manifest: namespace `studio.guidance`, name `business-document`, display name, description, licence. |
| `i18n.yaml` | Italian display name and description for the Marketplace; not sent to the assistant. |
| `LICENSE` | MIT licence text. |

## Installation

Published in the Cerase Marketplace as `studio.guidance/business-document`
([marketplace page](https://marketplace.cerase.ai/en/p/studio.guidance/business-document)).
A Cerase appliance also ships it in its image and attaches it to every
assistant; an administrator cannot detach it.

## License

MIT. See [LICENSE](LICENSE).
