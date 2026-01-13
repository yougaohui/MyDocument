# 🤖 AGENTS.md - Oh-My-OpenCode 文档项目指南

## 📋 项目概览
这是 Oh-My-OpenCode 使用手册的文档仓库，专注于 AI 增强开发工具的中文文档。

## 🚀 快速命令
```bash
# 验证文档完整性
find USING_MANUAL -name "*.md" -exec echo "✅ {}" \;

# 检查链接有效性
markdownlint-cli2 USING_MANUAL/**/*.md

# 生成文档统计
find USING_MANUAL -name "*.md" | xargs wc -l | tail -1

# 快速预览
head -20 USING_MANUAL/README.md
```

## 📝 文档规范
- 使用中文标点符号
- Emoji 统一使用 🚀📚🔧🪄🤖
- 代码块指定语言类型
- 表格使用 Markdown 标准格式

## 🔧 维护流程
1. 更新内容后检查链接
2. 验证 Markdown 语法
3. 提交使用语义化信息
4. 推送到 main 分支

## ⚡ 快速部署
```bash
git add . && git commit -m "📚 更新文档内容" && git push
```
