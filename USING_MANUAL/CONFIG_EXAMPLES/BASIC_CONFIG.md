# 🔧 基础配置示例

## 1. 最小配置

### opencode.json
```json
{
  "plugin": ["oh-my-opencode"],
  "model": "anthropic/claude-sonnet-4-5"
}
```

### oh-my-opencode.json
```json
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/master/assets/oh-my-opencode.schema.json",
  "agents": {
    "librarian": {
      "model": "opencode/glm-4.7-free"
    },
    "explore": {
      "model": "opencode/claude-haiku-4-5"
    }
  }
}
```

## 2. 开发者配置

### opencode.json (开发版)
```json
{
  "plugin": ["oh-my-opencode"],
  "model": "anthropic/claude-sonnet-4-5",
  "auto_intelligence": true,
  "debug": true,
  "performance": {
    "context_compression": "aggressive",
    "token_optimization": "balanced"
  }
}
```

### oh-my-opencode.json (开发版)
```json
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/master/assets/oh-my-opencode.schema.json",
  "magic_words": {
    "ultrawork": {
      "enabled": true,
      "parallel_agents": "all",
      "auto_optimize": true
    },
    "orchestrate": {
      "enabled": true,
      "workflow_templates": true
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
      "strategic_mode": true
    },
    "librarian": {
      "model": "opencode/glm-4.7-free",
      "cost_optimized": true
    },
    "explore": {
      "model": "anthropic/claude-haiku-4-5",
      "speed_optimized": true
    },
    "frontend-ui-ux-engineer": {
      "model": "google/antigravity-gemini-3-pro-high",
      "creative_mode": true
    },
    "document-writer": {
      "model": "google/antigravity-gemini-3-flash",
      "technical_writing": true
    },
    "multimodal-looker": {
      "model": "google/antigravity-gemini-3-flash",
      "visual_analysis": true
    }
  },
  "auto_features": {
    "context_management": "aggressive",
    "cost_optimization": "smart",
    "performance_monitoring": true,
    "auto_update_check": true
  }
}
```

## 3. 生产配置

### opencode.json (生产版)
```json
{
  "plugin": ["oh-my-opencode"],
  "model": "anthropic/claude-sonnet-4-5",
  "auto_intelligence": false,
  "performance": "stable",
  "security": {
    "encryption": true,
    "audit_logging": true
  },
  "cost_control": {
    "daily_budget": 100.00,
    "budget_alerts": true,
    "cost_optimization": "cost_first"
  }
}
```

### oh-my-opencode.json (生产版)
```json
{
  "$schema": "https://raw.githubusercontent.com/code-yeongyu/oh-my-opencode/master/assets/oh-my-opencode.schema.json",
  "magic_words": {
    "ultrawork": {
      "enabled": true,
      "parallel_agents": 6,
      "cost_limit": 50.0
    },
    "orchestrate": {
      "enabled": true,
      "max_parallel_tasks": 3
    }
  },
  "agents": {
    "sisyphus": {
      "model": "anthropic/claude-opus-4-5",
      "max_iterations": 50,
      "timeout": 600000
    },
    "oracle": {
      "model": "openai/gpt-5.2",
      "reasoning_effort": "high"
    }
  },
  "auto_features": {
    "context_management": "conservative",
    "error_handling": "graceful",
    "fallback_strategies": true
  },
  "monitoring": {
    "performance_metrics": true,
    "cost_tracking": true,
    "error_alerting": true
  }
}
```

## 4. 特殊用例配置

### 成本优化优先
```json
{
  "cost_control": {
    "priority": "cost_first",
    "prefer_free_models": true,
    "daily_budget": 25.00,
    "model_tiers": {
      "research": "free",
      "development": "low_cost",
      "deployment": "balanced"
    }
  }
}
```

### 性能优先
```json
{
  "performance": {
    "priority": "speed_first",
    "max_concurrent_agents": 20,
    "context_compression": "minimal",
    "use_fastest_models": true
  }
}
```

### 质量优先
```json
{
  "quality": {
    "priority": "quality_first",
    "use_best_models": true,
    "deep_analysis": true,
    "multiple_reviews": true,
    "extended_thinking": true
  }
}
```
