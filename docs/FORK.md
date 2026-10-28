# 本仓库的远程配置说明

本仓库的内容源自 [xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server)，
当前由自有仓库 `eazlong/xiaozhi_server` 维护。

## 远程

```
origin    git@github.com:eazlong/xiaozhi_server.git              # 自行维护，push 目标
upstream  https://github.com/xinnan-tech/xiaozhi-esp32-server     # 仅用于取用上游代码，push 已禁用
```

`upstream` 的 push 地址被设为 `DISABLED_USE_ORIGIN`，避免误把提交推到上游。

## 本仓库当前状态（重要）

`eazlong/xiaozhi_server` **不是 GitHub fork**，而是一个独立仓库，且历史被重新初始化过：

- 只有一个提交 `first commit`（`1294775`），**上游的提交历史不在本地**；
- 没有任何 tag（上游有 78 个）；
- 因此 `git merge upstream/main` 会因历史无关（unrelated histories）而失败。

若要再次取用上游改动，先确认历史关系，再决定是重新 `git clone` 上游后叠加本地改动，还是
`git merge upstream/main --allow-unrelated-histories`（后者会引入大量冲突，通常不划算）。

## 代码中保留上游地址的地方

下列引用**故意保留上游**，改动会导致功能失效：

| 位置 | 原因 |
| --- | --- |
| `Dockerfile-server` 的 `FROM ghcr.io/xinnan-tech/...:server-base` | 基础镜像由上游 CI 发布，本仓库无 `server-base` 标签 |
| `main/xiaozhi-server/docker-compose*.yml` 的 `image:` | 本仓库的 GHCR 包尚未发布（无 tag/release），拉取会返回 `401 DENIED` |
| `docker-setup.sh` 的镜像名与 `raw.githubusercontent.com` 下载地址 | 同上；脚本需拉取真实存在的镜像与配置模板 |
| README 的 release / star 徽章、star-history 图表 | 本仓库无 release、star 与历史数据，徽章会渲染成 `no releases or repo not found` |
| `issues/791` 等具体 issue 深链 | 这些 issue 在本仓库中不存在，回退到上游才能打开 |

其余指向本仓库文档、LICENSE、contributors 等路径的链接，已全部改为 `eazlong/xiaozhi_server`。

## 若要让本仓库自己发布镜像

1. 在仓库 Settings → Secrets 配置 `TOKEN`（`write:packages` 权限的 PAT，工作流使用该名称）。
2. 在 Settings → Actions 确认 Actions 已启用（当前该仓库的工作流数为 0）。
3. 推送 `v*.*.*` 形式的 tag 触发 `.github/workflows/docker-image.yml`；或手动触发 `workflow_dispatch`。
4. 首个 tag 会先触发 `build-base-image.yml` 生成 `server-base`，镜像发布后再把上表中的镜像坐标改为
   `ghcr.io/eazlong/xiaozhi_server`。

在此之前，部署请继续使用上游镜像。

