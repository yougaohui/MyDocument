# 📚 Oh-My-OpenCode 使用手册完整版

## 📋 文档结构

```
USING_MANUAL/
├── README.md                 # 完整使用手册
├── QUICK_START.md           # 5分钟快速上手
├── ADVANCED_FEATURES.md    # 高级功能详解
├── CONFIG_EXAMPLES/        # 配置示例
│   ├── BASIC_CONFIG.md       # 基础配置
│   ├── DEVELOPER_CONFIG.md    # 开发者配置
│   └── PRODUCTION_CONFIG.md # 生产环境配置
└── SUMMARY.md              # 本文档
```

## 🎯 核心特性总结

### 🪄 魔法指令系统

#### 5大核心魔法词
| 指令 | 功能 | 使用场景 | 效果级别 |
|------|------|----------|----------|
| `ulw` / `ultrawork` | 超级工作模式 | 🔥🔥🔥🔥 |
| `ultrathink` | 深度思考模式 | 🧠🧠🧠🧠 |
| `orchestrate` | 智能编排模式 | 🎼🎼🎼🎼 |
| `antigravity` | 无限制模式 | 🚀🚀🚀🚀 |
| `search` / `find` | 搜索模式 | 🔍🔍🔍🔍 |

#### 组合指令
- `ulw orchestrate`: 超级编排
- `ultrathink + orchestrate`: 深度分析+智能编排
- `ulw + antigravity`: 无限制超高速

### 🤖 7大专业代理

1. **Sisyphus** (主编排器)
   - 模型: Claude Opus 4.5
   - 专长: 项目管理、任务编排、决策制定
   - 特点: Todo强制完成、智能调度

2. **Oracle** (架构师)
   - 模型: GPT-5.2 Medium
   - 专长: 系统架构、技术决策、代码审查
   - 特点: 战略分析、深度推理

3. **Librarian** (研究员)
   - 模型: GLM-4.7 Free / Claude Sonnet 4.5
   - 专长: 文档研究、开源分析、实现示例
   - 特点: 多仓库搜索、证据驱动

4. **Explore** (探索者)
   - 模型: Claude Haiku 4.5 / Gemini 3 Flash
   - 专长: 代码探索、模式匹配、快速分析
   - 特点: AST-Grep、LSP工具

5. **Frontend-UI-UX-Engineer** (前端工程师)
   - 模型: Gemini 3 Pro Preview
   - 专长: UI/UX设计、前端开发、用户体验
   - 特点: 创意设计、响应式布局

6. **Document-Writer** (文档专家)
   - 模型: Gemini 3 Flash
   - 专长: 技术写作、文档生成、知识整理
   - 特点: 结构化输出、自动示例

7. **Multimodal-Looker** (多媒体分析师)
   - 模型: Gemini 3 Flash
   - 专长: 图片分析、PDF处理、视觉理解
   - 特点: 设计图分析、文档摘要

### ⚡ 高级自动化功能

#### 1. 智能模型选择
- 自动成本优化
- 性能优先模式
- 质量优先模式
- 免费模型优先

#### 2. 代理自动编排
- 任务依赖管理
- 并行执行控制
- 结果智能融合
- 冲突解决机制

#### 3. 上下文智能管理
- 积极压缩策略
- 智能摘要生成
- 关键信息保护
- 窗口监控

#### 4. 工具链自动化
- LSP → AST-Grep → Edit
- 搜索 → 分析 → 实现
- 自动重构管道
- 质量检查集成

### 🛠️ 工具生态系统

#### 1. LSP 工具 (11种)
- 智能代码导航
- 符号定义跳转
- 全工作区符号搜索
- 实时错误诊断
- 自动补全增强

#### 2. AST-Grep 工具
- 模式匹配搜索 (25语言)
- 智能代码替换
- 批量重构操作
- 语法安全保证
- 性能优化建议

#### 3. 会话管理工具
- 会话列表和过滤
- 全文搜索功能
- 待办事项追踪
- 导入导出支持

#### 4. MCP 服务器集成
- Context7 官方文档
- Exa AI 网络搜索
- Grep App GitHub搜索
- 自定义服务器支持

### 🔧 配置系统详解

#### 基础配置
```json
{
  "plugin": ["oh-my-opencode"],
  "model": "anthropic/claude-sonnet-4-5"
}
```

#### 高级配置
```json
{
  "magic_words": {
    "ultrawork": {
      "enabled": true,
      "parallel_agents": "all",
      "auto_optimize": true
    }
  },
  "agents": {
    "sisyphus": {
      "model": "anthropic/claude-opus-4-5",
      "auto_orchestrate": true,
      "todo_enforcement": true
    }
  },
  "auto_features": {
    "context_management": "aggressive",
    "cost_optimization": "smart",
    "performance_monitoring": true
  }
}
```

### 📋 实战案例模板

#### 1. 企业应用开发
```bash
# 研究阶段
ulw: @librarian 研究微服务架构和技术选型

# 架构设计阶段  
ulw: @oracle 基于研究结果设计系统架构

# 并行开发阶段
ulw orchestrate: @frontend-ui-ux-engineer 设计现代Web界面, @build 实现后端服务

# 质量保证阶段
@explore 全面审查代码质量和性能
```

#### 2. 系统重构
```bash
# 分析阶段
ultrathink: @explore 深度分析现有系统问题和改进机会

# 计划阶段
ulw: @oracle 制定详细重构计划和实施路线图

# 实施阶段
ulw orchestrate: @build 执行重构, @document-writer 更新文档
```

### ⚠️ 故障排除指南

#### 常见问题解决
1. 魔法指令不生效
2. 代理调用失败
3. 性能问题优化
4. 配置冲突解决

#### 高级调试
- 详细日志输出
- 性能监控分析
- 配置验证工具
- 缓存清理方法

---

## 🎊 使用建议

### 新手入门
1. 从 `QUICK_START.md` 开始
2. 先体验基础功能
3. 逐步学习高级特性
4. 加入社区讨论

### 进阶用户
1. 阅读完整手册
2. 自定义配置优化
3. 掌握多代理协作
4. 实践工作流程模板

### 高级用户
1. 探索实验性功能
2. 开发自定义扩展
3. 优化性能和成本
4. 贡献社区改进

---

## 📚 文档信息

- **版本**: v1.0
- **更新**: 2025年1月13日
- **基于**: Oh-My-OpenCode v3.0.0-beta.1
- **语言**: 简体中文
- **状态**: 完整版

## 🚀 立即开始

### 1️⃣ 快速验证安装
```bash
opencode --version  # 确认版本
opencode models    # 查看可用模型
```

### 2️⃣ 测试基础功能
```bash
opencode run "Hello, 测试基础连接"
```

### 3️⃣ 体验魔法指令
```bash
ulw  # 启动超高级工作模式
```

### 4️⃣ 尝试多代理协作
```bash
opencode run "ulw: @oracle @librarian 设计一个博客系统"
```

---

## 🎯 核心价值

Oh-My-OpenCode 重新定义了AI辅助开发：

### 🌟 超越传统工具
- 不再是简单的代码补全
- 而是智能的开发伙伴
- 具备项目管理和团队协作能力

### 🚀 性能革命
- 通过魔法指令解锁全部潜能
- 自动化配置和优化
- 智能资源管理和成本控制

### 🤖 协作进化
- 多专业代理自主协同工作
- 智能任务分配和结果整合
- 项目级的开发管理能力

### 🎯 开发范式转变
- 从人工驱动到AI驱动
- 从单打独斗到团队协作
- 从重复劳动到创意工作

**这不仅仅是工具的升级，这是开发方式革命！** 🎉

---

**开始您的AI增强开发之旅！** 🚀

更多资源：
- GitHub: https://github.com/code-yeongyu/oh-my-opencode
- Discord: https://discord.gg/PUwSMR9XNk
- 实验室: https://sisyphuslabs.ai
