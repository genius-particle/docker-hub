# docker-hub

基于 [opencode](https://github.com/anomalyco/opencode) 官方镜像（Alpine）的 Docker 镜像，通过 GitHub Actions 自动构建并推送到 GitHub Container Registry (ghcr.io)。

## 镜像

- **构建上下文**: `./opencode`
- **推送**: `ghcr.io/<owner>/<repo>:latest` 及 SHA 标签

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
- **结果**: 镜像构建并推送到 ghcr.io，可在仓库的 Packages 中查看
