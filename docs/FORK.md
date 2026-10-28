# 本仓库的远程配置说明

本仓库是 [xinnan-tech/xiaozhi-esp32-server](https://github.com/xinnan-tech/xiaozhi-esp32-server) 的 fork，已把 `origin` 指向自有仓库。

## 远程

```
origin    git@github.com:eazlong/xiaozhi-esp32-server.git   # 自行维护，push 目标
upstream  https://github.com/xinnan-tech/xiaozhi-esp32-server  # 仅用于同步，push 已禁用
```

`upstream` 的 push 地址被设为 `DISABLED_USE_ORIGIN`，避免误把提交推到上游。

## 与上游同步

```bash
git fetch upstream
git merge upstream/main        # 或 git rebase upstream/main
git push origin main
```

当前三方 HEAD 一致（`d9c2e8c5`），首次同步无需解决冲突。

## 代码中保留上游地址的地方

把仓库换成 fork 后，下列引用**故意保留上游**，改动会导致功能失效：

| 位置 | 原因 |
| --- | --- |
| `Dockerfile-server` 的 `FROM ghcr.io/xinnan-tech/...:server-base` | 基础镜像由上游 CI 发布，fork 尚无 `server-base` 标签 |
| `main/xiaozhi-server/docker-compose*.yml` 的 `image:` | fork 的 GHCR 包尚未发布（无 tag/release，Actions 也未产生镜像），拉取会返回 `401 DENIED` |
| `docker-setup.sh` 的镜像名与 `raw.githubusercontent.com` 下载地址 | 同上；脚本需拉取真实存在的镜像与配置模板 |
| README 的 release / star 徽章、star-history 图表 | fork 无 release、star 与历史数据，徽章会渲染成 `no releases or repo not found` |
| `issues/791` 等具体 issue 深链 | issue 在 fork 中不存在，回退到上游才能打开 |

其余指向本仓库文档、LICENSE、contributors 等路径的链接，已全部改为 `eazlong/xiaozhi-esp32-server`。

## 若要让 fork 自己发布镜像

1. 在仓库 Settings → Secrets 配置 `TOKEN`（`write:packages` 权限的 PAT，上游工作流使用该名称）。
2. 在 Settings → Actions 确认 Actions 已启用（fork 默认可能为关闭状态）。
3. 推送 `v*.*.*` 形式的 tag 触发 `.github/workflows/docker-image.yml`；或手动触发 `workflow_dispatch`。
4. 首个 tag 会先触发 `build-base-image.yml` 生成 `server-base`，镜像发布后再把上表中的镜像坐标改为 `ghcr.io/eazlong/xiaozhi-esp32-server`。

在此之前，部署请继续使用上游镜像；由于当前 commit 与上游完全相同，镜像内容与仓库代码一致。
