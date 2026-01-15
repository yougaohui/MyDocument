# 🏃 实践项目二：智能健身社交平台

## 🎯 项目概述

### 项目背景
从零开始构建一个完整的全栈健身社交应用，包含用户系统、健身追踪、社交互动和 AI 智能推荐功能。

### 技术栈
- **前端：** Next.js 14 + TypeScript + Tailwind CSS
- **后端：** NestJS + PostgreSQL + Redis
- **移动端：** React Native
- **AI：** OpenAI GPT-4
- **部署：** Vercel + Railway + Cloudflare

## 🏗️ 系统架构

```
┌─────────────────────────────────────────────────────────────────┐
│                         Frontend Layer                           │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐  │
│  │   Next.js SPA   │  │   React Native  │  │   Admin Panel   │  │
│  │   (Web App)     │  │   (Mobile)      │  │   (管理后台)    │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────┼─────────┐
                    ▼         ▼         ▼
          ┌───────────┐ ┌───────────┐ ┌───────────┐
          │   Vercel  │ │  Railway  │ │ Cloudflare│
          └───────────┘ └───────────┘ └───────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         API Gateway                              │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    NestJS REST API                          ││
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────────┐   ││
│  │  │Auth      │ │User      │ │Workout   │ │AI            │   ││
│  │  │Module    │ │Module    │ │Module    │ │Recommendation│   ││
│  │  └──────────┘ └──────────┘ └──────────┘ └──────────────┘   ││
│  └─────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         Data Layer                               │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────────────┐  │
│  │  PostgreSQL  │  │    Redis     │  │    OpenAI API        │  │
│  │  (主数据库)   │  │  (缓存层)    │  │  (AI 智能推荐)       │  │
│  └──────────────┘  └──────────────┘  └──────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

## 🚀 开发路线图

### Phase 1: 基础架构 (2周)

#### 第1周：项目搭建和认证系统

**Day 1-2: 项目初始化**

**Oh-My-OpenCode 配置：**
```yaml
# fitpro-social-init.yaml
name: "fitpro-social-init"
description: "智能健身社交平台项目初始化"
agents:
  - name: "fullstack-architect"
    task: "设计整体架构和技术选型"
    output: "docs/architecture.md"
  - name: "frontend-lead"
    task: "初始化 Next.js 项目和配置"
    workingDir: "apps/web"
  - name: "backend-lead"
    task: "初始化 NestJS 项目和数据库"
    workingDir: "apps/api"
  - name: "mobile-lead"
    task: "初始化 React Native 项目"
    workingDir: "apps/mobile"
```

**执行步骤：**
```bash
# 创建工作空间
mkdir fitpro-social
cd fitpro-social
pnpm init

# 创建 pnpm 工作空间配置
cat > pnpm-workspace.yaml << EOF
packages:
  - 'apps/*'
EOF

# 创建 Next.js 项目
cd apps
npx create-next-app@latest web --typescript --tailwind --app --src-dir
cd web

# 创建 NestJS 项目
cd ..
npx @nestjs/cli new api --package-manager pnpm
cd api

# 创建 React Native 项目
cd ..
npx expo init mobile --template blank-typescript
```

**Day 3-5: 用户认证系统**

**多智能体开发：**
```yaml
# auth-system.yaml
name: "auth-system"
description: "用户认证系统开发"
parallel: true
agents:
  - name: "backend-auth"
    task: "实现 JWT 认证模块"
    workingDir: "apps/api"
  - name: "web-auth"
    task: "实现 Web 端认证页面"
    workingDir: "apps/web"
  - name: "mobile-auth"
    task: "实现移动端认证页面"
    workingDir: "apps/mobile"
```

**核心功能：**
- 用户注册/登录
- JWT Token 管理
- 密码重置
- 第三方登录（可选）

#### 第2周：用户资料和社交关系

**Day 1-3: 用户资料管理**

**数据库设计：**
```prisma
// schema.prisma
model User {
  id            String    @id @default(cuid())
  email         String    @unique
  username      String    @unique
  avatar        String?
  bio           String?
  fitnessGoals  Json?     // 健身目标
  createdAt     DateTime  @default(now())
  
  // 社交关系
  followers     Follow[]  @relation("following")
  following     Follow[]  @relation("follower")
  
  // 健身数据
  workouts      Workout[]
  achievements  UserAchievement[]
  
  // 社交内容
  posts         Post[]
  comments      Comment[]
  likes         Like[]
}

model Follow {
  id          String    @id @default(cuid())
  followerId  String
  followingId String
  follower    User      @relation("follower", fields: [followerId], references: [id])
  following   User      @relation("following", fields: [followingId], references: [id])
  createdAt   DateTime  @default(now())
  
  @@unique([followerId, followingId])
}
```

**Day 4-5: 社交功能基础**

**核心功能：**
- 用户关注/取消关注
- 粉丝列表
- 用户搜索
- 资料编辑

### Phase 2: 核心功能 (3周)

#### 第3周：健身追踪功能

**Day 1-3: 健身记录模块**

**功能设计：**
```typescript
// 健身记录类型定义
interface Workout {
  id: string;
  userId: string;
  type: WorkoutType;
  name: string;
  duration: number;        // 分钟
  calories: number;
  distance?: number;       // 公里（跑步、骑行等）
  startTime: Date;
  endTime: Date;
  exercises: Exercise[];
  route?: Route;          // 运动轨迹
  notes?: string;
  isPublic: boolean;
}

type WorkoutType = 
  | 'running'
  | 'cycling'
  | 'swimming'
  | 'workout'
  | 'yoga'
  | 'hiit'
  | 'walking'
  | 'other';
```

**Day 4-5: 健身计划功能**

**功能设计：**
- 创建健身计划
- 计划日程安排
- 计划进度跟踪
- 计划模板库

#### 第4周：社交互动功能

**Day 1-3: 动态流和帖子**

**核心功能：**
```typescript
// 帖子创建
async function createPost(userId: string, content: string, mediaUrls: string[]) {
  const post = await prisma.post.create({
    data: {
      userId,
      content,
      mediaUrls,
      workoutId,  // 可选：关联健身记录
    },
    include: {
      user: {
        select: { id: true, username: true, avatar: true },
      },
    },
  });
  
  // 创建活动动态
  await createActivity(userId, 'post', post.id);
  
  return post;
}

// 点赞功能
async function toggleLike(userId: string, postId: string) {
  const existing = await prisma.like.findUnique({
    where: { userId_postId: { userId, postId } },
  });
  
  if (existing) {
    await prisma.like.delete({ where: { id: existing.id } });
    return { liked: false };
  }
  
  await prisma.like.create({ data: { userId, postId } });
  return { liked: true };
}
```

**Day 4-5: 社区功能**

**功能设计：**
- 帖子评论/回复
- 话题标签
- 用户举报
- 内容审核

#### 第5周：数据分析和成就系统

**Day 1-3: 数据统计分析**

**统计指标：**
```typescript
interface WorkoutStats {
  totalWorkouts: number;
  totalDuration: number;      // 分钟
  totalCalories: number;
  totalDistance: number;      // 公里
  
  // 周期对比
  weeklyProgress: {
    current: WeeklyStats;
    previous: WeeklyStats;
    change: number;
  };
  
  // 类型分布
  typeDistribution: {
    type: WorkoutType;
    count: number;
    percentage: number;
  }[];
  
  // 成就完成情况
  achievementsCompleted: number;
  achievementsInProgress: number;
}
```

**Day 4-5: 成就系统**

**成就类型：**
- 健身次数成就
- 时长成就
- 连续打卡成就
- 社交互动成就

### Phase 3: AI 和高级功能 (2周)

#### 第6周：AI 智能推荐

**Day 1-3: 健身计划推荐**

**AI Prompt 设计：**
```typescript
const workoutPlanPrompt = `
基于用户数据生成个性化健身计划：

用户信息：
- 健身目标：${user.fitnessGoals}
- 健身偏好：${user.workoutPreferences}
- 历史训练：${recentWorkouts}

请生成一份7天的健身计划，包括：
1. 每天的训练类型和时长
2. 预计消耗卡路里
3. 训练强度说明
4. 注意事项

请以 JSON 格式返回：
{
  "days": [
    {
      "day": 1,
      "type": "running",
      "duration": 30,
      "calories": 300,
      "intensity": "moderate",
      "description": "..."
    }
  ],
  "tips": [...]
}
`;
```

**Day 4-5: 智能建议**

**功能实现：**
- 训练提醒
- 进度鼓励
- 瓶颈突破建议
- 个性化推荐

#### 第7周：高级功能和完善

**功能列表：**
- 离线数据同步
- 实时消息推送
- 数据导出功能
- 多语言支持

### Phase 4: 测试和部署 (2周)

#### 第8周：测试和质量保证

**测试策略：**
```typescript
// 测试金字塔
const testingStrategy = {
  unit: {
    coverage: '>80%',
    framework: 'Jest',
    tools: ['@testing-library/react', '@testing-library/react-native'],
  },
  integration: {
    coverage: '>60%',
    framework: 'Supertest',
  },
  e2e: {
    coverage: '关键流程',
    framework: 'Cypress',
  },
};
```

#### 第9周：部署和运维

**部署架构：**
```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  web:
    image: fitpro-social/web:latest
    ports:
      - "3000:3000"
    environment:
      - NEXT_PUBLIC_API_URL=https://api.fitpro.social
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '0.5'
          memory: 512M

  api:
    image: fitpro-social/api:latest
    ports:
      - "3001:3001"
    environment:
      - DATABASE_URL=postgresql://...
      - REDIS_URL=redis://...
    deploy:
      replicas: 2
      resources:
        limits:
          cpus: '1'
          memory: 1G

  redis:
    image: redis:7-alpine
    volumes:
      - redis_data:/data
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 256M

volumes:
  redis_data:
```

## 📊 项目评估

### 功能完整性 (35%)
| 模块 | 功能点 | 状态 |
|------|--------|------|
| 用户系统 | 注册、登录、资料 | 待开发 |
| 健身追踪 | 记录、计划、统计 | 待开发 |
| 社交功能 | 帖子、点赞、评论 | 待开发 |
| AI 推荐 | 计划生成、智能建议 | 待开发 |

### 技术质量 (35%)
- 测试覆盖率 > 80%
- 性能指标达标
- 代码规范符合
- 安全性评估

### 用户体验 (30%)
- 界面美观度
- 操作流畅度
- 响应速度
- 可访问性

## 🎓 学习要点

### 技术深度
1. **Next.js 全栈开发**
   - App Router 架构
   - Server Components
   - API Routes

2. **NestJS 后端开发**
   - 模块化架构
   - 依赖注入
   - 装饰器模式

3. **React Native 移动开发**
   - 原生模块集成
   - 跨平台适配

4. **AI 集成**
   - Prompt Engineering
   - API 集成
   - 缓存策略

### 项目管理
1. Monorepo 工作流
2. 多智能体协作
3. CI/CD 自动化
4. 敏捷开发实践

## 🔗 相关资源

- [Next.js 文档](https://nextjs.org/docs)
- [NestJS 文档](https://nestjs.com/docs)
- [React Native 文档](https://reactnative.dev/docs)
- [OpenAI API 文档](https://platform.openai.com/docs)

---

**项目状态：** 🟡 待开始  
**预计开始时间：** 2026年2月20日  
**预计完成时间：** 2026年4月17日  
**难度：** ⭐⭐⭐⭐