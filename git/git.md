# Git 完全指南

## 基础概念

### Git是什么
Git是一个分布式版本控制系统，用于跟踪文件的变化，协调多人开发工作。主要特点：
- 分布式系统：每个开发者都拥有完整的代码仓库副本
- 强大的分支管理：支持多分支并行开发
- 数据完整性：使用SHA-1哈希算法确保数据完整性

### Git的三个区域
1. 工作区（Working Directory）：当前正在编辑的文件区域
2. 暂存区（Staging Area）：临时存储准备提交的修改
3. 版本库（Repository）：存储所有提交的历史版本

## 基本操作

### 仓库初始化和配置
```bash
# 初始化新仓库
git init
# 使用场景：开始一个新项目时，在项目根目录执行
# 注意：确保在正确的目录下初始化，避免在父目录初始化

# 配置用户信息
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
# 使用场景：首次安装git或在新电脑上使用git时
# 注意：公司电脑要使用公司邮箱，个人电脑使用个人邮箱

# 克隆远程仓库
git clone <仓库地址>
# 使用场景：加入新项目团队，需要获取现有项目代码
# 注意：确保有仓库访问权限，注意克隆时的网络环境
```

### 文件操作
```bash
# 查看文件状态
git status
# 使用场景：查看哪些文件被修改，确认当前工作区状态
# 注意：养成经常使用此命令的习惯，避免遗漏文件

# 添加文件到暂存区
git add <文件名>
git add .  # 添加所有修改
# 使用场景：完成一个功能后，准备提交相关文件
# 注意：使用 git add . 前先用 git status 确认，避免提交不必要的文件

# 提交更改
git commit -m "feat: 添加登录功能"
# 使用场景：完成一个独立的功能或修复后提交
# 注意：
# 1. 提交信息要清晰明确，遵循提交规范
# 2. 一个提交只包含相关的改动，不要把不相关的改动混在一起
```

### 分支管理
```bash
# 创建并切换到新分支
git checkout -b feature/login
# 使用场景：开始开发新功能时
# 注意：
# 1. 分支名要符合团队规范
# 2. 确保是从正确的基础分支创建新分支

# 合并分支
git merge feature/login
# 使用场景：功能开发完成，需要合并到主分支
# 注意：
# 1. 合并前先更新目标分支
# 2. 解决冲突时需要与相关开发者沟通
```

### 远程仓库操作
```bash
# 推送到远程
git push origin feature/login
# 使用场景：完成功能开发，需要推送到远程仓库
# 注意：
# 1. 推送前先pull更新
# 2. 确保本地提交都经过测试
# 3. 不要强制推送(force push)到公共分支

# 拉取远程更新
git pull origin develop
# 使用场景：开始工作时同步最新代码
# 注意：
# 1. 有本地修改时先stash或commit
# 2. 解决冲突时需要谨慎
```

### 提交git时忽略指定文件或文件夹
> 创建.gitignore文件，在文件中指定要忽略的文件或文件夹

常见的.gitignore配置：
```plaintext
# 忽略所有.log文件
*.log

# 忽略node_modules目录
node_modules/

# 忽略build目录
build/

# 忽略.env文件
.env

# 忽略但保留目录
!important.log
```

### 撤销操作

#### reset命令
```bash
# 软重置
git reset --soft HEAD~1
# 使用场景：提交后发现漏掉了某些文件，需要重新提交
# 注意：只能在未推送到远程仓库时使用

# 硬重置
git reset --hard HEAD~1
# 使用场景：完全放弃最近的提交，回到上一个版本
# 注意：
# 1. 使用前确保要丢弃的修改确实不需要
# 2. 已推送到远程的提交慎用hard reset
```

#### 其他撤销命令
```bash
# 撤销某次提交（创建新的提交来撤销更改）
git revert <commit>

# 查看操作历史
git reflog

# 丢弃工作区的��改
git checkout -- <文件名>
# 或使用新命令
git restore <文件名>

# 取消暂存
git restore --staged <文件名>
```

### 储藏（Stash）
```bash
# 储藏当前修改
git stash save "正在开发的登录功能"
# 使用场景：
# 1. 正在开发新功能时突然需要修复线上bug
# 2. 切换分支前临时保存工作进度
# 注意：
# 1. 给stash添加清晰的描述
# 2. 及时处理stash的内容，避免遗忘

# 应用储藏
git stash pop
# 使用场景：修复完bug后，继续之前的开发
# 注意：pop后可能产生冲突，需要解决
```

## 高级特性

### 标签管理
```bash
# 创建标签
git tag <标签名>

# 创建带注释的标签
git tag -a <标签名> -m "标签说明"

# 查看标签
git tag

# 删除标签
git tag -d <标签名>
```

### 子模块
```bash
# 添加子模块
git submodule add <仓库地址> <路径>

# 更新子模块
git submodule update --init --recursive
```

## 最佳实践

### 提交规范
建议使用统一的提交信息格式：
```
type(scope): subject

body

footer
```
常用的type：
- feat: 新功能
- fix: 修复bug
- docs: 文档更新
- style: 代码格式修改
- refactor: 重构
- test: 测试用例修改
- chore: 构建过程或辅助工具的变动

### 分支管理策略
推荐使用GitFlow工作流：
- master: 主分支，用于产品发布
- develop: 开发分支
- feature/*: 功能分支
- release/*: 发布分支
- hotfix/*: 紧急修复分支

## 实际工作流程示例

### 开发新功能
```bash
# 1. 确保当前分支是最新的
git checkout develop
git pull origin develop

# 2. 创建功能分支
git checkout -b feature/user-login

# 3. 开发过程中定期提交
git add .
git commit -m "feat: 完成登录表单界面"

# 4. 开发中途需要切换到其他分支
git stash save "登录功能开发到一半"
git checkout hotfix/bug-123
# 处理完bug后
git checkout feature/user-login
git stash pop

# 5. 完成功能后合并到开发分支
git checkout develop
git pull origin develop
git merge feature/user-login
git push origin develop
```

## 常见工作场景示例

### 代码review后的修改流程
```bash
# 1. 查看当前分支的修改
git diff

# 2. 针对review意见修改代码后
git add .
git commit --amend
# 使用场景：在原有提交上追加修改，避免产生多个提交记录
# 注意：已推送到远程的提交慎用amend

# 3. 如果需要强制推送
git push origin feature/login -f
# 注意：强制推送前确保没有其他人基于此分支开发
```

### 紧急修复线上bug流程
```bash
# 1. 从主分支创建热修复��支
git checkout master
git checkout -b hotfix/critical-bug

# 2. 修复bug并提交
git commit -m "fix: 修复关键性bug"

# 3. 合并到主分支和开发分支
git checkout master
git merge hotfix/critical-bug
git push origin master

git checkout develop
git merge hotfix/critical-bug
git push origin develop

# 4. 删除热修复分支
git branch -d hotfix/critical-bug
```

### 版本发布流程
```bash
# 1. 创建发布分支
git checkout develop
git checkout -b release/v1.0.0

# 2. 修复发布相关问题
git commit -m "chore: 更新版本号"

# 3. 合并到主分支和开发分支
git checkout master
git merge release/v1.0.0
git tag -a v1.0.0 -m "发布1.0.0版本"
git push origin master --tags

git checkout develop
git merge release/v1.0.0
git push origin develop
```

### 代码回滚场景

#### 回滚单个文件
```bash
# 查看文件历史
git log --follow filename.js
# 使用场景：需要了解文件的修改历史

# 回滚单个文件到指定版本
git checkout <commit_hash> filename.js
git commit -m "revert: 回滚filename.js到之前版本"
# 注意：确保只回滚需要的文件，避免影响其他文件
```

#### 回滚整个分支
```bash
# 使用revert回滚（推荐）
git revert <commit_hash>
# 使用场景：需要撤销某次提交，但保留提交历史
# 注意：可能需要解决冲突

# 使用reset回滚（谨慎使用）
git reset --hard <commit_hash>
git push -f origin branch-name
# 使用场景：需要完全删除某些提交记录
# 注意：这会改变git历史，团队其他成员需要强制更新
```

### 多人协作场景

#### 合并其他人的修改
```bash
# 1. 更新远程分支信息
git fetch origin
# 使用场景：获取其他人的最新修改
# 注意：fetch不会自动合并

# 2. 查看变更
git log origin/feature/login
# 使用场景：了解其他人的修改内容

# 3. 合并修改
git merge origin/feature/login
# 注意：合并前先提交或储藏本地修改
```

#### 解决复杂冲突
```bash
# 使用图形化工具解决冲突
git mergetool
# 使用场景：复杂冲突需要可视化对比

# 放弃合并
git merge --abort
# 使用场景：合并产生严重问题需要重新开始
# 注意：确保重要修改已备份
```

### 维护技巧

#### 仓库清理
```bash
# 清理无用的远程分支引用
git remote prune origin
# 使用场景：清理已删除的远程分支记录

# 清理大文件历史
git filter-branch --force --tree-filter 'rm -f path/to/large/file' HEAD
# 使用场景：需要从git历史中完全删除大文件
# 注意：这会改变所有提交历史，需要团队协调
```

#### 性���优化
```bash
# 压缩仓库
git gc
# 使用场景：仓库体积变大，需要优化存储

# 查找大文件
git rev-list --objects --all | grep -f <(git verify-pack -v .git/objects/pack/*.idx | sort -k 3 -n | tail -10 | awk '{print$1}')
# 使用场景：排查仓库体积过大的原因
```

## 安全建议

1. 避免提交敏感信息
2. 使用.gitignore忽略敏感文件
3. 定期备份仓库
4. 谨慎使用force push
5. 为重要分支设置保护规则

## 工具推荐

1. GUI客户端
   - SourceTree
   - GitKraken
   - GitHub Desktop

2. IDE插件
   - VS Code的Git插件
   - IntelliJ的Git集成

3. 命令行增强
   - Oh My Zsh的git插件
   - Git Bash

## Git进阶技巧

### 高级日志查看
```bash
# 查看指定作者的提交
git log --author="用户名"
# 使用场景：查看团队成员的贡献记录

# 查看某个时间段的提交
git log --since="2024-01-01" --until="2024-03-01"
# 使用场景：统计某个时期的开发进度

# 图形化显示分支历史
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
# 使用场景：直观查看分支合并历史
```

### 补丁管理
```bash
# 创建补丁
git format-patch -1 <commit_hash>
# 使用场景：需要将改动发送给其他开发者审查

# 应用补丁
git apply patch_name.patch
# 使用场景：在不同仓库间转移改动
# 注意：应用前先测试补丁是否可用
git apply --check patch_name.patch
```

### 二分查找Bug
```bash
# 开始二分查找
git bisect start

# 标记当前版本有问题
git bisect bad

# 标记最后一个正常版本
git bisect good <commit_hash>

# 测试完当前版本后标记
git bisect good  # 或 git bisect bad

# 完成查找后退出
git bisect reset
# 使用场景：定位引入bug的具体提交
```

### 工作流程进阶

#### 功能开发最佳实践
```bash
# 1. 从最新develop创建功能分支
git checkout develop
git pull --rebase origin develop
git checkout -b feature/new-feature

# 2. 定期与develop同步
git fetch origin develop
git rebase origin/develop
# 注意：rebase可能需要解决冲突

# 3. 在提交PR前压缩提交
git rebase -i HEAD~<提交数量>
# 使用场景：整理提交历史，使之更清晰
```

#### 复杂合并策略
```bash
# 使用rebase合并
git checkout feature/branch
git rebase develop
# 使用场景：保持线性提交历史
# 注意：只对未推送到远程的分支使用rebase

# 挑选指定提交合并
git cherry-pick <commit_hash>
# 使用场景：只需要某个分支的特定改动
```

### 配置管理

#### 别名配置
```bash
# 配置常用命令别名
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status

# 配置复杂命令别名
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

#### 钩子脚本
```bash
# pre-commit钩子示例（.git/hooks/pre-commit）
#!/bin/sh
npm run lint
npm run test

# 使用场景：
# 1. 提交前代码检查
# 2. 运行测试用例
# 3. 格式化代码
```

### 团队协作规范

#### 分支命名规范
```
feature/    # 新功能分支
├── user-login
├── payment-integration
└── api-optimization

bugfix/     # 问题修复分支
├── login-validation
└── memory-leak

hotfix/     # 紧急修复分支
└── security-vulnerability

release/    # 发布分支
└── v2.1.0
```

#### 提交信息模板
```bash
# 配置提交模板
git config --global commit.template ~/.gitmessage

# ~/.gitmessage 内容示例
type(scope): subject

# 问题描述
[问题描述]

# 解决方案
[解决方案]

# 副作用
[可能的副作用]

# 关联问题
Issue #123
```

### 性能调优

#### 大仓库优化
```bash
# 只克隆最近的历史
git clone --depth 1 <仓库地址>
# 使用场景：仓库历史太大，只需要最新代码

# 稀疏检出
git sparse-checkout set <目录路径>
# 使用场景：只需要仓库中的特定目录

# 配置文件压缩
git config --global core.compression 9
# 使用场景：优化网络传输性能
```

#### 自动化脚本
```bash
#!/bin/bash
# 自动清理脚本示例
git fetch -p  # 清理远程分支引用
git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -D  # 清理已删除的远程分支对应的本地分支
git gc --aggressive  # 压缩仓库
```

### Git与CI/CD集成

#### GitHub Actions配置
```yaml
# .github/workflows/main.yml
name: CI/CD Pipeline

on:
  push:
    branches: [ master, develop ]
  pull_request:
    branches: [ master, develop ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0  # 获取完整历史用于版本比较
    
    - name: 运行测试
      run: |
        npm install
        npm test
        
    - name: 构建应用
      if: github.ref == 'refs/heads/master'
      run: npm run build
```

#### GitLab CI配置
```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

test:
  stage: test
  script:
    - npm install
    - npm test
  only:
    - master
    - develop
```

### Git高级操作技巧

#### 交互式暂存
```bash
# 交互式添加文件
git add -i
# 使用场景：从同一个文件中选择性地暂存部分修改

# 交互式暂存补丁
git add -p
# 使用场景：精确控制要提交的代码块
# 注意：确保每个代码块的完整性
```

#### 历史修改
```bash
# 修改最近的提交信息
git commit --amend --author="新作者名 <新邮箱>"
# 使用场景：修正作者信息

# 重写提交历史
git rebase -i HEAD~3
# 命令说明：
# p, pick = 使用提交
# r, reword = 使用提交，但修改提交信息
# e, edit = 使用提交，但停下来修改
# s, squash = 使用提交，但合并到前一个提交
```

### Git工作流最佳实践

#### 代码审查流程
```bash
# 1. 创建功能分支前
git checkout -b feature/new-feature origin/develop
git pull --rebase

# 2. 提交代码审查前
git fetch origin develop
git rebase origin/develop
git push origin feature/new-feature

# 3. 代码审查后的修改
git add .
git commit --fixup HEAD
git rebase -i --autosquash HEAD~2
```

#### 发布流程管理
```bash
# 1. 创建发布分支
git checkout -b release/2.0.0 develop

# 2. 版本号更新
npm version 2.0.0
git add package.json
git commit -m "chore: bump version to 2.0.0"

# 3. 合并到主分支
git checkout master
git merge --no-ff release/2.0.0
git tag -a v2.0.0 -m "Release version 2.0.0"

# 4. 同步回开发分支
git checkout develop
git merge --no-ff release/2.0.0
```

### 高级故障排除

#### 丢失提交恢复
```bash
# 查找所有操作历史
git reflog
# 使用场景：找回误删的提交或分支

# 恢复已删除的分支
git checkout -b recover-branch <commit-hash>
# 使用场景：恢复误删的分支

# 从对象库中恢复文件
git fsck --lost-found
# 使用场景：恢复已删除的文件
```

#### 性能问题诊断
```bash
# 检查仓库大小
git count-objects -vH
# 使用场景：诊断仓库体积问题

# 查找大文件历史
git rev-list --objects --all | \
    git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
    sed -n 's/^blob //p' | \
    sort -k2nr | \
    head -10
# 使用场景：找出历史中的大文件
```

### 高级配置技巧

#### 自定义合并策略
```bash
# 配置默认合并策略
git config --global merge.defaultToUpstream true

# 设置特定文件的合并驱动
git config merge.ours.driver true
# 使用场景：特定文件总是保留本地版本
```

#### 工作区定制
```bash
# 配置文件权限
git config core.fileMode false
# 使用场景：在不同操作系统间协作

# 配置行尾符号
git config --global core.autocrlf input
# 使用场景：跨平台开发时的换行符处理
```

### 安全最佳实践

#### 敏感信息保护
```bash
# 使用git-secrets防止敏感信息提交
git secrets --install
git secrets --register-aws

# 配置全局钩子模板
git config --global init.templateDir ~/.git-templates
git config --global core.hooksPath ~/.git-templates/hooks
```

#### 签名验证
```bash
# 配置GPG签名
git config --global user.signingkey <GPG-KEY-ID>
git config --global commit.gpgsign true

# 创建签名的标签
git tag -s v1.0.0 -m "Signed release 1.0.0"
```