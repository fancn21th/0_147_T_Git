# GIT

## data model

### tree / blob

```
.(root)
├── css                      # 文件夹 / tree
│   └── main.css             # 文件 / blob
├── js                       # 文件夹 / tree
│   ├── vendor               # 文件夹 / tree
│   │   └── jquery.js        # 文件 / blob
│   └── app.js               # 文件 / blob
└── index.html               # 文件 / blob
```

### commits

```
  (foo) <--- (bar) <--- (feature) <---- (feature + bugfix)
               ^                         |
               └──---- (bugfix)   <------|
```

### commit meta data

- commit
  - author
  - message

### low level model

- 伪代码

  ```
    type blob = array <byte>

    type tree = map <string, tree | blob>

    type commit = struct {
      parents: array <commit>
      author: string
      message: string
      snapshot: tree
    }
  ```

  ```

    // how git store blob | tree | commit

    type object = blob | tree | commit

    objects = map <string, object>

  ```

  ```
    // how git store in 伪代码
    // hash of commit

    def store(o)
      id = sha1(o)
      objects[id] = o

    def load(id)
      return objects[id]

  ```

  ```
    // refs

    references = map <string, string>

    // string 1 is message
    // string 2 is hash
    // references are immutable

  ```

## commands

> 所有的命令 都是 操作 refs 或者 objects

### local

> 绘制 commits 流

- git init

- git cat-file -p [hash]

- HEAD

  - is an reference
  - 一般而言是最后一次 commit / snapshot

- git checkout [hash] | [branch name]

  - 在不同 commit 之间游走
  - 移动 HEAD
  - 修改工作区文件
    - ⚠️ 警告 如果有没有跟踪的修改文件
  - 向回拷贝!

- git diff [hash from] [hash to] [file name] \*\*
  - 默认与 HEAD 比较

### branch

> 使用 js 文件来演示 不同 branch 的不同 功能 例如输出

- git checkout [filename]

  - 放弃修改

- git branch [branch name]

  - branch name is an reference
  - 注意 不同的 commit 指向 相同的 commit | snapshot \*\*
  - 关注 HEAD 的变化 以及 branch 的指向变化

- git checkout -b [branch name]

  - 等于 git branch [branch name] ; git checkout [branch name]

- 关注 log 中分支的 显示形式

- git merge

  - git merge branch A
    - Fast-forward \*\* // 聪明的实现
  - git merge branch B

- 冲突

  - git mergetool
  - 取消
    - git merge --abort
  - 完成
    - git add [conflict file name] \*\* // 注意要先 add ?
    - git merge --continue

### remote

> 使用 两个 console 演示不同的 repos

- remote init

  - git init --bare

- remote add

  - git remote add [name] [url | folder path]

- push

  - git push <remote name> <local branch name>:<remote branch name>

- clone

  - git clone [url | folder path] [folder name]

- git branch -u [branch]

  > checkout h

  - git branch -u [remote name/branch name]

- git fetch [remote name]

- git pull
  - 等于 git fetch; git merge
