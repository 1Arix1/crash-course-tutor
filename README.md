# crash-course-tutor：速成学习教练 Skill

一个面向 AI 助手的速成学习 skill（可复用的教学指令）：把"我想快速学会 X"变成一个可以反复循环的教学流程。每次只讲一个知识点，配一道完整例题，让你亲手做题，批改后针对错因再练，直到真正会了再往下走。

不限于 Claude：支持技能加载的工具可以按各自的方式安装；ChatGPT、Gemini 等聊天工具也可以把 `SKILL.md` 的教学指令作为提示词使用。不同平台的安装方式、文件读取和工具能力有所不同，具体用法见下文。

> **English summary.** A reusable learning skill for AI assistants that turns "I want to learn X fast" into a repeatable loop: define a concrete finish line, teach one concept at a time with a fully worked example, give graded practice, grade the answers, and re-drill the exact mistake with a fresh problem. It is not limited to Claude: install it in a compatible skill-enabled tool, or use the teaching instructions from `SKILL.md` as a prompt in a chat assistant. Installation and available tools vary by platform. Mastery is judged by performance (with hints, independently, and after a delay in a new context), and the way it is checked is adapted to the field: exams, languages, software and programming, writing and design, and hands-on skills. The skill text is written in Chinese.

## 它解决什么问题

- 看完课件、视频觉得懂了，一做题就不会。
- 资料很多，不知道先学哪个、哪里是重点。
- 做错了只看答案，下次还错同一个坑。
- "学会"没有标准，不知道自己到底到了什么程度。

## 核心流程

1. **定终点**：把"学会某个领域"改写成一张终点卡，写明要完成的具体任务、允许的帮助、合格标准，并区分短期可用、考试达标、长期熟练三种目标。
2. **读资料**：你提供课件、PDF、笔记、真题时，先读完，按资料的范围讲，不脱离资料；用真题统计题型和高频点来排顺序。没有资料就自己列知识点顺序，请你确认。
3. **一次一个知识点**：先讲它是什么、为什么这样，新概念说清含义；再用一道完整例题，说明每一步为什么这样做、怎么判断、怎么检查结果，不跳基础步骤。
4. **分级练习**：前面几道带提示热身，最后一两道不给提示、情境不同，作为独立任务。等你作答。
5. **批改**：给一张逐题结果表，只展开有问题的题，指出错在哪一步、属于哪类错误，给出正确过程。
6. **针对错因换同类新题**：数字不同，陷阱相同。同类错误反复出现，就换讲法或补前置知识，而不是把同样的话再说一遍。

## 怎样判断"学会了"

用三档，而不是凭"这题做对了"：

| 档位 | 含义 |
|---|---|
| 有提示能做 | 照着例题或步骤能做出来 |
| 能独立完成 | 不看提示、情境不同，自己做对 |
| 隔一段时间、换个情境仍能完成 | 过了几个别的知识点之后，换了问法仍然会 |

- 刚看完例题后做对同类题，只算第一档，不能据此宣布掌握。
- 重要内容（终点要求的、真题高频的、后面依赖的）必须有独立任务和后续回顾。
- 偶发小错（笔误、算错数）不阻塞进度；反复的概念错误才停下来处理。

## 按领域选择验证方式

不会把所有学习都做成问答题。

| 领域 | 怎么验证 | 文字交流验证不了的 |
|---|---|---|
| 考试和解题 | 解题、限时小测、整卷模拟，按评分标准打分；记忆内容用默写、填空、简答 | — |
| 语言 | 理解（不给译文回答问题）和实际表达（造句、短文、对话） | 发音、语调、听辨、流利度 |
| 软件和编程 | 做出文件或能运行的代码，贴出输出和报错；再用新数据重做一次变式 | 实际操作的熟练度、速度、环境问题 |
| 写作和设计 | 给评价标准，提交作品，按标准修改后再提交 | 主观观感的全部 |
| 需要动手的技能 | 原理、步骤、对错判断，以及你提供的视频、照片、录音 | 动作质量、手感、速度 |

## 计算类内容的格式规则

只在数学、物理、工程等有公式和数值计算的内容里启用：

- 公式用 LaTeX，字母用正体，如 `\mathrm{F}=\mathrm{m}\mathrm{a}`。
- 解题过程写成"中文名 符号 = 算式 = 数值和单位"，一行一个量，不堆一串字母。
- 先统一单位；求导、积分不跳步，写出用到的规则；先求导或化简，最后才代入数值。
- 先定正方向和基准；题目给的常数用题目的值。
- 每题检查：单位、量级估算（专抓差 10 倍的失误）、边界情形、能用另一种方法核对就核对。

## 安装与使用

核心文件是 `crash-course-tutor/SKILL.md`。支持技能的工具使用完整技能文件夹；普通聊天工具使用其中的教学指令。`.skill` 是打包文件，不是所有平台都能直接导入。

### Codex

把 `crash-course-tutor/` 文件夹放到个人技能目录 `~/.agents/skills/`，或放到项目的 `.agents/skills/` 下。最终路径应为：

```text
~/.agents/skills/crash-course-tutor/SKILL.md
```

Windows 的个人目录对应 `%USERPROFILE%\.agents\skills\crash-course-tutor\SKILL.md`。安装后可在对话中使用 `$crash-course-tutor` 明确调用；如果没有识别到新技能，重启 Codex 后再试。目录和加载规则见 [Codex 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

### Claude.ai

下载 Release 里的 `crash-course-tutor.skill`，按你所用版本的 skill 安装方式导入。在对话里打开 `.skill` 文件时，如果你的组织允许创建 skill，文件卡片上会有"Save skill"按钮。

### Claude Code

把 `crash-course-tutor/` 文件夹放到个人 skill 目录：

```bash
mkdir -p ~/.claude/skills
cp -r crash-course-tutor ~/.claude/skills/
```

也可以放到项目的 `.claude/skills/` 下，只在该项目生效。

### 其他支持技能的工具

按该工具的官方说明，将 `crash-course-tutor/` 放入它支持的技能目录，或通过其技能管理界面导入。保留文件夹内的 `SKILL.md` 和相关资源，不要直接套用 Claude 或 Codex 的目录。

### ChatGPT、Gemini 等聊天工具：作为提示词使用

如果所用界面没有兼容的技能安装功能，可以打开 `SKILL.md`，复制开头 `---` 元数据区块之后的教学指令，粘贴到新对话中，再补充自己的学习目标、截止时间和资料。也可以在支持文件上传的界面上传 `SKILL.md`，并明确要求按其中的教学指令开展学习。

这属于在当前对话中使用提示词，不等于安装了可自动触发的技能；开启新对话时通常需要重新提供指令。读取课件、运行代码、查看图片等能力取决于所用平台。

## 怎么触发

在支持自动选择技能的工具中，安装后可以直接说你想学什么；也可以按工具支持的方式明确调用。作为普通提示词使用时，先提供教学指令，再说明学习目标。例如：

- "下周一考大学物理，牛顿运动定律完全不会，带我从零速成。"
- "这是老师的课件和一套真题，帮我过一遍，出题给我练，再批改。"
- "我想一周学会用数据透视表，带我一步步来，我边学边练。"
- "两天记住这几个条约，帮我讲一下，再考我。"

不适用的情况：只要一个简短答案、翻译、文章总结，不需要教学和练习的请求。

## 仓库结构

```
.
├── README.md
├── crash-course-tutor/
│   ├── SKILL.md            # skill 本体：触发描述 + 全部指令
│   └── evals/              # 三个测试案例（计算类、记忆类、技能类）
│       ├── calc-newton-second-law/
│       ├── memory-opium-war-treaties/
│       └── skill-excel-pivot-table/
└── crash-course-tutor.skill  # 供支持导入该格式的平台使用（建议放在 Release）
```

## 测试情况

`evals/` 里有三个不同类型的测试提示（计算类、记忆类、技能类），每个带一段对预期结果的描述。目前只做过结构校验和人工查看第一轮输出，**没有做对照实验和定量评测**。欢迎提 issue 反馈某个领域效果不好的地方。

## 自定义

所有行为都在 `SKILL.md` 里，可以直接改：

- 想换练习的数量和难度分布，改"给一小组练习"。
- 想加入新的领域验证方式，在"按领域选择讲法和验证方式"里加一段。
- 想去掉公式格式要求，删掉"仅计算类内容使用"那一节。

## License

请在发布前补充你选择的开源协议，并在仓库中添加 `LICENSE` 文件。
