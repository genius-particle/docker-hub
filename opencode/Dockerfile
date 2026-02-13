# 使用官方镜像作为基础
FROM ghcr.io/anomalyco/opencode:latest

# 切换到 root 用户以安装软件
USER root

# 安装基础工具和 Python（Alpine 使用 apk）
RUN apk add --no-cache \
    curl \
    python3 \
    py3-pip


# (可选) 安装 Python 库，如果你的 MCP 或 Skills 需要的话
# Alpine 下部分包需编译：先装构建依赖，再安装，最后删除以减小镜像
COPY requirements.txt .
RUN apk update \
    && apk add --no-cache --virtual .build-deps \
    build-base musl-dev python3-dev libffi-dev
RUN pip3 install --no-cache-dir -r requirements.txt
RUN apk del .build-deps

# 如果你依然使用 opencode web，确保启动命令正确
# 注意：官方镜像的入口脚本可能会重置用户，这里只是示例
# CMD ["opencode", "web", "--hostname", "0.0.0.0", "--port", "3000"]