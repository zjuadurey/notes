# 区分 GitHub 与 Overleaf 的 Git 使用方式

本项目里有两个独立 Git 仓库：

- `~/QuantumComputing/`：外层代码仓库，推送到 GitHub
- `~/QuantumComputing/EuorSys/26_FailureOps/paper/`：论文仓库，推送到 Overleaf

二者不会冲突。关键规则是：在哪个目录执行 Git 命令，就操作哪个仓库。

## 判断当前操作的是哪个仓库

查看 GitHub 仓库：

    git -C ~/QuantumComputing status
    git -C ~/QuantumComputing remote -v

查看 Overleaf 论文仓库：

    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper status
    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper remote -v

GitHub 仓库的 remote 应该是 `origin`，指向 GitHub。

Overleaf 仓库的 remote 应该是 `overleaf`，指向：

    https://git.overleaf.com/6a02e6447e7eb81b976a1766

## 推送论文到 Overleaf

只在 `paper/` 仓库中操作：

    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper pull --rebase overleaf master
    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper add .
    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper commit -m "update paper"
    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper push overleaf HEAD:master

Overleaf 的远端分支固定是 `master`，所以推送时使用：

    git push overleaf HEAD:master

## 从 Overleaf 拉取论文

    git -C ~/QuantumComputing/EuorSys/26_FailureOps/paper pull --rebase overleaf master

这只会影响 `paper/` 目录，不会影响外层 GitHub 仓库。

## 推送代码到 GitHub

代码在外层仓库中提交和推送：

    git -C ~/QuantumComputing pull --rebase origin main
    git -C ~/QuantumComputing add EuorSys/26_FailureOps/
    git -C ~/QuantumComputing commit -m "update failureops code"
    git -C ~/QuantumComputing push origin main

如果 GitHub 主分支是 `master`，把 `main` 改成 `master`。

## 避免误提交论文仓库

外层 GitHub 仓库的 `.gitignore` 中应忽略 Overleaf 论文目录和备份目录：

    EuorSys/26_FailureOps/paper/
    EuorSys/26_FailureOps/paper_backup_before_overleaf_push/
    EuorSys/26_FailureOps/paper_old_messy_git/
    EuorSys/26_FailureOps/_archive/

这样在 `~/QuantumComputing` 中执行 `git add .` 时，不会把 Overleaf 论文仓库加入 GitHub。

## 核心规则

- 论文：只在 `~/QuantumComputing/EuorSys/26_FailureOps/paper/` 中操作，推到 Overleaf。
- 代码：只在 `~/QuantumComputing/` 中操作，推到 GitHub。
- 推 Overleaf：`git push overleaf HEAD:master`
- 推 GitHub：`git push origin main`
- 不要把代码、缓存、数据文件放进 Overleaf 论文仓库。