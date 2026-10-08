# Writing into a document that already exists

This applies when your text goes into a document someone already has: a Google Doc a colleague started, a proposal waiting for a section, a formatted letterhead. The document's layout, styles, header and footer belong to it, and your text has to land inside them as if the author had typed it.

Stages 1, 2 and 4 of `SKILL.md` still apply to what you write: the brief, the outline of your part with its figures, and the revision.

## 1. Before writing: read the document

1. **What it is.** `call_recipe("google-workspace.getDocumentInfo", {"documentId": "<id>"})`. When it has tabs, `call_recipe("google-workspace.listDocumentTabs", {"documentId": "<id>"})`, and pass the right `tabId` to every call below.
2. **Its sections.** `call_recipe("google-workspace.readGoogleDoc", {"documentId": "<id>", "format": "markdown"})` gives the headings and paragraphs in order. Find the section your text belongs to.
3. **The place and its style.** `call_recipe("google-workspace.getGoogleDocContent", {"documentId": "<id>", "includeFormatting": true})` gives each span with its indices, font, size and colour. For a long document read it in pages with `call_recipe("google-workspace.getGoogleDocContentPaginated", {"documentId": "<id>", "includeFormatting": true, "offset": 0, "limit": 50000})`. Note, for the paragraph before your text and the one after it: their start and end indices, their paragraph style, their font family, size and colour, and whether they are list items.
4. **Say where your text goes**, before any write, in the person's language: after which paragraph, before which heading, in which style, quoting a few words of each neighbour. When two places fit, ask which one.

When the person has not said whether to change the original or work on a copy, ask. A copy is `call_recipe("google-workspace.copyFile", {"fileId": "<id>", "newName": "<title> — draft"})`.

## 2. Writing

- **Insert at a paragraph boundary.** The index is the start index of the paragraph your text goes before, and your text ends with a newline (`\n`) so it becomes paragraphs of its own. Before inserting, check in the content you read that the character before that index is the newline closing the previous paragraph. An index inside a paragraph splits a word or a sentence.
- `call_recipe("google-workspace.insertText", {"documentId": "<id>", "text": "<your paragraphs, each ending with \n>", "index": <start index of the following paragraph>})`.
- **Every write moves the indices after it.** Read the content again before the next write, or write from the end of the document towards its start.
- **Plain text only.** `insertText` writes characters as they are, so Markdown syntax (`#`, `**`, `|`, `- `) appears in the document as symbols. Headings, bold and lists are applied after the text is in, with the calls below.
- **Give your text the style of the section it joins**, over the indices it now occupies. Inserted text takes the style of the paragraph it was inserted into, so text placed just before a heading comes out as a heading until you set it:
  - `call_recipe("google-workspace.applyParagraphStyle", {"documentId": "<id>", "startIndex": <start>, "endIndex": <end>, "namedStyleType": "<the neighbours' style, such as NORMAL_TEXT or HEADING_2>"})`, adding `alignment`, `spaceAbove` or `spaceBelow` when the neighbours differ from the style's default;
  - `call_recipe("google-workspace.applyTextStyle", {"documentId": "<id>", "startIndex": <start>, "endIndex": <end>, "fontFamily": "<font>", "fontSize": <size>, "foregroundColor": "<#hex>"})`, with `bold` or `italic` only where the neighbours have them;
  - when the neighbours are list items, `call_recipe("google-workspace.createParagraphBullets", {"documentId": "<id>", "startIndex": <start>, "endIndex": <end>, "bulletPreset": "<the neighbours' preset>"})`.
- **A placeholder in a template**, such as a date or a recipient's name between brackets, is replaced in place, and the replacement keeps the placeholder's style: first `call_recipe("google-workspace.findAndReplaceInDoc", {"documentId": "<id>", "findText": "<placeholder>", "replaceText": "<value>", "matchCase": true, "dryRun": true})`, and only when it counts exactly the matches you mean, the same call without `dryRun`.
- **Never replace a formatted document's whole content.** No `google-workspace.updateGoogleDoc` on it, and no rewriting it from its text: either loses its layout, its styles, its header and footer, and on a letterhead the letterhead itself.
- **A letterhead.** In Google Docs, copy it for each new letter with `copyFile` and fill the copy's body by insertion or by placeholders, as above. A letterhead that is a Word file is the `docx` skill's template, passed as `reference_doc_path`.

## 3. After writing: read it back

Read the area again with `getGoogleDocContent` and `"includeFormatting": true`, and check:

- your text sits between the two paragraphs you named to the person, and no word or sentence of theirs was split;
- no Markdown symbol is left in it;
- its paragraph style, font, size and colour are those of its neighbours.

Correct what does not hold with the style calls, then tell the person what the document now contains, from what you read back.

A write that fails may have done nothing, or part of the change. Read the document back before saying anything about it, and tell the person what you found there.

## 4. A PDF of a Google Doc

A PDF of a Google Doc, Sheet or Slides is the one Google makes, never one rebuilt from its text, which loses the layout:

```
call_recipe("google-workspace.downloadFile", {"fileId": "<id>", "localPath": "/home/agent/cerase/workspace/downloads/<slug>.pdf", "exportMimeType": "application/pdf"})
```

The answer names the file's path in your workspace; deliver it with `[[attach: <that path>]]`. The same call exports a Doc to Word with `"exportMimeType": "application/vnd.openxmlformats-officedocument.wordprocessingml.document"`, a Sheet to `application/vnd.openxmlformats-officedocument.spreadsheetml.sheet` and Slides to `application/vnd.openxmlformats-officedocument.presentationml.presentation`, each with its extension in the name.

## The calls

These are the complete set for an existing document: `getDocumentInfo`, `listDocumentTabs`, `readGoogleDoc`, `getGoogleDocContent`, `getGoogleDocContentPaginated`, `copyFile`, `insertText`, `applyParagraphStyle`, `applyTextStyle`, `createParagraphBullets`, `findAndReplaceInDoc` and `downloadFile`, all of the `google-workspace` connector. Do not invent others. Without that connector, say in the person's language that writing into a Google Doc needs it, which the organisation's admin assigns, and offer the document as a PDF from stage 5.
