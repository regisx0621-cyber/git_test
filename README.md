# git_test

这个仓库用于直接演示 **Git 与 GitHub 常用操作**，并给出一个典型 **C++ GitHub 仓库结构**示例。

## 1. Git 常用操作（命令演示）

### 1.1 初始化与基础配置

```bash
git config --global user.name "your_name"
git config --global user.email "your_email@example.com"
git clone <your_repo_url>
cd git_test
git status
```

### 1.2 提交代码（add / commit）

```bash
echo "hello git" > demo.txt
git add demo.txt
git commit -m "feat: add demo.txt"
git log --oneline -n 5
```

### 1.3 分支开发与合并（branch / merge）

```bash
git switch -c feature/demo
echo "feature line" >> demo.txt
git add demo.txt
git commit -m "feat: update demo in feature branch"
git switch main
git merge feature/demo
```

### 1.4 线性历史（rebase）

```bash
git switch -c feature/rebase-demo
echo "rebase change" >> README.md
git add README.md
git commit -m "docs: rebase demo commit"
git switch main
echo "main change" >> README.md
git add README.md
git commit -m "docs: main branch change"
git switch feature/rebase-demo
git rebase main
```

### 1.5 临时保存工作区（stash）

```bash
echo "wip" >> wip.txt
git stash push -m "wip: temp save"
git stash list
git stash pop
```

### 1.6 回退与恢复（revert / reset / reflog）

```bash
git revert <commit_sha>
git reset --soft HEAD~1
git reflog
```

> `git reset --hard` 会直接丢弃未保存改动，谨慎使用。

### 1.7 标签与发布版本（tag）

```bash
git tag -a v1.0.0 -m "release v1.0.0"
git push origin v1.0.0
git tag --list
```

### 1.8 选择性摘取提交（cherry-pick）

```bash
git cherry-pick <commit_sha>
```

## 2. GitHub 常用操作（流程演示）

### 2.1 Issue 与需求管理

```text
1) 在 GitHub 创建 Issue（Bug / Feature）。
2) 设置 Label、Assignee、Milestone。
3) 在 PR 描述中写 "Closes #<issue_number>" 自动关闭 Issue。
```

### 2.2 Pull Request 协作流程

```bash
git switch -c feature/pr-demo
echo "pr demo" > pr_demo.txt
git add pr_demo.txt
git commit -m "feat: add PR demo file"
git push -u origin feature/pr-demo
```

```text
然后在 GitHub 页面发起 PR，填写变更说明，请求 Review，等待 CI 通过后合并。
```

### 2.3 Code Review 常见动作

```text
- Reviewer: Add comment / Request changes / Approve
- Author: 回复评论，提交修复 commit，再次请求 review
- 合并前确认 conversation resolved + checks passed
```

### 2.4 GitHub Actions（CI）

```text
在 PR 页面查看 Checks：
- 绿色：通过
- 红色：失败，进入对应 job 查看日志并修复后再次 push
```

### 2.5 Release 发布

```text
1) 推送 tag（如 v1.0.0）
2) 在 GitHub Releases 页面创建 release
3) 填写 release notes 并发布
```

## 3. 一个常见的 C++ GitHub 仓库结构

```text
cpp-project/
├─ .github/
│  └─ workflows/
│     └─ ci.yml
├─ include/
│  └─ project/
│     └─ calculator.h
├─ src/
│  ├─ calculator.cpp
│  └─ main.cpp
├─ tests/
│  └─ test_calculator.cpp
├─ docs/
│  └─ design.md
├─ CMakeLists.txt
├─ README.md
├─ LICENSE
└─ .gitignore
```

对应最小 CMake 启动方式通常是：

```bash
mkdir -p build
cd build
cmake ..
cmake --build .
ctest --output-on-failure
```

## 4. Git 与 GitHub 常用知识（简明版）

- Git 是本地版本控制，GitHub 是远程托管与协作平台。
- 日常最常用命令：`status`、`add`、`commit`、`switch`、`merge`、`rebase`、`log`、`diff`。
- 协作主线：Issue -> 分支开发 -> PR -> Review -> CI -> Merge -> Tag/Release。
- 提交信息建议使用清晰前缀：`feat:` `fix:` `docs:` `refactor:` `test:` `chore:`。
- 遇到历史问题先看：`git log --oneline --graph --decorate --all` 与 `git reflog`。
