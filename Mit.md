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

### remote
