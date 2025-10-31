---
name: git-commit-helper
description: Use this skill for ANY git commit operation unless the user specifically requests otherwise. This skill helps analyze changes, suggest appropriate commit messages following project conventions, split multiple changes into logical commits, and ensure commit messages are professional without AI-generated markers.
---

# Git Commit Helper

帮助创建专业的 git commits，遵循项目约定。

**语言规则：**
- 默认使用中文（除非用户指定其他语言）
- Type 类型保持英文（add/update/fix/docs/chore）

## 核心工作流程

### 1. 分析变更
```bash
git status && git diff && git log -5 --oneline
```

**判断提交策略：**
- 单个 commit：所有改动服务于同一目的
- 多个 commits：包含独立的功能/修复/不同类型改动

### 2. 提交信息格式
```
<type>: <简洁的描述>

- <详细说明 1>
- <详细说明 2>
```

**Type 类型：**
- `add`: 新增功能/组件/文件
- `update`: 更新/优化/改进现有功能
- `fix`: 修复 bug
- `docs`: 文档变更
- `chore`: 构建/工具/依赖

**规则：**
- 首行 < 50 字符
- 使用现在时（"新增" 而非 "新增了"）
- 描述清晰具体

### 3. 创建提交

**多行消息：**
```bash
git commit -m "$(cat <<'EOF'
add: 新增 pricing 组件

- 三栏价格表布局,支持月付/年付切换
- 使用 CSS 变量实现主题定制
EOF
)"
```

**单行消息：**
```bash
git commit -m "fix: 修复图片路径错误"
```

### 4. 验证
```bash
git log -1 --format="%h - %s%n%b" && git status
```

---

## 多变更拆分示例

```bash
# 场景：组件修改 + 文档更新 + Bug 修复

# Commit 1: 组件
git add src/templates/news-card/
git commit -m "update: 优化 news-card 组件样式"

# Commit 2: 文档
git add CLAUDE.md README.md
git commit -m "docs: 更新组件使用文档"

# Commit 3: 修复
git add src/components/Preview.astro
git commit -m "fix: 修复预览窗口尺寸计算错误"
```

---

## 执行流程

1. 分析变更（git status/diff）
2. 建议分组策略
3. 起草提交信息
4. 执行并验证
