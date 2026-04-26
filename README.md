# Tutorial Writer Skill

`tutorial-writer` 是一个 Codex skill，用来把微信公众号文章、技术博客、官方文档或已有教程，整理成更适合学习的中文教程。

它适合这类任务：

- 基于若干文章链接，从 0 到 1 写一篇使用教程或学习教程。
- 给已有教程补充新材料，随着技术更新持续扩充。
- 不提供新链接时，主动搜索官方文档、release notes、近期博客，检查教程是否过时。
- 把 Claude Code、Codex、WSL2、Linux、Ubuntu、开发工具等技术主题写成由浅入深的教程。

目标读者默认是有一定基础的本科生、研究生或程序员。写作风格偏务实，不绕弯，但关键概念会用更容易理解的方式解释。

## 工作流程

这个 skill 按四步工作：

1. **读**：进入用户提供的链接，通读原文，提取关键步骤、概念、版本、环境假设和作者经验。
2. **写**：重新组织材料，把原文内容改写成从低难度到高难度的教程。
3. **验**：搜索官方文档、更新日志、仓库说明或可信博客，检查教程内容是否过时或有误。
4. **润**：通读全文，去掉 AI 味和空话，让文字更像一个认真写教程的人。

如果公众号文章、博客或文档页面无法读取，skill 会要求用户提供原文、导出的 Markdown/HTML/PDF 或截图，不会只根据标题脑补内容。

## 支持的工作模式

### 从 0 到 1 写教程

用户提供文章链接后，skill 会先读原文，再重排成清晰教程。

示例：

```text
Use $tutorial-writer 基于下面几篇公众号文章，写一篇 Codex 新手到进阶教程。
链接：
- ...
- ...
```

### 从 1 到 n 扩充教程

用户提供已有教程和新链接后，skill 会判断哪些内容需要补充、更新或重排，而不是默认推倒重写。

示例：

```text
Use $tutorial-writer 用这些新文章更新我现有的 WSL2 教程，保留原来的结构，补充过时部分。
```

### 全面审阅教程是否过时

用户不提供新链接时，skill 会主动搜索官方资料和近期资料，检查安装命令、版本说明、功能边界、平台限制等是否需要更新。

示例：

```text
Use $tutorial-writer 全面审阅这篇 Ubuntu 使用教程，检查是否有过时内容，并直接改成最新版。
```

## 目录结构

```text
tutorial-writer/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    └── style-checklist.md
```

- `SKILL.md`：核心工作流，定义读、写、验、润四个阶段。
- `references/style-checklist.md`：最终润色检查表，重点去掉 AI 味、空话和机械结构。
- `agents/openai.yaml`：Codex UI 展示元数据。

## 安装方式

把 `tutorial-writer` 文件夹复制到 Codex skills 目录：

```powershell
Copy-Item -Recurse .\tutorial-writer "$env:USERPROFILE\.codex\skills\"
```

安装后，新会话或重启 Codex 通常即可通过 `$tutorial-writer` 调用。

## 设计原则

- 教程必须基于实际读过的来源，不根据标题或搜索摘要编造。
- 快速变化的主题必须查官方资料或最新可信资料。
- 教程顺序要符合学习路径：先跑通，再理解，再扩展。
- 关键概念可以类比，一般技巧直接说清楚即可。
- 最终文字要高效、务实、通俗，但不要像产品宣传稿。

## 验证状态

本仓库中的 skill 已通过 Codex `skill-creator` 的 `quick_validate.py` 校验。
