# Rust OpenFHE 开发环境

本项目提供了一个基于 Docker 的 Rust 和 OpenFHE 开发环境。这个环境适用于 x86_64 架构,并且可以在 Apple Silicon (M1) Mac 上运行。

## 前提条件

- 安装 [Docker Desktop](https://www.docker.com/products/docker-desktop)
- 如果使用 M1 Mac,确保启用了 Rosetta 2 以支持 x86_64 模拟

## 设置开发环境

1. 克隆此仓库:
   ```
   git clone <your-repository-url>
   cd <your-repository-name>
   ```

2. 构建 Docker 镜像:
   ```
   docker build -t rust-openfhe-dev -f .devcontainer/Dockerfile .
   ```

## 设置开发环境

...

3. 运行 Docker 容器:
   ```
   docker run -it --rm --platform linux/amd64 -v $(pwd):/workspace -w /workspace rust-openfhe-dev bash
   ```

   这个命令会:
   - 使用 x86_64 平台运行容器
   - 将当前目录挂载到容器的 `/workspace` 目录
   - 在容器内打开一个 bash shell
   - 在您退出容器时自动删除容器

## 开发工作流

1. 启动一个新的容器实例来编译和运行代码:
   ```
   docker run -it --rm --platform linux/amd64 -v $(pwd):/workspace -w /workspace rust-openfhe-dev bash
   ```

2. 在容器内编译和运行代码:
   ```
   cargo build
   cargo run
   ```

3. 完成工作后，输入 `exit` 或按 Ctrl+D 退出容器。容器将自动删除，但您的本地文件更改会保留。