---
name: git-commit-helper
description: Use this skill for ANY git commit operation unless the user specifically requests otherwise. This skill helps analyze changes, suggest appropriate commit messages following project conventions, split multiple changes into logical commits, and ensure commit messages are professional without AI-generated markers.
---

# Git Commit Helper

自动帮助创建专业的 git commits,遵循项目约定。

## 核心工作流程

### 第一步:分析变更

```bash
# 查看当前状态和改动
git status && git diff --stat && git diff
```

**判断提交策略:**

- **单个 commit**: 所有改动服务于同一目的(功能、修复或优化)
- **多个 commits**: 包含独立功能、不同类型改动、或可分离的修改

**拆分原则:**

1. 功能性改动独立提交
2. Bug 修复独立提交
3. 文档/配置独立提交
4. 样式调整可合并到相关功能

---

### 第二步:生成提交信息

#### 格式规范

```
<type>: <简洁的描述>

- <详细说明 1>
- <详细说明 2>
- <详细说明 3>
```

#### Type 分类

| Type       | 使用场景                      | 示例                       |
| ---------- | ----------------------------- | -------------------------- |
| `add`      | 新增功能/组件/文件/页面       | add: 新增用户登录功能      |
| `update`   | 更新/优化/改进现有功能        | update: 优化图片加载性能   |
| `fix`      | 修复 bug/错误                 | fix: 修复移动端布局错误    |
| `docs`     | 文档变更/注释                 | docs: 更新 API 使用说明    |
| `style`    | 代码格式/样式调整(不影响逻辑) | style: 统一代码缩进格式    |
| `refactor` | 重构代码(不改变功能)          | refactor: 重构用户认证模块 |
| `chore`    | 构建/工具/依赖更新            | chore: 更新 React 至 18.3  |

#### 格式要求

- 首行 < 50 字符(中文约 25 字)
- 详细说明使用列表(- 开头)
- 每条说明清晰具体
- 避免 AI 痕迹("根据分析"、"建议"等)

---

### 第三步:执行提交

**多行消息** (推荐):
```bash
git commit -m "$(cat <<'EOF'
add: 新增 pricing 组件

- 三栏价格表布局,支持月付/年付切换
- 使用 CSS 变量实现主题定制
EOF
)"
```

**单行消息**:
```bash
git commit -m "fix: 修复图片路径错误"
```

---

### 第四步:验证提交

```bash
git log -1 --format="%C(yellow)%h%Creset - %s%n%b"
git status
```

---

## 多变更拆分

**应该拆分:**
- 新功能 + 旧功能优化 → 2 commits
- 功能改动 + Bug 修复 → 2 commits
- 代码逻辑 + 文档更新 → 2 commits

**可以合并:**
- 组件代码 + 组件样式 → 1 commit
- 功能代码 + 功能测试 → 1 commit

**示例:**
```bash
# 改动: 新组件 + 文档 + bug修复

# Commit 1: 新功能
git add src/components/NewsCard/ src/pages/news.astro
git commit -m "add: 新增 NewsCard 组件"

# Commit 2: 修复
git add src/utils/date.ts
git commit -m "fix: 修复日期格式化问题"

# Commit 3: 文档
git add README.md
git commit -m "docs: 更新组件说明"
```

