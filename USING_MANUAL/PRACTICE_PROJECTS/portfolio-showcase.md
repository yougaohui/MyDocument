# 💼 实践项目三：个人技术作品展示网站

## 🎯 项目概述

### 项目背景
创建一个专业的个人技术作品展示网站，展示你的学习成果、项目经验和技能水平，提升个人技术品牌影响力。

### 项目目标
- 建立个人技术品牌形象
- 展示全栈开发能力
- 分享技术学习和实践经验
- 连接潜在机会和资源

### 技术栈
- **框架：** Next.js 14 + TypeScript
- **样式：** Tailwind CSS + Framer Motion
- **内容：** MDX + Contentlayer
- **部署：** Vercel + GitHub Pages

## 🎨 设计理念

### 设计原则
1. **简洁专业** - 突出内容，减少干扰
2. **响应式设计** - 适配所有设备
3. **性能优先** - 快速加载，流畅体验
4. **可维护性** - 易于更新和维护

### 设计风格
- **配色方案：** 深色主题为主，渐变点缀
- **字体选择：** Inter + JetBrains Mono
- **交互风格：** 平滑动画，细微反馈
- **排版布局：** 留白充足，层次分明

## 🏗️ 网站架构

### 页面结构
```
┌─────────────────────────────────────────────────────┐
│                      Pages                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │    首页     │  │   项目展示   │  │   技术博客   │ │
│  │  (Home)     │  │ (Projects)  │  │  (Blog)     │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   关于我    │  │   技能展示   │  │   联系方式   │ │
│  │   (About)   │  │ (Skills)    │  │  (Contact)  │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                    Components                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   Layout    │  │   SEO       │  │   UI        │ │
│  │   布局组件   │  │   优化组件   │  │   基础组件   │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   Anim      │  │   Data      │  │   Hooks     │ │
│  │   动画组件   │  │   数据组件   │  │   自定义钩子 │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────┐
│                    Content                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │   Projects  │  │   Posts     │  │   Skills    │ │
│  │  项目数据    │  │   博客文章   │  │   技能数据   │ │
│  │  (MDX)      │  │  (MDX)      │  │  (JSON)     │ │
│  └─────────────┘  └─────────────┘  └─────────────┘ │
└─────────────────────────────────────────────────────┘
```

## 🚀 开发计划

### Phase 1: 基础框架 (1周)

#### 第1天：项目初始化

**Oh-My-OpenCode 配置：**
```yaml
# portfolio-init.yaml
name: "portfolio-init"
description: "个人作品网站初始化"
agents:
  - name: "frontend-dev"
    task: "初始化 Next.js 项目并配置 Tailwind"
    output: "next.config.js"
  - name: "content-dev"
    task: "配置 MDX 和 Contentlayer"
    output: "contentlayer.config.ts"
  - name: "design-dev"
    task: "设计系统组件库"
    output: "src/components/ui/"
```

**初始化命令：**
```bash
# 创建 Next.js 项目
npx create-next-app@latest portfolio \
  --typescript \
  --tailwind \
  --app \
  --src-dir \
  --import-alias "@/*"

# 安装依赖
cd portfolio
npm install framer-motion contentlayer clsx tailwind-merge lucide-react
npm install -D @tailwindcss/typography
```

**项目配置：**
```typescript
// next.config.js
/** @type {import('next').NextConfig} */
const nextConfig = {
  experimental: {
    mdxRs: true,
  },
  images: {
    domains: ['avatars.githubusercontent.com', 'github.com'],
  },
};

module.exports = nextConfig;

// tailwind.config.js
module.exports = {
  content: [
    './src/**/*.{js,ts,jsx,tsx,mdx}',
    './content/**/*.{md,mdx}',
  ],
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#f0f9ff',
          100: '#e0f2fe',
          // ... 其他颜色
        },
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        mono: ['JetBrains Mono', 'monospace'],
      },
    },
  },
  plugins: [
    require('@tailwindcss/typography'),
  ],
};
```

#### 第2-3天：布局和导航系统

**核心布局组件：**
```tsx
// src/components/layout/MainLayout.tsx
import { Header } from '@/components/layout/Header';
import { Footer } from '@/components/layout/Footer';

export default function MainLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="min-h-screen bg-gray-950 text-white">
      <Header />
      <main className="container mx-auto px-4 py-8">
        {children}
      </main>
      <Footer />
    </div>
  );
}

// src/components/layout/Header.tsx
import Link from 'next/link';
import { useState } from 'react';
import { Menu, X } from 'lucide-react';

const navItems = [
  { href: '/', label: '首页' },
  { href: '/projects', label: '项目' },
  { href: '/blog', label: '博客' },
  { href: '/about', label: '关于' },
];

export const Header = () => {
  const [isOpen, setIsOpen] = useState(false);
  
  return (
    <header className="sticky top-0 z-50 bg-gray-950/80 backdrop-blur-md">
      <nav className="container mx-auto px-4 py-4">
        <div className="flex items-center justify-between">
          <Link href="/" className="text-xl font-bold bg-gradient-to-r from-blue-400 to-purple-500 bg-clip-text text-transparent">
            ygh.dev
          </Link>
          
          {/* 桌面导航 */}
          <div className="hidden md:flex items-center gap-6">
            {navItems.map((item) => (
              <Link
                key={item.href}
                href={item.href}
                className="text-gray-300 hover:text-white transition-colors"
              >
                {item.label}
              </Link>
            ))}
          </div>
          
          {/* 移动端菜单按钮 */}
          <button
            className="md:hidden"
            onClick={() => setIsOpen(!isOpen)}
          >
            {isOpen ? <X /> : <Menu />}
          </button>
        </div>
        
        {/* 移动端导航 */}
        {isOpen && (
          <div className="md:hidden mt-4 pb-4">
            {navItems.map((item) => (
              <Link
                key={item.href}
                href={item.href}
                className="block py-2 text-gray-300 hover:text-white"
                onClick={() => setIsOpen(false)}
              >
                {item.label}
              </Link>
            ))}
          </div>
        )}
      </nav>
    </header>
  );
};
```

#### 第4-5天：首页和个人介绍

**首页组件：**
```tsx
// src/app/page.tsx
import { Hero } from '@/components/home/Hero';
import { TechStack } from '@/components/home/TechStack';
import { RecentProjects } from '@/components/home/RecentProjects';
import { LatestPosts } from '@/components/home/LatestPosts';

export default function HomePage() {
  return (
    <div className="space-y-20">
      <Hero />
      <TechStack />
      <RecentProjects />
      <LatestPosts />
    </div>
  );
}

// src/components/home/Hero.tsx
import { motion } from 'framer-motion';
import Link from 'next/link';

export const Hero = () => {
  return (
    <section className="min-h-[80vh] flex items-center justify-center">
      <div className="text-center">
        <motion.div
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5 }}
        >
          <h1 className="text-5xl md:text-7xl font-bold mb-6">
            <span className="bg-gradient-to-r from-blue-400 via-purple-500 to-pink-500 bg-clip-text text-transparent">
              全栈开发者
            </span>
          </h1>
          <p className="text-xl text-gray-400 mb-8 max-w-2xl mx-auto">
            专注于 Android 开发，正在向全栈发展。热爱开源，喜欢通过 Oh-My-OpenCode 探索多智能体协作开发。
          </p>
          
          <div className="flex justify-center gap-4">
            <Link
              href="/projects"
              className="px-8 py-3 bg-gradient-to-r from-blue-500 to-purple-500 rounded-full font-medium hover:opacity-90 transition-opacity"
            >
              查看项目
            </Link>
            <Link
              href="/about"
              className="px-8 py-3 border border-gray-600 rounded-full font-medium hover:bg-gray-800 transition-colors"
            >
              了解更多
            </Link>
          </div>
        </motion.div>
      </div>
    </section>
  );
};
```

### Phase 2: 内容展示 (1周)

#### 第6-7天：项目展示页面

**项目数据管理：**
```typescript
// content/projects/fitpro-web.mdx
---
title: "FitPro2 Web 管理后台"
description: "为 FitPro2 Android 应用添加的 Web 管理后台"
tech: ["React", "Node.js", "PostgreSQL"]
github: "https://github.com/ygh/fitpro-web"
demo: "https://fitpro-web.example.com"
image: "/images/projects/fitpro-web.png"
featured: true
---

# 项目概述

这是一个为 FitPro2 Android 健身应用开发的 Web 管理后台...

## 主要功能

- 用户数据可视化
- 设备管理
- 健康数据分析
- 报表生成

## 技术亮点

- 使用 React + TypeScript 开发
- Node.js + Express 后端
- PostgreSQL 数据库
- Oh-My-OpenCode 多智能体协作开发
```

**项目卡片组件：**
```tsx
// src/components/projects/ProjectCard.tsx
import Link from 'next/link';
import { Github, ExternalLink } from 'lucide-react';

interface ProjectCardProps {
  project: {
    title: string;
    description: string;
    tech: string[];
    github?: string;
    demo?: string;
    image?: string;
  };
}

export const ProjectCard = ({ project }: ProjectCardProps) => {
  return (
    <div className="group bg-gray-900 rounded-xl overflow-hidden border border-gray-800 hover:border-gray-700 transition-all">
      {/* 项目图片 */}
      <div className="aspect-video bg-gray-800 relative overflow-hidden">
        {project.image ? (
          <img
            src={project.image}
            alt={project.title}
            className="object-cover w-full h-full group-hover:scale-105 transition-transform"
          />
        ) : (
          <div className="flex items-center justify-center h-full">
            <span className="text-gray-600">暂无图片</span>
          </div>
        )}
      </div>
      
      {/* 项目信息 */}
      <div className="p-6">
        <h3 className="text-xl font-bold mb-2 group-hover:text-blue-400 transition-colors">
          {project.title}
        </h3>
        <p className="text-gray-400 mb-4 line-clamp-2">
          {project.description}
        </p>
        
        {/* 技术标签 */}
        <div className="flex flex-wrap gap-2 mb-4">
          {project.tech.map((tech) => (
            <span
              key={tech}
              className="px-3 py-1 text-sm bg-gray-800 text-gray-300 rounded-full"
            >
              {tech}
            </span>
          ))}
        </div>
        
        {/* 链接 */}
        <div className="flex gap-4">
          {project.github && (
            <Link
              href={project.github}
              target="_blank"
              className="flex items-center gap-2 text-gray-400 hover:text-white transition-colors"
            >
              <Github size={20} />
              <span>代码</span>
            </Link>
          )}
          {project.demo && (
            <Link
              href={project.demo}
              target="_blank"
              className="flex items-center gap-2 text-gray-400 hover:text-white transition-colors"
            >
              <ExternalLink size={20} />
              <span>演示</span>
            </Link>
          )}
        </div>
      </div>
    </div>
  );
};
```

#### 第8-9天：技术博客系统

**博客配置：**
```typescript
// contentlayer.config.ts
import { defineDocumentType, makeSource } from 'contentlayer/source-files';

export const Post = defineDocumentType(() => ({
  name: 'Post',
  filePathPattern: 'posts/**/*.mdx',
  fields: {
    title: { type: 'string', required: true },
    description: { type: 'string', required: true },
    date: { type: 'string', required: true },
    tags: { type: 'list', of: { type: 'string' } },
    published: { type: 'boolean', default: true },
  },
  computedFields: {
    slug: { type: 'string', resolve: (doc) => doc._raw.sourceFileName.replace(/\.mdx$/, '') },
    readingTime: { type: 'json', resolve: (doc) => calculateReadingTime(doc.body.raw) },
  },
}));

export default makeSource({ contentDirPath: 'content', documentTypes: [Post] });
```

**博客列表页面：**
```tsx
// src/app/blog/page.tsx
import Link from 'next/link';
import { format } from 'date-fns';
import { getAllPosts } from '@/lib/contentlayer';

export default function BlogPage() {
  const posts = getAllPosts().filter(post => post.published);
  
  return (
    <div className="max-w-4xl mx-auto">
      <h1 className="text-4xl font-bold mb-8">技术博客</h1>
      
      <div className="space-y-6">
        {posts.map((post) => (
          <article
            key={post.slug}
            className="p-6 bg-gray-900 rounded-xl border border-gray-800 hover:border-gray-700 transition-all"
          >
            <Link href={`/blog/${post.slug}`}>
              <h2 className="text-2xl font-bold mb-2 hover:text-blue-400 transition-colors">
                {post.title}
              </h2>
            </Link>
            
            <p className="text-gray-400 mb-4">{post.description}</p>
            
            <div className="flex items-center gap-4 text-sm text-gray-500">
              <time>{format(new Date(post.date), 'yyyy年MM月dd日')}</time>
              <span>·</span>
              <span>{post.readingTime.text}</span>
              <span>·</span>
              <div className="flex gap-2">
                {post.tags.map((tag) => (
                  <span key={tag} className="text-blue-400">#{tag}</span>
                ))}
              </div>
            </div>
          </article>
        ))}
      </div>
    </div>
  );
}
```

### Phase 3: 完善和优化 (1周)

#### 第10天：技能展示页面

**技能可视化：**
```tsx
// src/components/skills/SkillsChart.tsx
interface Skill {
  name: string;
  level: number; // 0-100
  category: string;
}

const skills: Skill[] = [
  { name: 'Android', level: 90, category: '移动端' },
  { name: 'React', level: 80, category: '前端' },
  { name: 'Node.js', level: 75, category: '后端' },
  { name: 'TypeScript', level: 85, category: '语言' },
  // ...
];

export const SkillsChart = () => {
  const categories = [...new Set(skills.map(s => s.category))];
  
  return (
    <div className="space-y-8">
      {categories.map((category) => (
        <div key={category}>
          <h3 className="text-xl font-bold mb-4">{category}</h3>
          <div className="space-y-3">
            {skills.filter(s => s.category === category).map((skill) => (
              <div key={skill.name}>
                <div className="flex justify-between mb-1">
                  <span>{skill.name}</span>
                  <span className="text-gray-400">{skill.level}%</span>
                </div>
                <div className="h-2 bg-gray-800 rounded-full overflow-hidden">
                  <div
                    className="h-full bg-gradient-to-r from-blue-500 to-purple-500 rounded-full"
                    style={{ width: `${skill.level}%` }}
                  />
                </div>
              </div>
            ))}
          </div>
        </div>
      ))}
    </div>
  );
};
```

#### 第11-12天：性能优化和 SEO

**优化配置：**
```typescript
// src/components/seo/SEO.tsx
interface SEOProps {
  title: string;
  description: string;
  image?: string;
  url?: string;
}

export const SEO = ({ title, description, image, url }: SEOProps) => {
  return (
    <>
      <title>{title}</title>
      <meta name="description" content={description} />
      
      {/* Open Graph */}
      <meta property="og:title" content={title} />
      <meta property="og:description" content={description} />
      {image && <meta property="og:image" content={image} />}
      {url && <meta property="og:url" content={url} />}
      
      {/* Twitter */}
      <meta name="twitter:card" content="summary_large_image" />
      <meta name="twitter:title" content={title} />
      <meta name="twitter:description" content={description} />
      {image && <meta name="twitter:image" content={image} />}
    </>
  );
};

// next.config.js 优化
const nextConfig = {
  // 压缩
  compress: true,
  
  // 图片优化
  images: {
    formats: ['image/avif', 'image/webp'],
  },
  
  // 静态优化
  swcMinify: true,
  
  // 头部配置
  async headers() {
    return [
      {
        source: '/:path*',
        headers: [
          {
            key: 'X-DNS-Prefetch-Control',
            value: 'on',
          },
        ],
      },
    ];
  },
};
```

#### 第13-14天：部署和发布

**Vercel 部署配置：**
```yaml
# vercel.json
{
  "buildCommand": "pnpm build",
  "outputDirectory": ".next",
  "framework": "nextjs",
  "env": {
    "NEXT_PUBLIC_SITE_URL": "https://ygh.dev"
  },
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        }
      ]
    }
  ]
}
```

**部署命令：**
```bash
# 安装 Vercel CLI
npm i -g vercel

# 部署
vercel

# 生产环境部署
vercel --prod
```

## 📊 网站内容规划

### 项目展示 (6-8个)
1. FitPro2 Web 管理后台 - 全栈项目
2. 智能健身社交平台 - 进阶全栈
3. Android 健身应用 - 移动端项目
4. 开源工具库 - 工具类项目
5. 个人博客系统 - 内容平台
6. Oh-My-OpenCode 贡献 - 开源贡献

### 技术博客 (10+ 篇)
1. Oh-My-OpenCode 多智能体开发实践
2. 从 Android 到全栈的转型之路
3. Next.js 14 新特性探索
4. React 性能优化指南
5. Node.js 微服务架构设计
6. TypeScript 最佳实践
7. 多智能体协作开发工作流
8. 开源贡献入门指南
9. CI/CD 自动化部署实践
10. 个人技术品牌建设心得

### 技能展示
- **移动端：** Android, Kotlin, Java, Jetpack Compose
- **前端：** React, Next.js, TypeScript, Tailwind CSS
- **后端：** Node.js, NestJS, PostgreSQL, Redis
- **工具：** Git, Docker, Oh-My-OpenCode

## 🎯 项目评估

### 网站质量 (40%)
| 指标 | 目标值 | 当前值 |
|------|--------|--------|
| Lighthouse 性能 | > 90 | - |
| Lighthouse 可访问性 | > 90 | - |
| Lighthouse 最佳实践 | > 90 | - |
| Lighthouse SEO | > 90 | - |

### 内容质量 (35%)
| 指标 | 目标值 | 当前值 |
|------|--------|--------|
| 项目数量 | > 5 | - |
| 博客文章 | > 10 | - |
| 内容更新频率 | 每月 | - |

### 用户体验 (25%)
| 指标 | 目标值 | 当前值 |
|------|--------|--------|
| 首屏加载时间 | < 2s | - |
| 交互响应时间 | < 100ms | - |
| 移动端适配 | 完美 | - |

## 🎓 学习要点

### 技术要点
1. **Next.js 全栈开发**
   - App Router 架构
   - Server Components
   - MDX 内容管理

2. **现代 UI 开发**
   - Tailwind CSS
   - Framer Motion
   - 响应式设计

3. **性能优化**
   - 图片优化
   - 代码分割
   - SEO 优化

### 个人品牌
1. **内容创作**
   - 技术写作
   - 项目展示
   - 经验分享

2. **在线形象**
   - GitHub 活跃度
   - 开源贡献
   - 社区参与

## 🔗 相关资源

- [Next.js 文档](https://nextjs.org/docs)
- [Tailwind CSS 文档](https://tailwindcss.com/docs)
- [Framer Motion 文档](https://www.framer.com/motion/)
- [Contentlayer 文档](https://contentlayer.dev/docs)
- [Vercel 部署文档](https://vercel.com/docs)

---

**项目状态：** 🟡 待开始  
**预计开始时间：** 2026年4月10日  
**预计完成时间：** 2026年4月24日  
**难度：** ⭐⭐