# 📱 实践项目一：FitPro2 Web 管理后台

## 🎯 项目概述

### 项目背景
基于现有的 FitPro2 Android 应用，添加 Web 管理后台，实现用户数据可视化、设备管理、健康分析等功能。

### 技术栈
- **前端：** React 18 + TypeScript + Ant Design
- **后端：** Node.js + Express + PostgreSQL
- **移动端：** Android（现有项目）
- **工具：** Oh-My-OpenCode 多智能体协作

## 🚀 开发计划

### 阶段一：基础架构搭建 (1周)

#### 第1天：项目初始化

**任务目标：** 搭建前后端项目基础结构

**Oh-My-OpenCode 配置：**
```yaml
# fitpro-web-init.yaml
name: "fitpro-web-init"
description: "FitPro2 Web 管理后台初始化"
agents:
  - name: "frontend-architect"
    task: "初始化 React 项目并配置基础架构"
    workingDir: "fitpro-web-frontend"
  - name: "backend-architect"
    task: "初始化 Node.js 项目并配置数据库"
    workingDir: "fitpro-web-backend"
```

**执行命令：**
```bash
# 前端项目初始化
npx create-react-app fitpro-web-frontend --template typescript
cd fitpro-web-frontend
npm install antd react-router-dom axios @tanstack/react-query
npm install -D tailwindcss postcss autoprefixer

# 后端项目初始化
mkdir fitpro-web-backend
cd fitpro-web-backend
npm init -y
npm install express cors helmet morgan prisma @prisma/client
npm install -D typescript ts-node @types/express
npx prisma init
```

**验收标准：**
- [ ] 前端项目能够正常运行
- [ ] 后端 API 能够启动
- [ ] 数据库连接正常

#### 第2-3天：用户认证模块

**任务目标：** 实现用户注册、登录和权限管理

**多智能体任务配置：**
```yaml
# user-auth.yaml
name: "user-auth-module"
description: "用户认证模块开发"
agents:
  - name: "backend-dev"
    task: "实现 JWT 认证 API"
    output: "src/middleware/auth.ts"
  - name: "frontend-dev"
    task: "实现登录注册页面"
    output: "src/pages/auth/"
  - name: "qa"
    task: "编写认证模块测试用例"
```

**关键代码实现：**
```typescript
// 后端认证中间件
export const authenticateToken = (req: Request, res: Response, next: NextFunction) => {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  
  if (!token) {
    return res.status(401).json({ error: 'Access denied' });
  }
  
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET!);
    req.user = decoded as UserPayload;
    next();
  } catch (error) {
    return res.status(403).json({ error: 'Invalid token' });
  }
};
```

**验收标准：**
- [ ] 用户能够注册和登录
- [ ] JWT Token 正确生成和验证
- [ ] 未授权访问被正确拒绝

#### 第4-5天：数据可视化模块

**任务目标：** 实现健康数据的统计图表展示

**技术选型：**
- **图表库：** Recharts / ECharts
- **数据处理：** Lodash
- **UI 组件：** Ant Design Charts

**实现示例：**
```tsx
// 健身数据趋势图
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';

export const WorkoutTrendChart = ({ data }) => {
  return (
    <ResponsiveContainer width="100%" height={400}>
      <LineChart data={data}>
        <CartesianGrid strokeDasharray="3 3" />
        <XAxis dataKey="date" />
        <YAxis />
        <Tooltip />
        <Line type="monotone" dataKey="duration" stroke="#8884d8" name="运动时长" />
        <Line type="monotone" dataKey="calories" stroke="#82ca9d" name="消耗卡路里" />
      </LineChart>
    </ResponsiveContainer>
  );
};
```

**验收标准：**
- [ ] 展示运动时长趋势
- [ ] 展示卡路里消耗趋势
- [ ] 支持时间范围筛选

### 阶段二：核心功能开发 (2周)

#### 第1周：设备管理和数据同步

**任务目标：** 实现蓝牙设备管理和数据同步功能

**核心功能：**
1. 设备列表展示
2. 设备绑定/解绑
3. 数据同步状态监控
4. 远程配置管理

#### 第2周：报表和导出功能

**任务目标：** 实现数据报表生成和导出功能

**核心功能：**
1. 日/周/月报表生成
2. PDF/Excel 导出
3. 自定义报表配置
4. 报表定时发送

### 阶段三：测试和部署 (1周)

#### 任务：全面测试和部署

**测试覆盖：**
- 单元测试
- 集成测试
- E2E 测试
- 性能测试

**部署配置：**
```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://backend:3001

  backend:
    build: ./backend
    ports:
      - "3001:3001"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/fitpro
    depends_on:
      - db

  db:
    image: postgres:14
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=fitpro
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass

volumes:
  postgres_data:
```

## 📊 项目评估

### 功能完整性 (40%)
| 功能 | 状态 | 优先级 |
|------|------|--------|
| 用户认证 | 待开发 | 高 |
| 数据可视化 | 待开发 | 高 |
| 设备管理 | 待开发 | 中 |
| 报表导出 | 待开发 | 中 |

### 代码质量 (30%)
- 测试覆盖率 > 80%
- ESLint 无错误
- 文档完整性

### 性能指标 (30%)
- 首屏加载 < 3s
- API 响应 < 500ms
- 支持 100+ 并发用户

## 🎓 学习要点

### 技术要点
1. React 组件化和状态管理
2. JWT 认证和权限控制
3. 数据可视化实现
4. PostgreSQL 数据库设计

### 开发流程
1. 多智能体协作开发
2. 代码审查和合并
3. 自动化测试
4. CI/CD 部署

## 🔗 相关资源

- [React 官方文档](https://react.dev)
- [Ant Design 组件库](https://ant.design)
- [Node.js 开发指南](https://nodejs.org/docs)
- [Prisma ORM 文档](https://prisma.io/docs)

---

**项目状态：** 🟡 待开始  
**预计开始时间：** 2026年1月30日  
**预计完成时间：** 2026年2月19日  
**难度：** ⭐⭐⭐