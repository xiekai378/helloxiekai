# 你好谢凯 - Vercel + Supabase 留言板

一个使用 Vercel 和 Supabase 构建的简单留言板应用。

## 🚀 部署步骤

### 1. 设置 Supabase

1. 访问 [supabase.com](https://supabase.com) 并登录
2. 创建新项目
3. 在 SQL Editor 中运行以下 SQL 创建表：

```sql
-- 创建留言表
CREATE TABLE messages (
  id BIGSERIAL PRIMARY KEY,
  name TEXT NOT NULL,
  message TEXT NOT NULL,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 启用行级安全策略
ALTER TABLE messages ENABLE ROW LEVEL SECURITY;

-- 允许所有人读取
CREATE POLICY "允许所有人读取留言" ON messages
  FOR SELECT
  USING (true);

-- 允许所有人插入
CREATE POLICY "允许所有人创建留言" ON messages
  FOR INSERT
  WITH CHECK (true);
```

4. 获取项目的 URL 和 anon key：
   - 进入项目设置 (Settings)
   - 点击 API
   - 复制 `Project URL` 和 `anon public key`

### 2. 配置项目

在 `index.html` 中找到这两行（第 118-119 行）：

```javascript
const SUPABASE_URL = 'YOUR_SUPABASE_URL';
const SUPABASE_ANON_KEY = 'YOUR_SUPABASE_ANON_KEY';
```

替换为你的实际 Supabase 凭证。

### 3. 部署到 Vercel

#### 方法一：使用 Vercel CLI（推荐）

```bash
# 安装 Vercel CLI
npm install -g vercel

# 登录
vercel login

# 部署
vercel
```

#### 方法二：通过 GitHub 部署

1. 将代码推送到 GitHub
2. 访问 [vercel.com](https://vercel.com)
3. 点击 "Import Project"
4. 选择你的 GitHub 仓库
5. 点击 "Deploy"

#### 方法三：直接拖拽部署

1. 访问 [vercel.com](https://vercel.com)
2. 将整个项目文件夹拖拽到 Vercel 网站
3. 点击 "Deploy"

## 📝 功能特性

- ✅ 显示欢迎信息"你好谢凯"
- ✅ 留言板功能
- ✅ 实时数据存储（Supabase）
- ✅ 响应式设计
- ✅ 优雅的 UI 界面

## 🛠️ 技术栈

- **前端**: HTML, CSS, JavaScript
- **数据库**: Supabase (PostgreSQL)
- **部署**: Vercel
- **CDN**: Supabase JS SDK (CDN)

## 📂 项目结构

```
.
├── index.html          # 主页面
├── package.json        # 项目配置
├── vercel.json         # Vercel 部署配置
├── .env.example        # 环境变量示例
└── README.md           # 说明文档
```

## 🔧 本地开发

```bash
# 安装依赖
npm install

# 启动本地服务器
npm run dev
```

然后在浏览器中访问 `http://localhost:3000`

## ⚠️ 注意事项

- 请不要将 Supabase 凭证提交到公共仓库
- 生产环境建议使用环境变量管理敏感信息
- 可以在 Vercel 项目设置中添加环境变量

## 📄 许可证

MIT
