# 新增文档并完成一次 Git 提交

本阶段练习的是 Git 最常见的日常操作流程：

```text
新增文件
→ 查看状态
→ 添加到暂存区
→ 创建本地提交
→ 推送到 GitHub
```

这类操作适用于平时新增代码文件、文档文件、配置文件等场景。

------

## 1. 新增一个 md 文档

在 `docs/` 目录下新增一个 Markdown 文档，例如：

```text
docs/3_新增文档并完成一次 Git 提交.md
```

新增文件后，Git 会把它识别为一个还没有被跟踪的新文件。

------

## 2. 查看当前 Git 状态

```powershell
git status
```

作用：查看当前工作区发生了哪些变化。

如果只是新增了一个文档，正常会看到类似：

```text
Untracked files:
  docs/3_新增文档并完成一次 Git 提交.md
```

含义是：

```text
该文件已经存在于本地项目目录中
但还没有被 Git 纳入版本管理
也不会自动进入下一次 commit
```

------

## 3. 将新增文档加入暂存区

```powershell
git add "docs/3_新增文档并完成一次 Git 提交.md"
```

作用：把这个新增文档加入暂存区。

暂存区表示“下一次提交准备包含的内容”。
只有执行 `git add` 后，该文件才会进入下一次 `git commit`。

如果文件名中包含中文、空格或特殊符号，建议用英文双引号包住路径。

------

## 4. 再次查看状态

```powershell
git status
```

作用：确认新增文件已经进入暂存区。

正常会看到类似：

```text
Changes to be committed:
  new file:   docs/3_新增文档并完成一次 Git 提交.md
```

含义是：该文件已经准备好进入下一次提交。

------

## 5. 创建本地提交

```powershell
git commit -m "Add Git new document workflow"
```

作用：创建一次新的本地提交。

其中：

```text
git commit
```

表示创建提交记录。

```text
-m
```

表示直接在命令中填写提交说明。

```text
"Add Git new document workflow"
```

是本次提交的说明，表示新增了 Git 文档操作流程。

提交成功后，Git 会生成一个新的 commit 记录。

------

## 6. 推送到 GitHub

```powershell
git push
```

作用：把本地新提交上传到 GitHub。

由于之前已经执行过：

```powershell
git push -u origin main
```

本地 `main` 分支已经和远程 `origin/main` 建立追踪关系，所以后续推送时只需要执行：

```powershell
git push
```

不需要再写完整的：

```powershell
git push origin main
```

------

## 本次操作使用的核心命令

```powershell
git status
git add "docs/3_新增文档并完成一次 Git 提交.md"
git status
git commit -m "Add Git new document workflow"
git push
```

------

## 本次操作完成后的状态

完成后，本地仓库和 GitHub 远程仓库都会包含这个新增的 md 文档。

这次练习对应的是最基础、最常用的 Git 日常工作流：

```text
改动文件
→ git status
→ git add
→ git commit
→ git push
```