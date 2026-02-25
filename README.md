# Docker Image Sync (Multi-Arch) 🚀

这是一个基于 GitHub Actions 和 [Crane](https://github.com/google/go-containerregistry/tree/main/cmd/crane) 的轻量级容器镜像同步工具。

### 🌟 核心优势
- **多架构支持**：原生 OCI 拷贝，完美保留 `amd64`, `arm64`, `arm/v7` 等所有架构信息。
- **极速同步**：通过 `crane cp` 直接在 Registry 之间传输，无需拉取到本地，不受 Runner 磁盘空间限制。
- **纯净安全**：不修改镜像内容，仅做仓库间的搬运工。

---

## 🛠️ 配置指南

在使用之前，请确保在仓库的 **Settings > Secrets and variables > Actions** 中添加以下两个 Secrets：

1. `DOCKERHUB_USERNAME`: 你的 Docker Hub 用户名。
2. `DOCKERHUB_TOKEN`: 你的 Docker Hub 访问令牌 (Access Token)。

> **提示**：为了安全，建议在 Docker Hub 设置中生成一个专门用于此 Workflow 的 Read/Write Token。

---

## 🚀 使用方法

1. 点击仓库顶部的 **Actions**。
2. 在左侧选择工作流：`Docker Image Sync (Multi-Arch)`。
3. 点击 **Run workflow** 下拉按钮并填写：
   - **源镜像**: 输入原始镜像（如 `ghcr.io/szemeng76/lunatv:latest`）。
   - **Docker Hub 仓库名**: 你要存放在自己仓库的名称（不含用户名）。
   - **镜像标签**: 目标镜像的标签（如 `latest` 或 `v1.2.3`）。
4. 点击 **Run workflow** 启动同步。

---

## 📝 实现原理

工作流执行流程如下：
- **Setup Crane**: 安装 Google 官方提供的 OCI 镜像管理工具。
- **Auth**: 通过 `GITHUB_TOKEN` 登录 GHCR，通过 Secrets 登录 Docker Hub。
- **Native Sync**: 执行 `crane cp "$SOURCE" "$TARGET"`，在不解压镜像的情况下完成跨仓库迁移。

---

## ⚖️ 开源协议 (MIT)

本项目采用 **MIT License**。你可以自由地使用、修改和分发本项目。

```text
Copyright (c) 2026 Patr1ck-74

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
