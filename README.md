# MFAdapter — Songloft Plugin

**MFAdapter** 是一个 [Songloft](https://songloft.app) 插件，它作为一个运行时适配器，直接在 Songloft 的 QuickJS 沙箱环境中运行。

## 开发

```bash
# 安装依赖
npm install

# 启动开发服务器（热更新）
npm run dev

# 构建
npm run build
```

## 技术栈

- **TypeScript** — 核心逻辑
- **@songloft/plugin-sdk** — Songloft 插件 SDK
- **QuickJS** — 沙箱运行时环境
- **原生 JS** — Web 管理界面（无框架依赖）

## 免责声明

本项目仅供个人学习与技术研究，禁止商用。音源脚本、歌曲、歌词、封面和平台数据的版权归其各自权利人所有。用户须自行确认使用行为符合当地法律、平台条款和版权要求，并自行清除使用过程中产生的版权数据。项目维护者不提供、不托管、不推荐任何第三方音源脚本，也不对第三方脚本或数据的可用性、安全性、合法性负责。

## 许可

MIT

License
Apache-2.0
