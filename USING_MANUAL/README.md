# 🚀 Oh-My-OpenCode 完整使用手册

## 📋 目录

1. [🎯 快速开始](#1-🎯-快速开始)
2. [🪄 魔法指令](#2-🪄-魔法指令)
3. [⚡ 高级功能](#3-⚡-高级功能)
4. [🤖 专业代理系统](#4-🤖-专业代理系统)
5. [🔧 配置详解](#5-🔧-配置详解)
6. [🛠️ 工具集](#6-🛠️-工具集)
7. [📋 实战案例](#7-📋-实战案例)
8. [⚠️ 故障排除](#8-⚠️-故障排除)

---

## 1️⃣ 🎯 快速开始

### 1.1 一键安装
```bash
# 交互式安装（推荐）
bunx oh-my-opencode install

# 非交互式安装
bunx oh-my-opencode install --no-tui --claude=max20 --chatgpt=yes --gemini=yes
```

### 1.2 验证安装
```bash
opencode --version  # 应该显示 1.0.150+
cat ~/.config/opencode/opencode.json | grep "oh-my-opencode"  # 应该存在
```

### 1.3 立即开始
```bash
# 启动 Oh-My-OpenCode 增强的 OpenCode
opencode

# 测试魔法指令
ulw  # 启动超级工作模式
```

---

## 2️⃣ 🪄 魔法指令

### 2.1 核心魔法词

| 指令 | 效果 | 使用场景 |
|------|------|----------|
| `ultrawork` / `ulw` | 🔥 超级工作模式 | 复杂项目，需要全功能 |
| `ultrathink` | 🧠 深度思考模式 | 需要深度分析 |
| `orchestrate` | 🎼 智能编排模式 | 多代理协作 |
| `antigravity` | 🚀 反重力模式 | 跳过限制，最大性能 |

### 2.2 魔法指令详解

#### 🚀 `ulw` (Ultra Work)
**效果**: 启动最强性能模式
- 所有代理并行工作
- 自动选择最优模型
- 最大化资源利用
- 无限制执行

**使用方法**:
```bash
# 在任何提示中包含
opencode run "ulw: 构建一个完整的电商系统"

# 或直接启动
ulw
```

#### 🎯 `ultrathink` (Ultra Think)
**效果**: 深度分析模式
- 扩展思考时间
- 多角度分析
- 详细推理过程
- 高质量输出

**使用方法**:
```bash
opencode run "ultrathink: 分析这个架构设计的优缺点"
```

#### 🎼 `orchestrate` (Orchestrate)
**效果**: 智能多代理协作
- 自动分配任务
- 协调工作流程
- 整合多代理结果
- 项目管理级别

**使用方法**:
```bash
opencode run "orchestrate: 设计并实现一个微服务架构"
```

#### 🚀 `antigravity` (Antigravity)
**效果**: 突破所有限制
- 绕过速率限制
- 最大模型性能
- 无约束执行
- 实验性功能

**使用方法**:
```bash
opencode run "antigravity: 快速原型开发，不要限制"
```

### 2.3 组合魔法词

#### 🔥 `ulw + orchestrate`
```bash
opencode run "ulw orchestrate: 构建企业级应用，包含前端、后端、数据库"
```

#### 🧠 `ultrathink + orchestrate`
```bash
opencode run "ultrathink orchestrate: 深度分析并设计复杂的分布式系统"
```

#### ⚡ `ulw + antigravity`
```bash
opencode run "ulw antigravity: 极速开发和部署，追求最大效率"
```

---

## 3️⃣ ⚡ 高级功能

### 3.1 自动化配置

#### 智能模型选择
```json
{
  "auto_model_selection": true,
  "cost_optimization": true,
  "performance_priority": "balanced"
}
```

#### 代理自动编排
```json
{
  "auto_orchestrate": true,
  "default_workflow": "research -> plan -> implement -> review"
}
```

#### 工具链自动化
```json
{
  "auto_tools": true,
  "tool_chain": "lsp -> ast_grep -> edit"
}
```

### 3.2 多智能体协作

#### 指定多代理
```bash
opencode run "agents: claude, gpt-4, gemini-pro: 设计一个完整的SaaS平台"
```

#### 代理角色定义
```json
{
  "agent_roles": {
    "architect": "claude-opus-4-5",
    "frontend": "gemini-3-pro",
    "backend": "gpt-4",
    "database": "claude-sonnet-4-5"
  }
}
```

#### 协作流程模板
```json
{
  "workflows": {
    "full_stack": "librarian -> oracle -> frontend-ui-ux-engineer -> build",
    "research": "librarian + explore (并行)",
    "optimization": "explore -> oracle -> build"
  }
}
```

### 3.3 背景任务系统

#### 并行代理执行
```bash
# 启动多个背景任务
background_task --agent librarian --prompt="研究市场趋势" &
background_task --agent explore --prompt="分析竞品" &
background_task --agent oracle --prompt="设计架构" &
wait  # 等待所有完成
```

#### 任务依赖管理
```json
{
  "task_dependencies": {
    "implementation": ["research", "architecture"],
    "testing": ["implementation"],
    "deployment": ["testing"]
  }
}
```

---

## 4️⃣ 🤖 专业代理系统

### 4.1 核心代理详解

#### 🧠 Sisyphus (主编排器)
- **模型**: Claude Opus 4.5
- **专长**: 项目管理、任务编排、决策制定
- **特点**: 
  - Todo 驱动工作流
  - 强制完成机制
  - 智能代理调度
  - 自动上下文管理

#### 🔮 Oracle (架构师)
- **模型**: GPT-5.2 Medium
- **专长**: 系统架构、技术决策、代码审查
- **特点**:
  - 深度逻辑推理
  - 战略级分析
  - 最佳实践建议
  - 风险评估

#### 📚 Librarian (研究员)
- **模型**: GLM-4.7 Free / Claude Sonnet 4.5
- **专长**: 文档研究、开源分析、实现示例
- **特点**:
  - 多仓库并行搜索
  - 权威资料整合
  - 证据驱动回答
  - 成本效益优化

#### 🔍 Explore (探索者)
- **模型**: Claude Haiku 4.5 / Gemini 3 Flash
- **专长**: 代码探索、模式匹配、快速分析
- **特点**:
  - 超快响应速度
  - AST 级别搜索
  - 上下文感知grep
  - 时代码导航

#### 🎨 Frontend-UI-UX-Engineer (前端工程师)
- **模型**: Gemini 3 Pro Preview
- **专长**: UI/UX设计、前端开发、用户体验
- **特点**:
  - 创意设计能力
  - 现代化代码生成
  - 响应式设计
  - 可访问性优化

#### 📝 Document-Writer (文档专家)
- **模型**: Gemini 3 Flash
- **专长**: 技术写作、文档生成、知识整理
- **特点**:
  - 结构化文档生成
  - 清晰的技术写作
  - 自动示例生成
  - 多格式输出

#### 👁️ Multimodal-Looker (多媒体分析师)
- **模型**: Gemini 3 Flash
- **专长**: 图片分析、PDF处理、视觉理解
- **特点**:
  - 多媒体内容理解
  - 设计图分析
  - 文档摘要生成
  - 视觉信息提取

### 4.2 代理调用方式

#### 直接调用
```bash
@oracle 请审查这个架构设计
@librarian 研究React 18的新特性
@explore 查找所有性能瓶颈
@frontend-ui-ux-engineer 设计一个现代化的仪表板
@document-writer 为这个API编写文档
@multimodal-looker 分析这个架构图
```

#### 背景调用
```bash
background_task --agent oracle --prompt="审查架构" &
background_task --agent librarian --prompt="研究特性" &
background_task --agent explore --prompt="找瓶颈" &
```

#### 批量调用
```bash
opencode run "agents: oracle, librarian, explore: 全面分析这个项目"
```

---

## 5️⃣ 🔧 配置详解

### 5.1 基础配置文件

#### `~/.config/opencode/opencode.json`
```json
{
  "plugin": ["oh-my-opencode"],
  "auto_intelligence": true,
  "performance_mode": "maximum",
  "providers": {
    "anthropic": { /* Claude 配置 */ },
    "openai": { /* OpenAI 配置 */ },
    "google": { /* Gemini 配置 */ }
  }
}
```

#### `~/.config/opencode/oh-my-opencode.json`
```json
{
  "magic_words": {
    "ultrawork": {
      "enabled": true,
      "parallel_agents": "all",
      "auto_optimize": true
    },
    "orchestrate": {
      "enabled": true,
      "workflow_templates": true,
      "smart_delegation": true
    }
  },
  "agents": {
    "sisyphus": {
      "model": "anthropic/claude-opus-4-5",
      "auto_orchestrate": true,
      "todo_enforcement": true
    },
    "oracle": {
      "model": "openai/gpt-5.2",
      "strategic_mode": true,
      "deep_analysis": true
    }
  },
  "auto_features": {
    "context_management": "aggressive",
    "cost_optimization": "smart",
    "performance_monitoring": true
  }
}
```

### 5.2 高级配置选项

#### 性能优化配置
```json
{
  "performance": {
    "max_concurrent_agents": 10,
    "context_compression": "aggressive",
    "token_optimization": "maximum",
    "caching_strategy": "smart"
  }
}
```

#### 成本控制配置
```json
{
  "cost_control": {
    "daily_budget": 50.00,
    "model_optimization": "cost_first",
    "free_model_priority": true,
    "budget_alerts": true
  }
}
```

#### 工作流配置
```json
{
  "workflows": {
    "development": {
      "phases": ["research", "design", "implement", "review"],
      "auto_progression": true,
      "phase_transitions": "smart"
    },
    "analysis": {
      "parallel_agents": ["librarian", "explore"],
      "synthesis_agent": "oracle",
      "depth_level": "comprehensive"
    }
  }
}
```

---

## 6️⃣ 🛠️ 工具集

### 6.1 LSP 工具

#### 智能代码导航
```bash
lsp_hover file.ts:15:10           # 悬停查看类型信息
lsp_goto_definition file.ts:15:10 # 跳转到符号定义
lsp_find_references symbol         # 查找所有引用
lsp_document_symbols file.ts     # 查看文件结构
lsp_workspace_symbols query       # 全工作区符号搜索
```

#### 代码操作工具
```bash
lsp_prepare_rename oldName      # 验证重命名操作
lsp_rename newName             # 执行符号重命名
lsp_code_actions               # 获取可用代码操作
lsp_code_action_resolve         # 应用代码修复或重构
```

### 6.2 AST-Grep 工具

#### 模式匹配搜索
```bash
ast_grep_search 'useEffect\(.*\)' --lang typescript  # 搜索 Hook 模式
ast_grep_search 'class.*extends React.Component' --lang typescript  # 搜索 React 组件
ast_grep_search 'async function.*await' --lang javascript   # 搜索异步函数
```

#### 智能代码替换
```bash
ast_grep_replace 'console.log' '$LOGGER.info' --lang typescript  # 替换日志语句
ast_grep_replace 'var ' 'const' --lang javascript      # var 改 const
```

### 6.3 会话管理工具

#### 会话操作
```bash
session_list --limit 10 --date-filter "2024-01"  # 列出最近的会话
session_read --session-id ses_123 --include_todos  # 读取会话包含待办
session_search "React hooks" --session-id ses_123  # 在会话中搜索
session_info --session-id ses_123               # 获取会话统计信息
```

#### 会话导出导入
```bash
opencode export session-123 > backup.json     # 导出会话
opencode import backup.json                    # 导入会话
opencode share --session current               # 生成分享链接
```

### 6.4 MCP 服务器

#### 内置 MCP 服务器
```json
{
  "mcp_servers": {
    "context7": {
      "enabled": true,
      "priority": "high"
    },
    "websearch_exa": {
      "enabled": true,
      "priority": "medium"
    },
    "grep_app": {
      "enabled": true,
      "priority": "medium"
    }
  }
}
```

#### 自定义 MCP 配置
```yaml
# .mcp.json
name: "custom-tools"
version: "1.0.0"
servers:
  playwrigh
