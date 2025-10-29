# Git Commit 规约 - 完整参考

本文档包含项目完整的 Git Commit 规约，包括格式、类型、粒度原则、实际案例和最佳实践。

## Commit Message 格式

### 基本格式

```
<type>: <简洁的中文描述>

- <详细说明 1>
- <详细说明 2>
- <详细说明 3>
```

### 重要规则

- ❌ **禁止添加 AI 生成标识** - 不要包含 "🤖 Generated with Claude Code" 或 "Co-Authored-By: Claude" 等标识
- ✅ **保持简洁专业** - commit message 应该只包含变更的内容描述

### 格式要求

- **首行简洁明了**（建议 50 字符以内）
- **使用中文描述**（符合项目语言设定）
- **使用现在时态**（例如："新增" 而非 "新增了"）
- **详细说明用列表**（提高可读性）
- ❌ **不要添加 AI 生成标识**（保持 commit 历史的专业性）

## Type 类型

### add
新增功能、组件、文件

**使用场景：**
- 添加新的组件或页面
- 创建新的功能模块
- 新增配置文件或资源文件

**示例：**
```bash
add: 新增 pricing 组件
add: 新增用户认证功能
add: 新增 Snippets 功能
```

### update
更新、优化、改进现有功能（包含样式调整、重构等）

**使用场景：**
- 优化现有功能的性能或体验
- 重构代码结构
- 调整样式或布局
- 改进现有实现方式

**示例：**
```bash
update: 优化 Preview 组件响应式尺寸设置
update: 重构 news-card 组件以使用 Pulse Design System
update: 移除组件展示页面中的 CSS 变量说明部分
```

### fix
修复 bug、解决问题

**使用场景：**
- 修复功能性错误
- 解决显示问题
- 修正逻辑错误

**示例：**
```bash
fix: 修复 news-card 页面图片无法显示的问题
fix: 修复预览窗口尺寸计算错误
fix: 修复移动端菜单点击无响应的问题
```

### docs
文档相关的变更

**使用场景：**
- 更新 README 或项目文档
- 添加或修改代码注释
- 更新开发指南

**示例：**
```bash
docs: 更新 Git Commit 规约,明确禁止 AI 生成标识
docs: 添加组件使用示例
docs: 完善 API 文档说明
```

### chore
构建配置、开发工具、依赖更新

**使用场景：**
- 更新依赖包版本
- 修改构建脚本
- 调整开发工具配置
- 更新 .gitignore 等配置文件

**示例：**
```bash
chore: 更新 Astro 到最新版本
chore: 添加 ESLint 配置
chore: 调整开发服务器配置
```

## Commit 粒度原则

### 核心原则

**1 个逻辑变更 = 1 个 commit**

- 多个独立的变更应分别提交
- 相关的变更可以合并提交
- 避免将无关变更混在一起

### 好的示例

```bash
# ✅ 按功能分割，每个 commit 都有明确的目的
git commit -m "add: 新增 news-list 组件"
git commit -m "update: 优化 Preview 组件响应式尺寸"
git commit -m "fix: 移除 news-card 的 max-width 限制"
```

### 不好的示例

```bash
# ❌ 多个无关变更混在一起
git commit -m "update: 更新多个文件"

# ❌ 描述不清楚
git commit -m "fix: 修复问题"

# ❌ 包含 AI 生成标识
git commit -m "add: 新增功能

🤖 Generated with Claude Code"
```

## Commit 前检查清单

在创建 commit 之前，务必确认：

1. **确认变更内容**: 使用 `git diff` 查看所有改动
2. **评估分割可能**: 是否可以拆分成多个逻辑 commit
3. **分组相关文件**: 同一目的的变更应归到一起
4. **明确 message**: 清楚说明"改了什么"和"为什么改"

## 实际案例

### 案例 1: 新增组件

**场景：** 添加一个完整的新组件，包括模板、页面和缩略图

```bash
git add src/templates/pricing/ src/pages/components/pricing.astro public/images/thumbnails/pricing.png
git commit -m "add: 新增 pricing 组件

- 三栏价格表布局，支持月付/年付切换
- 使用 CSS 变量实现主题定制
- 包含组件展示页面和缩略图"
```

**分析：**
- 使用 `add` 类型，因为是新增功能
- 首行简洁说明新增了什么
- 详细说明列出了组件的主要特性
- 所有相关文件（模板、页面、图片）在一个 commit 中，因为它们是一个完整的功能

### 案例 2: 功能优化

**场景：** 优化现有组件的实现方式

```bash
git add src/components/Preview.astro
git commit -m "update: 优化 Preview 组件响应式尺寸设置

- Desktop 视口从 1280px 调整为 1024px，更符合主流桌面尺寸
- 将 Tailwind 类替换为原生 CSS，提高可读性和精确控制"
```

**分析：**
- 使用 `update` 类型，因为是改进现有功能
- 说明了具体的优化内容
- 解释了优化的原因（为什么这样改）

### 案例 3: Bug 修复

**场景：** 修复一个具体的显示问题

```bash
git add src/pages/components/news-card.astro
git commit -m "fix: 修复 news-card 页面图片无法显示的问题

- 图片路径从相对路径改为绝对路径
- 补充缺失的 alt 属性"
```

**分析：**
- 使用 `fix` 类型，因为是修复错误
- 首行清楚说明修复了什么问题
- 详细说明列出了具体的修复措施

### 案例 4: 简单变更

**场景：** 简单的配置调整

```bash
git add package.json
git commit -m "update: 开发服务器增加 --host 参数

允许局域网访问开发服务器，方便在移动设备上测试。"
```

**分析：**
- 简单的变更也可以有详细说明
- 说明了修改的目的和好处
- 单行详细说明时可以不使用列表格式

### 案例 5: 重构代码

**场景：** 重构组件以使用新的设计系统

```bash
git add src/templates/news-card/ src/pages/components/news-card.astro
git commit -m "update: 重构 news-card 组件以使用 Pulse Design System

- 替换硬编码颜色为 Pulse CSS 变量
- 使用 Pulse 的间距和字体大小系统
- 保持向后兼容，提供 fallback 值
- 更新展示页面中的样式说明"
```

**分析：**
- 使用 `update` 类型，因为重构属于改进
- 详细列出了重构的各个方面
- 强调了向后兼容性

### 案例 6: 文档更新

**场景：** 更新项目规约文档

```bash
git add CLAUDE.md
git commit -m "docs: 更新 Git Commit 规约,明确禁止 AI 生成标识

- 在重要规则中强调不要添加 AI 标识
- 补充注意事项说明
- 更新示例代码"
```

**分析：**
- 使用 `docs` 类型
- 说明了文档更新的主要内容
- 列出了具体的修改点

## 拆分多个变更的示例

### 场景：混合变更

假设你修改了以下内容：
1. 优化了 news-card 组件样式
2. 更新了文档
3. 修复了 Preview 组件的一个 bug

**正确做法：拆分成 3 个 commit**

```bash
# Commit 1: 组件优化
git add src/templates/news-card/
git commit -m "update: 优化 news-card 组件样式

- 调整卡片间距以提升视觉层次
- 优化 hover 效果的过渡动画
- 改进移动端的响应式布局"

# Commit 2: 文档更新
git add CLAUDE.md README.md
git commit -m "docs: 更新组件使用文档

- 补充 news-card 的自定义变量说明
- 添加 Pulse Design System 集成指南
- 更新开发工作流程说明"

# Commit 3: Bug 修复
git add src/components/Preview.astro
git commit -m "fix: 修复预览窗口尺寸计算错误

- 修正 viewport 尺寸计算逻辑
- 确保在不同屏幕尺寸下正确显示"

# 最后确认所有变更已提交
git status
```

**为什么要拆分？**
- 每个 commit 都有独立的目的
- 如果需要回滚某个修改，不会影响其他修改
- Git 历史更清晰，易于追踪和理解
- Code review 时更容易审查

## 常见错误和改进建议

### 错误 1: 描述太笼统

```bash
# ❌ 不好
git commit -m "update: 更新文件"

# ✅ 好
git commit -m "update: 优化 news-card 组件的响应式布局

- 调整移动端的卡片间距
- 改进平板电脑视图的排列方式"
```

### 错误 2: 混合多个无关变更

```bash
# ❌ 不好：一个 commit 包含了功能、修复和文档
git add .
git commit -m "update: 各种更新"

# ✅ 好：拆分成多个 commit
git add src/templates/pricing/
git commit -m "add: 新增 pricing 组件"

git add src/components/Preview.astro
git commit -m "fix: 修复预览窗口bug"

git add README.md
git commit -m "docs: 更新使用说明"
```

### 错误 3: 包含 AI 生成标识

```bash
# ❌ 不好：包含 AI 标识
git commit -m "add: 新增功能

🤖 Generated with Claude Code

Co-Authored-By: Claude <noreply@anthropic.com>"

# ✅ 好：只包含变更描述
git commit -m "add: 新增功能

- 实现用户认证
- 添加权限验证"
```

### 错误 4: 使用英文描述

```bash
# ❌ 不好：使用英文（项目规定使用中文）
git commit -m "update: update news card component"

# ✅ 好：使用中文
git commit -m "update: 更新 news-card 组件"
```

### 错误 5: 使用过去时态

```bash
# ❌ 不好：使用过去时
git commit -m "add: 新增了 pricing 组件"

# ✅ 好：使用现在时
git commit -m "add: 新增 pricing 组件"
```

## 特殊情况处理

### 情况 1: 紧急 hotfix

紧急修复也要遵循规约，但可以适当简化详细说明：

```bash
git commit -m "fix: 修复生产环境图片加载失败

紧急修复：CDN 路径配置错误导致图片无法加载"
```

### 情况 2: 大量文件重命名

```bash
git commit -m "chore: 重命名组件文件以符合命名规范

- 将 newsCard 重命名为 news-card
- 将 pricingTable 重命名为 pricing
- 更新所有导入路径"
```

### 情况 3: 依赖更新

```bash
git commit -m "chore: 更新依赖包到最新版本

- Astro 升级到 4.0
- Tailwind CSS 升级到 3.4
- 解决安全漏洞警告"
```

### 情况 4: 配置调整

```bash
git commit -m "chore: 调整 Vite 配置以支持局域网访问

在 astro.config.mjs 中添加 server.host: true 配置"
```

## 最佳实践总结

### 提交频率

- ✅ 完成一个逻辑功能就提交
- ✅ 修复一个 bug 就提交
- ❌ 不要等到完成一天的工作才提交
- ❌ 不要每改一行就提交

### Message 质量

- ✅ 首行简洁有力，一眼看懂改了什么
- ✅ 详细说明解释为什么这样改
- ✅ 使用列表格式提高可读性
- ❌ 不要写"修复bug"这样的空洞描述
- ❌ 不要包含 AI 生成标识

### 代码审查友好

- ✅ 每个 commit 都应该是可以独立审查的
- ✅ 相关的修改放在一个 commit
- ✅ 无关的修改拆分成多个 commit
- ❌ 不要在一个 commit 里混杂多个功能

### Git 历史清晰

好的 commit 历史应该像这样：

```
287f528 add: 新增 Snippets 功能
9d339b2 docs: 更新 Git Commit 规约,明确禁止 AI 生成标识
da36817 update: 移除组件展示页面中的 CSS 变量说明部分
888223f update: 重构 news-list 组件以使用 Pulse Design System
f1ef814 update: 重构 news-card 组件以使用 Pulse Design System
```

每个 commit 都清楚说明了做了什么，易于理解和追踪。

## 使用 Heredoc 格式化多行 Commit Message

为了确保格式正确，建议使用 heredoc 语法：

```bash
git commit -m "$(cat <<'EOF'
<type>: <简洁描述>

- <详细说明 1>
- <详细说明 2>
- <详细说明 3>
EOF
)"
```

**优点：**
- 保证换行格式正确
- 避免 shell 转义问题
- 易于编辑多行内容
- 可以安全地包含特殊字符

**示例：**

```bash
git commit -m "$(cat <<'EOF'
update: 优化组件加载性能

- 实现组件懒加载机制
- 减少首屏加载时间约 40%
- 优化图片资源加载策略
EOF
)"
```

## 工作流程建议

1. **编写代码** - 专注于实现功能
2. **检查变更** - `git status` 和 `git diff` 审查所有修改
3. **规划 commits** - 决定是单个还是多个 commit
4. **分组文件** - 使用 `git add` 分组相关文件
5. **撰写 message** - 遵循规约编写清晰的 commit message
6. **提交代码** - 使用 heredoc 格式提交
7. **验证结果** - `git log` 检查 commit 是否符合预期

## 总结

遵循这套 Git Commit 规约可以：

- ✅ 保持 Git 历史清晰易读
- ✅ 方便团队协作和代码审查
- ✅ 便于追踪和回滚特定修改
- ✅ 提升项目的专业性
- ✅ 帮助新成员快速理解项目演进过程

记住最重要的两条原则：

1. **1 个逻辑变更 = 1 个 commit**
2. **❌ 禁止添加 AI 生成标识**
