# Git 远程与同步命令说明

本文档记录当前仓库的远程配置和常用一键同步命令。

## 1. 远程仓库

- `origin`（个人 fork）: `https://github.com/895252509/dify.git`
- `upstream`（官方仓库）: `https://github.com/langgenius/dify.git`

查看远程：

```bash
git remote -v
```

## 2. 已配置的一键命令（Git Alias）

### `git syncup`

按 `merge` 方式同步官方 `main` 到本地并推送到 fork：

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

直接执行：

```bash
git syncup
```

### `git syncup-rebase`

按 `rebase` 方式同步官方 `main` 到本地并推送到 fork（提交历史更线性）：

```bash
git fetch upstream
git checkout main
git rebase upstream/main
git push origin main
```

直接执行：

```bash
git syncup-rebase
```

## 3. 冲突处理（rebase 场景）

如果 `git syncup-rebase` 过程中出现冲突：

```bash
# 1) 手动解决冲突后
git add .

# 2) 继续 rebase
git rebase --continue

# 3) 推送到个人仓库
git push origin main
```

## 4. 如需在其他仓库复用

当前 alias 是“本仓库级别”配置。如要在其它仓库也能直接使用，可执行全局配置：

```bash
git config --global alias.syncup "!git fetch upstream ; git checkout main ; git merge upstream/main ; git push origin main"
git config --global alias.syncup-rebase "!git fetch upstream ; git checkout main ; git rebase upstream/main ; git push origin main"
```
