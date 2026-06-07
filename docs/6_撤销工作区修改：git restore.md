## 第 1 步：先确认当前修改内容

执行：

```
git diff
```

### 作用

确认当前还没有提交的修改是什么。

这一步是为了避免误删重要内容。
 在真实项目中，执行撤销命令前应先看 `git diff`。

------

## 第 2 步：撤销 README.md 的工作区修改

执行：

```
git restore README.md
```

### 作用

把 `README.md` 恢复到最近一次 commit 的版本。

注意：这个命令会丢弃当前未提交的修改。
 如果修改没有 commit，也没有 stash，撤销后通常无法通过 Git 找回。

------

## 第 3 步：查看状态

执行：

```
git status
```

正常应该看到：

```
nothing to commit, working tree clean
```

含义是：

```
README.md 已恢复
当前工作区没有未提交内容
```