# Claude Skills Collection

我的个人 Claude Code 技能集合，用于在多台设备间同步和分享自定义技能。

## 📦 已包含的技能

### git-commit-helper
Git 提交助手 - 帮助创建规范、专业的 git commit message。

**功能：**
- 🔍 智能分析代码变更
- 📝 生成符合规约的中文 commit message
- ✂️ 自动拆分多个逻辑变更
- 🚫 确保不包含 AI 生成标识
- ✅ 遵循项目 commit 规约（add/update/fix/docs/chore）

**触发条件：**
- "提交这些改动"
- "帮我创建 commit"
- "commit these changes"

[查看详细文档](./git-commit-helper/SKILL.md)

---

## 🚀 安装使用

### 首次安装

```bash
# 克隆仓库到 Claude 技能目录
git clone https://github.com/你的用户名/claude-skills.git ~/.claude/skills
```

### 更新技能

```bash
# 拉取最新的技能更新
cd ~/.claude/skills
git pull
```

### 添加新技能

```bash
cd ~/.claude/skills
# 添加你的新技能目录
git add .
git commit -m "add: 新增 xxx 技能"
git push
```

---

## 📚 关于 Claude Skills

Skills 是 Claude Code 的模块化扩展系统，可以为 Claude 提供：

- **专业工作流** - 特定领域的多步骤流程
- **工具集成** - 特定文件格式或 API 的操作说明
- **领域知识** - 公司特定的知识、规范、业务逻辑
- **资源包** - 脚本、参考文档、模板资源

### Skill 结构

```
skill-name/
├── SKILL.md                    # 主技能文件（必需）
│   ├── YAML frontmatter        # 元数据：name, description
│   └── Markdown 指令           # 技能的工作流程和说明
└── 资源文件（可选）
    ├── scripts/                # 可执行脚本
    ├── references/             # 参考文档
    └── assets/                 # 模板和资源文件
```

### 技能自动加载

Claude 会根据 SKILL.md 中的 `description` 字段判断何时使用该技能。确保描述清晰地说明：
- 技能的功能
- 适用场景
- 触发条件

---

## 🛠️ 创建自己的技能

### 使用 skill-creator

Claude Code 提供了官方的技能创建工具：

```bash
# 在 Claude Code 中运行
/skill example-skills:skill-creator
```

### 手动创建

1. 在 `~/.claude/skills/` 下创建技能目录
2. 创建 `SKILL.md` 文件，包含 YAML frontmatter 和说明
3. 添加必要的资源文件
4. 提交到仓库

---

## 📝 License

MIT License - 自由使用和修改

---

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

## 📮 联系方式

如有问题或建议，欢迎通过 GitHub Issues 联系。
