# 第1章：环境安装与配置

本章将介绍如何在本地环境中安装和配置 OpenClaw，为接下来的开发和使用做好准备。

## 环境需求
- **操作系统**：
  - MacOS
  - Linux
  - Windows 10+
- **软件依赖**：
  - Node.js 最新版（推荐 v18+）
  - Git（用于版本管理）

## 安装步骤

### 1. 克隆 OpenClaw 项目
确保系统安装了 Node.js 和 Git，打开终端执行以下命令：

```bash
git clone https://github.com/openclaw/openclaw.git
cd openclaw
```

### 2. 安装依赖
进入项目目录后，安装必要依赖：

```bash
npm install
```

### 3. 配置环境变量
根据项目提供的示例，复制配置文件：

```bash
cp .env.example .env
```
配置过程中，可以根据需要调整 `API_KEYS`，具体内容请参考官方文档。

### 4. 启动服务
一切准备就绪后，启动 OpenClaw：

```bash
npx openclaw start
```

## 常见问题
- **Q**: 安装依赖时遇到网络问题怎么办？
  - **A**: 请切换到国内 npm 镜像：
    ```bash
    npm config set registry https://registry.npmmirror.com
    ```
- **Q**: 启动失败提示端口占用？
  - **A**: 修改 `.env` 文件中 `PORT` 的值，避免冲突。

安装完成后，您已经准备好进入下一章内容。