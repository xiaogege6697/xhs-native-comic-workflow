# Native Text Prompting

## Principle

The image should look finished before any post-processing. Critical text belongs inside the world: on paper, screens, receipts, sticky notes, whiteboards, folders, tables, and speech bubbles.

## Prompt Skeleton

```text
Use case: illustration-story
Asset type: Xiaohongshu vertical comic page, finished published page
Aspect ratio: 3:4 vertical
Primary request: Create page X of a Chinese educational comic. Native in-scene Chinese text only; no later overlay.
Scene/backdrop: ...
Characters: ...
Composition: ...
Exact Chinese text to render, verbatim:
L1 title: ...
L2 conclusion: ...
Dialogue: ...
Labels: ...
Page number: 第X/N页
Hard constraints: no blank speech bubbles, no blank bills, no blank phone screens, no blank tables, no pseudo-Chinese, no English, no watermark, no extra legal book titles, no law article numbers, no phone numbers, no account numbers.
```

## Good Text Objects

- Phone: short message, not a full paragraph.
- Bill: 3-5 rows with amount/category.
- Transfer card: amount + remark.
- Sticky note: one short judgment.
- Whiteboard: page title or 2-4 labels.
- Folder: category name.
- Table: headers + one sample row.

## Common Failure Handling

| Failure | Action |
|---|---|
| blank frame/speech bubble | regenerate same page with “no blank containers” and fewer elements |
| garbled critical title | regenerate; do not fix by pretending it is acceptable |
| model adds law book/title | regenerate with “no legal book titles, no extra Chinese text” |
| table has wrong headers | regenerate; action pages need exact headers |
| too much tiny text | reduce labels and rerender |
| beautiful but wrong conclusion | fail the page |

## Prompt Tightening Pattern

When a page fails, do not rewrite the whole episode. Regenerate only that page:

```text
Regenerate page X with simpler clean layout.
Render only the text listed below.
No other Chinese text.
No books, ads, decorative notices, or extra labels.
Keep the same characters, clothing, and page number.
```

