# 📚 五谷丰登

私人阅读记录 · 云端同步

一个为 BL 小说及其他书目打造的轻量级阅读记录工具，支持多用户、公共书架、三维评分、标签管理等功能。

---

## ✨ 功能

### 我的书架
- 添加、编辑、删除读书记录
- 支持书目类型：BL小说 🌙、文学小说 📖、非虚构书籍 📝、广播剧 🎧
- **三维评分**：文笔 / 情节 / 人设（0~5星，支持半星），自动计算综合评分（0~10）
- 标签系统：内置标签 + 自定义标签，按用户存储
- 字段：书名、类型、阅读日期、作者、主角、标签、评分、锐评、原文介绍截图、故事梗概、读后感
- 草稿自动保存（localStorage）
- 搜索：书名 / 标签 / 笔记 / 作者 / 主角
- 日历视图：按日期或月份筛选
- 统计面板：本月记录数、累计书写字数、按类型分布
- 分页显示（每页10条）
- 👁 图标标记已公开书目

### 公共书架
- 登录后可见，展示所有用户公开的书目
- 按书名合并，每位用户评分单独一行（书名、作者、评分、昵称、标签、日期）
- 支持搜索、类型筛选、分页
- 手动刷新

### 账户
- 邮箱 + 密码注册 / 登录（注册时设置昵称）
- 数据完全隔离，他人无法访问私人记录
- 公开书目仅展示：书名、作者、评分、标签

---

## 🛠 技术栈

| 层级 | 技术 |
|------|------|
| 前端 | 纯静态 HTML + Vanilla JS |
| 数据库 | [Supabase](https://supabase.com)（PostgreSQL + RLS） |
| 托管 | GitHub Pages |
| 字体 | Noto Sans SC 300（fonts.googleapis.cn） |

---

## 🗄 数据库结构

### `spirit_records`
| 字段 | 类型 | 说明 |
|------|------|------|
| id | uuid | 主键 |
| user_id | uuid | 关联用户 |
| name | text | 书名 |
| type | text | 类型 |
| rating | numeric | 综合评分 |
| rating_writing | numeric | 文笔评分 |
| rating_plot | numeric | 情节评分 |
| rating_character | numeric | 人设评分 |
| tags | text[] | 标签 |
| author | text | 作者 |
| main_characters | text | 主角 |
| review_date | date | 阅读日期 |
| notes | text | 读后感 |
| story_summary | text | 故事梗概 |
| personal_review | text | 锐评 |
| cover_url | text | 封面图 URL |
| intro | text | 原文介绍截图 URL |
| is_public | boolean | 是否公开到公共书架 |
| created_at | timestamptz | 创建时间 |

### `profiles`
| 字段 | 类型 | 说明 |
|------|------|------|
| id | uuid | 关联 auth.users |
| nickname | text | 昵称 |
| created_at | timestamptz | 创建时间 |

---

## 🔒 安全

- 所有表启用 RLS（行级安全策略）
- 用户只能读写自己的记录
- 公开记录对所有已登录用户可见，但仅展示有限字段
- anon key 写在前端（静态网站限制），RLS 保障数据安全

---

## 📱 PWA 支持

支持添加到手机主屏幕作为 App 使用：

- **iOS（Safari）**：底部分享按钮 → 添加到主屏幕
- **Android（Chrome）**：浏览器提示安装 / 菜单 → 添加到主屏幕

---

## 📁 文件结构

```
├── index.html       # 主应用（我的书架）
├── public.html      # 公共书架
├── config.js        # Supabase 配置
├── manifest.json    # PWA 配置
├── sw.js            # Service Worker
├── icon-192.png     # PWA 图标
├── icon-512.png     # PWA 图标
└── README.md
```

---

## 🚀 部署

1. Fork 或 clone 本仓库
2. 修改 `config.js` 填入自己的 Supabase URL 和 anon key
3. 在 Supabase 创建对应表并配置 RLS
4. 开启 GitHub Pages（Branch: main, / root）

---

*私人项目，仅供学习交流*
