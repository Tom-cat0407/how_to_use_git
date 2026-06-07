# Git 环境检查与 GitHub SSH 配置指南

> **说明**：本文档未包含 Git 安装步骤，默认已安装 Git。如需安装，可直接向 AI 提问：  
> *“我目前是什么环境（Windows、Linux、macOS），想要安装 Git 环境，告诉我如何做，给我详细的步骤。”*

---

## 1、检查当前 Git 环境

> 当前电脑系统为 Windows 系统，因此本文档所有操作均在 Windows 系统下操作，命令行也是如此。其他系统的命令差别不大，可作参考。

### 第 1 步：打开终端

在 Windows 上任选一个终端工具，**推荐：PowerShell**。

按 `Win` 键，搜索 `PowerShell` 并打开。

### 第 2 步：检查 Git 是否可用

输入以下命令：

```bash
git --version
```

**作用**：检查当前电脑是否能调用 Git。

**正常结果类似**：

```
git version 2.49.0.windows.1
```

如果显示版本号，说明 Git 已安装。  
如果显示 `git : The term 'git' is not recognized`，说明 Git 未安装或环境变量未配置好。

---

## 检查 Git 安装位置

输入：

```bash
where git
```

**作用**：确认 Windows 当前调用的是哪一个 Git 程序。

**正常结果类似**：

```
C:\Program Files\Git\cmd\git.exe
```

如果能显示路径，说明 Git 的环境变量基本正常。

---

## 检查 Git 用户名

输入：

```bash
git config --global user.name
```

**作用**：查看 Git 提交代码时使用的名字。

如果没有输出，说明还未设置。

---

## 检查 Git 邮箱

输入：

```bash
git config --global user.email
```

**作用**：查看 Git 提交代码时使用的邮箱。

如果没有输出，说明还未设置。

---

## 检查 GitHub 连通状态

在 PowerShell 中输入：

```bash
ssh -T git@github.com
```

**作用**：测试当前电脑是否可以通过 SSH 认证连接 GitHub。该命令不会登录 GitHub shell，也不会修改任何文件，仅做连接测试。

### 情况 1：已经连通

如果输出类似：

```
Hi your-github-username! You've successfully authenticated, but GitHub does not provide shell access.
```

说明 GitHub 已经连通。可跳过后续 SSH 配置步骤，直接进行 `clone` / `push` / `pull` 等操作。

---

### 情况 2：第一次连接 GitHub

如果输出类似：

```
The authenticity of host 'github.com (...)' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

输入 `yes` 确认。

**作用**：这是 Windows 第一次连接 GitHub SSH 服务器时的安全确认。确认后，GitHub 会被加入本机的可信主机列表。

---

### 情况 3：没有配置 SSH key

如果输出类似：

```
git@github.com: Permission denied (publickey).
```

说明当前电脑还没有成功配置 GitHub SSH key，需要进行以下操作：

```
生成 SSH key → 添加到 GitHub → 重新测试连接
```

---

## 检查本机是否已有 SSH key

在 PowerShell 中输入：

```bash
Get-ChildItem -Force "$env:USERPROFILE\.ssh"
```

**作用**：查看 Windows 用户目录下是否已有 SSH 配置文件和密钥文件。

### 你可能看到的情况

**情况 1：有这些文件**

例如：

```
id_ed25519
id_ed25519.pub
known_hosts
```

或：

```
id_rsa
id_rsa.pub
known_hosts
```

说明本机已有 SSH key，下一步是把 `.pub` 公钥添加到 GitHub。

---

**情况 2：只有 known_hosts**

例如：

```
known_hosts
```

说明刚刚连接过 GitHub，但还没有 SSH key，需要生成 SSH key。

---

**情况 3：报错找不到路径**

例如：

```
Cannot find path 'C:\Users\...\ .ssh'
```

说明 `.ssh` 文件夹还不存在，同样需要生成 SSH key。

---

## 复制现有公钥并配置到 GitHub

### 复制现有公钥

在 PowerShell 中输入：

```bash
Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
```

**作用**：查看你的 SSH **公钥**内容。

公钥一般长这样：

```
ssh-rsa AAAA...很多字符... user@email.com
```

> ⚠️ **注意**：只能复制 `id_rsa.pub` 公钥文件。  
> **不要**打开、复制或发送 `id_rsa` 私钥文件，私钥不能给任何人，也不能粘贴到 GitHub 网页里。

---

### 快速复制公钥到剪贴板

在 PowerShell 中输入以下命令，直接将公钥内容复制到剪贴板：

```bash
Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub" | Set-Clipboard
```

**作用**：读取公钥文件内容并复制到 Windows 剪贴板，无需手动选中复制。

---

### 把公钥添加到 GitHub

1. 打开 GitHub，进入：  
   `右上角头像 → Settings → SSH and GPG keys → New SSH key`

2. 填写信息：
   - **Title**：`Windows Administrator`（可自定义）
   - **Key type**：`Authentication Key`
   - **Key**：直接 `Ctrl + V` 粘贴公钥内容

3. 点击 `Add SSH key` 保存。

添加完成后，回到 PowerShell 测试连接：

```bash
ssh -T git@github.com
```

---

## 在 GitHub 创建仓库

打开 GitHub，进入：

```
右上角 + 号 → New repository
```

填写信息：
- **Repository name**：`how_to_use_git`
- **Visibility**：`Public`

按需填写其他选项后，点击 `Create repository` 即可完成创建。

