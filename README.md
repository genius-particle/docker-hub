# docker-hub

本仓库用于对各类基础镜像做定制改造，每个子目录对应一个**改造对象**，构建出的镜像以改造对象命名并推送到 GitHub Container Registry (ghcr.io)。

## 当前镜像

| 改造对象 | 目录 | 镜像名 |
|----------|------|--------|
| [opencode](https://github.com/anomalyco/opencode) | `./opencode` | `ghcr.io/<owner>/opencode:latest` |

新增改造对象时：在仓库下新建同名目录（含 Dockerfile），并在 workflow 的 `matrix.target` 中增加该项。

## 本地创建仓库并推送（GitHub MCP 不可用时）

```bash
# 1. 在 GitHub 网页创建空仓库 docker-hub（或使用 GitHub CLI）
gh repo create docker-hub --public --source=. --remote=origin --push

# 或手动：
# 2. 在 https://github.com/new 创建仓库名 docker-hub，不要勾选 README
# 3. 添加远程并推送
git remote add origin https://github.com/<你的用户名>/docker-hub.git
git branch -M main
git add .
git commit -m "ci: add Dockerfile and GitHub Actions workflow"
git push -u origin main
```

## GitHub Actions

- **工作流**: [.github/workflows/docker-build-push.yml](.github/workflows/docker-build-push.yml)
- **触发**: 推送到 `main`/`master` 或 Actions 页手动运行
- **镜像命名**: `ghcr.io/<owner>/<target>`，其中 `<target>` 为改造对象（如 `opencode`），与子目录名一致
- **结果**: 各 target 分别构建并推送到 ghcr.io，可在仓库的 Packages 中查看
