# 🐙 OctopusFrp 官方网站 (OctopusFrp Web)

基于 Vue 3 + Vite + Tailwind CSS 构建的 **OctopusFrp (八爪鱼穿透)** 官方落地页与中继节点招募门户。

## 🌟 页面核心功能与亮点

- **深色科技美学**：沉浸式深海科技风（Dark Oceanic Cyber），配备霓虹青蓝、紫罗兰渐变光晕及玻璃拟态卡片。
- **加入目的与互惠网络理念**：
  - 阐述家宽上行充裕但无固定 IPv4、廉价公网 VPS（3~5M）严重限速的痛点。
  - 宣传“人人为我，我为人人”的带宽众筹理念。
  - 端到端 TLS 传输切片加密，零信任透明安全保障。
  - 节点常驻仅需 `< 15MB` 内存，极低系统占用。
- **动态带宽聚合交互模拟器**：
  - 交互式拖拽/勾选不同中继服务器（腾讯云 5M、阿里云 5M、华为云 10M、社区节点 15M 等）。
  - 实时计算并动态演示总出站吞吐量倍增，直观对比远程桌面 (RDP) 60 FPS 顺畅度与 NAS 大文件下载耗时。
- **一键部署脚本生成器**：
  - 支持 **Linux (Systemd)**、**Docker 容器**、**Windows (PowerShell)** 三大平台。
  - 支持自定义中继节点名称（Node ID）、共享带宽限速、监听端口、认证 Token。
  - 实时联动生成部署单行指令、`octopus-server.toml` 完整配置预览及系统服务管理命令，支持一键复制。
- **活跃中继节点态势看板**：展示国内与海外节点的实时可用率、延迟与 SWRR 权重状态。
- **常见问题解答 (FAQ)**：解答流量防超额、隐私加密安全性、断网自动隔离自愈机制等疑问。

---

## 🛠️ 本地开发与构建

### 安装依赖
```bash
npm install
```

### 启动本地开发服务
```bash
npm run dev -- --host 127.0.0.1 --port 5199
```
访问本地预览：[http://127.0.0.1:5199](http://127.0.0.1:5199)

### 生产环境打包
```bash
npm run build
```
编译产物将输出至 `dist/` 目录，可直接托管至任意静态服务器（如 Nginx、GitHub Pages、Cloudflare Pages 等）。

---

## 📁 目录结构

```
OctopusFrpWeb/
├── index.html
├── package.json
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
└── src/
    ├── main.js
    ├── App.vue
    ├── assets/
    │   └── main.css             # Tailwind 指令 + 科技光效与玻璃拟物样式
    └── components/
        ├── Navbar.vue           # 顶部固定响应式导航栏与 GitHub 快速入口
        ├── HeroSection.vue      # 首屏视觉焦点、项目核心标语与动态核心指标
        ├── PurposeSection.vue   # 为什么加入中转节点（解决痛点、互惠共享、安全保障）
        ├── AggregationDemo.vue  # 动态带宽聚合模拟器（交互式调节与场景对比）
        ├── JoinStepsSection.vue # 极简 3 步加入流程
        ├── ScriptGenerator.vue  # 一键部署脚本与配置文件实时生成器（核心功能）
        ├── NodeShowcase.vue     # 活跃中继节点态势与网络健康看板
        ├── FaqSection.vue       # 常见顾虑与疑问解答折叠面板
        └── FooterSection.vue    # 页脚信息与开源协议
```