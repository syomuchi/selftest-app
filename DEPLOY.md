# 部署指南 — 学会了吗？V3 Cloud

> 跟着做就行，每一步都有截图说明。大约 20 分钟搞定。

---

## 你要做的事（共 4 步）

| 步骤 | 做什么 | 耗时 |
|------|--------|------|
| ① | 注册 Supabase → 建数据库 | 5 分钟 |
| ② | 注册 Vercel → 部署网页 | 5 分钟 |
| ③ | 填入密钥（2 个） | 1 分钟 |
| ④ | 打开你的网址，注册账号，开始用 | 1 分钟 |

---

## 步骤 ①：注册 Supabase + 建数据库

### 1.1 注册
1. 打开 https://supabase.com
2. 点 "Start your project"
3. 用 GitHub 账号注册（没有就注册一个 GitHub，免费的）
4. 授权登录

### 1.2 创建项目
1. 点 "New Project"
2. 填写：
   - **Name**：`selftest`（随便起）
   - **Database Password**：点 "generate" 自动生成，**复制保存好**
   - **Region**：选 `Southeast Asia (Singapore)` 或最近的
3. 点 "Create new project"
4. 等待 1-2 分钟初始化完成

### 1.3 执行数据库脚本
1. 左侧菜单点 **SQL Editor**
2. 点 "New query"
3. 打开项目文件夹里的 `supabase-schema.sql`，**全选复制**
4. 粘贴到 SQL Editor 里
5. 点 "Run"（运行）
6. 看到 "Success" 就完成了

### 1.4 获取密钥
1. 左侧菜单点 **Project Settings**（齿轮图标）
2. 点 **API**
3. 找到以下两个值，**先记在别的地方**：
   - **Project URL**：类似 `https://xxxxx.supabase.co`
   - **Project API Keys** → **anon public**：一长串字母数字

---

## 步骤 ②：注册 Vercel + 部署

### 2.1 注册 Vercel
1. 打开 https://vercel.com
2. 点 "Sign Up"
3. 用 GitHub 账号注册（和 Supabase 用同一个就行）

### 2.2 上传项目
有两种方式，选一种：

**方式 A：通过 GitHub（推荐）**
1. 在 GitHub 创建一个新仓库（New Repository），名字 `selftest-app`
2. 把项目文件夹里的所有文件上传到这个仓库
3. 回到 Vercel，点 "Add New" → "Project"
4. 选择你刚创建的仓库
5. 点 "Deploy"（其他都不用改）
6. 等 1 分钟部署完成

**方式 B：直接拖拽上传**
1. 在 Vercel 首页点 "Add New" → "Project"
2. 找到 "Deploy without Git" 选项
3. 把项目文件夹直接拖进去
4. 等待部署完成

---

## 步骤 ③：填入密钥

部署完成后，你需要在代码里填入 Supabase 的密钥。

### 3.1 编辑 config.js

如果用的是 **GitHub 方式**：
1. 打开你的 GitHub 仓库
2. 找到 `config.js`，点编辑
3. 把你的 Supabase URL 和 anon key 填进去：

```js
const SUPABASE_URL = 'https://xxxxx.supabase.co';  // ← 替换成你的
const SUPABASE_ANON_KEY = 'eyJhbG...你的key...';     // ← 替换成你的
```

4. 保存（Commit changes）
5. Vercel 会自动重新部署（约 30 秒）

如果用的是**拖拽方式**：
1. 在 Vercel 项目页面点 "Files"
2. 找到 `config.js`，编辑
3. 填入密钥，保存

---

## 步骤 ④：开始使用

1. 打开 Vercel 给你的网址（类似 `https://selftest-app.vercel.app`）
2. 第一次打开会看到登录/注册页面
3. 点 "注册"，填邮箱和密码
4. **检查邮箱**，Supabase 会发一封确认邮件，点里面的链接确认
5. 回到网页，登录
6. 数据自动同步到云端 🎉

---

## 常见问题

**Q: 注册后没收到确认邮件？**
A: 检查垃圾邮件。如果确实没有，去 Supabase → Authentication → Users，手动点 "Confirm"。

**Q: 可以关掉邮箱确认吗？**
A: 可以。Supabase → Authentication → Providers → Email → 关掉 "Confirm email"。

**Q: 免费额度够用吗？**
A: 个人用完全够。Supabase 免费版 500MB 数据库 + 5 万月活用户，你一个人用 4 年也用不完。Vercel 免费版每月 100GB 流量，足够了。

**Q: 换电脑怎么用？**
A: 打开你的 Vercel 网址，登录同一个账号，数据自动同步过来。

**Q: 数据安全吗？**
A: 每个用户的数据有行级安全策略（RLS）保护，你只能看到自己的数据，别人看不到。

**Q: 不想用了怎么删数据？**
A: Supabase → Authentication → Users → 删除你的账号，所有关联数据会自动删除。

---

## 文件说明

| 文件 | 作用 |
|------|------|
| `index.html` | 主应用（含所有功能） |
| `config.js` | Supabase 密钥配置（你需要编辑这个） |
| `supabase-schema.sql` | 数据库表结构（粘贴到 Supabase SQL Editor 执行） |
| `DEPLOY.md` | 本文档 |
