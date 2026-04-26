# My Awesome Prompts and Skills

这是我日常使用、整理和迭代的一组 prompts 与 Codex skills。

这个仓库不是单篇教程，也不是某一个 skill 的说明页，而是一个索引型仓库：每个目录对应一个可复用的 prompt、skill 或相关资源。后续新增内容时，先在这里登记用途、适用场景和入口文件，方便自己和他人快速找到能用的东西。

## 仓库内容

目前包含：

| 名称 | 类型 | 用途 | 入口 |
| --- | --- | --- | --- |
| Tutorial Writer | Codex skill | 基于公众号文章、博客、官方文档或已有教程，撰写、扩充、审阅和润色中文教程 | [`tutorial-writer/SKILL.md`](tutorial-writer/SKILL.md) |

## 使用方式

### 使用 Codex skill

把需要使用的 skill 目录复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse .\tutorial-writer "$env:USERPROFILE\.codex\skills\"
```

安装后，新会话或重启 Codex 通常即可通过 `$skill-name` 调用。例如：

```text
Use $tutorial-writer 基于下面几篇文章，写一篇 Codex 从入门到进阶的教程。
```

### 直接参考 prompt 或说明

如果某个目录不是 skill，而是 prompt 或说明文档，可以直接打开对应 Markdown 文件复制、改写或作为工作流参考。

## 目录约定

每个条目尽量保持独立，通常包含：

```text
name/
├── SKILL.md              # Codex skill 的核心说明，若该条目是 skill
├── README.md             # 可选，面向人类读者的更详细说明
├── agents/               # 可选，Codex UI 元数据
├── references/           # 可选，工作流中按需读取的参考材料
└── assets/               # 可选，模板、图片或其他资源
```

根目录 README 只做总览和索引；具体工作流、使用细节和维护说明放在各自目录里。

## 索引

### Tutorial Writer

`tutorial-writer` 是一个 Codex skill，用来把微信公众号文章、技术博客、官方文档或已有教程，整理成更适合学习的中文教程。

它适合这类任务：

- 基于若干文章链接，从 0 到 1 写一篇使用教程或学习教程。
- 给已有教程补充新材料，随着技术更新持续扩充。
- 不提供新链接时，主动搜索官方文档、release notes、近期博客，检查教程是否过时。
- 把 Claude Code、Codex、WSL2、Linux、Ubuntu、开发工具等技术主题写成由浅入深的教程。

目标读者默认是有一定基础的本科生、研究生或程序员。写作风格偏务实，不绕弯，但关键概念会用更容易理解的方式解释。

工作流程：

1. **读**：进入用户提供的链接，通读原文，提取关键步骤、概念、版本、环境假设和作者经验。
2. **写**：重新组织材料，把原文内容改写成从低难度到高难度的教程。
3. **验**：搜索官方文档、更新日志、仓库说明或可信博客，检查教程内容是否过时或有误。
4. **润**：通读全文，去掉 AI 味和空话，让文字更像一个认真写教程的人。

如果公众号文章、博客或文档页面无法读取，skill 会要求用户提供原文、导出的 Markdown/HTML/PDF 或截图，不会只根据标题脑补内容。

目录：

```text
tutorial-writer/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── style-checklist.md
```

文件说明：

- [`tutorial-writer/SKILL.md`](tutorial-writer/SKILL.md)：核心工作流，定义读、写、验、润四个阶段。
- [`tutorial-writer/references/style-checklist.md`](tutorial-writer/references/style-checklist.md)：最终润色检查表，重点去掉 AI 味、空话和机械结构。
- [`tutorial-writer/agents/openai.yaml`](tutorial-writer/agents/openai.yaml)：Codex UI 展示元数据。

示例：

```text
Use $tutorial-writer 基于下面几篇公众号文章，写一篇 Codex 新手到进阶教程。
```

## 维护原则

- 新增 prompt 或 skill 时，同步更新本 README 的索引。
- 每个 skill 应保留清晰的入口文件和最小必要资源。
- 能验证就验证，不把未验证的工作流写成已可用。
- 快速变化的工具类内容，应优先查官方文档和最新发布说明。
