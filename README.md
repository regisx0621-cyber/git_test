# git_test

这个仓库用于**全面练习与演示 Git 常用操作**以及**GitHub 常用功能**。

## 1. Git 常用操作练习清单

> 建议按顺序练习，每一步都用 `git status` 和 `git log --oneline --graph --decorate -n 10` 观察变化。

### 1.1 基础配置与初始化

```bash
git config --global user.name "your_name"
git config --global user.email "your_email@example.com"
git clone <your_repo_url>
cd git_test
```

### 1.2 文件生命周期

```bash
echo "hello git" > demo.txt
git status
git add demo.txt
git commit -m "feat: add demo.txt"
git rm demo.txt
git commit -m "chore: remove demo.txt"
```

### 1.3 分支与合并

```bash
git switch -c feature/demo-branch
echo "feature work" > feature.txt
git add feature.txt
git commit -m "feat: add feature work"
git switch main
git merge feature/demo-branch
```

### 1.4 变基（rebase）

```bash
git switch -c feature/rebase-demo
echo "rebase line" >> README.md
git add README.md
git commit -m "docs: add rebase line"
git switch main
echo "main line" >> README.md
git add README.md
git commit -m "docs: add main line"
git switch feature/rebase-demo
git rebase main
```

### 1.5 暂存现场（stash）

```bash
echo "wip change" >> wip.txt
git stash push -m "wip: stash demo"
git stash list
git stash pop
```

### 1.6 回滚与修复

```bash
git revert <commit_sha>
git reset --soft HEAD~1
git reset --hard HEAD~1
```

> ⚠️ `reset --hard` 会丢弃工作区修改，练习时请谨慎。

### 1.7 标签与发布

```bash
git tag v0.1.0
git tag -a v0.1.1 -m "annotated tag"
git push origin v0.1.0
```

### 1.8 挑选提交（cherry-pick）

```bash
git cherry-pick <commit_sha>
```

---

## 2. GitHub 常用功能演示清单

### 2.1 Issue 管理
- 创建 Issue（Bug / Feature Request）
- 添加 Label、Assignee、Milestone
- 使用关键字关联 PR（例如：`Closes #1`）

### 2.2 Pull Request 流程
1. 从功能分支推送代码
2. 发起 PR 并填写变更说明
3. 请求 Reviewer
4. 根据 Review Comment 修改并追加提交
5. CI 通过后 Merge

### 2.3 Code Review 常用动作
- 添加行级评论（Line Comment）
- 发起 `Approve` / `Request changes`
- 对评论逐条回复并标记已解决

### 2.4 GitHub Actions（CI）
- 查看 workflow run 状态
- 查看失败 job 日志并定位问题
- 修复后重新触发 workflow

### 2.5 Releases
- 基于 tag 创建 Release
- 填写 Release Notes
- 附件上传（可选）

### 2.6 Discussions / Wiki（可选）
- 使用 Discussions 做问答和提案讨论
- 使用 Wiki 记录项目文档

---

## 3. 推荐完整演练流程（端到端）

1. 新建分支：`git switch -c feature/practice-flow`
2. 修改任意文件并提交：`git commit -m "feat: practice flow step 1"`
3. 推送分支并创建 PR
4. 在 PR 中触发 Review 与 CI
5. 根据反馈再次提交
6. 合并 PR
7. 打 tag 并创建 Release
8. 在 Issue 中验证关闭状态

---

## 4. 常用排查命令速查

```bash
git status
git log --oneline --graph --decorate --all -n 20
git reflog
git diff
git diff --staged
git branch -vv
git remote -v
```
