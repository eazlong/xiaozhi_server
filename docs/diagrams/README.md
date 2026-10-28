# 架构图（Archify 生成）

本目录存放项目架构图，均由 [Archify](https://github.com/tt-a1i/archify) 从 JSON 声明生成，无外部依赖。

## 图清单

| 文件 | 类型 | 说明 |
| --- | --- | --- |
| [xiaozhi-architecture.html](./xiaozhi-architecture.html) | 系统架构 | 端侧设备 → Python 语音服务 → 智控台管理面，含 provider 与外部云依赖 |
| [xiaozhi-voice-sequence.html](./xiaozhi-voice-sequence.html) | 时序 | 一次语音对话从 WS 握手、上行音频、识别推理到流式回推与打断 |
| [xiaozhi-deployment.html](./xiaozhi-deployment.html) | 部署拓扑 | 全模块 docker compose 四容器的端口、卷与启动顺序 |

对应可编辑的声明文件：`*.architecture.json` / `*.sequence.json`。

## 打开与导出

直接用浏览器打开任一 `.html`：

- 右上角 `Dark / Light` 切换主题（偏好写入 `localStorage`，首次跟随系统 `prefers-color-scheme`）
- 右上角 `Export` 菜单：复制 PNG 到剪贴板；下载 PNG / JPEG / WebP（最高 4× 分辨率）；下载双主题 SVG（跟随宿主 `prefers-color-scheme`，适合嵌进 GitHub README）
- 快捷键：`T` 切换主题，`E` 打开导出菜单

## 修改与重新生成

```bash
# 编辑 JSON 后重新渲染（把 <type> 换成 architecture 或 sequence）
node ~/.agents/skills/archify/bin/archify.mjs render architecture \
  docs/diagrams/xiaozhi-architecture.architecture.json \
  docs/diagrams/xiaozhi-architecture.html

# 只校验布局，不生成文件
node ~/.agents/skills/archify/bin/archify.mjs validate architecture \
  docs/diagrams/xiaozhi-architecture.architecture.json

# 校验已生成的 HTML（斜线箭头、非有限值、图例遮挡）
node ~/.agents/skills/archify/bin/archify.mjs check docs/diagrams/xiaozhi-architecture.html
```

校验器会拦截组件重叠、标签压住组件、箭头过短、连线斜穿、图例被箭头穿过等问题，失败时按提示直接改 JSON 的 `pos` / `labelAt` / `labelDy`，不要手改 HTML。

## 配色约定

三张图共用一套语义色，含义与代码对应：

| 类型 | 含义 | 本项目对应 |
| --- | --- | --- |
| Frontend | 客户端界面 | manager-web、manager-mobile、Nginx |
| Backend | 自研服务 | xiaozhi-server、manager-api、各 provider |
| Database | 存储 | MySQL、Redis |
| Cloud | 托管资源 / 挂载卷 | 云 ASR/LLM/TTS、data/models 卷 |
| Message bus | 异步 / 工具通道 | 统一工具层 |
| External | 项目外部 | ESP32 设备、MCP 接入点、浏览器 |

箭头语义：实线 = 主链路，虚线 = 异步或可选，玫红虚线 = 鉴权 / 配置下发。
