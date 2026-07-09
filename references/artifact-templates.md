# Artifact Templates

## source.md

```markdown
# Source Material

## Topic

...

## User Requirements

- ...

## Case Setup

- ...

## Scope

- jurisdiction/date/platform/domain
```

## episode-brief.md

```yaml
topic:
industry:
platform:
mode:
audience:
real_question:
stakes:
known_facts:
unknowns:
evidence_assets:
professional_framework:
common_belief:
cognitive_reversal:
action:
scope:
compliance:
```

## cognitive-path.md

```yaml
before_belief:
after_belief:
memory_line:
final_action:
steps:
  - action: stop
    question:
    answer:
    evidence:
  - action: relate
    question:
    answer:
    evidence:
```

## storyboard.md

Include:

- unified style
- page count
- page table
- page role
- cognitive action
- visual anchor
- exact text budget
- risk notes

## characters/characters.md

Include for every recurring character:

- function
- age
- face/hair
- clothing
- color role
- props
- personality
- forbidden drift

## prompt file

```markdown
---
page:
role:
cognitive_action:
panels:
aspect: "3:4"
---

Purpose:
Single goal:
Reader takeaway:
Character invariants:
Scene and props:
Composition:
Exact text:
Visual style:
Hard constraints:
```

## qa-report.md

```markdown
# QAReport

## Overall

## Gate Table

| Page | Truth | Scope | Cognition | Density | Continuity | Typography | Safety | Decision |

## Page Notes

### Page 00

- Pass:
- Warning:
- Fix:
```

## publishing-pack.md

Include:

- 5 titles
- publish-ready body
- comment prompts
- hashtags
- replay/iteration notes

## final publishing .txt

For large-scale delivery, convert `publishing-pack.md` into one final `.txt` file:

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

The final delivery folder should contain this `.txt` plus final images only.
