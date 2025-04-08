<div align="center">

<svg width="120" height="120" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
  <path d="M60 10L105 35V85L60 110L15 85V35L60 10Z" fill="url(#paint0_linear)" stroke="#2D6CDF" stroke-width="2"/>
  <path d="M60 30L80 40V75L60 85L40 75V40L60 30Z" fill="white" stroke="#2D6CDF" stroke-width="2"/>
  <circle cx="60" cy="57" r="10" fill="#2D6CDF"/>
  <path d="M60 43V57L68 65" stroke="white" stroke-width="3" stroke-linecap="round"/>
  <defs>
    <linearGradient id="paint0_linear" x1="15" y1="60" x2="105" y2="60" gradientUnits="userSpaceOnUse">
      <stop stop-color="#61DAFB"/>
      <stop offset="1" stop-color="#2D6CDF"/>
    </linearGradient>
  </defs>
</svg>

# NaviHive - 现代化的网站导航管理系统

![NaviHive 导航站](https://img.shields.io/badge/NaviHive-导航站-blue)
![React](https://img.shields.io/badge/React-19.0.0-61dafb)
![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178c6)
![Material UI](https://img.shields.io/badge/Material_UI-7.0-0081cb)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Workers-f38020)

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/zqq-nuli/Cloudflare-Navihive)

</div>

NaviHive 是一个精美的网站导航管理系统，帮助你整理和管理你收藏的网站链接。支持分组管理、拖拽排序、暗色模式等功能，让你的网站收藏更有条理、更易访问。

## 🌐 在线演示

体验 NaviHive 的功能：[https://navihive.xingqiong.icu/](https://navihive.xingqiong.icu/)

**演示账号**：linuxdo  
**演示密码**：linuxdo

## ✨ 特性

-   📚 **分组管理** - 将网站按类别整理成分组
-   🔄 **拖拽排序** - 直观地调整分组和网站的排列顺序
-   🔐 **用户认证** - 内置登录系统，保护你的导航数据
-   🌓 **暗色/亮色模式** - 随时切换主题，保护你的眼睛
-   📱 **响应式设计** - 完美适配桌面和移动设备
-   🎨 **自定义配置** - 支持自定义网站标题、名称和 CSS 样式
-   🚀 **高性能** - 基于 Cloudflare Workers 和 D1 数据库构建

## 📸 演示截图

<details>
<summary><b>全局设置</b></summary>
<img src="https://img.zhengmi.org/file/1743801673107_1743801661335.jpg" alt="全局设置" width="100%">
</details>

<details>
<summary><b>网站设置</b></summary>
<img src="https://img.zhengmi.org/file/1743801939121_image.png" alt="网站设置" width="100%">
</details>

<details>
<summary><b>暗色模式</b></summary>
<img src="https://img.zhengmi.org/file/1743801684425_image.png" alt="暗色模式" width="100%">
</details>

<details>
<summary><b>拖拽排序（暗色）</b></summary>
<img src="https://img.zhengmi.org/file/1743801720324_image.png" alt="拖拽排序（暗色）" width="100%">
</details>

## 🛠️ 技术栈

-   **前端**：

    -   React 19
    -   TypeScript
    -   Material UI 7.0
    -   DND Kit (拖拽功能)
    -   Tailwind CSS 4.1
    -   Vite 6

-   **后端**：
    -   Cloudflare Workers
    -   Cloudflare D1 (SQLite)
    -   JWT 认证
    -   Cloudflare Workers API

## 🚀 部署指南

### 一、准备工作

在开始部署之前，您需要：

1. 一个 [Cloudflare 账号](https://dash.cloudflare.com/sign-up)（免费）
2. 一个 GitHub 账号（如果您想 fork 此项目或使用一键部署功能）
3. 基本的网络和浏览器操作知识

### 二、一键部署方法（推荐小白用户）

最简单的部署方式是使用一键部署功能：
1. fork本仓库，修改`wrangler.template.jsonc`为`wrangler.jsonc`
2. 点击上方的"Deploy to Cloudflare Workers"按钮
3. 登录您的 Cloudflare 账号
4. 在部署界面上，您需要配置以下内容：
    - **项目名称**：为您的导航站项目取个名字
    - **D1 数据库**：点击"创建新数据库"，命名为`navigation-db`
    - **环境变量**：
        - `AUTH_ENABLED`：设置为`true`启用登录认证
        - `AUTH_USERNAME`：管理员用户名
        - `AUTH_PASSWORD`：管理员密码
        - `AUTH_SECRET`：JWT 密钥（使用随机字符串）
5. 点击"部署"按钮

部署完成后，您将获得一个类似`https://your-project-name.username.workers.dev`的网址，这就是您的导航站地址。

6. 初始化项目数据库  
   - 登录您的 [Cloudflare 控制台](https://dash.cloudflare.com/)
   - 进入"Workers & Pages"部分
   - 选择您刚刚部署的项目
   - 在左侧菜单中点击"设置" > "数据库"，您将看到已绑定的数据库（名为"navigation-db"）
   - 点击数据库名称以进入数据库管理界面：

   ![数据库管理界面](https://img.zhengmi.org/file/1743843332374_image.png)

   - 在数据库管理界面，点击"控制台"选项卡进入SQL编辑器
   - 在SQL编辑器中，逐个复制并粘贴以下SQL命令：

   ```sql
   -- 创建分组表
   CREATE TABLE IF NOT EXISTS groups (
       id INTEGER PRIMARY KEY AUTOINCREMENT, 
       name TEXT NOT NULL, 
       order_num INTEGER NOT NULL, 
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
       updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   -- 创建站点表
   CREATE TABLE IF NOT EXISTS sites (
       id INTEGER PRIMARY KEY AUTOINCREMENT, 
       group_id INTEGER NOT NULL, 
       name TEXT NOT NULL, 
       url TEXT NOT NULL, 
       icon TEXT, 
       description TEXT, 
       notes TEXT, 
       order_num INTEGER NOT NULL, 
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
       updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP, 
       FOREIGN KEY (group_id) REFERENCES groups(id) ON DELETE CASCADE
   );

   -- 创建配置表
   CREATE TABLE IF NOT EXISTS configs (
       key TEXT PRIMARY KEY,
       value TEXT NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
       updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );

   -- 设置初始化标志
   INSERT INTO configs (key, value) VALUES ('DB_INITIALIZED', 'true');
   ```

   - 点击"运行"按钮执行SQL命令：

   ![SQL编辑器界面](https://img.zhengmi.org/file/1743843528319_image.png)

   - 如果SQL命令执行成功，您将看到"查询成功"的提示信息
   - 至此，数据库初始化完成，您可以访问您的导航站首页并使用配置的管理员账号登录

### 三、手动部署方法（适合开发者）

如果您希望更细致地控制部署过程，可以按照以下步骤手动部署：

#### 1. 克隆仓库

```bash
git clone https://github.com/zqq-nuli/NaviHive.git
cd NaviHive
```

#### 2. 安装依赖

```bash
pnpm install
```

#### 3. 配置 Cloudflare

**安装 Wrangler 工具**

```bash
npm install -g wrangler
```

**登录 Cloudflare**

```bash
wrangler login
```

**创建 D1 数据库**

```bash
wrangler d1 create navigation-db
```

创建后，您会获得一个数据库 ID，记下这个 ID，稍后需要使用。

#### 4. 修改配置文件

编辑`wrangler.jsonc`文件：

```json
{
    "$schema": "node_modules/wrangler/config-schema.json",
    "name": "您的项目名称",
    "main": "worker/index.ts",
    "compatibility_date": "2025-04-05",
    "assets": {
        "not_found_handling": "single-page-application"
    },
    "observability": {
        "enabled": true
    },
    // D1数据库绑定
    "d1_databases": [
        {
            "binding": "DB",
            "database_name": "navigation-db",
            "database_id": "您的数据库ID"  // 替换为您刚创建的数据库ID
        }
    ],
    "vars": {
        "AUTH_ENABLED": "true",  // 是否启用认证
        "AUTH_USERNAME": "admin",  // 管理员用户名
        "AUTH_PASSWORD": "password",  // 管理员密码 (请修改为安全密码)
        "AUTH_SECRET": "your-secret-key"  // JWT密钥 (请使用随机字符串)
    }
}
```

#### 5. 开发模式

```bash
pnpm dev
```

#### 6. 构建项目

```bash
pnpm build
```

#### 7. 部署项目

```bash
pnpm deploy
```

部署完成后，您将获得一个类似`https://您的项目名称.您的用户名.workers.dev`的网址。

### 四、初始化与数据库设置

无论您使用哪种部署方法，部署完成后，需要进行数据库初始化。您有两种方式：

#### 方式一：通过SQL初始化（推荐）

如一键部署方法中的步骤5所述，通过Cloudflare控制台执行SQL命令初始化数据库。

#### 方式二：通过API初始化(弃用)

1. 访问`https://您的网站地址/init`
2. 如果看到"数据库初始化成功"的消息，说明初始化成功

初始化完成后，访问您的导航站首页，使用您配置的管理员用户名和密码登录。

## 📝 使用指南

### 登录系统

首次访问您的导航站时，您需要使用在部署时设置的管理员账号和密码登录。

### 配置您的导航站

登录后，您可以：

1. **添加新的分组**：点击页面上方的"新增分组"按钮
2. **添加网站**：在分组中点击"添加卡片"按钮
3. **自定义设置**：点击"网站设置"按钮，可以修改网站标题、名称和自定义 CSS
4. **拖拽排序**：点击"编辑排序"按钮，可以拖拽调整分组和网站的顺序

### 使用自定义域名（可选）

如果您想使用自己的域名，而不是 Cloudflare Workers 提供的子域名，您可以：

1. 在 Cloudflare 控制面板中，进入"Workers & Pages"
2. 选择您的导航站项目
3. 点击"触发器(Triggers)"选项卡
4. 在"自定义域(Custom Domains)"部分，点击"添加自定义域"
5. 输入您想使用的域名，并按照指示完成 DNS 配置

## 🔧 常见问题解答

**Q: 我忘记了管理员密码，怎么办？**  
A: 您可以通过修改环境变量重置密码。在 Cloudflare 控制面板中，进入您的项目，点击"设置" > "环境变量"，修改`AUTH_PASSWORD`的值。

**Q: 我想关闭登录认证，可以吗？**  
A: 可以。将环境变量`AUTH_ENABLED`设置为`false`即可关闭认证功能。

**Q: 部署后如何更新到最新版本？**  
A: 如果使用的是一键部署，可以再次点击部署按钮；如果是手动部署，拉取最新代码后重新构建并部署。

**Q: 我想备份我的数据，应该怎么做？**  
A: 您可以使用 Wrangler 工具导出 D1 数据库：

```bash
wrangler d1 database export navigation-db
```

**Q: 数据库结构是什么样的？**  
A: NaviHive 使用两个主要表格：

-   `groups`: 存储分组信息
-   `sites`: 存储网站信息
-   `configs`: 存储配置信息

## 🗂️ 项目结构

```
├── worker/               # Cloudflare Workers函数
│   └── index.ts          # Workers入口文件
├── public/               # 静态资源
├── src/                  # 前端源码
│   ├── API/              # API客户端
│   ├── components/       # React组件
│   └── App.tsx           # 主应用组件
├── wrangler.jsonc        # Cloudflare Workers配置
├── vite.config.ts        # Vite配置文件
├── package.json          # 项目依赖
└── README.md             # 项目说明
```

## 🤝 贡献

欢迎贡献代码、报告问题或提出改进建议！

1. Fork 这个仓库
2. 创建你的特性分支 (`git checkout -b feature/amazing-feature`)
3. 提交你的改动 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 提交 Pull Request

## 📄 许可证

此项目采用 MIT License 许可证 - 详情见 [LICENSE](LICENSE) 文件

## 🙏 鸣谢

-   [React](https://reactjs.org/)
-   [Material UI](https://mui.com/)
-   [DND Kit](https://dndkit.com/)
-   [Cloudflare Workers](https://workers.cloudflare.com/)
-   [Vite](https://vitejs.dev/)
-   [Tailwind CSS](https://tailwindcss.com/)
-   [TypeScript](https://www.typescriptlang.org/)
-   [Cloudflare D1](https://developers.cloudflare.com/d1/)
-   [Curosr](https://www.cursor.com)

## 📅 更新日志
### v1.0.1 (2025-04-06)
- 🔄 更新Chrome浏览器标签数据转换工具

### v1.0.0 (2025-04-05)
- 🚀 首次发布
- ✨ 基础导航功能实现
- 📚 分组管理功能
- 🔄 拖拽排序功能
- 🔐 用户认证系统
- 🌓 暗色/亮色模式切换
- 📱 响应式设计适配
---

## ⭐ 支持一下作者

- 给项目点个 Star，分享给您的朋友
- 通过微信赞赏支持我的持续开发
<div align="center">
  <img src="https://img.zhengmi.org/file/1743956440128_4b965550184c06d8164f8077fa42b5d.jpg" alt="微信赞赏码" width="300">
</div>

**NaviHive** - 让网站导航更简单、更美观！
