# 🌐 Phase 3: 全栈项目实战 (3-4周)

## 🎯 阶段目标

**核心目标：** 从零开始构建完整的全栈健身社交平台

**具体目标：**
- ✅ 设计和实现完整的全栈应用架构
- ✅ 实现用户认证、社交功能、健身追踪等核心功能
- ✅ 掌握现代全栈开发最佳实践
- ✅ 完成应用部署和运维

## 📋 项目概述

### 项目名称
**FitPro Social - 智能健身社交平台**

### 项目描述
一个完整的健身社交平台，支持用户记录健身数据、分享健身计划、与朋友互动、获取个性化推荐。

### 功能特性
- 用户注册和社交网络
- 健身计划和记录
- 数据分析和可视化
- 社区互动功能
- 个性化 AI 推荐

### 技术架构
```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend (Next.js)                        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌────────────┐ │
│  │  用户模块   │ │  健身模块   │ │  社区模块   │ │  分析模块  │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Backend API (NestJS)                        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌────────────┐ │
│  │  Auth 模块  │ │  User 模块  │ │  Workout 模块│ │  Social   │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └────────────┘ │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                        Database Layer                            │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌────────────┐ │
│  │ PostgreSQL  │ │    Redis    │ │   S3/OSS    │ │   AI SDK   │ │
│  │  用户/数据  │ │   缓存      │ │  文件存储   │ │  智能推荐  │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

## 📅 周计划

### 第6-7周：项目设计和架构搭建

#### 任务 3.1: 系统架构设计 (3天)

**目标：** 完成完整的系统架构设计和技术选型

**具体步骤：**

1. **需求分析和功能设计**
   - 用户故事和用例图
   - 功能模块划分
   - 非功能性需求（性能、安全、可扩展性）

2. **技术架构设计**
   - 前端架构：Next.js 14 + TypeScript
   - 后端架构：NestJS + GraphQL/REST
   - 数据库架构：PostgreSQL + Prisma
   - 缓存架构：Redis + Docker
   - 部署架构：Vercel + Railway/阿里云

3. **多智能体任务分配**
   ```yaml
   # architecture-design.yaml
   name: "fitpro-social-architecture"
   description: "健身社交平台架构设计"
   agents:
     - name: "system-architect"
       role: "系统架构师"
       tasks:
         - "整体架构设计"
         - "技术选型和权衡分析"
         - "非功能性需求定义"
     - name: "frontend-architect"
       role: "前端架构师"
       tasks:
         - "前端架构设计"
         - "组件库和状态管理选型"
         - "性能优化策略"
     - name: "backend-architect"
       role: "后端架构师"
       tasks:
         - "后端服务架构设计"
         - "数据库架构设计"
         - "API 设计和规范"
     - name: "devops-architect"
       role: "DevOps 架构师"
       tasks:
         - "CI/CD 流程设计"
           - "云服务选型"
           - "监控和日志方案"
   ```

**交付物：**
- 系统架构文档（包含架构图）
- 技术选型报告
- 非功能性需求规格
- 项目路线图

#### 任务 3.2: 项目初始化和基础配置 (2天)

**目标：** 完成项目基础结构搭建和开发环境配置

**具体步骤：**

1. **创建 Monorepo 结构**
   ```bash
   # 创建项目根目录
   mkdir fitpro-social
   cd fitpro-social
   
   # 初始化 Git
   git init
   git remote add origin https://github.com/ygh/fitpro-social.git
   
   # 创建子项目
   mkdir apps
   cd apps
   
   # 创建前端项目
   npx create-next-app@latest frontend --typescript --tailwind --app
   cd frontend
   
   # 创建后端项目
   cd ..
   npx @nestjs/cli new backend --package-manager npm
   cd backend
   
   # 初始化pnpm工作空间
   cd ..
   pnpm init-workspace
   ```

2. **基础配置**
   ```typescript
   // pnpm-workspace.yaml
   packages:
     - 'apps/*'
     
   // tsconfig.json (root)
   {
     "compilerOptions": {
       "target": "ES2020",
       "module": "ESNext",
       "moduleResolution": "node",
       "esModuleInterop": true,
       "strict": true,
       "skipLibCheck": true,
       "paths": {
         "@fitpro/*": ["apps/*/src/*"]
       }
     }
   }
   ```

3. **Oh-My-OpenCode 配置**
   ```yaml
   # .oh-my-opencode/config.yaml
   name: "fitpro-social"
   version: "1.0.0"
   
   agents:
     - id: "frontend-dev"
       model: "gpt-4"
       role: "前端开发"
       workingDir: "apps/frontend"
     - id: "backend-dev"
       model: "claude-3-5-sonnet"
       role: "后端开发"
       workingDir: "apps/backend"
     - id: "mobile-dev"
       model: "claude-3-5-sonnet"
       role: "移动端开发"
       workingDir: "apps/mobile"
     - id: "devops"
       model: "gpt-4"
       role: "DevOps"
   
   workflows:
     default:
       - frontend-dev
       - backend-dev
     mobile-feature:
       - backend-dev
       - mobile-dev
   ```

**交付物：**
- 可运行的 monorepo 项目结构
- 基础配置文件（TypeScript、ESLint、Prettier）
- 开发环境文档
- Oh-My-OpenCode 项目配置

#### 任务 3.3: 数据库设计和初始化 (2天)

**目标：** 完成数据库设计和初始化

**具体步骤：**

1. **数据库建模**
   ```prisma
   // schema.prisma
   generator client {
     provider = "prisma-client-js"
   }
   
   datasource db {
     provider = "postgresql"
     url      = env("DATABASE_URL")
   }
   
   model User {
     id            String    @id @default(cuid())
     email         String    @unique
     username      String    @unique
     passwordHash  String
     avatar        String?
     bio           String?
     createdAt     DateTime  @default(now())
     updatedAt     DateTime  @updatedAt
     
     workouts      Workout[]
     posts         Post[]
     comments      Comment[]
     likes         Like[]
     followers     Follow[]  @relation("following")
     following     Follow[]  @relation("follower")
     achievements  UserAchievement[]
   }
   
   model Workout {
     id          String    @id @default(cuid())
     userId      String
     user        User      @relation(fields: [userId], references: [id])
     type        WorkoutType
     name        String
     duration    Int       // 分钟
     calories    Int
     distance    Float?    // 公里
     startTime   DateTime
     endTime     DateTime
     exercises   Exercise[]
     createdAt   DateTime  @default(now())
   }
   
   model Exercise {
     id          String    @id @default(cuid())
     workoutId   String
     workout     Workout   @relation(fields: [workoutId], references: [id])
     name        String
     sets        Int
     reps        Int?
     weight      Float?
     duration    Int?      // 秒
   }
   
   model Post {
     id          String    @id @default(cuid())
     userId      String
     user        User      @relation(fields: [userId], references: [id])
     content     String
     mediaUrls   String[]
     workoutId   String?
     createdAt   DateTime  @default(now())
     updatedAt   DateTime  @updatedAt
     
     comments    Comment[]
     likes       Like[]
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
   
   model Achievement {
     id          String    @id @default(cuid())
     name        String    @unique
     description String
     icon        String
     requirement Int       // 达成条件
     type        AchievementType
     
     users       UserAchievement[]
   }
   
   model UserAchievement {
     id            String    @id @default(cuid())
     userId        String
     user          User      @relation(fields: [userId], references: [id])
     achievementId String
     achievement   Achievement @relation(fields: [achievementId], references: [id])
     progress      Int       @default(0)
     completedAt   DateTime?
     createdAt     DateTime  @default(now())
     
     @@unique([userId, achievementId])
   }
   ```

2. **数据库迁移**
   ```bash
   # 生成迁移
   cd apps/backend
   npx prisma migrate dev --name init
   
   # 生成 Prisma Client
   npx prisma generate
   
   # 验证数据库连接
   npx prisma studio
   ```

**交付物：**
- 完整的 Prisma Schema
- 数据库迁移文件
- 种子数据脚本
- 数据库文档

### 第8-9周：核心功能开发

#### 任务 3.4: 用户认证系统 (3天)

**目标：** 实现完整的用户认证和授权系统

**具体步骤：**

1. **后端认证模块**
   ```typescript
   // apps/backend/src/auth/auth.module.ts
   import { Module } from '@nestjs/common';
   import { JwtModule } from '@nestjs/jwt';
   import { PassportModule } from '@nestjs/passport';
   import { AuthService } from './auth.service';
   import { AuthController } from './auth.controller';
   import { JwtStrategy } from './strategies/jwt.strategy';
   import { UserModule } from '../user/user.module';
   
   @Module({
     imports: [
       UserModule,
       PassportModule.register({ defaultStrategy: 'jwt' }),
       JwtModule.register({
         secret: process.env.JWT_SECRET,
         signOptions: { expiresIn: '7d' },
       }),
     ],
     controllers: [AuthController],
     providers: [AuthService, JwtStrategy],
     exports: [AuthService],
   })
   export class AuthModule {}
   
   // apps/backend/src/auth/auth.service.ts
   import { Injectable, UnauthorizedException } from '@nestjs/common';
   import { JwtService } from '@nestjs/jwt';
   import * as bcrypt from 'bcrypt';
   import { UserService } from '../user/user.service';
   
   @Injectable()
   export class AuthService {
     constructor(
       private userService: UserService,
       private jwtService: JwtService,
     ) {}
   
     async register(registerDto: RegisterDto) {
       const existingUser = await this.userService.findByEmail(registerDto.email);
       if (existingUser) {
         throw new UnauthorizedException('邮箱已被注册');
       }
       
       const hashedPassword = await bcrypt.hash(registerDto.password, 10);
       const user = await this.userService.create({
         ...registerDto,
         passwordHash: hashedPassword,
       });
   
       const token = this.generateToken(user);
       return { user: this.sanitizeUser(user), token };
     }
   
     async login(loginDto: LoginDto) {
       const user = await this.userService.findByEmail(loginDto.email);
       if (!user) {
         throw new UnauthorizedException('邮箱或密码错误');
       }
       
       const isPasswordValid = await bcrypt.compare(loginDto.password, user.passwordHash);
       if (!isPasswordValid) {
         throw new UnauthorizedException('邮箱或密码错误');
       }
   
       const token = this.generateToken(user);
       return { user: this.sanitizeUser(user), token };
     }
   
     async validateUser(userId: string) {
       return this.userService.findById(userId);
     }
   
     private generateToken(user: User) {
       const payload = { sub: user.id, email: user.email };
       return this.jwtService.sign(payload);
     }
   
     private sanitizeUser(user: User) {
       const { passwordHash, ...result } = user;
       return result;
     }
   }
   ```

2. **前端认证模块**
   ```tsx
   // apps/frontend/src/contexts/AuthContext.tsx
   import { createContext, useContext, useState, useEffect } from 'react';
   import { authApi } from '@/lib/api';
   
   interface AuthContextType {
     user: User | null;
     token: string | null;
     login: (email: string, password: string) => Promise<void>;
     register: (data: RegisterData) => Promise<void>;
     logout: () => void;
     isLoading: boolean;
   }
   
   export const AuthContext = createContext<AuthContextType | null>(null);
   
   export const AuthProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
     const [user, setUser] = useState<User | null>(null);
     const [token, setToken] = useState<string | null>(null);
     const [isLoading, setIsLoading] = useState(true);
   
     useEffect(() => {
       const storedToken = localStorage.getItem('token');
       if (storedToken) {
         setToken(storedToken);
         fetchUser(storedToken);
       } else {
         setIsLoading(false);
       }
     }, []);
   
     const fetchUser = async (authToken: string) => {
       try {
         const response = await authApi.getProfile(authToken);
         setUser(response.data);
       } catch {
         localStorage.removeItem('token');
         setToken(null);
       } finally {
         setIsLoading(false);
       }
     };
   
     const login = async (email: string, password: string) => {
       const response = await authApi.login({ email, password });
       const { user, token } = response.data;
       localStorage.setItem('token', token);
       setToken(token);
       setUser(user);
     };
   
     const register = async (data: RegisterData) => {
       const response = await authApi.register(data);
       const { user, token } = response.data;
       localStorage.setItem('token', token);
       setToken(token);
       setUser(user);
     };
   
     const logout = () => {
       localStorage.removeItem('token');
       setToken(null);
       setUser(null);
     };
   
     return (
       <AuthContext.Provider value={{ user, token, login, register, logout, isLoading }}>
         {children}
       </AuthContext.Provider>
     );
   };
   ```

3. **多智能体开发配置**
   ```yaml
   # auth-development.yaml
   name: "auth-system-development"
   description: "用户认证系统开发"
   parallel: true
   agents:
     - name: "backend-auth-dev"
       task: "实现后端 JWT 认证系统"
       workingDir: "apps/backend"
       output: "src/auth/"
     - name: "frontend-auth-dev"
       task: "实现前端认证上下文和组件"
       workingDir: "apps/frontend"
       output: "src/contexts/ src/components/auth/"
     - name: "security-reviewer"
       task: "安全审计和漏洞检查"
       context: "认证代码"
   ```

**交付物：**
- 完整的认证后端 API
- 前端认证组件
- JWT 中间件和策略
- 安全测试报告

#### 任务 3.5: 健身追踪功能 (3天)

**目标：** 实现健身记录和分析功能

**具体步骤：**

1. **健身记录功能**
   ```typescript
   // apps/backend/src/workouts/workouts.service.ts
   import { Injectable, NotFoundException } from '@nestjs/common';
   import { PrismaService } from '../prisma/prisma.service';
   import { CreateWorkoutDto } from './dto/create-workout.dto';
   
   @Injectable()
   export class WorkoutsService {
     constructor(private prisma: PrismaService) {}
   
     async create(userId: string, dto: CreateWorkoutDto) {
       const workout = await this.prisma.workout.create({
         data: {
           userId,
           type: dto.type,
           name: dto.name,
           duration: dto.duration,
           calories: dto.calories,
           distance: dto.distance,
           startTime: new Date(dto.startTime),
           endTime: new Date(dto.endTime),
           exercises: {
             create: dto.exercises.map(ex => ({
               name: ex.name,
               sets: ex.sets,
               reps: ex.reps,
               weight: ex.weight,
               duration: ex.duration,
             })),
           },
         },
         include: {
           exercises: true,
         },
       });
   
       await this.updateUserStats(userId);
       return workout;
     }
   
     async findAll(userId: string, query: WorkoutQueryDto) {
       const workouts = await this.prisma.workout.findMany({
         where: {
           userId,
           type: query.type,
           startTime: {
             gte: query.startDate,
             lte: query.endDate,
           },
         },
         include: {
           exercises: true,
         },
         orderBy: { startTime: 'desc' },
         skip: query.skip,
         take: query.take,
       });
   
       const total = await this.prisma.workout.count({
         where: {
           userId,
           type: query.type,
           startTime: {
             gte: query.startDate,
             lte: query.endDate,
           },
         },
       });
   
       return { workouts, total };
     }
   
     async getStats(userId: string, period: string) {
       const startDate = new Date();
       switch (period) {
         case 'week':
           startDate.setDate(startDate.getDate() - 7);
           break;
         case 'month':
           startDate.setMonth(startDate.getMonth() - 1);
           break;
         case 'year':
           startDate.setFullYear(startDate.getFullYear() - 1);
           break;
       }
   
       const workouts = await this.prisma.workout.findMany({
         where: {
           userId,
           startTime: { gte: startDate },
         },
         include: { exercises: true },
       });
   
       return {
         totalWorkouts: workouts.length,
         totalDuration: workouts.reduce((sum, w) => sum + w.duration, 0),
         totalCalories: workouts.reduce((sum, w) => sum + w.calories, 0),
         totalDistance: workouts.reduce((sum, w) => sum + (w.distance || 0), 0),
         workoutsByType: this.groupByType(workouts),
         weeklyProgress: this.getWeeklyProgress(workouts),
       };
     }
   
     private async updateUserStats(userId: string) {
       const achievements = await this.checkAchievements(userId);
       for (const achievement of achievements) {
         await this.prisma.userAchievement.upsert({
           where: {
             userId_achievementId: {
               userId,
               achievementId: achievement.id,
             },
           },
           create: {
             userId,
             achievementId: achievement.id,
             progress: achievement.progress,
           },
           update: {
             progress: achievement.progress,
             completedAt: achievement.completed ? new Date() : null,
           },
         });
       }
     }
   }
   ```

2. **前端健身追踪界面**
   ```tsx
   // apps/frontend/src/pages/workouts/index.tsx
   import { useState } from 'react';
   import { Card, Button, Modal, Form, Select, InputNumber, DatePicker } from 'antd';
   import { PlusOutlined } from '@ant-design/icons';
   import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
   import { workoutApi } from '@/lib/api';
   import { WorkoutList } from '@/components/workouts/WorkoutList';
   import { WorkoutChart } from '@/components/workouts/WorkoutChart';
   
   export default function WorkoutsPage() {
     const [isModalOpen, setIsModalOpen] = useState(false);
     const [form] = Form.useForm();
     const queryClient = useQueryClient();
   
     const { data: workouts, isLoading } = useQuery({
       queryKey: ['workouts'],
       queryFn: () => workoutApi.getAll(),
     });
   
     const { data: stats } = useQuery({
       queryKey: ['workoutStats'],
       queryFn: () => workoutApi.getStats('month'),
     });
   
     const createMutation = useMutation({
       mutationFn: (data: WorkoutFormData) => workoutApi.create(data),
       onSuccess: () => {
         queryClient.invalidateQueries({ queryKey: ['workouts'] });
         queryClient.invalidateQueries({ queryKey: ['workoutStats'] });
         setIsModalOpen(false);
         form.resetFields();
       },
     });
   
     const onFinish = (values: any) => {
       createMutation.mutate({
         ...values,
         startTime: values.timeRange[0].toISOString(),
         endTime: values.timeRange[1].toISOString(),
         exercises: [],
       });
     };
   
     return (
       <div className="workouts-page">
         <div className="page-header">
           <h1>我的健身</h1>
           <Button type="primary" icon={<PlusOutlined />} onClick={() => setIsModalOpen(true)}>
             记录健身
           </Button>
         </div>
   
         <div className="stats-section">
           <Card>
             <Statistic title="本月健身次数" value={stats?.totalWorkouts || 0} />
           </Card>
           <Card>
             <Statistic title="总时长" value={stats?.totalDuration || 0} suffix="分钟" />
           </Card>
           <Card>
             <Statistic title="消耗卡路里" value={stats?.totalCalories || 0} suffix="kcal" />
           </Card>
           <Card>
             <Statistic title="总距离" value={stats?.totalDistance || 0} suffix="km" />
           </Card>
         </div>
   
         <Card title="健身趋势" className="chart-card">
           <WorkoutChart data={stats?.weeklyProgress || []} />
         </Card>
   
         <Card title="健身记录" className="list-card">
           <WorkoutList workouts={workouts?.workouts || []} isLoading={isLoading} />
         </Card>
   
         <Modal
           title="记录健身"
           open={isModalOpen}
           onCancel={() => setIsModalOpen(false)}
           footer={null}
         >
           <Form form={form} layout="vertical" onFinish={onFinish}>
             <Form.Item name="type" label="健身类型" rules={[{ required: true }]}>
               <Select
                 options={[
                   { value: 'running', label: '跑步' },
                   { value: 'cycling', label: '骑行' },
                   { value: 'swimming', label: '游泳' },
                   { value: 'workout', label: '力量训练' },
                   { value: 'yoga', label: '瑜伽' },
                 ]}
               />
             </Form.Item>
             <Form.Item name="name" label="健身名称" rules={[{ required: true }]}>
               <Input />
             </Form.Item>
             <Form.Item name="duration" label="时长（分钟）" rules={[{ required: true }]}>
               <InputNumber min={1} style={{ width: '100%' }} />
             </Form.Item>
             <Form.Item name="calories" label="消耗卡路里">
               <InputNumber min={0} style={{ width: '100%' }} />
             </Form.Item>
             <Form.Item name="timeRange" label="健身时间" rules={[{ required: true }]}>
               <DatePicker.RangePicker showTime />
             </Form.Item>
             <Form.Item>
               <Button type="primary" htmlType="submit" loading={createMutation.isLoading}>
                 保存
               </Button>
             </Form.Item>
           </Form>
         </Modal>
       </div>
     );
   }
   ```

**交付物：**
- 完整的健身追踪后端 API
- 前端健身记录和统计界面
- 数据分析和可视化组件
- 成就系统集成

#### 任务 3.6: 社交功能 (3天)

**目标：** 实现社区互动和社交功能

**具体步骤：**

1. **社交功能后端**
   ```typescript
   // apps/backend/src/social/social.service.ts
   import { Injectable, ForbiddenException } from '@nestjs/common';
   import { PrismaService } from '../prisma/prisma.service';
   
   @Injectable()
   export class SocialService {
     constructor(private prisma: PrismaService) {}
   
     async createPost(userId: string, content: string, mediaUrls: string[], workoutId?: string) {
       return this.prisma.post.create({
         data: {
           userId,
           content,
           mediaUrls,
           workoutId,
         },
         include: {
           user: {
             select: { id: true, username: true, avatar: true },
           },
           workout: true,
           _count: {
             select: { comments: true, likes: true },
           },
         },
       });
     }
   
     async getFeed(userId: string, page = 1, limit = 20) {
       const following = await this.prisma.follow.findMany({
         where: { followerId: userId },
         select: { followingId: true },
       });
   
       const userIds = [userId, ...following.map(f => f.followingId)];
   
       const posts = await this.prisma.post.findMany({
         where: { userId: { in: userIds } },
         include: {
           user: {
             select: { id: true, username: true, avatar: true },
           },
           workout: true,
           comments: {
             include: {
               user: {
                 select: { id: true, username: true, avatar: true },
               },
             },
             orderBy: { createdAt: 'desc' },
             take: 3,
           },
           likes: {
             where: { userId },
             select: { userId: true },
           },
           _count: {
             select: { comments: true, likes: true },
           },
         },
         orderBy: { createdAt: 'desc' },
         skip: (page - 1) * limit,
         take: limit,
       });
   
       return posts.map(post => ({
         ...post,
         isLiked: post.likes.length > 0,
         likes: undefined,
       }));
     }
   
     async likePost(userId: string, postId: string) {
       const existing = await this.prisma.like.findUnique({
         where: {
           userId_postId: { userId, postId },
         },
       });
   
       if (existing) {
         await this.prisma.like.delete({
           where: { id: existing.id },
         });
         return { liked: false };
       }
   
       await this.prisma.like.create({
         data: { userId, postId },
       });
       return { liked: true };
     }
   
     async followUser(followerId: string, followingId: string) {
       if (followerId === followingId) {
         throw new ForbiddenException('不能关注自己');
       }
   
       const existing = await this.prisma.follow.findUnique({
         where: {
           followerId_followingId: { followerId, followingId },
         },
       });
   
       if (existing) {
         await this.prisma.follow.delete({
           where: { id: existing.id },
         });
         return { followed: false };
       }
   
       await this.prisma.follow.create({
         data: { followerId, followingId },
       });
       return { followed: true };
     }
   }
   ```

2. **前端社区界面**
   ```tsx
   // apps/frontend/src/pages/feed/index.tsx
   import { useState } from 'react';
   import { Card, Avatar, Button, Input, Image, Dropdown } from 'antd';
   import { HeartOutlined, HeartFilled, CommentOutlined, ShareAltOutlined } from '@ant-design/icons';
   import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
   import { socialApi } from '@/lib/api';
   import { useAuth } from '@/contexts/AuthContext';
   
   interface PostCardProps {
     post: Post;
   }
   
   export const PostCard: React.FC<PostCardProps> = ({ post }) => {
     const { user } = useAuth();
     const queryClient = useQueryClient();
   
     const likeMutation = useMutation({
       mutationFn: () => socialApi.likePost(post.id),
       onSuccess: () => {
         queryClient.invalidateQueries({ queryKey: ['feed'] });
       },
     });
   
     const followMutation = useMutation({
       mutationFn: () => socialApi.followUser(post.user.id),
       onSuccess: () => {
         queryClient.invalidateQueries({ queryKey: ['feed'] });
       },
     });
   
     return (
       <Card className="post-card">
         <div className="post-header">
           <Avatar src={post.user.avatar} size={48} />
           <div className="post-info">
             <span className="username">{post.user.username}</span>
             <span className="time">{formatTime(post.createdAt)}</span>
           </div>
           {user?.id !== post.user.id && (
             <Button
               size="small"
               onClick={() => followMutation.mutate()}
             >
               {post.isFollowing ? '取消关注' : '关注'}
             </Button>
           )}
         </div>
   
         <div className="post-content">
           <p>{post.content}</p>
         </div>
   
         {post.mediaUrls.length > 0 && (
           <div className="post-media">
             <Image.PreviewGroup>
               {post.mediaUrls.map((url, index) => (
                 <Image key={index} src={url} />
               ))}
             </Image.PreviewGroup>
           </div>
         )}
   
         {post.workout && (
           <Card size="small" className="workout-card">
             <span>🏃 {post.workout.name} - {post.workout.duration}分钟</span>
           </Card>
         )}
   
         <div className="post-actions">
           <Button
             type="text"
             icon={post.isLiked ? <HeartFilled style={{ color: '#ff4d4f' }} /> : <HeartOutlined />}
             onClick={() => likeMutation.mutate()}
           >
             {post._count.likes}
           </Button>
           <Button type="text" icon={<CommentOutlined />}>
             {post._count.comments}
           </Button>
           <Button type="text" icon={<ShareAltOutlined />} />
         </div>
       </Card>
     );
   };
   
   export default function FeedPage() {
     const [newPost, setNewPost] = useState('');
     const queryClient = useQueryClient();
   
     const { data: posts, isLoading } = useQuery({
       queryKey: ['feed'],
       queryFn: () => socialApi.getFeed(),
     });
   
     const createPostMutation = useMutation({
       mutationFn: (content: string) => socialApi.createPost(content),
       onSuccess: () => {
         queryClient.invalidateQueries({ queryKey: ['feed'] });
         setNewPost('');
       },
     });
   
     return (
       <div className="feed-page">
         <Card className="new-post-card">
           <Input.TextArea
             value={newPost}
             onChange={(e) => setNewPost(e.target.value)}
             placeholder="分享你的健身动态..."
             autoSize={{ minRows: 2, maxRows: 4 }}
           />
           <div className="post-actions">
             <Button
               type="primary"
               disabled={!newPost.trim()}
               onClick={() => createPostMutation.mutate(newPost)}
               loading={createPostMutation.isLoading}
             >
               发布
             </Button>
           </div>
         </Card>
   
         <div className="posts-list">
           {posts?.map((post: Post) => (
             <PostCard key={post.id} post={post} />
           ))}
         </div>
       </div>
     );
   }
   ```

**交付物：**
- 完整的社交后端 API
- 前端动态流和帖子组件
- 点赞、评论、关注功能
- 实时更新支持

### 第10周：AI 功能和部署

#### 任务 3.7: AI 智能推荐 (2天)

**目标：** 实现个性化健身推荐功能

**具体步骤：**

1. **AI 推荐服务**
   ```typescript
   // apps/backend/src/ai/ai.service.ts
   import { Injectable } from '@nestjs/common';
   import { OpenAIService } from './openai.service';
   import { PrismaService } from '../prisma/prisma.service';
   
   @Injectable()
   export class AIService {
     constructor(
       private openai: OpenAIService,
       private prisma: PrismaService,
     ) {}
   
     async generateWorkoutPlan(userId: string, preferences: WorkoutPreferences) {
       const user = await this.prisma.user.findUnique({
         where: { id: userId },
         include: {
           workouts: {
             orderBy: { startTime: 'desc' },
             take: 30,
           },
           achievements: {
             include: { achievement: true },
           },
         },
       });
   
       const prompt = this.buildWorkoutPrompt(user, preferences);
       const response = await this.openai.complete(prompt);
   
       return this.parseWorkoutPlan(response);
     }
   
     async getSmartSuggestion(userId: string) {
       const recentWorkouts = await this.prisma.workout.findMany({
         where: { userId },
         orderBy: { startTime: 'desc' },
         take: 7,
       });
   
       const achievements = await this.prisma.userAchievement.findMany({
         where: { userId, completedAt: null },
         include: { achievement: true },
       });
   
       const prompt = `基于用户最近7天的健身数据和待完成的成就，生成一条鼓励和建议：
       最近健身次数：${recentWorkouts.length}
       待完成成就：${achievements.map(a => a.achievement.name).join(', ')}
       最近一次健身类型：${recentWorkouts[0]?.type || '无'}
       
       请用简洁鼓励的语气生成建议（不超过50字）：`;
   
       const suggestion = await this.openai.complete(prompt);
       return suggestion.trim();
     }
   
     async analyzeWorkoutForm(userId: string, workoutData: any) {
       const prompt = `分析以下健身数据，给出改进建议：
       健身类型：${workoutData.type}
       持续时间：${workoutData.duration}分钟
       消耗卡路里：${workoutData.calories}
       训练频率：${workoutData.frequency}
       
       请从以下方面分析：
       1. 训练强度评估
       2. 改进建议
       3. 下一步训练目标建议`;
   
       return this.openai.complete(prompt);
     }
   
     private buildWorkoutPrompt(user: any, preferences: WorkoutPreferences) {
       // 构建详细的健身计划生成提示词
     }
   
     private parseWorkoutPlan(response: string) {
       // 解析 AI 返回的训练计划
     }
   }
   ```

**交付物：**
- AI 推荐服务
- 健身计划生成功能
- 智能建议功能
- 表单分析功能

#### 任务 3.8: 应用部署 (3天)

**目标：** 完成全栈应用的部署和运维配置

**具体步骤：**

1. **前端部署（Vercel）**
   ```typescript
   // apps/frontend/vercel.json
   {
     "buildCommand": "pnpm build",
     "outputDirectory": ".next",
     "framework": "nextjs",
     "rewrites": [
       {
         "source": "/api/:path*",
         "destination": "https://api.fitpro.social/:path*"
       }
     ],
     "headers": [
       {
         "source": "/(.*)",
         "headers": [
           {
             "key": "X-Frame-Options",
             "value": "DENY"
           },
           {
             "key": "X-Content-Type-Options",
             "value": "nosniff"
           }
         ]
       }
     ]
   }
   
   // .env.production
   NEXT_PUBLIC_API_URL=https://api.fitpro.social
   NEXT_PUBLIC_APP_URL=https://fitpro.social
   ```

2. **后端部署（Railway/阿里云）**
   ```yaml
   # apps/backend/Dockerfile
   FROM node:20-alpine
   
   WORKDIR /app
   
   COPY package*.json ./
   RUN npm ci --only=production
   
   COPY prisma ./prisma/
   RUN npx prisma generate
   
   COPY . .
   
   RUN npm run build
   
   EXPOSE 3001
   
   CMD ["npm", "start"]
   ```

3. **CI/CD 配置**
   ```yaml
   # .github/workflows/deploy.yml
   name: Deploy
   
   on:
     push:
       branches: [main]
   
   jobs:
     deploy-frontend:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: pnpm/action-setup@v2
         - uses: actions/setup-node@v4
           with:
             node-version: '20'
             cache: 'pnpm'
         - run: pnpm install --frozen-lockfile
         - run: pnpm build
           env:
             NEXT_PUBLIC_API_URL: ${{ secrets.API_URL }}
         - uses: amondnet/vercel-action@v25
           with:
             vercel-token: ${{ secrets.VERCEL_TOKEN }}
             vercel-org-id: ${{ secrets.ORG_ID }}
             vercel-project-id: ${{ secrets.PROJECT_ID }}
             vercel-args: '--prod'
   
     deploy-backend:
       runs-on: ubuntu-latest
       steps:
         - uses: actions/checkout@v4
         - uses: pnpm/action-setup@v2
         - uses: actions/setup-node@v4
           with:
             node-version: '20'
             cache: 'pnpm'
         - run: pnpm install --frozen-lockfile
         - run: pnpm build
           env:
             DATABASE_URL: ${{ secrets.DATABASE_URL }}
             JWT_SECRET: ${{ secrets.JWT_SECRET }}
         - uses: docker/build-push-action@v5
           with:
             context: ./apps/backend
             push: true
             tags: ghcr.io/ygh/fitpro-social-backend:${{ github.sha }}
   ```

4. **监控和日志**
   ```typescript
   // apps/backend/src/main.ts
   import { NestFactory } from '@nestjs/core';
   import { AppModule } from './app.module';
   import { WinstonModule } from 'nest-winston';
   import { winstonConfig } from './config/winston.config';
   
   async function bootstrap() {
     const app = await NestFactory.create(AppModule, {
       logger: WinstonModule.createLogger(winstonConfig),
     });
     
     // 启用 CORS
     app.enableCors({
       origin: process.env.FRONTEND_URL,
       credentials: true,
     });
     
     await app.listen(process.env.PORT || 3001);
   }
   bootstrap();
   ```

**交付物：**
- 前端 Vercel 部署配置
- 后端 Docker 部署配置
- CI/CD 自动化流程
- 监控和日志配置
- 性能测试报告

## 🎯 交付物清单

### 文档交付物
- [ ] 系统架构文档
- [ ] API 接口文档（Swagger/OpenAPI）
- [ ] 部署运维手册
- [ ] 用户使用指南
- [ ] 数据库文档
- [ ] 测试报告

### 代码交付物
- [ ] 完整的前端项目（Next.js）
- [ ] 完整的后端项目（NestJS）
- [ ] 数据库 Schema 和迁移
- [ ] CI/CD 配置文件
- [ ] 监控和日志配置

### 功能交付物
- [ ] 用户认证系统
- [ ] 健身追踪功能
- [ ] 社交互动功能
- [ ] AI 智能推荐
- [ ] 数据分析展示

---

**阶段状态：** 🟡 准备开始  
**预计开始时间：** 2026年2月20日  
**预计完成时间：** 2026年3月19日  

> 💡 提示：本阶段是整个学习计划的核心，需要投入更多时间和精力。建议使用 Oh-My-OpenCode 的多智能体功能来加速开发。