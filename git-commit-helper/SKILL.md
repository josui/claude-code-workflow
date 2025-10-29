---
name: git-commit-helper
description: This skill should be used when committing code changes to git. It helps analyze changes, suggest appropriate commit messages following project conventions, split multiple changes into logical commits, and ensure commit messages are professional without AI-generated markers. Use when the user asks to "commit changes", "create commits", or after completing code modifications.
---

# Git Commit Helper

## Overview

Assist with creating professional, well-structured git commits that follow the project's commit conventions. This skill analyzes code changes, suggests appropriate commit types and messages in Chinese, helps split multiple changes into logical commits, and ensures commits are clean without AI-generated markers.

## When to Use This Skill

Use this skill when:
- User explicitly requests to commit changes (e.g., "提交这些改动", "创建 commit", "commit these changes")
- User asks for help with commit messages
- User wants to split mixed changes into multiple commits
- After completing a significant code modification and ready to commit

## Core Workflow

### Step 1: Analyze Current Changes

Before creating any commits, understand what has changed:

```bash
# Run these commands in parallel to gather information
git status                    # See untracked and modified files
git diff                      # See unstaged changes
git diff --staged            # See staged changes
git log -5 --oneline         # See recent commit style
```

Analyze the changes to:
1. Identify logical groupings (features, bug fixes, documentation, etc.)
2. Determine if changes should be split into multiple commits
3. Understand the purpose and impact of each change

### Step 2: Determine Commit Strategy

Based on the analysis, decide:

**Single Commit** - When changes are:
- All related to one logical purpose
- Part of the same feature or fix
- Interdependent and cannot be separated

**Multiple Commits** - When changes include:
- Multiple independent features or fixes
- Different types of changes (feature + docs, fix + refactor)
- Changes to unrelated components or files

### Step 3: Group and Stage Changes

For multiple commits, group related files:

```bash
# Group 1: Feature addition
git add src/templates/pricing/ src/pages/components/pricing.astro

# Group 2: Documentation update
git add README.md CLAUDE.md

# Group 3: Bug fix
git add src/components/Preview.astro
```

### Step 4: Craft Commit Message

Follow the project's commit message format:

**Format:**
```
<type>: <简洁的中文描述>

- <详细说明 1>
- <详细说明 2>
- <详细说明 3>
```

**Commit Types:**
- `add`: 新增功能、组件、文件
- `update`: 更新、优化、改进现有功能（包含样式调整、重构等）
- `fix`: 修复 bug、解决问题
- `docs`: 文档相关的变更
- `chore`: 构建配置、开发工具、依赖更新

**Key Rules:**
- ❌ **NEVER include AI-generated markers** - No "🤖 Generated with Claude Code" or "Co-Authored-By: Claude"
- ✅ Use concise Chinese descriptions
- ✅ First line should be under 50 characters
- ✅ Use present tense (e.g., "新增" not "新增了")
- ✅ Use bullet points for detailed explanations
- ✅ Explain "what changed" and "why"

### Step 5: Create Commit

Use heredoc format for multi-line commit messages:

```bash
git commit -m "$(cat <<'EOF'
<type>: <简洁描述>

- <详细说明 1>
- <详细说明 2>
EOF
)"
```

For simple commits, single-line is acceptable:
```bash
git commit -m "fix: 修复图片路径错误"
```

### Step 6: Verify Commit

After committing, verify success:

```bash
git log -1 --format="%h - %s%n%b"  # Show the commit just created
git status                          # Confirm clean or expected state
```

## Commit Examples

### Example 1: New Component
```bash
git add src/templates/pricing/ src/pages/components/pricing.astro public/images/thumbnails/pricing.png
git commit -m "$(cat <<'EOF'
add: 新增 pricing 组件

- 三栏价格表布局，支持月付/年付切换
- 使用 CSS 变量实现主题定制
- 包含组件展示页面和缩略图
EOF
)"
```

### Example 2: Feature Update
```bash
git add src/components/Preview.astro
git commit -m "$(cat <<'EOF'
update: 优化 Preview 组件响应式尺寸设置

- Desktop 视口从 1280px 调整为 1024px，更符合主流桌面尺寸
- 将 Tailwind 类替换为原生 CSS，提高可读性和精确控制
EOF
)"
```

### Example 3: Bug Fix
```bash
git add src/pages/components/news-card.astro
git commit -m "$(cat <<'EOF'
fix: 修复 news-card 页面图片无法显示的问题

- 图片路径从相对路径改为绝对路径
- 补充缺失的 alt 属性
EOF
)"
```

### Example 4: Simple Change
```bash
git add package.json
git commit -m "update: 开发服务器增加 --host 参数

允许局域网访问开发服务器，方便在移动设备上测试。"
```

## Splitting Multiple Changes

When `git status` shows multiple unrelated changes:

1. **Identify logical groups** by file purpose and change type
2. **Stage each group separately** using `git add <files>`
3. **Create one commit per group** with appropriate message
4. **Verify after each commit** that staging area is as expected

Example workflow for mixed changes:
```bash
# Scenario: Modified news-card component, updated docs, fixed a bug

# Commit 1: Component update
git add src/templates/news-card/
git commit -m "update: 优化 news-card 组件样式"

# Commit 2: Documentation
git add CLAUDE.md README.md
git commit -m "docs: 更新组件使用文档"

# Commit 3: Bug fix
git add src/components/Preview.astro
git commit -m "fix: 修复预览窗口尺寸计算错误"
```

## Pre-Commit Checklist

Before creating any commit, ensure:
- [ ] Reviewed all changes with `git diff`
- [ ] Evaluated if changes should be split
- [ ] Grouped related files together
- [ ] Crafted clear, descriptive commit message in Chinese
- [ ] **Removed any AI-generated markers from message**
- [ ] Used appropriate commit type (add/update/fix/docs/chore)
- [ ] Used present tense in descriptions

## Common Pitfalls to Avoid

❌ **Don't:**
- Include AI-generated markers or co-author tags
- Mix unrelated changes in one commit
- Use vague messages like "update: 更新多个文件"
- Write commit messages in English (project uses Chinese)
- Use past tense ("新增了" instead of "新增")

✅ **Do:**
- Keep commits focused on single logical changes
- Write clear, specific descriptions
- Split independent changes into separate commits
- Follow the type conventions strictly
- Explain both what and why in detailed descriptions

## Interactive Guidance

When helping users commit:

1. **Show what will be committed** - Display `git status` and `git diff` summary
2. **Suggest grouping strategy** - Recommend single or multiple commits
3. **Propose commit messages** - Draft messages following conventions
4. **Confirm before executing** - Let user review suggested commits
5. **Execute and verify** - Run git commands and show results

## Resources

This skill includes a reference document with the complete commit convention:

### references/commit-convention.md

Complete project commit convention including:
- Detailed format specifications
- All commit types with examples
- Commit granularity principles
- Real-world case studies
- Best practices and pitfalls

Load this reference when:
- User asks for detailed commit convention
- Need to verify edge cases or special scenarios
- User wants to understand the rationale behind conventions
