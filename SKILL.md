---
name: business-document
description: "Applies when the person asks for a quote, an offer, a bid for a tender, a proposal, a report, a business letter or another document written for a client or for management, and when text has to go into a document that already exists, such as a Google Doc or a letterhead. Builds the document in five stages: a brief, an outline the person agrees, a Markdown draft, a revision that recomputes every figure with the calculator and traces every claim to its source, and a PDF rendered from the Markdown and delivered as an attachment. Not for a slide deck, which is the deck skill, nor for the text of an email, which is email-drafting."
---
# Business document — a quote, an offer, a proposal, a report, a letter

Each stage writes a file in the workspace that the next one reads. Go through them in order, and tell the person in one line which stage you are on. `<slug>` is the document's title as a slug, such as `quote-office-cleaning-2027`, chosen in the brief and kept to the end.

| Stage | Read first | Reads | Writes |
|---|---|---|---|
| 1. Brief | `brief.md` | the interview and the sources | `<slug>-brief.md` |
| 2. Outline | `outline.md` | the brief and the sources | `<slug>-outline.md`, agreed with the person |
| 3. Draft | `draft.md` | the outline, the brief, the sources | `<slug>.md` |
| 4. Revision | `revise.md` | `<slug>.md`, the outline, the sources | `<slug>-revision.md`, and `<slug>.md` corrected |
| 5. Render and deliver | this file | `<slug>.md` | `outputs/<slug>.pdf`, or the format the person asked for |

The stage files sit next to this one; read each when its stage starts, not before. When a stage's input file is missing, do not invent it: offer to run the stage before, or ask the person for the content.

Text that goes into a document that already exists, such as a Google Doc someone started or a formatted letterhead, is written as `existing-document.md` says; stages 1, 2 and 4 still apply to it.

**No draft before the outline is agreed, and no delivery before stage 4 has run.** Written in one pass, a document copies its sources' labels, leaves material unused and prints amounts that do not multiply out.

## Rules that hold in every stage

- **Nothing is invented.** A detail nobody gave you does not enter the document: no discount, deadline, date, name, guarantee, reference or promised result.
- **A missing datum is named, and you stop on that point.** Do not derive it from what is nearby, carry a default forward or estimate it: the reader cannot tell a plausible figure from a real one. Once you have written that the material does not support a figure, a date or a name, do not supply one anyway. Say what would settle it; pressed to decide regardless, name who can decide and on what.
- **Every figure comes from its source or from the calculator**, never from your own arithmetic.
- **Nothing in the document is about how it was made.** For each sentence ask who it is about: the subject the reader acts on stays; you, your method, what you tried, changed or checked goes, and belongs in the chat.
- **A result you cannot vouch for is left out, with no disclaimer in its place.** A figure with a warning beside it is still acted on. Tell the person in one line how much is missing and what it would take. The one limit that stays in the document is one that changes what the reader may conclude.
- **A total that does not add up stops the delivery.** Correct it from the source or ask the person.

## The calculator

These four calls are the complete set. Every number goes in as a string in machine form: a dot for decimals, no thousands separator, no currency symbol, no percent sign (`22%` is `0.22`).

```
call_recipe("cerase-calc.calculate", {"expression": "36 * 680"})
call_recipe("cerase-calc.sum", {"values": ["24480", "13600"]})
call_recipe("cerase-calc.product", {"values": ["36", "680"]})
call_recipe("cerase-calc.round", {"value": "1468.8", "places": 2})
```

Each answers `{value, value_it, expression, rounded}`. `value` is machine form, for the next call and for a spreadsheet cell; `value_it` (`1.234,56`) is what an Italian document prints, and a document in another language writes `value` with that language's separators. `rounded: true` means `value` is not the exact result, and `note` says why. When the calculator refuses an input, correct the input as its message says; never work the figure out yourself instead.

A spreadsheet cell takes machine form too: with a decimal comma or a thousands separator it holds text, or a number a thousand times off, and every formula reading it is silently wrong. Format the column afterwards.

## Stage 5 — render and deliver

After the revision has closed with no open finding:

```
call_recipe("cerase-office-converter.render_document", {"path": "<slug>.md", "output_filename": "<slug>.pdf", "paper": "A4"})
```

It answers `{path, filename, size_bytes, format, pages}`; the YAML block atop `<slug>.md` becomes the title block. Add `"orientation": "landscape"` only when the brief asks. When the brief records a brand, add `"template_css": "<css>"`: the person's CSS as it is, or a minimal override with only the colours and fonts they gave. An `output_filename` ending in `.html` gives the HTML page. `cerase-office-converter.convert_md_to_pdf` is not used for a document a person will send: its layout reads as an academic paper.

Read the PDF back with `call_recipe("cerase-docreader.read_document", {"path": "outputs/<slug>.pdf"})`: the title block, every section and every total must be the ones in `<slug>.md`. A failed render may have written nothing or part of a file: look in `outputs/` before saying anything, render once more, and report what exists.

Word or a Google Doc only when the person asks, made from `<slug>.md` through the `docx` skill; the Markdown stays the original. Without that skill, say the organisation's admin enables it, and offer the PDF.

Deliver with `[[attach: outputs/<slug>.pdf]]`, never the content or any base64 in the chat. Before calling it done, check what you hand over against what was asked, part by part: sections, figures, recipient, attachment, quoting only values the tools wrote. A file or a mail still carrying a placeholder is not finished, whatever the call returned, and a mail that says the file is attached carries it, or is not sent. Then say in a few lines what the document contains, and what is missing and what would settle it.

## Language

- Chat: the person's language, always.
- Brief, outline, revision file and document: the document's language, which the brief records; by default the person's.
