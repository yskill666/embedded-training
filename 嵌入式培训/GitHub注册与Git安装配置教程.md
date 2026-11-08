# GitHub 账号注册与 Git 安装配置教程

> 本文基于《Git 与 GitHub 入门教程》的「前置准备工作」章节整理，并补充了注册细节、安装选项说明、跨平台安装方法与常见问题排查。
>
> **适用对象**：零基础入门 · Windows 为主（附 macOS / Linux 安装说明）
>
> **完成目标**：拥有一个可用的 GitHub 账号，在本地装好 Git 并完成身份与 SSH 配置，为后续多人协作开发做好准备。

---

## 目录

- [0. 先认识三个概念](#0-先认识三个概念)
- [1. 注册 GitHub 账号](#1-注册-github-账号)
- [2. 下载与安装 Git](#2-下载与安装-git)
- [3. Git 基础配置](#3-git-基础配置)
- [4. 配置 SSH 密钥连接 GitHub](#4-配置-ssh-密钥连接-github)
- [5. 常见问题排查](#5-常见问题排查)
- [6. 完成自查清单](#6-完成自查清单)
- [7. 下一步学什么](#7-下一步学什么)

---

## 0. 先认识三个概念

| 概念 | 一句话解释 | 解决什么问题 |
|------|-----------|-------------|
| **Git** | 开源的分布式版本控制系统，装在每个人自己的电脑上 | 追踪每一次代码变更，随时回滚历史版本、并行开发分支，解决多人协作时代码互相覆盖的问题 |
| **Git 仓库** | 存放项目代码与全部历史记录的集合，分本地仓库与远程仓库 | 本地记录提交历史，远程托管在云端，团队通过推送（Push）/ 拉取（Pull）共享代码 |
| **GitHub** | 基于 Git 的云端代码托管平台，全球最大的开源社区 | 让远程仓库有一个稳定的「家」，并提供 Fork、Pull Request 等协作机制 |

> 💡 三者的关系：**Git 是工具，仓库是数据的家，GitHub 是云端的家。** 本教程先把工具装好、把账号建好、把两者连接起来。

---

## 1. 注册 GitHub 账号

### 1.1 注册前准备（补充）

- **一个能收信的邮箱**：若无其他邮箱，可直接使用 **QQ 邮箱**（格式：`你的QQ号@qq.com`）。
- **想一个好用户名**：只能包含英文、数字和短横线 `-`，简短易记。它会出现在你所有仓库的网址里（`github.com/用户名/仓库名`），注册后虽可修改，但尽量一次想好。
- **想一个好密码**：GitHub 要求**至少 15 个字符**；或**至少 8 个字符且同时包含数字和小写字母**。建议直接使用密码管理器生成。

### 1.2 注册步骤

1. 打开 GitHub 官网：[https://github.com/](https://github.com/)，点击右上角的 **Sign up**（注册）。
2. 输入邮箱，点击 **Continue**。
3. 设置密码，点击 **Continue**。
4. 设置用户名，点击 **Continue**（提示不可用就换一个）。
5. 查收 GitHub 发来的 **8 位验证码**邮件，填入完成邮箱验证（收不到先翻垃圾邮件）。
6. 完成人机验证拼图，按需填写问卷（可跳过），进入个人主页即注册成功。

### 1.3 注册后建议（补充）

- **开启两步验证（2FA）**：头像 → **Settings** → **Password and authentication**，用验证器 App 扫码绑定，账号安全等级大幅提升。
- **完善 Profile**：上传头像、填写昵称与简介，让未来的协作者认识你。
- **习惯全英文界面**：未来开发中你需要具备一定的英语读写能力，从现在开始适应。

---

## 2. 下载与安装 Git

### 2.1 Git Bash 是什么

| 问题 | 回答 |
|------|------|
| **是什么？** | 专为 Windows 设计的命令行工具，集成 Git 版本控制功能，并模拟类 Unix（Linux）命令行环境 |
| **有什么用？** | 既能用 `git add`、`git commit` 管理代码，又能用 `ls`、`cd` 等 Linux 风格命令操作文件 |
| **为什么选它？** | 比 CMD / PowerShell 更接近原生 Linux 终端体验，是目前最主流、最标准的 Git 命令行使用方式 |

### 2.2 Windows 安装步骤

1. 打开下载页：[https://git-scm.com/download/win](https://git-scm.com/download/win)，下载 **64-bit Git for Windows Setup**。
2. 运行安装程序，**保持默认选项，一路 Next** 完成安装。
3. 几个关键默认项的含义（补充，了解即可，无需改动）：

| 安装选项 | 默认值 | 含义 |
|----------|--------|------|
| 默认编辑器 | Vim | 可下拉改为 VS Code 等你熟悉的编辑器 |
| PATH 环境 | 中间项（推荐） | 让 CMD、PowerShell、第三方软件也能调用 `git` |
| 行尾转换 | Checkout Windows-style, commit Unix-style | 跨平台协作时自动统一行尾符，避免无意义差异 |
| 终端模拟器 | MinTTY | Git Bash 使用的终端窗口 |

### 2.3 验证安装（补充）

在桌面或文件夹空白处**右键 → Git Bash Here**（Windows 11 需先点「显示更多选项」），输入：

```bash
git --version
```

看到类似 `git version 2.47.0.windows.1` 的输出，说明安装成功。

### 2.4 macOS 与 Linux 安装（补充）

**macOS**（二选一）：

```bash
# 方式一：触发系统自动安装 Xcode 命令行工具
git --version

# 方式二：使用 Homebrew 安装最新版
brew install git
```

**Linux**：

```bash
# Debian / Ubuntu
sudo apt install git

# Fedora
sudo dnf install git

# Arch
sudo pacman -S git
```

---

## 3. Git 基础配置

### 3.1 配置用户名和邮箱

打开 **Git Bash**，依次输入以下命令（将引号内替换为你的信息）：

```bash
# 配置全局用户名（使用你的 GitHub 用户名）
git config --global user.name "你的用户名"

# 配置全局邮箱（使用你的 GitHub 注册邮箱）
git config --global user.email "你的邮箱"
```

> 📌 **说明**：这里的用户名和邮箱会记录在你每一次 Git 提交中，建议与 GitHub 账号保持一致，以便正确关联提交记录。

### 3.2 推荐补充配置（补充）

```bash
# 新仓库的默认主分支命名为 main（与 GitHub 保持一致）
git config --global init.defaultBranch main

# Windows：检出时转为 CRLF，提交时转回 LF，跨平台协作不乱码
git config --global core.autocrlf true

# macOS / Linux 用户请改用：
# git config --global core.autocrlf input
```

### 3.3 检查配置

```bash
# 查看全部配置
git config --list

# 单独查看某一项
git config user.name
git config user.email
```

---

## 4. 配置 SSH 密钥连接 GitHub

SSH 密钥是一种安全的身份认证方式，配置后推送代码**无需每次输入账号密码**。

> 🔑 **原理一句话（补充）**：SSH 密钥是一对文件——**私钥留在自己电脑，公钥交给 GitHub**。两者配对成功即证明「你是你」，之后所有推送、拉取自动完成认证。

### 第一步：生成 SSH 密钥

在 Git Bash 中输入以下命令（**将邮箱替换为你的 GitHub 注册邮箱**）：

```bash
ssh-keygen -t ed25519 -C "你的github注册邮箱"
```

> 🔐 `-t ed25519` 指定使用 Ed25519 算法（当前**推荐方案**，比传统的 RSA 更安全、性能更好）。

执行后按提示操作：

1. **密钥保存路径**：直接按 `Enter`，接受默认路径 `~/.ssh/id_ed25519`
2. **密码短语（passphrase）**：建议直接按 `Enter` 留空，避免每次使用都要输入密码

### 第二步：启动 ssh-agent 并将密钥添加到其中

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 第三步：复制公钥内容

```bash
cat ~/.ssh/id_ed25519.pub
```

手动选中并复制输出的**全部内容**（以 `ssh-ed25519` 开头，以邮箱结尾）。也可以直接复制到剪贴板：

```bash
clip < ~/.ssh/id_ed25519.pub
```

### 第四步：将公钥添加到 GitHub

1. 登录 GitHub，点击右上角头像 → **Settings**
2. 左侧边栏选择 **SSH and GPG keys**
3. 点击绿色的 **New SSH Key** 按钮
4. **Title** 输入便于识别的名称（如 `My-Work-PC`）
5. **Key** 框中粘贴刚复制的公钥内容
6. 点击 **Add SSH Key** 保存

### 第五步：验证 SSH 连接是否成功

```bash
ssh -T git@github.com
```

首次连接会提示确认主机指纹，输入 `yes` 并回车。看到类似以下信息即配置成功：

```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

> ⚠️ 如果连接超时或报错，可能是网络环境屏蔽了 SSH 默认的 **22 端口**，请参考 [5.1 节](#51-连接超时改用-443-端口) 配置走 **443 端口**。

---

## 5. 常见问题排查

### 5.1 连接超时：改用 443 端口

公司内网、校园网等环境的防火墙可能屏蔽 SSH 默认的 **22 端口**，导致 `Connection timed out`。GitHub 官方提供了通过 **443 端口**连接的备用方案。

**第一步：测试 443 端口是否可用**

```bash
ssh -T -p 443 git@ssh.github.com
```

> ⚠️ 注意：443 端口对应的主机名是 **`ssh.github.com`**，而非 `github.com`。看到包含你用户名的欢迎信息即说明可用。

**第二步：修改 SSH 配置文件**

```bash
cd ~/.ssh
touch config
```

用文本编辑器打开 `config` 文件（无扩展名），添加以下内容（已有内容则在末尾追加）：

```
Host github.com
    Hostname ssh.github.com
    Port 443
    User git
```

**第三步：验证配置是否生效**

```bash
ssh -T git@github.com
```

看到欢迎信息即成功，后续所有 GitHub 的 SSH 操作都将自动走 443 端口。

### 5.2 Permission denied (publickey)（补充）

- 执行 `ssh-add -l` 查看 agent 中已加载的密钥；若为空，执行 `ssh-add ~/.ssh/id_ed25519` 重新添加。
- 确认 GitHub 上粘贴的是 **`.pub` 公钥的完整内容**（以 `ssh-ed25519` 开头），不要粘贴私钥。
- 一台电脑生成一对密钥即可；多台电脑应各自生成、各自添加到 GitHub。

### 5.3 'git' 不是内部或外部命令（补充）

- 多为安装时 **PATH 选项未选对**：重新运行安装程序，选择中间项（Git from the command line and also from 3rd-party software），或直接重装保持默认。
- 安装完成后需**重启终端 / VSCode**，新的 PATH 才会生效。

### 5.4 HTTPS 和 SSH 地址怎么选（补充）

| 方式 | 地址格式 | 特点 |
|------|----------|------|
| **SSH** ✅ 推荐 | `git@github.com:用户名/仓库.git` | 配好密钥后全程免密 |
| **HTTPS** | `https://github.com/用户名/仓库.git` | 配合 Git Credential Manager 记住凭据 |

> ⚠️ GitHub 自 2021 年起**不再支持账号密码推送**。使用 HTTPS 方式时，需以 Personal Access Token（PAT）代替密码。

### 5.5 收不到验证码邮件（补充）

- 检查垃圾邮件 / 订阅邮件分类。
- 在注册页面点击 **Resend** 重新发送。
- QQ 邮箱可在「自助查询」中查看是否被系统拦截。

---

## 6. 完成自查清单

- [ ] GitHub 账号注册完成，邮箱已验证，可正常登录
- [ ] `git --version` 正常输出版本号
- [ ] `user.name` 与 GitHub 用户名一致
- [ ] `user.email` 与 GitHub 注册邮箱一致
- [ ] `ssh -T git@github.com` 显示 `Hi 你的用户名!`
- [ ] （可选）已开启两步验证 2FA

全部打勾，说明准备工作就绪，可以进入 Git 协作流程的学习。

---

## 7. 下一步学什么

准备工作完成后，先熟悉这几条最高频的命令：

| 指令 | 作用 |
|------|------|
| `git clone` | 把远程仓库完整复制到本地 |
| `git status` | 查看当前哪些文件被修改 |
| `git add` | 把修改放入暂存区 |
| `git commit` | 生成一个版本快照 |
| `git push` / `git pull` | 推送 / 拉取远程代码 |
| `git switch` | 创建与切换分支 |

完整的协作流程（克隆仓库 → Fork 工作流 → 创建分支 → 提交 PR → 同步上游）请见《Git 与 GitHub 入门教程》第 2 章；熟练后再进阶学习 `git rebase`、`git stash`、`git cherry-pick`。

---

*本教程内容已对照 GitHub 官方文档及业界最佳实践进行交叉验证。配套可视化页面见同目录下的 `GitHub注册与Git安装配置教程.html`。*