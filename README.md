# 微信小程序直播插件 (Live Streaming Plugin)

这是一个用于微信小程序的直播插件，专为在线教育和直播场景设计。它封装了直播观看、互动聊天、课件下载等核心功能，方便第三方小程序快速接入直播能力。

## ✨ 主要功能

该插件提供了一套完整的直播间解决方案，包含以下核心组件：

*   **直播播放 (Live Player)**: 支持实时视频流播放，适配多种直播协议。
*   **互动聊天 (Live Chat)**: 观众与讲师/助教的实时互动，支持发送和接收消息。
*   **课件资料 (Live File)**: 展示直播相关的附件与课件，支持用户查看或下载。
*   **直播详情 (Live Desc)**: 展示当前直播课程的详细信息。
*   **多标签页 (Live Tabs)**: 便捷切换聊天、简介、课件等不同视图。
*   **角色权限**: 支持不同身份登录（学生、助教、讲师），适配不同的权限逻辑。
*   **回放支持**: 支持通过 `planId` 观看课程回放。

## 🛠 技术栈

*   **核心框架**: 微信小程序原生开发 (Native WeChat Mini Program)
    *   WXML (结构)
    *   WXSS (样式)
    *   JavaScript (逻辑, ES6+)
    *   JSON (配置)
*   **插件架构**: 微信小程序插件规范 (Plugin Protocol)
*   **代码规范**:
    *   ESLint (代码质量检查)
    *   Prettier (代码格式化)

## 📂 项目结构

```
.
├── plugin/             # 插件核心源码
│   ├── components/     # 插件暴露的组件 (播放器、聊天、文件等)
│   ├── service/        # 接口请求层 (API 交互)
│   ├── utils/          # 工具函数
│   └── plugin.json     # 插件配置文件
├── miniprogram/        # 宿主小程序 (用于开发调试插件)
├── doc/                # 说明文档
├── project.config.json # 项目配置文件
└── .eslintrc.js        # Lint 配置
```

## 🚀 快速接入

### 1. 引入插件

在宿主小程序的 `app.json` 中声明插件引入。

### 2. 初始化配置

在使用组件前（通常在页面 `onLoad` 或应用启动时），需要设置 API 地址和用户 Token：

```javascript
const plugin = requirePlugin('live-plugin')

// 设置 API 域名
plugin.setApiHost('YOUR_API_HOST') 
// 设置用户 Token
plugin.setAccountToken('YOUR_TOKEN')
```

### 3. 组件使用

在页面的 WXML 中直接使用 `<live-plugin>` 组件：

```html
<live-plugin
  classId="{{classId}}"       <!-- 教室 ID -->
  liveRoomId="{{liveRoomId}}" <!-- 直播间 ID -->
  identity="{{identity}}"     <!-- 身份: 1(学生), 2(助教), 3(讲师) -->
  account="{{account}}"       <!-- 用户账号 -->
  token="{{token}}"           <!-- 用户 Token -->
  planId="{{planId}}"         <!-- (可选) 回放计划 ID -->
/>
```

## 📦 开发与构建

本项目依赖微信开发者工具进行构建和调试。

*   **Lint**: 项目根目录包含 `.eslintrc.js`，遵循标准 JavaScript 规范及微信小程序全局变量规则。
*   **Format**: 项目包含 `.prettierrc`，统一代码风格（单引号、无分号、2空格缩进）。

## 📄 许可证

查看 [LICENSE](./LICENSE) 文件了解更多详情。
