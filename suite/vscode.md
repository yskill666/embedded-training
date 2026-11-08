# C 语言学习前导：编译器选择与 VSCode 环境搭建

> 本文是 C 语言学习的「第 0 课」：先搞清楚编辑器与编译器的关系，选定编译器，再动手完成 VSCode 的下载、汉化与 C/C++ 环境配置，最后用 Hello VSCode 程序验收。
>
> **适用对象**：零基础入门 · Windows 10 / 11
>
> **完成目标**：VSCode 全中文界面，C 语言可编译、可运行、有输出。
>
> **前置阅读**：建议先完成《GitHub 账号注册与 Git 安装配置教程》（本文最后的 GitHub 登录会用到账号）。

---

## 目录

- [0. 前导：写代码到底需要哪些工具](#0-前导写代码到底需要哪些工具)
- [1. 编译器选择](#1-编译器选择)
- [2. VSCode 下载与基础配置（汉化）](#2-vscode-下载与基础配置汉化)
- [3. VSCode C/C++ 环境配置](#3-vscode-cc-环境配置)
- [4. 第一个程序：Hello VSCode（验收）](#4-第一个程序hello-vscode验收)
- [5. 可选扩展内容](#5-可选扩展内容)
  - [5.1 终端输出中文乱码问题](#51-终端输出中文乱码问题)
  - [5.2 界面美化](#52-界面美化)
  - [5.3 登录绑定 GitHub](#53-登录绑定-github)
- [6. 完成自查清单](#6-完成自查清单)
- [7. 下一步学习路线](#7-下一步学习路线)

---

## 0. 前导：写代码到底需要哪些工具

C 语言是**嵌入式开发的母语**：STM32 单片机、RTOS、Linux 内核都以 C 为主。学会 C，你才能真正理解「代码是如何在芯片上跑起来的」。

动手之前，先分清三类工具——这是新手最容易混淆的概念：

| 工具类型 | 作用 | 类比 | 本教程的选择 |
|----------|------|------|-------------|
| **编辑器** | 写代码的地方，本质是「高级记事本」 | 稿纸 | VSCode |
| **编译器** | 把 `.c` 源文件翻译成电脑能执行的 `.exe` | 翻译官 | GCC（MinGW-w64） |
| **IDE** | 编辑器 + 编译器 + 调试器的全家桶 | 精装工作室 | VSCode + 插件 + MinGW 自行组装 |

一个 C 程序的完整生命周期：

```
hello.c（源代码） → gcc 编译 → hello.exe（可执行文件） → 终端运行 → 输出结果
```

> 💡 **关键认知**：VSCode 本身**不会编译代码**，它只负责写和展示；真正干活的是编译器。所以「装 VSCode」和「装编译器」是两步，缺一不可。

---

## 1. 编译器选择

Windows 上常见的 C/C++ 编译器有三家：

| 编译器 | 平台 | 特点 | 适合谁 |
|--------|------|------|--------|
| **GCC（MinGW-w64）** ✅ | Windows / Linux | 开源免费、轻量解压即用，教学与嵌入式领域的主流 | 本教程选择，初学者首选 |
| **MSVC** | Windows | 微软官方，随 Visual Studio 安装，体积动辄几个 G | Windows 桌面软件开发 |
| **Clang（LLVM）** | 全平台 | 报错信息友好，macOS 默认 | 进阶可选 |

**为什么选 MinGW-w64**：它是 GCC 在 Windows 上的移植版。后续学习 STM32 时使用的 `arm-none-eabi-gcc` 与它同属 GCC 家族，命令习惯一脉相承；而且免费开源、解压即用，不写注册表。

**下载链接**（任选其一）：

- **WinLibs（推荐）**：[https://winlibs.com/](https://winlibs.com/) —— 免安装压缩包，内含 GCC / GDB / Make 全套工具链，页面往下翻找 **Zip archive** 下载
- **GitHub 发布页（备选）**：[https://github.com/niXman/mingw-builds-binaries/releases](https://github.com/niXman/mingw-builds-binaries/releases) —— 版本最新，协会学长常备
- 官方下载说明页：[https://www.mingw-w64.org/downloads/](https://www.mingw-w64.org/downloads/)

**版本怎么选**（以 Windows 10 / 11 64 位为例）：认准文件名中的四个关键词 `x86_64` + `posix` + `seh` + `ucrt`，例如：

```
x86_64-16.2.0-release-posix-seh-ucrt-rt_v14-rev1.7z
```

> 📌 **说明**：32 位老电脑选 `i686` 开头的版本；Windows 7 等老系统选 `msvcrt` 结尾的版本。`.zip` 包 Windows 可直接解压；`.7z` 包需要 7-Zip 或 Bandizip 等解压软件。

---

## 2. VSCode 下载与基础配置（汉化）

### 2.1 下载与安装

1. 打开 VSCode 官网：[https://code.visualstudio.com/](https://code.visualstudio.com/)，点击 **Download for Windows**（也可直接访问 [https://code.visualstudio.com/Download](https://code.visualstudio.com/Download)）。
2. 运行下载的安装程序，建议勾选 **「添加到 PATH」** 和 **「通过 Code 打开」右键菜单**，其余保持默认，一路下一步完成安装。
3. **如果遇到网络问题无法下载**：直接问学长要安装包（协会群文件里一般有备用）。

### 2.2 安装中文汉化插件

1. 打开 VSCode，点击**左侧活动栏「四个小方块」图标**（扩展 / Extensions），或按快捷键 `Ctrl+Shift+X`。
2. 在搜索框输入 `Chinese`，找到插件：

   **Chinese (Simplified) (简体中文) Language Pack for Visual Studio Code**

   > ⚠️ 认准发布者是 **Microsoft**（扩展 ID：`ms-ceintl.vscode-language-pack-zh-hans`），不要装第三方仿冒汉化包。
3. 点击 **Install** 安装，完成后**右下角会弹出提示，点击「Change Language and Restart」（更改语言并重启）**。
4. 重启后界面变为全中文，**基础配置部分结束**。

> 💡 如果右下角没有弹窗：按 `Ctrl+Shift+P` 打开命令面板，输入 `Configure Display Language`，选择 `zh-cn`，然后手动重启 VSCode。

---

## 3. VSCode C/C++ 环境配置

### 3.1 解压 MinGW 到 VSCode 目录

1. 按 [第 1 节](#1-编译器选择) 的链接下载**对应你电脑版本**的 MinGW 压缩包。
2. 将压缩包**解压到你的 VSCode 安装目录下**，得到一个 `mingw64` 文件夹。例如 VSCode 装在 D 盘，则结构为：

   ```
   D:\Microsoft VS Code\
   ├── Code.exe
   └── mingw64\          ← 解压出来的编译器
       ├── bin\          ← 关键目录，里面有 gcc.exe
       ├── include\
       └── lib\
   ```

3. 打开 `mingw64\bin`，确认里面有 `gcc.exe`、`gdb.exe`，然后**复制这个 bin 文件夹的完整路径**（如 `D:\Microsoft VS Code\mingw64\bin`）。

> 📌 路径中不要出现中文；若解压时提示权限不足，用管理员身份运行解压软件。

### 3.2 把 bin 路径配置到系统环境变量

1. 按 `Win` 键搜索 **「编辑系统环境变量」** 并打开，点击右下角 **「环境变量」**。
2. 在下方 **「系统变量」** 区域找到并双击 **`Path`**。
3. 点击 **「新建」**，粘贴刚才复制的 bin 路径（如 `D:\Microsoft VS Code\mingw64\bin`）。
4. 一路点击 **「确定」** 保存退出。

**验证配置**：重新打开一个终端（`Win+R` 输入 `cmd`，或打开 Git Bash），输入：

```bash
gcc --version
gdb --version
```

两条命令都输出版本号，说明环境变量配置成功。

> ⚠️ **必须是新开的终端**才能读到新的 Path；已打开的终端 / VSCode 请关掉重开。

### 3.3 安装 C/C++ 插件

1. 回到 VSCode 扩展页（四个小方块图标），搜索 `C/C++`。
2. 安装 Microsoft 发布的 **C/C++** 插件（提供代码补全、错误提示、调试与运行按钮）。
   - 也可以直接安装 **C/C++ Extension Pack**（全家桶，内含 C/C++ 主题与 CMake Tools，学习阶段装基础版即可）。
3. （可选）搜索安装 **Code Runner**，获得更简单的「一键运行」体验。

**环境配置部分结束。**

---

## 4. 第一个程序：Hello VSCode（验收）

1. 在桌面**新建一个文件夹**（如 `c-study`），**右键 →「通过 Code 打开」**（Open with Code）。
2. 在 VSCode 左侧资源管理器中**新建文件 `hello.c`**，编写以下基础程序：

```c
#include <stdio.h>

int main(void)
{
    printf("Hello, VSCode!\n");
    return 0;
}
```

3. 保存后，点击编辑器**右上角的 ▶ 运行按钮**（C/C++ 插件提供的「运行 C/C++ 文件」；装了 Code Runner 则是 Run Code）。
   - 首次运行若提示选择环境：选 **C++ (GDB/LLDB)** → **C/C++: gcc.exe 生成和调试活动文件**。
   - 也可以在下方终端手动编译运行，效果相同：

   ```bash
   gcc hello.c -o hello
   .\hello.exe
   ```

4. 终端正确输出：

```
Hello, VSCode!
```

**看到输出，说明你的基础环境配置完毕！**

> ✅ **当前状态**：VSCode 已汉化 · C 语言可编译输出。

---

## 5. 可选扩展内容

以下三项不影响基础环境，按需选做。

### 5.1 终端输出中文乱码问题

**现象**：`printf("你好");` 输出变成 `浣犲ソ` 之类的乱码。

**原因**：VSCode 保存的源文件是 **UTF-8** 编码，而 Windows 终端默认使用 **GBK（代码页 936）**，两边编码不一致。

**解决方案（任选其一）**：

```bash
# 方案 A：运行前把当前终端切换为 UTF-8（临时，重开终端失效）
chcp 65001

# 方案 B：编译时让程序按 GBK 输出中文
gcc hello.c -o hello -fexec-charset=GBK
```

**方案 C（推荐，配合 Code Runner 一劳永逸）**：打开 VSCode 设置（`Ctrl+,`），点击右上角「打开设置(JSON)」图标，在 `settings.json` 中加入：

```json
"code-runner.executorMap": {
    "c": "cd $dir && gcc $fileName -o $fileNameWithoutExt -fexec-charset=GBK && $dir$fileNameWithoutExt"
}
```

> ⚠️ 另有「系统区域设置 → 勾选 Beta 版 UTF-8 支持」的方案，但会影响整个系统的老软件，**不建议新手使用**。

### 5.2 界面美化

| 项目 | 推荐 | 操作 |
|------|------|------|
| 颜色主题 | One Dark Pro / GitHub Theme | 扩展页搜索安装，`Ctrl+K Ctrl+T` 切换 |
| 文件图标 | Material Icon Theme | 扩展页搜索安装，按提示启用 |
| 编程字体 | Cascadia Code / JetBrains Mono | 安装字体后在设置中指定 |

字体与细节的参考配置（`settings.json`）：

```json
{
    "editor.fontFamily": "'Cascadia Code', Consolas, monospace",
    "editor.fontLigatures": true,
    "editor.fontSize": 16,
    "editor.minimap.enabled": false,
    "editor.bracketPairColorization.enabled": true
}
```

### 5.3 登录绑定 GitHub

用上一篇教程注册的 GitHub 账号登录 VSCode，开启**设置同步**：

1. 点击 VSCode **左下角的账户图标**（小人像）→ 选择 **「登录以使用设置同步」**（或「备份和同步设置」）。
2. 在弹出的列表中选择 **GitHub**，浏览器会跳转到 GitHub 授权页面，点击 **Authorize** 授权。
3. 回到 VSCode，确认开启 **Settings Sync（设置同步）**。

**好处**：主题、插件、快捷键、代码片段全部云端备份，换电脑登录同一账号即可一键恢复；后续还能直接在 VSCode 里克隆、提交、推送 GitHub 仓库，与 Git 教程无缝衔接。

---

## 6. 完成自查清单

- [ ] VSCode 从官网（或学长安装包）安装成功
- [ ] 中文汉化完成，界面全中文
- [ ] MinGW 已解压到 VSCode 目录，bin 路径已加入系统 Path
- [ ] 新终端中 `gcc --version` 正常输出版本号
- [ ] C/C++ 插件已安装
- [ ] `hello.c` 点击运行，终端正确输出 `Hello, VSCode!`

全部打勾：**VSCode 汉化完成，C 语言编译输出就绪**，可以正式开始学 C 了。

---

## 7. 下一步学习路线

建议按以下顺序推进 C 语言基础，**每学一个知识点就改写 `hello.c` 动手验证**：

```
变量与数据类型 → 运算符 → 顺序/分支/循环 → 函数 → 数组与字符串 → 指针 → 结构体 → 文件操作
```

- 指针是 C 的灵魂，也是嵌入式的核心，务必多写多练。
- 后续衔接 STM32 开发时，`arm-none-eabi-gcc` 与今天的 `gcc` 命令习惯完全一致，今天的环境搭建经验会直接复用。

---

*本教程与《GitHub 账号注册与 Git 安装配置教程》配套，构成协会新手入门的「环境搭建双件套」。如有疑问，欢迎在协会群内交流讨论。*