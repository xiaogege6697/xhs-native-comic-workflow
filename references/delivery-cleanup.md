# Delivery Cleanup

## Purpose

Large-scale comic production must end with clean deliverables. Intermediate planning files are useful for quality control, but they should not clutter the final output.

## Two States

### Working State

Keep all process files while building and QAing:

- `source.md`
- `episode-brief.md`
- `cognitive-path.md`
- `storyboard.md`
- `characters/`
- `prompts/`
- `pages/`
- `qa-report.md`
- `publishing-pack.md`

### Delivery State

After QA passes, export only:

- final images
- one publishing `.txt`

## Final Folder Naming

Use:

```text
outputs/comic-final/<episode-number>-<topic-slug>/
```

Examples:

```text
outputs/comic-final/001-breakup-money/
outputs/comic-final/002-cohabitation-rent/
outputs/comic-final/003-pet-custody/
```

Use zero-padded episode numbers for batch order. Use short English slugs for filesystem stability.

## Final Image Naming

Use:

```text
00-cover.png
01.png
02.png
03.png
04.png
05.png
06.png
07.png
```

If an episode has fewer than 8 images, keep sequential naming and do not create placeholders.

## Publishing TXT Naming

Use:

```text
<episode-number>-<topic-slug>-发布文案.txt
```

Example:

```text
001-breakup-money-发布文案.txt
```

## Publishing TXT Template

```text
【选题】

...

【标题备选】
1. ...
2. ...
3. ...
4. ...
5. ...

【正文】

...

【评论区引导】
1. ...
2. ...
3. ...

【标签】
#... #... #...
```

## Cleanup Rules

Do not delete anything before:

1. all final images exist,
2. the publishing `.txt` exists,
3. QA has passed or the user explicitly accepts warnings,
4. final folder has been inspected.

For batch production, default to removing working folders after final export if the user asked to avoid clutter. If auditability matters, archive working folders under:

```text
outputs/comic-archive/<batch-date>/
```

Never remove the final delivery folder.

