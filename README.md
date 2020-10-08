# GIT

## 基础与概念

### 版本管理系统类型

- 中心化
- 分布式

### 使用方式

- command line
- GUI
  - VS Code Plugin
    - gitlens

### 安装

- command line
  - [for windows](www.gitforwindows.org)

### 配置

- 基本配置

  - 名字
  - 邮箱
  - 默认编辑器
  - Line Ending

- 级别

  - system (for all users)
  - global (for all repos for current user)
  - local (current repo)

- 案例

  - 配置默认的编辑器

    `git config --global core.editor "code --wait"`

  - 编辑配置文件

    `git config —-global -e`

  - LF 跨平台配置

    - autocrlf = true // windows
    - autocrlf = input // mac

  - Help
    - `git config -h`

## 基本命令

### command line

- style
  - mac
    - zsh with git plugin
  - windows
    - posh-git

### workflow

> commit

- working area

- staging area

- snapshot

### commands

- status -s

  | 文件名     | staging | working |
  | ---------- | :-----: | :-----: |
  | file1.txt  |    A    |    M    |
  | file2.txt  |    A    |         |
  | file11.txt |    ?    |    ?    |

- 跳过 staging area

  `git commit -a -m 'message'`

- 显示 staging area 的文件

  `git ls-files`

- 移除文件

  `git rm file-name`

- rename 文件

  `git mv old-file-name new-file-name`

- 先提交忽略文件再修改.gitignore

  `git rm --cached file-name`

- diff 命令 对比 working 和 staging

  `git diff`

- diff 命令 对比 staging 和 snapshot

  `git diff --staged`

- difftool 命令

  `git difftool --staged`

- log reverse

  `git log --oneline --reverse`

### commit 最佳实践

- xs, m, xl

- commit often

- 每一个 commit 是一个 逻辑单位

- 有意义的 message

### .gitignore
