# 🔧 开发者配置示例

## 🎯 开发环境完整配置

### 1. opencode.json (开发版)
```json
{
  "plugin": [
    "oh-my-opencode",
    "opencode-antigravity-auth@1.2.8",
    "opencode-openai-codex-auth@4.3.0"
  ],
  "model": "anthropic/claude-sonnet-4-5",
  "auto_intelligence": true,
  "debug": true,
  "performance": {
    "context_compression": "aggressive",
    "token_optimization": "balanced",
    "max_concurrent_agents": 10
  },
  "providers": {
    "anthropic": {
      "name": "Anthropic",
      "models": {
        "claude-sonnet-4-5": {
          "name": "Claude Sonnet 4.5",
          "limit": {
            "context": 200000,
            "output": 8192
          },
          "modalities": {
            "input": ["text", "image"],
            "output": ["text"]
          }
        },
        "claude-opus-4-5": {
          "name": "Claude Opus 4.5",
          "limit": {
            "context": 200000,
            "output": 4096
          },
          "modalities": {
            "input": ["text", "image"],
            "output": ["text"]
          }
        }
      },
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}",
        "timeout": 600000
      }
    },
    "openai": {
      "name": "OpenAI",
      "models": {
        "gpt-5.2": {
          "name": "GPT 5.2",
          "limit": {
            "context": 272000,
            "output": 128000
          },
          "modalities": {
            "input": ["text", "image"],
            "output": ["text"]
          }
        }
      },
      "options": {
        "apiKey": "{env:OPENAI_API_KEY}",
        "timeout": 600000
      }
    },
    "google": {
      "name": "Google",
      "models": {
        "gemini-3-pro-preview": {
          "name": "Gemini 3 Pro Preview",
          "limit": {
            "context": 128000,
            "output": 8192
          },
          "modalities": {
            "input": ["text", "image", "audio"],
            "output": ["text"]
          }
        }
      },
      "options": {
        "apiKey": "{env:GOOGLE_API_KEY}",
        "timeout": 600000
      }
    }
  }
}
```

### 2. oh-my-opencode.json (开发版)
```json
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/master/assets/oh-my-opencode.schema.json",
  "magic_words": {
    "ultrawork": {
      "enabled": true,
      "parallel_agents": "all",
      "auto_optimize": true,
      "max_concurrent_tasks": 20
    },
    "orchestrate": {
      "enabled": true,
      "workflow_templates": true,
      "smart_delegation": true,
      "auto_progression": true
    },
    "ultrathink": {
      "enabled": true,
      "extended_thinking": true,
      "deep_analysis": true,
      "multi_perspective": true
    },
    "antigravity": {
      "enabled": true,
      "bypass_limits": true,
      "max_performance": true,
      "experimental_features": true
    }
  },
  "agents": {
    "sisyphus": {
      "model": "anthropic/claude-opus-4-5",
      "auto_orchestrate": true,
      "todo_enforcement": true,
      "max_iterations": 100,
      "timeout": 600000,
      "temperature": 0.3,
      "system_prompt": "You are Sisyphus, the ultimate AI orchestrator. Plan, delegate, and execute complex tasks using specialized subagents with aggressive parallel execution."
    },
    "oracle": {
      "model": "openai/gpt-5.2",
      "strategic_mode": true,
      "deep_analysis": true,
      "reasoning_effort": "high",
      "temperature": 0.1,
      "system_prompt": "You are Oracle, the strategic architect. Provide deep analysis, architectural decisions, and strategic guidance with logical precision."
    },
    "librarian": {
      "model": "opencode/glm-4.7-free",
      "cost_optimized": true,
      "parallel_search": true,
      "evidence_based": true,
      "system_prompt": "You are Librarian, the research expert. Provide evidence-based answers from official docs, open source implementations, and codebase exploration."
    },
    "explore": {
      "model": "anthropic/claude-haiku-4-5",
      "speed_optimized": true,
      "ast_grep_enabled": true,
      "lsp_tools": true,
      "system_prompt": "You are Explore, the code exploration expert. Use AST-Grep, LSP tools, and contextual search for fast, accurate code analysis."
    },
    "frontend-ui-ux-engineer": {
      "model": "google/antigravity-gemini-3-pro-high",
      "creative_mode": true,
      "modern_design": true,
      "responsive_design": true,
      "system_prompt": "You are Frontend UI/UX Engineer. Create beautiful, modern, responsive user interfaces with excellent user experience."
    },
    "document-writer": {
      "model": "google/antigravity-gemini-3-flash",
      "technical_writing": true,
      "structured_output": true,
      "auto_examples": true,
      "system_prompt": "You are Document Writer. Create clear, structured technical documentation with examples and best practices."
    },
    "multimodal-looker": {
      "model": "google/antigravity-gemini-3-flash",
      "visual_analysis": true,
      "pdf_processing": true,
      "image_understanding": true,
      "system_prompt": "You are Multimodal Looker. Analyze images, PDFs, diagrams, and visual content to extract meaningful information."
    }
  },
  "auto_features": {
    "context_management": "aggressive",
    "cost_optimization": "smart",
    "performance_monitoring": true,
    "auto_update_check": true,
    "error_recovery": true,
    "session_backup": true
  },
  "background_task": {
    "default_concurrency": 10,
    "provider_concurrency": {
      "anthropic": 5,
      "openai": 10,
      "google": 15
    },
    "model_concurrency": {
      "anthropic/claude-opus-4-5": 2,
      "google/antigravity-gemini-3-flash": 20,
      "opencode/glm-4.7-free": 30
    }
  },
  "tools": {
    "lsp": {
      "enabled": true,
      "auto_activation": true,
      "enhanced_features": true
    },
    "ast_grep": {
      "enabled": true,
      "parallel_search": true,
      "smart_replacement": true
    },
    "session": {
      "enabled": true,
      "auto_backup": true,
      "search_index": true
    }
  },
  "hooks": {
    "pre_tool_use": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "eslint --fix $FILE",
            "timeout": 10000
          }
        ]
      }
    ],
    "post_tool_use": [
      {
        "matcher": "bash",
        "hooks": [
          {
            "type": "notification",
            "message": "Command executed: $COMMAND"
          }
        ]
      }
    ]
  },
  "mcp": {
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
  },
  "skills": {
    "playwright": {
      "enabled": true,
      "auto_install": true
    },
    "git_master": {
      "enabled": true,
      "auto_install": true
    }
  },
  "debug": {
    "verbose_logging": true,
    "performance_tracing": true,
    "error_diagnostics": true,
    "agent_communication_log": true
  }
}
```

## 🎯 开发环境特性

### 1. 调试功能
- **详细日志**: 记录所有代理通信
- **性能追踪**: 监控响应时间和资源使用
- **错误诊断**: 自动错误检测和报告
- **代理通信日志**: 完整的对话记录

### 2. 开发工具集成
- **ESLint 自动修复**: 代码写入后自动格式化
- **Git 钩子**: 自动提交前检查
- **通知系统**: 命令执行结果通知
- **实时监控**: 开发过程实时反馈

### 3. 高级功能
- **并行任务**: 最多20个并发背景任务
- **智能缓存**: 多层缓存策略
- **自动更新**: 自动检查和更新配置
- **错误恢复**: 自动错误检测和恢复

### 4. 实验性功能
- **反重力模式**: 绕过所有限制
- **扩展思考**: 深度分析模式
- **实验模型**: 使用最新实验性模型
- **高级工作流**: 复杂的多阶段工作流

## 🚀 开发者使用建议

### 1. 日常开发
```bash
# 启动开发模式
opencode --debug

# 使用魔法指令进行复杂任务
ulw: 开发一个包含用户认证、数据存储、API服务的完整应用

# 监控性能
opencode monitor --real-time
```

### 2. 调试问题
```bash
# 启用详细日志
opencode --log-level DEBUG run "测试消息"

# 检查配置
opencode config validate

# 性能基准测试
opencode benchmark run "性能测试"
```

### 3. 实验新功能
```bash
# 启用实验性功能
opencode --experimental

# 使用反重力模式
antigravity: 快速原型开发，不要限制

# 深度分析模式
ultrathink: 深度分析这个复杂系统的架构设计
```

## ⚠️ 注意事项

### 1. 成本控制
- 开发配置可能消耗更多 token
- 建议设置每日预算限制
- 监控使用情况

### 2. 性能影响
- 调试功能可能影响性能
- 并行任务增加资源消耗
- 建议在开发环境使用

