# MusicFree Adapter — Songloft Plugin

**musicfree-adapter** 是一个 [Songloft](https://songloft.app) 插件，它作为一个运行时适配器，让 [MusicFree](https://github.com/maotoumao/MusicFree) 格式的音源插件能够直接在 Songloft 的 QuickJS 沙箱环境中运行。

## 工作原理

MusicFree 生态拥有大量开箱即用的音源插件（.js 文件），但它们依赖 Node.js / Hermes 运行时。本项目通过以下方式弥合差异：

1. **代码加载** — 从 URL 下载 MusicFree 插件的 JS 文件，持久化到 Songloft 的 data 目录，下次启动时可离线使用。
2. **代码预处理** — 自动将 ESM 格式（`export default`）转为 CommonJS，并将 `let/const` 替换为 `var` 以规避 QuickJS 严格的参数重声明检查。
3. **运行时垫片** — 提供 `crypto-js`、`axios`、`env`、`require` 等常用依赖的纯 JS 实现，确保 MusicFree 插件的 API 调用在 QuickJS 下正常工作。
4. **REST API** — 通过 Songloft 的 HTTP 插件接口暴露搜索、获取播放地址、歌词、歌单导入等功能。
5. **Web UI** — 内置管理界面，支持插件的添加/卸载/启用/停用，以及音乐搜索与播放。

## 功能

- 安装/卸载 MusicFree 音源插件
- 启用/停用已安装的插件
- 聚合搜索（同时搜索所有已启用的插件）
- 获取歌曲播放地址（支持多音质切换）
- 获取歌词
- 导入歌单 URL
- 插件本地缓存，支持离线使用
- Web 管理界面

## API 端点

| 方法 | 路径 | 说明 |
|------|------|------|
| `GET` | `/plugins` | 列出已安装的插件及其能力 |
| `POST` | `/plugins` | 安装插件（body: `{ url }`） |
| `DELETE` | `/plugins` | 卸载插件（body: `{ url }`） |
| `PUT` | `/plugins` | 启用/停用插件（body: `{ url, enabled }`） |
| `GET` | `/search` | 搜索音乐（`?q=keyword&page=1&type=music&platform=`） |
| `POST` | `/source` | 获取播放地址（body: `{ musicItem, quality }`） |
| `GET` | `/lyric` | 获取歌词（`?platform=&id=&title=&artist=`） |
| `GET` | `/playlist/import` | 导入歌单（`?url=`） |

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

## 许可

MIT
