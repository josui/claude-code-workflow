---
name: git-commit-helper
description: Use this skill for ANY git commit operation unless the user specifically requests otherwise. This skill helps analyze changes, suggest appropriate commit messages following project conventions, split multiple changes into logical commits, and ensure commit messages are professional without AI-generated markers.
---

# Git Commit Helper

帮助创建专业的 git commits，遵循项目约定，使用中文提交信息，不包含 AI 生成标记。

## 核心工作流程

### 1. 分析变更
```bash
git status && git diff && git log -5 --oneline
```

判断是否需要拆分为多个 commit：
- **单个 commit**: 所有改动服务于同一个目的
- **多个 commits**: 包含独立的功能、修复或不同类型的改动

### 2. 提交信息格式

```
<type>: <简洁的中文描述>

- <详细说明 1>
- <详细说明 2>
```

**类型 (type):**
- `add`: 新增功能、组件、文件
- `update`: 更新、优化、改进现有功能
- `fix`: 修复 bug
- `docs`: 文档变更
- `chore`: 构建配置、工具、依赖

**关键规则:**
- ❌ 不包含 AI 生成标记 (如 "🤖 Generated with Claude Code")
- ✅ 使用中文描述
- ✅ 首行 < 50 字符
- ✅ 使用现在时 ("新增" 而非 "新增了")

### 3. 创建提交

多行消息使用 heredoc:
```bash
git commit -m "$(cat <<'EOF'
add: 新增 pricing 组件

- 三栏价格表布局,支持月付/年付切换
- 使用 CSS 变量实现主题定制
EOF
)"
```

简单改动可用单行:
```bash
git commit -m "fix: 修复图片路径错误"
```

### 4. 验证提交
```bash
git log -1 --format="%h - %s%n%b" && git status
```

## 拆分多个变更示例

```bash
# 场景：修改了组件、更新了文档、修复了 bug

# Commit 1: 组件更新
git add src/templates/news-card/
git commit -m "update: 优化 news-card 组件样式"

# Commit 2: 文档
git add CLAUDE.md README.md
git commit -m "docs: 更新组件使用文档"

# Commit 3: Bug 修复
git add src/components/Preview.astro
git commit -m "fix: 修复预览窗口尺寸计算错误"
```

## 交互式指导

帮助用户提交时:
1. 显示当前变更 (`git status` 和 `git diff` 摘要)
2. 建议分组策略 (单个或多个 commits)
3. 起草提交信息
4. 执行并验证结果
