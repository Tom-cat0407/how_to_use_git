## Git 基础流程记录：第一次本地提交并上传到 GitHub

本阶段完成的是 Git 最基础的一条完整流程：

```text
进入项目目录
→ 初始化本地 Git 仓库
→ 创建或准备项目文件
→ 查看 Git 状态
→ 添加文件到暂存区
→ 创建第一次本地提交
→ 修改默认分支名
→ 连接 GitHub 远程仓库
→ 推送到 GitHub
```

------

## 1. 进入项目目录

```powershell
cd "C:\Users\xxxxxxxxxx\how_to_use_git"
```

作用：进入当前项目所在的本地文件夹。
Git 命令通常需要在项目根目录中执行，否则可能会初始化或操作到错误的位置。

确认当前路径：

```powershell
pwd
```

作用：检查当前 PowerShell 所在目录，确认已经进入目标项目路径。

------

## 2. 初始化本地 Git 仓库

```powershell
git init
```

作用：把当前文件夹初始化为一个 Git 仓库。

执行后，项目目录中会生成隐藏文件夹：

```text
.git
```

`.git` 文件夹用于保存 Git 的版本记录、分支信息、提交历史和远程仓库配置。
没有执行 `git init` 之前，这个文件夹只是普通文件夹；执行后，它才开始被 Git 管理。

------

## 3. 创建 README.md 文件

```powershell
Set-Content -Path README.md -Value "# how_to_use_git" -Encoding UTF8
```

作用：在项目根目录创建 `README.md` 文件，并写入项目标题：

```markdown
# how_to_use_git
```

`README.md` 通常用于说明项目内容、使用方法、目录结构和开发记录。
GitHub 会自动在仓库主页显示 `README.md` 的内容。

------

## 4. 查看当前 Git 状态

```powershell
git status
```

作用：查看当前仓库中哪些文件还没有被 Git 管理，哪些文件已经准备提交，哪些文件发生了修改。

此时状态中出现：

```text
Untracked files:
  README.md
  docs/
```

含义是：

```text
README.md 和 docs/ 已经存在于项目目录中
但还没有被 Git 跟踪
也还没有进入提交记录
```

------

## 5. 添加文件到暂存区

```powershell
git add README.md docs/
```

作用：把 `README.md` 和 `docs/` 加入暂存区。

暂存区可以理解为下一次提交的准备区域。
只有进入暂存区的文件，才会被包含进下一次 `git commit`。

再次查看状态：

```powershell
git status
```

此时显示：

```text
Changes to be committed:
  new file:   README.md
  new file:   docs/how_to_use_git.md
```

含义是：这些文件已经准备好进入下一次提交。

------

## 6. 创建第一次本地提交

```powershell
git commit -m "Initial commit"
```

作用：创建第一次本地提交记录。

`-m` 后面的内容是提交说明：

```text
Initial commit
```

这次提交包含两个文件：

```text
README.md
docs/how_to_use_git.md
```

提交成功后，Git 会生成一个 commit 记录，例如：

```text
[master (root-commit) 40ec3d8] Initial commit
```

其中：

```text
master
```

表示当前提交发生在 `master` 分支上。

```text
root-commit
```

表示这是当前仓库的第一个提交。

```text
40ec3d8
```

是本次提交的短哈希值，用于唯一标识这次提交。

------

## 7. 确认工作区是否干净

```powershell
git status
```

如果显示：

```text
nothing to commit, working tree clean
```

含义是：

```text
当前没有未提交的修改
暂存区为空
工作区和最后一次 commit 保持一致
```

这表示第一次本地提交已经完成。

------

## 8. 修改默认分支名为 main

```powershell
git branch -M main
```

作用：把当前本地分支从 `master` 改名为 `main`。

Git 初始化后，当前分支可能默认叫：

```text
master
```

而 GitHub 新仓库默认常用：

```text
main
```

为了和 GitHub 保持一致，将本地分支改名为 `main`，可以减少后续推送和分支管理时的混乱。

------

## 9. 添加 GitHub 远程仓库地址

```powershell
git remote add origin git@github.com:Tom-cat0407/how_to_use_git.git
```

作用：把本地 Git 仓库和 GitHub 上的远程仓库连接起来。

其中：

```text
origin
```

是远程仓库的默认名称。
通常第一个远程仓库都命名为 `origin`。

```text
git@github.com:Tom-cat0407/how_to_use_git.git
```

是 GitHub 仓库的 SSH 地址。

添加远程仓库后，本地 Git 才知道后续要把代码推送到哪个 GitHub 仓库。

------

## 10. 检查远程仓库配置

```powershell
git remote -v
```

作用：查看当前本地仓库已经配置的远程仓库地址。

正常结果类似：

```text
origin  git@github.com:Tom-cat0407/how_to_use_git.git (fetch)
origin  git@github.com:Tom-cat0407/how_to_use_git.git (push)
```

其中：

```text
fetch
```

表示从远程仓库拉取代码时使用的地址。

```text
push
```

表示向远程仓库上传代码时使用的地址。

------

## 11. 第一次推送到 GitHub

```powershell
git push -u origin main
```

作用：把本地 `main` 分支推送到 GitHub 的 `origin` 远程仓库。

其中：

```text
git push
```

表示上传本地提交到远程仓库。

```text
origin
```

表示目标远程仓库。

```text
main
```

表示要推送的本地分支。

```text
-u
```

表示建立本地 `main` 分支和远程 `origin/main` 分支的追踪关系。

推送成功后，输出中会出现：

```text
[new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

含义是：

```text
本地 main 分支已经上传到 GitHub
远程仓库中创建了 main 分支
本地 main 已经和 origin/main 建立默认关联
```

建立追踪关系后，以后在同一个分支上继续提交并上传时，通常只需要执行：

```powershell
git push
```

不需要每次都写：

```powershell
git push origin main
```

------

这是 Git 最基础的完整上传流程。后续日常开发通常会重复以下流程：

```text
修改文件
→ git status
→ git add
→ git commit
→ git push
```