# Claude Code 配置体系

本项目的完整 Claude Code 配置体系，包含 Skills、Subagents、Commands 三大模块，用于提升开发效率和工作流自动化。

## 🎯 项目意图

构建一个完整的、可复用的 Claude Code 配置体系，实现：

- **Skills（技能）**: 模块化的工作流程和领域知识
- **Subagents（子代理）**: 特定任务的 AI 代理配置
- **Commands（命令）**: 快速触发的自定义指令

所有配置存放在项目的 `.claude/` 目录中，便于版本控制和团队共享。

## 📂 目录结构

```
.claude/
├── README.md                 # 本文档
├── skills/                   # 技能模块
│   ├── git-commit-helper/    # Git 提交助手
│   └── [待添加更多...]
├── subagents/                # 子代理配置（待创建）
│   └── [待规划...]
├── commands/                 # 自定义命令（待创建）
│   └── [待规划...]
└── settings.json             # Claude 全局设置（可选）
```

---

## 📦 Skills（技能）

### git-commit-helper

Git 提交助手 - 帮助创建规范、专业的 git commit message。

[查看详细文档](./skills/git-commit-helper/SKILL.md)

---

## 🤖 Subagents（子代理）

> 📋 **规划中** - 用于定义特定任务的 AI 代理行为和配置

### 计划添加的子代理

- **code-reviewer**: 代码审查代理
- **planner**

---

## ⚡ Commands（命令）

> 📋 **规划中** - 快速触发的自定义 slash 命令

### 计划添加的命令

- `/review-pr [number]`: 审查 Pull Request

---

## 🚀 使用说明

### 项目级配置

本项目的 `.claude/` 目录包含了项目特定的配置：

1. **Skills**: 存放在 `.claude/skills/` 目录
2. **Commands**: 存放在 `.claude/commands/` 目录
3. **Subagents**: 存放在 `.claude/subagents/` 目录

Claude Code 会自动识别项目根目录的 `.claude/` 配置。

### 全局共享

如需在多个项目间共享配置，可以：

```bash
# 方式 1: 软链接到全局 skills 目录
ln -s /path/to/project/.claude/skills/git-commit-helper ~/.claude/skills/

# 方式 2: 复制到全局目录
cp -r .claude/skills/* ~/.claude/skills/
```

---

## 📝 License

MIT License
