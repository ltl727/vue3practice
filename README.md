任务管理系统
一个基于 Vue 3 + Element Plus 的轻量级任务管理演示应用，实现了任务的增删改查、搜索过滤、本地数据持久化等核心功能。项目结构清晰，代码遵循 ESLint 规范，可作为 Vue 3 组合式 API 的入门实践参考。


🚀 在线演示
如果你将项目部署到了 Gitee Pages 或其他静态托管平台，可以在这里放置访问链接。

📦 技术栈
Vue 3 - 使用组合式 API (setup 语法)

Element Plus - 桌面端 UI 组件库

Vue CLI - 项目脚手架

localStorage - 浏览器本地存储，实现数据持久化

✨ 功能特性
✅ 任务列表展示：以表格形式展示所有任务，包含 ID、任务名称、内容、分类

✅ 添加任务：填写任务名称、内容并选择分类，支持标题唯一性校验及表单非空校验

✅ 编辑任务：点击“编辑”按钮回填表单，修改后提交更新；编辑时可保留原标题，避免误判重复

✅ 删除任务：一键删除指定任务

✅ 搜索过滤：输入关键词实时（或点击搜索按钮）按任务名称/内容模糊过滤

✅ 数据持久化：首次加载从 localStorage 读取数据，无数据时写入默认任务列表；刷新页面数据不丢失

🛠 安装与运行
环境要求
Node.js (推荐 v16 或更高)

npm / yarn / pnpm

步骤
bash
# 1. 克隆仓库
git clone https://gitee.com/flyfacat/vue-front-end-practice-works

# 2. 进入项目目录
cd task-manager

# 3. 安装依赖
npm install

# 4. 启动开发服务器
npm run serve
启动后，在浏览器中访问 http://localhost:8080 即可看到应用。

生产构建
bash
npm run build
构建产物位于 dist/ 目录，可部署至任何静态文件服务器。

📁 项目结构
text
task-manager/
├── public/                  # 静态资源
│   └── index.html
├── src/
│   ├── assets/             # 全局静态资源（如图片）
│   ├── components/
│   │   └── works.vue       # 主要任务管理组件（表格、表单、搜索）
│   ├── App.vue             # 根组件
│   ├── main.js             # 入口文件，注册 Element Plus
│   └── ...
├── .gitignore
├── babel.config.js
├── jsconfig.json           # IDE 配置（可选）
├── package.json
├── README.md
└── vue.config.js           # Vue CLI 配置文件（可选）
🔧 核心实现要点
响应式数据：使用 ref 定义任务列表、表单字段、搜索关键词等。

计算属性：search 根据关键词动态过滤任务列表。

本地存储：initdata 函数在组件初始化时执行，从 localStorage 读取/写入默认数据；如需每次修改都自动持久化，可自行添加 watch 监听 works。

唯一性校验：添加/编辑时通过 ifexist 函数检查任务标题是否已存在（编辑时排除自身）。

编辑状态：利用 titlebefore 记录编辑前的标题，用于定位任务及重复校验。

📝 待改进/扩展方向（供参考）
改用 <script setup> 语法，使代码更简洁

拆分表格、表单、搜索栏为独立组件

添加 watch 深度监听 works，自动同步至 localStorage

使用 Pinia 管理全局状态

增加任务分类筛选、分页功能

添加单元测试

🤝 贡献
本项目为前端练习作品，欢迎提出 issues 或 pr 进行交流。
