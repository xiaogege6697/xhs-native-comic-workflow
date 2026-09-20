# 小红书原生漫画工作流（xhs-native-comic-workflow）

> 生成"发布即成品"的小红书漫画图文：故事、证据、对话和文字在生图之前就设计好，并作为场景物件原生渲染在画面里——不是"先生成漂亮图片、再事后贴字"。
>
> Build Xiaohongshu-ready native-text comic posts: story, evidence, dialogue, and in-scene text are designed before image generation and rendered natively inside the scene.

## 为什么做这个

用 AI 生图做漫画图文，最常见的翻车方式都一样：

- 图很漂亮，但文字是乱码、伪中文，或者干脆是空白的气泡/账单/手机屏，等着后期贴字；
- 每页角色长相、衣服、颜色都不一样，翻到第三页读者就出戏；
- 图里的金额、日期、对话前后矛盾，证据经不起细看；
- 内容只是抽象说教，没有具体案例故事，用户划走不心疼。

这个 Skill 把漫画图文当成一条**受控的认知路径**来生产，而不是一组图片的拼接：

```text
停留 -> 代入 -> 看见事实 -> 学会判断 -> 完成反转 -> 采取行动
```

它硬性强制完整工作流——即使用户说"直接出图""先打样"也不跳步，因为跳步的产物就是上面那些翻车现场。

## 核心特性

- **13 步不可协商契约**：`source.md` → `episode-brief.md` → `cognitive-path.md` → `storyboard.md` → `characters/characters.md` → 每页一个 prompt 文件 → 逐页生成 → 逐页检查 → 只重做失败页 → `qa-report.md` → `publishing-pack.md`。
- **原生场景文字规则**：关键文字必须作为场景物件设计——手机消息、账单行、转账卡、便利贴、白板标签、文件夹标签、表头、短气泡；逐字写进 prompt，指示模型只渲染列出的文字，杜绝伪中文、水印和不相关内容。
- **页面体系**：默认 5-8 页，一页只做一个认知动作；封面 = 首屏钩子（冲突 + 主角 + 关键物 + 一个价值承诺）；尾页可独立收藏、可照做。页面类型、文字预算见 [`references/page-architecture.md`](references/page-architecture.md)。
- **故事与证据规则**：每集必须有具体案例故事（主角、冲突方、时间线、触发事件、具体证据文件、争议点、专业分类、行动回复），跨页的金额、日期、备注、类目、对话必须内部一致。
- **7 道 QA 门**：Truth（事实可支撑）/ Scope（管辖、日期、条件、例外不丢失）/ Cognition（一页一认知动作）/ Density（手机读者约 10 秒看懂要点）/ Continuity（角色、服装、道具、页码一致）/ Typography（关键中文、金额、箭头可读且正确）/ Safety（无绝对承诺、性别对立、隐私泄露）。漂亮的页配错字 = 失败页。
- **法律漫画专项规则**：先确立管辖、日期、双方关系、时间线、举证责任与例外，结论强度跟随可验证的权威来源走。见 [`references/legal-comic-rules.md`](references/legal-comic-rules.md)。
- **批量生产规则**：先做一个样品过完 QA、把失败经验固化回母版 prompt，再按 5-10 集一批量产，每批 QA 通过才继续——不允许一上来就批量生产 100 篇。
- **交付清理契约**：最终交付文件夹只保留成品页图 + 一份发布文案 `.txt`（标题、正文、评论引导、话题标签），中间过程文件按约定清理或归档。

## 工作目录结构

```text
outputs/comic/<topic-slug>/
├── source.md              # 素材与范围
├── episode-brief.md       # 本集简介
├── cognitive-path.md      # 认知路径设计
├── storyboard.md          # 分镜
├── characters/characters.md  # 角色圣经（批量复用）
├── prompts/               # 每页一个 prompt 文件
├── pages/                 # 验收通过的成品页 + contact-sheet
├── qa-report.md           # 逐页 QA 记录
└── publishing-pack.md     # 发布包
```

## 快速开始

```bash
# 安装到任意支持 Agent Skills 的客户端（Claude Code / Codex 等）
git clone https://github.com/xiaogege6697/xhs-native-comic-workflow.git \
  ~/.agents/skills/xhs-native-comic-workflow
```

需要配合一个图像生成工具使用（Agent 内置生图能力或外部生图模型均可）。安装后直接用自然语言触发。

## 使用示例

```text
使用 $xhs-native-comic-workflow 做一期"分手后要求返还转账"的法律科普漫画，
8 页，含证据页和行动清单，走完整工作流和 QA。

帮我把这个案例改成小红书漫画图文，文字要在画面里，不要事后贴字。

批量生产 10 期婚姻家事科普漫画，先用第 1 期打样，QA 通过后再量产。
```

## 边界

- **不自动发布**：Skill 的产出止于发布包（成品图 + 发布文案），发布动作始终由用户自己完成。
- 法律、医疗、金融等高危领域先确立范围；无法验证权威来源时降低结论强度、避免具体引用，不给绝对化结论。
- 不生成绝对承诺、性别对立、隐私泄露、违法建议或虚构权威内容。
- 不覆盖既有样品目录（除非明确要求），版本化目录（如 `breakup-money-native-v1`）保留可回溯性。

## 相关项目

- [xiaogege6697](https://github.com/xiaogege6697) — 更多 AI Agent Skills（获客选题、网页采集、人物分身等）

<!-- AI/Friendly Search Metadata -->
**keywords: Xiaohongshu, rednote, comic workflow, native text, in-scene text, QA gates, content creation, Claude Code, Codex, skill, 小红书, 漫画工作流, 原生文字, 质量门**

