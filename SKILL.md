---
name: xhs-native-comic-workflow
description: Build Xiaohongshu-ready native-text comic posts and serialized image-text comics. Use when the user asks to create, sample, batch-produce, refine, or QA a comic post/漫画图文/法律科普漫画/小红书图文/几页纸一期漫画, especially when the output must include an attractive cover, coherent case story, character continuity, evidence details, native in-scene text, page-by-page prompts, generated pages, QA, and publishing copy. This skill hard-enforces the full workflow and must not be shortened into blank templates or post-added text overlays.
---

# XHS Native Comic Workflow

## Purpose

Create publishable Xiaohongshu-style comic image posts where the story, evidence, dialogue, and text are designed before image generation and rendered natively inside the scene.

The output is not “pretty pictures plus later captions.” It is a controlled cognitive path:

```text
停留 -> 代入 -> 看见事实 -> 学会判断 -> 完成反转 -> 采取行动
```

## Non-Negotiable Contract

Do not skip these steps, even when the user asks to “直接出图” or “先打样”:

1. Create `source.md`.
2. Create `episode-brief.md`.
3. Create `cognitive-path.md`.
4. Create `storyboard.md`.
5. Create `characters/characters.md`.
6. Create one prompt file per page under `prompts/`.
7. Generate pages one by one, not as one huge batch prompt.
8. Copy final page images into `pages/`.
9. Inspect generated pages for text, story, evidence, continuity, and safety.
10. Regenerate only failed pages.
11. Create `qa-report.md`.
12. Create `publishing-pack.md` when the user wants usable social-media output or batch production.
13. For large-scale production, run the delivery cleanup contract after QA passes.

If a page has blank speech bubbles, blank bills, blank phone screens, blank tables, garbled key Chinese text, missing evidence, or a legal/professional conclusion that is too absolute, mark it failed and redo that page.

## Working Folder Shape

Use a new output directory for each sample or episode:

```text
outputs/comic/<topic-slug>/
├── source.md
├── episode-brief.md
├── cognitive-path.md
├── storyboard.md
├── characters/
│   └── characters.md
├── prompts/
│   ├── 00-cover.md
│   ├── 01-*.md
│   └── ...
├── pages/
│   ├── 00-cover.png
│   ├── 01-*.png
│   └── contact-sheet.png
├── qa-report.md
└── publishing-pack.md
```

Do not overwrite an earlier sample unless the user explicitly asks. Use versioned folders such as `breakup-money-native-v1`.

This is the working folder, not necessarily the final delivery folder. Keep it while planning, generating, debugging, and QA are active.

## Page System

- Use 5-8 pages by default.
- Use 8 pages when the topic needs evidence, exception handling, and an action checklist.
- Use one cognitive action per page.
- Use one panel per page unless there is a clear comparison, cause-effect, before-after, or emotion-to-evidence relation.
- Make the cover a first-viewport hook: it must show the conflict, protagonist, key object, and one-value promise.
- Make the final page independently collectible and executable.

Use [references/page-architecture.md](references/page-architecture.md) for page types, text budgets, and cover/body/action design.

## Native Text Rules

Design all critical text as scene objects:

- phone messages
- bill rows
- transfer cards
- sticky notes
- whiteboard labels
- file-folder labels
- table headers
- short speech bubbles

Never accept a generated page that looks like an empty template waiting for later captions. Prefer fewer words that are readable and story-relevant.

Critical text must be supplied verbatim in the page prompt. Instruct the image model to render only listed text and to avoid pseudo-Chinese, English, watermarks, extra legal book titles, law article numbers, ads, phone numbers, and account numbers.

Use [references/native-text-prompting.md](references/native-text-prompting.md) for prompt patterns and failure handling.

## Story And Evidence Rules

Every episode must contain a concrete case story, not only abstract teaching:

- protagonist and conflict party
- realistic timeline
- triggering message or event
- specific documents/evidence
- disputed issue
- professional classification
- action reply or checklist

Evidence shown in images must be internally consistent. Amounts, dates, remarks, categories, and dialogue must not contradict across pages.

For legal, medical, financial, or other high-stakes domains, first establish scope and verify current authoritative sources when necessary. If authority cannot be verified, lower conclusion strength and avoid specific citations.

Use [references/legal-comic-rules.md](references/legal-comic-rules.md) for legal comics.

## Generation Workflow

1. Write all planning files first.
2. Write page prompts as separate files.
3. Generate page `00-cover`.
4. Inspect the generated page immediately.
5. Copy the accepted image into `pages/`.
6. Continue to the next page only after accepting or regenerating the current page.
7. Build `contact-sheet.png` after all pages are saved.
8. Inspect the contact sheet for continuity and story flow.
9. Write QA and publishing pack.
10. If this is a batch-production or final-delivery task, create the final delivery folder and clean up intermediate files after QA passes.

When using the built-in image generator, generated images may be saved outside the project. Always copy accepted final images into the episode `pages/` folder.

## QA Gates

Each page must pass these gates:

1. `Truth Gate`: facts and professional claims are supportable.
2. `Scope Gate`: jurisdiction, date, conditions, and exceptions are not lost.
3. `Cognition Gate`: one page, one cognitive action.
4. `Density Gate`: mobile reader can understand the key point in about 10 seconds.
5. `Continuity Gate`: characters, clothes, colors, props, and page numbering are consistent.
6. `Typography Gate`: critical Chinese text, amounts, arrows, labels, and page numbers are readable and correct.
7. `Safety Gate`: no absolute promise, gender hostility, privacy leak, illegal advice, or fake authority.

Record pass/fail/warning for every page in `qa-report.md`. A beautiful page with wrong text is a failed page.

## Delivery Cleanup Contract

Use this contract whenever the user is producing many posts, asks for “批量生产”, “最终交付”, “不要留垃圾”, or wants only usable publishing assets.

After an episode passes QA, create a separate final folder:

```text
outputs/comic-final/<episode-number>-<topic-slug>/
├── 00-cover.png
├── 01.png
├── 02.png
├── 03.png
├── 04.png
├── 05.png
├── 06.png
├── 07.png
└── <episode-number>-<topic-slug>-发布文案.txt
```

The final delivery folder must contain only:

- final page images
- one `.txt` publishing pack

The `.txt` file must include:

- titles
- publish-ready body
- comment prompts
- hashtags

Do not keep planning files, prompt files, QA reports, contact sheets, failed generations, source notes, or character bibles in the final delivery folder unless the user explicitly asks for an audit/archive package.

Do not delete the working folder before QA passes. After final delivery is built and verified, intermediate working files may be removed or archived according to the user’s cleanup preference. When no preference is given for large batches, keep the final delivery folder and remove batch working folders.

Use [references/delivery-cleanup.md](references/delivery-cleanup.md) for naming rules and the `.txt` template.

## Batch Production Rule

Do not batch-produce 100 final posts until one sample has passed QA and the reusable mother workflow has been updated from its failures.

For large batches:

1. Build topic bank.
2. Group topics by legal/professional framework.
3. Create one reusable character bible.
4. Generate one sample per framework.
5. Freeze prompt mother templates.
6. Produce in batches of 5-10 episodes.
7. QA each batch before continuing.
8. Export each passed episode to `outputs/comic-final/`.
9. Clean or archive working folders so the batch leaves only necessary deliverables.

Use [references/artifact-templates.md](references/artifact-templates.md) for file templates.
