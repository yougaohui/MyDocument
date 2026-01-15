# 🔄 Phase 2: 混合项目实践 (2-3周)

## 🎯 阶段目标

**核心目标：** 在现有 Android 项目（FitPro2）上实践多智能体开发，创建 Web 管理后台

**具体目标：**
- ✅ 设计并实现 FitPro2 的 Web 管理后台
- ✅ 实现 Android 与 Web 应用的数据同步
- ✅ 掌握多智能体分工协作流程
- ✅ 完成前后端 API 设计和实现

## 📋 项目概述

### 项目名称
**FitPro2 Web Management System**

### 项目描述
为现有的 FitPro2 Android 健身应用添加 Web 管理后台，实现用户数据可视化、设备管理、健康分析等功能。

### 技术架构
```
┌─────────────────────────────────────────────────────┐
│                   Web Frontend                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │
│  │  用户管理   │  │  数据分析   │  │  设备管理   │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                   RESTful API                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │
│  │  用户接口   │  │  数据接口   │  │  设备接口   │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                   Backend Server                    │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  │
│  │  Node.js    │  │  PostgreSQL │  │  Redis      │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  │
└─────────────────────────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
┌─────────────┐   ┌─────────────┐   ┌─────────────┐
│   Android   │   │   Cloud     │   │  External   │
│   App       │   │   Storage   │   │   APIs      │
└─────────────┘   └─────────────┘   └─────────────┘
```

## 📅 周计划

### 第3周：项目设计和基础搭建

#### 任务 2.1: 需求分析和系统设计 (3天)

**目标：** 完成系统需求分析和架构设计

**具体步骤：**

1. **功能需求分析**
   - 用户管理功能
   - 数据可视化需求
   - 设备管理需求
   - 报表统计需求

2. **系统架构设计**
   - 前端架构选择
   - 后端架构设计
   - 数据库设计
   - API 设计

3. **多智能体任务分配**
   ```yaml
   # project-setup.yaml
   name: "fitpro-web-system"
   description: "FitPro2 Web 管理后台系统"
   agents:
     - name: "architect"
       role: "系统架构师"
       task: "整体架构设计和技术选型"
     - name: "frontend-lead"
       role: "前端负责人"
       task: "前端架构设计和组件库选择"
     - name: "backend-lead"
       role: "后端负责人"
       task: "后端架构设计和数据库设计"
     - name: "android-lead"
       role: "移动端负责人"
       task: "Android 集成方案设计"
   ```

**交付物：**
- 需求分析文档
- 系统架构设计图
- 数据库设计文档
- API 接口文档

#### 任务 2.2: 开发环境搭建 (2天)

**目标：** 完成项目开发环境搭建

**具体步骤：**

1. **前端环境搭建**
   ```bash
   # 创建 React 项目
   npm create vite@latest fitpro-web -- --template react-ts
   
   # 安装依赖
   cd fitpro-web
   npm install antd @ant-design/icons react-router-dom axios
   npm install -D tailwindcss postcss autoprefixer
   
   # 初始化 Tailwind CSS
   npx tailwindcss init -p
   ```

2. **后端环境搭建**
   ```bash
   # 创建 Node.js 项目
   mkdir fitpro-api
   cd fitpro-api
   npm init -y
   
   # 安装依赖
   npm install express cors helmet morgan
   npm install -D typescript ts-node @types/express
   npm install prisma @prisma/client
   ```

3. **数据库搭建**
   ```bash
   # 安装 PostgreSQL (使用 Docker)
   docker run --name fitpro-db \
     -e POSTGRES_PASSWORD=your_password \
     -p 5432:5432 \
     -d postgres:14
   
   # 初始化 Prisma
   npx prisma init
   ```

4. **Oh-My-OpenCode 配置**
   ```bash
   # 创建项目配置
   oh-my-opencode init fitpro-web-system
   
   # 配置智能体
   oh-my-opencode config add agent frontend
   oh-my-opencode config add agent backend
   ```

**交付物：**
- 可运行的前端项目
- 可运行的后端项目
- 数据库连接配置
- Oh-My-OpenCode 项目配置

### 第4周：核心功能开发

#### 任务 2.3: 用户管理模块 (3天)

**目标：** 实现用户注册、登录和管理功能

**具体步骤：**

1. **后端用户模块**
   ```typescript
   // src/modules/user/user.controller.ts
   import { Request, Response } from 'express';
   import { UserService } from './user.service';
   
   export class UserController {
     private userService: UserService;
     
     constructor() {
       this.userService = new UserService();
     }
     
     async register(req: Request, res: Response) {
       try {
         const user = await this.userService.createUser(req.body);
         res.status(201).json(user);
       } catch (error) {
         res.status(400).json({ error: error.message });
       }
     }
     
     async login(req: Request, res: Response) {
       try {
         const token = await this.userService.login(req.body);
         res.json({ token });
       } catch (error) {
         res.status(401).json({ error: error.message });
       }
     }
     
     async getProfile(req: Request, res: Response) {
       const user = await this.userService.getUserById(req.params.id);
       res.json(user);
     }
   }
   ```

2. **前端用户界面**
   ```tsx
   // src/pages/Login.tsx
   import { Form, Input, Button, Card } from 'antd';
   import { useNavigate } from 'react-router-dom';
   import { useMutation } from '@tanstack/react-query';
   import axios from 'axios';
   
   export const Login = () => {
     const navigate = useNavigate();
     const loginMutation = useMutation(
       (data: { email: string; password: string }) =>
         axios.post('/api/auth/login', data),
       {
         onSuccess: (response) => {
           localStorage.setItem('token', response.data.token);
           navigate('/dashboard');
         },
       }
     );
   
     const onFinish = (values: any) => {
       loginMutation.mutate(values);
     };
   
     return (
       <div className="login-container">
         <Card title="FitPro2 管理后台">
           <Form onFinish={onFinish}>
             <Form.Item name="email" rules={[{ required: true }]}>
               <Input placeholder="邮箱" />
             </Form.Item>
             <Form.Item name="password" rules={[{ required: true }]}>
               <Input.Password placeholder="密码" />
             </Form.Item>
             <Form.Item>
               <Button type="primary" htmlType="submit" loading={loginMutation.isLoading}>
                 登录
               </Button>
             </Form.Item>
           </Form>
         </Card>
       </div>
     );
   };
   ```

3. **多智能体任务配置**
   ```yaml
   # user-module.yaml
   name: "user-management-module"
   description: "用户管理模块开发"
   parallel: true
   agents:
     - name: "backend-dev"
       task: "实现用户 CRUD API"
       output: "src/modules/user/"
     - name: "frontend-dev"
       task: "实现用户管理界面"
       output: "src/pages/users/"
   ```

**交付物：**
- 用户管理后端 API
- 用户管理前端页面
- 用户认证流程
- 测试用例

#### 任务 2.4: 数据可视化模块 (2天)

**目标：** 实现健康数据的统计和可视化

**具体步骤：**

1. **数据统计后端**
   ```typescript
   // src/modules/analytics/analytics.service.ts
   import { PrismaClient } from '@prisma/client';
   
   export class AnalyticsService {
     private prisma = new PrismaClient();
     
     async getUserActivityStats(userId: string, period: string) {
       const startDate = this.getStartDate(period);
       
       return this.prisma.activity.findMany({
         where: {
           userId,
           createdAt: { gte: startDate },
         },
         include: {
           user: true,
           device: true,
         },
       });
     }
     
     async getHealthSummary(userId: string) {
       const recentActivities = await this.prisma.activity.findMany({
         where: { userId },
         orderBy: { createdAt: 'desc' },
         take: 30,
       });
       
       return {
         totalSteps: recentActivities.reduce((sum, a) => sum + a.steps, 0),
         avgHeartRate: this.calculateAverage(recentActivities.map(a => a.heartRate)),
         sleepHours: this.calculateSleepAverage(recentActivities),
         caloriesBurned: recentActivities.reduce((sum, a) => sum + a.calories, 0),
       };
     }
     
     private getStartDate(period: string): Date {
       const now = new Date();
       switch (period) {
         case 'week': return new Date(now.setDate(now.getDate() - 7));
         case 'month': return new Date(now.setMonth(now.getMonth() - 1));
         case 'year': return new Date(now.setFullYear(now.getFullYear() - 1));
         default: return new Date(0);
       }
     }
   }
   ```

2. **数据可视化前端**
   ```tsx
   // src/pages/Analytics.tsx
   import { useQuery } from '@tanstack/react-query';
   import { LineChart, Card, Statistic } from 'antd';
   import axios from 'axios';
   
   export const Analytics = () => {
     const { data: healthData, isLoading } = useQuery(
       ['healthSummary'],
       () => axios.get('/api/analytics/health-summary').then(res => res.data)
     );
     
     const { data: activityData } = useQuery(
       ['activityStats'],
       () => axios.get('/api/analytics/activity-stats').then(res => res.data)
     );
     
     if (isLoading) return <div>加载中...</div>;
     
     return (
       <div className="analytics-page">
         <div className="stats-grid">
           <Card>
             <Statistic title="总步数" value={healthData?.totalSteps} />
           </Card>
           <Card>
             <Statistic title="平均心率" value={healthData?.avgHeartRate} suffix="bpm" />
           </Card>
           <Card>
             <Statistic title="睡眠时长" value={healthData?.sleepHours} suffix="小时" />
           </Card>
           <Card>
             <Statistic title="消耗卡路里" value={healthData?.caloriesBurned} />
           </Card>
         </div>
         
         <Card title="活动趋势" className="chart-card">
           <LineChart
             data={activityData?.map(a => ({
               date: a.createdAt,
               steps: a.steps,
               calories: a.calories,
             }))}
             xField="date"
             yField="steps"
           />
         </Card>
       </div>
     );
   };
   ```

**交付物：**
- 数据统计后端服务
- 数据可视化前端组件
- 报表导出功能
- 测试用例

#### 任务 2.5: 设备管理模块 (2天)

**目标：** 实现蓝牙设备的连接、状态监控和管理功能

**具体步骤：**

1. **设备管理后端**
   ```typescript
   // src/modules/device/device.controller.ts
   import { Request, Response } from 'express';
   import { DeviceService } from './device.service';
   
   export class DeviceController {
     private deviceService = new DeviceService();
     
     async getDevices(req: Request, res: Response) {
       const devices = await this.deviceService.getUserDevices(req.user.id);
       res.json(devices);
     }
     
     async pairDevice(req: Request, res: Response) {
       const device = await this.deviceService.pairDevice(
         req.user.id,
         req.body.deviceInfo
       );
       res.json(device);
     }
     
     async getDeviceStatus(req: Request, res: Response) {
       const status = await this.deviceService.getDeviceStatus(req.params.deviceId);
       res.json(status);
     }
     
     async updateDevice(req: Request, res: Response) {
       const device = await this.deviceService.updateDevice(
         req.params.deviceId,
         req.body
       );
       res.json(device);
     }
     
     async unpairDevice(req: Request, res: Response) {
       await this.deviceService.unpairDevice(req.params.deviceId);
       res.status(204).send();
     }
   }
   ```

2. **设备管理前端**
   ```tsx
   // src/pages/Devices.tsx
   import { Table, Button, Modal, Tag, Space } from 'antd';
   import { useQuery, useMutation, useQueryClient } from '@tanstack/react-query';
   import axios from 'axios';
   
   export const Devices = () => {
     const queryClient = useQueryClient();
     const { data: devices, isLoading } = useQuery(
       ['devices'],
       () => axios.get('/api/devices').then(res => res.data)
     );
     
     const unpairMutation = useMutation(
       (deviceId: string) => axios.delete(`/api/devices/${deviceId}`),
       {
         onSuccess: () => {
           queryClient.invalidateQueries(['devices']);
         },
       }
     );
     
     const columns = [
       {
         title: '设备名称',
         dataIndex: 'name',
         key: 'name',
       },
       {
         title: '设备类型',
         dataIndex: 'type',
         key: 'type',
         render: (type: string) => (
           <Tag color={type === 'watch' ? 'blue' : 'green'}>
             {type === 'watch' ? '手表' : '手环'}
           </Tag>
         ),
       },
       {
         title: '连接状态',
         dataIndex: 'status',
         key: 'status',
         render: (status: string) => (
           <Tag color={status === 'connected' ? 'success' : 'default'}>
             {status === 'connected' ? '已连接' : '未连接'}
           </Tag>
         ),
       },
       {
         title: '操作',
         key: 'actions',
         render: (_, record: any) => (
           <Space>
             <Button type="link" size="small">查看</Button>
             <Button 
               type="link" 
               danger 
               size="small"
               onClick={() => unpairMutation.mutate(record.id)}
             >
               解除绑定
             </Button>
           </Space>
         ),
       },
     ];
     
     return (
       <div className="devices-page">
         <div className="page-header">
           <h2>设备管理</h2>
           <Button type="primary">添加设备</Button>
         </div>
         <Table 
           columns={columns} 
           dataSource={devices} 
           loading={isLoading}
           rowKey="id"
         />
       </div>
     );
   };
   ```

**交付物：**
- 设备管理后端 API
- 设备管理前端页面
- 设备状态监控
- 测试用例

### 第5周：集成和测试

#### 任务 2.6: Android 集成 (2天)

**目标：** 实现 Android 应用与 Web 后端的数据同步

**具体步骤：**

1. **API 客户端封装**
   ```java
   // com.xfkj.fitpro.utils.ApiClient.java
   public class ApiClient {
       private static final String BASE_URL = "https://api.fitpro2.com";
       private static ApiClient instance;
       private Retrofit retrofit;
       
       private ApiClient() {
           OkHttpClient okHttpClient = new OkHttpClient.Builder()
               .addInterceptor(chain -> {
                   Request original = chain.request();
                   Request.Builder requestBuilder = original.newBuilder()
                       .header("Authorization", "Bearer " + getToken())
                       .header("Content-Type", "application/json");
                   return chain.proceed(requestBuilder.build());
               })
               .build();
           
           retrofit = new Retrofit.Builder()
               .baseUrl(BASE_URL)
               .client(okHttpClient)
               .addConverterFactory(GsonConverterFactory.create())
               .build();
       }
       
       public static synchronized ApiClient getInstance() {
           if (instance == null) {
               instance = new ApiClient();
           }
           return instance;
       }
       
       public UserApi getUserApi() {
           return retrofit.create(UserApi.class);
       }
       
       public DataApi getDataApi() {
           return retrofit.create(DataApi.class);
       }
       
       public DeviceApi getDeviceApi() {
           return retrofit.create(DeviceApi.class);
       }
   }
   ```

2. **数据同步服务**
   ```java
   // com.xfkj.fitpro.services.DataSyncService.java
   public class DataSyncService {
       private static final String TAG = "DataSyncService";
       
       public void syncHealthData(Context context) {
           List<HealthData> localData = getLocalHealthData(context);
           
           ApiClient.getInstance().getDataApi()
               .uploadHealthData(localData)
               .enqueue(new Callback<SyncResult>() {
                   @Override
                   public void onResponse(Call<SyncResult> call, Response<SyncResult> response) {
                       if (response.isSuccessful() && response.body() != null) {
                           markDataAsSynced(context, localData);
                           Log.d(TAG, "数据同步成功");
                       }
                   }
                   
                   @Override
                   public void onFailure(Call<SyncResult> call, Throwable t) {
                       Log.e(TAG, "数据同步失败", t);
                   }
               });
       }
       
       private List<HealthData> getLocalHealthData(Context context) {
           // 从本地数据库获取未同步的数据
       }
       
       private void markDataAsSynced(Context context, List<HealthData> data) {
           // 标记数据为已同步
       }
   }
   ```

3. **多智能体集成任务**
   ```yaml
   # android-integration.yaml
   name: "android-integration"
   description: "Android 应用与 Web 后端集成"
   agents:
     - name: "android-dev"
       task: "实现 API 客户端和数据同步服务"
       context: "现有 FitPro2 Android 项目"
     - name: "backend-dev"
       task: "提供 API 文档和测试支持"
       context: "后端 API 开发"
     - name: "qa"
       task: "测试 Android 与后端的集成"
       context: "集成测试"
   ```

**交付物：**
- Android API 客户端
- 数据同步服务
- API 集成文档
- 测试报告

#### 任务 2.7: 系统测试和优化 (3天)

**目标：** 完成系统测试并进行性能优化

**具体步骤：**

1. **API 测试**
   ```bash
   # 使用 Jest 和 Supertest 进行后端测试
   npm install --save-dev jest @types/jest supertest
   
   # 运行测试
   npm test
   ```

2. **前端测试**
   ```bash
   # 安装测试依赖
   npm install --save-dev @testing-library/react @testing-library/jest-dom
   
   # 运行测试
   npm test
   ```

3. **性能优化**
   - 后端：数据库查询优化、缓存策略
   - 前端：代码分割、懒加载、CDN
   - 网络：请求合并、压缩传输

4. **多智能体测试任务**
   ```yaml
   # system-testing.yaml
   name: "system-testing"
   description: "系统集成测试和性能优化"
   agents:
     - name: "qa-engineer"
       task: "编写和执行测试用例"
     - name: "backend-dev"
       task: "后端性能优化"
     - name: "frontend-dev"
       task: "前端性能优化"
   ```

**交付物：**
- 完整的测试用例
- 测试报告
- 性能优化报告
- 系统部署文档

## 🎯 交付物清单

### 文档交付物
- [ ] 需求分析文档
- [ ] 系统架构设计文档
- [ ] 数据库设计文档
- [ ] API 接口文档
- [ ] 用户操作手册
- [ ] 部署运维文档

### 代码交付物
- [ ] Web 前端项目（React）
- [ ] 后端 API 项目（Node.js）
- [ ] Android 集成代码
- [ ] 数据库迁移脚本
- [ ] 部署配置文件

### 测试交付物
- [ ] 后端测试用例
- [ ] 前端测试用例
- [ ] 集成测试报告
- [ ] 性能测试报告

## 📊 评估标准

### 功能完整性
- ✅ 用户管理功能完整
- ✅ 数据可视化展示正确
- ✅ 设备管理功能正常
- ✅ Android 集成顺畅

### 代码质量
- ✅ 代码规范符合最佳实践
- ✅ 单元测试覆盖率高
- ✅ 性能指标达标
- ✅ 安全漏洞已修复

### 项目管理
- ✅ 进度按计划推进
- ✅ 文档更新及时
- ✅ 团队协作顺畅
- ✅ 问题解决及时

## 🔧 技术要点

### 核心 API 接口
```typescript
// 用户相关
POST   /api/auth/register
POST   /api/auth/login
GET    /api/users/profile
PUT    /api/users/profile

// 数据分析
GET    /api/analytics/health-summary
GET    /api/analytics/activity-stats
GET    /api/analytics/sleep-analysis

// 设备管理
GET    /api/devices
POST   /api/devices/pair
GET    /api/devices/:id/status
DELETE /api/devices/:id
```

### 多智能体协作配置
```yaml
# fitpro-project.yaml
name: "fitpro-web-management"
version: "1.0.0"
agents:
  architect:
    model: "claude-3-5-sonnet"
    responsibilities: ["系统设计", "技术选型"]
  frontend:
    model: "gpt-4"
    responsibilities: ["前端开发", "UI 实现"]
  backend:
    model: "claude-3-5-sonnet"
    responsibilities: ["后端开发", "API 设计"]
  android:
    model: "claude-3-5-sonnet"
    responsibilities: ["Android 集成", "数据同步"]
  qa:
    model: "gpt-4"
    responsibilities: ["测试", "质量保证"]

workflows:
  default:
    parallel: true
    maxAgents: 3
```

---

**阶段状态：** 🟡 准备开始  
**预计开始时间：** 2026年1月30日  
**预计完成时间：** 2026年2月19日  

> 💡 提示：本阶段重点是实践多智能体协作，不要追求完美，先完成再优化。