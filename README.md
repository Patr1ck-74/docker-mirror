# Docker Image Sync (Multi-Arch) 🚀

这是一个基于 GitHub Actions 和 [Crane](https://github.com/google/go-containerregistry/tree/main/cmd/crane) 的轻量级容器镜像同步工具。

### 🌟 为什么使用本项目？
- **多架构支持**：完美同步 `amd64`, `arm64`, `v7` 等所有架构，不会丢失 Manifest 信息。
- **无需拉取 (Serverless)**：使用 `crane cp` 直接在注册表之间传输 OCI 层，无需 `docker pull` 和 `push`，速度极快。
- **配置简单**：全自动化工作流，通过 GitHub Actions 手动触发。

---

## 🛠️ 准备工作

在使用之前，请确保在仓库的 **Settings > Secrets and variables > Actions** 中配置了以下 Secrets：

| 变量名 | 说明 |
| :--- | :--- |
| `DOCKERHUB_USERNAME` | 你的 Docker Hub 用户名 |
| `DOCKERHUB_TOKEN` | 你的 Docker Hub Access Token (推荐使用 Token 而非密码) |

*注：`GITHUB_TOKEN` 是 GitHub 自动生成的，无需手动添加。*

---

## 🚀 使用指南

1. 进入仓库的 **Actions** 选项卡。
2. 在左侧列表选择 **Docker Image Sync (Multi-Arch)**。
3. 点击右侧的 **Run workflow** 下拉按钮。
4. 填写以下参数：
   - **源镜像 (source_image)**: 完整的原始镜像地址 (例: `ghcr.io/szemeng76/lunatv:latest`)
   - **Docker Hub 仓库名 (target_repo)**: 目标仓库名称 (不含用户名，例: `moontv`)
   - **镜像标签 (target_tag)**: 想要生成的标签 (例: `latest`)
5. 点击 **Run workflow** 开始同步。

---

## 📝 实现原理

本项目核心逻辑非常简洁：
1. **Setup Crane**: 安装 Google 开发的容器管理工具。
2. **Auth**: 同时登录 GHCR 和 Docker Hub 确保权限。
3. **Native Copy**: 使用 `crane cp` 命令直接在服务端完成镜像流转，避免了本地构建可能带来的架构缺失问题。

---

## ⚖️ 开源协议
[MIT License](LICENSE)
