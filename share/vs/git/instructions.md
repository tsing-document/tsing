# 指令

1.1 获取仓库  
1.2 文件更新到仓库  
1.3 获取提交历史  
1.4 撤销修改  
1.5 远程仓库  
1.6 标签

## 1.1 获取仓库

### 1.1.1 自己创建仓库

初始化后，当前目录中会出现一个.git的目录，所有 Git 需要的数据和资源都存放在这个目录中。

```text
    $ git init
```

和 Git 打个招呼

```text
    # 随便创建一个文件
    # 将文件添加到仓库中
    $ git add .

    # 提交到仓库中
    $ git commit -m "提交代码的信息描述"
```

### 1.1.2 已有仓库

```text
    $ git clone <url>
```

## 1.2 文件更新到仓库

### 1.2.1 已跟踪

已跟踪的文件时本来就被纳入版本控制管理的文件，在上次的快照中有他们的记录，在工作一段时间后，他们的状态可能时未更新，已修改或者放入暂存区。

### 1.2.2 未跟踪

他们既没有上次更新时的快照，也不在当前的暂存区域，初次克隆的仓库，工作目录下的所有文件都是属于已跟踪的文件，并且状态是未修改的状态。

![avatar](./image/1.5.png)

### 1.2.3 检查当前文件的状态

要确定文件在什么状态，可以通过 `git status` 命令查看。下面这个状态说明工作目录中没有任何需要提交的。信息中还说明了你当前所在的分支是 `master`。

```text
        $ git status
            # On branch master
            nothing to commit (working directory clean)
```

### 1.2.4 新建文件

在状态报告中可以看到新建的README文件出现在“Untracked files”下面。未跟踪的文件意味着Git在之前的快照（提交）中没有这些文件；Git 不会自动将之纳入跟踪范围，除非你明明白白地告诉它“我需要跟踪该文件”，因而不用担心把临时文件什么的也归入版本管理。不过现在的例子中，我们确实想要跟踪管理 README 这个文件。

```text
        $ vim README

        $ git status
            # On branch master
            # Untracked files:
            # (use "git add <file>..." to include in what will be committed)
            # README
            nothing added to commit but untracked files present (use "git add" to track)
```

### 1.2.5 跟踪新文件

```text
    # 使用命令 `git add` 跟踪文件
        $ git add README

    # 此时再运行 git status 命令，会看到 README 文件已被跟踪，并处于暂存状态,只要在 “Changes to be committed” 这行下面的，就说明是已暂存状态。

        $ git status
            # On branch master
            # Changes to be committed:
            # (use "git reset HEAD <file>..." to unstage)
            #
            # new file: README
            #
```

### 1.2.6 暂存已修改文件

现在我们修改下之前已跟踪过的文件 benchmarks.rb，然后再次运行 status 命令，会看到这样的状态报告：

```text
   $ git status
    # On branch master
    # Changes to be committed:
    # (use "git reset HEAD <file>..." to unstage)
    #
    # new file: README
    #
    # Changes not staged for commit:
    # (use "git add <file>..." to update what will be committed)
    #
    # modified: benchmarks.rb
    #
```

文件 benchmarks.rb 出现在 “Changes not staged for commit” 这行下面，说明已跟踪文件的内容发生了变化，但还没有放到暂存区。要暂存这次更新，需要运行 git add 命令（这是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等）。现在让我们运行 git add 将 benchmarks.rb 放到暂存区，然后再看看 git status 的输出：

```text
    $ git add benchmarks.rb
    $ git status
        # On branch master
        # Changes to be committed:
        # (use "git reset HEAD <file>..." to unstage)
        #
        # new file: README
        # modified: benchmarks.rb
        #
```

现在两个文件都已暂存，下次提交时就会一并记录到仓库。假设此时，你想要在 benchmarks.rb 里再加条注释，重新编辑存盘后，准备好提交。不过且慢，再运行 git status 看看：

```text
    $ vim benchmarks.rb
    $ git status
        # On branch master
        # Changes to be committed:
        # (use "git reset HEAD <file>..." to unstage)
        #
        # new file: README
        # modified: benchmarks.rb
        #
        # Changes not staged for commit:
        # (use "git add <file>..." to update what will be committed)
        #
        # modified: benchmarks.rb
        #
```

实际上 Git 只不过暂存了你运行 git add 命令时的版本，如果现在提交，那么提交的是添加注释前的版本，而非当前工作目录中的版本。所以，运行了 git add 之后又作了修订的文件，需要重新运行 git add 把最新版本重新暂存起来。

### 1.2.7 忽略某些文件

在 `.gitignore` 文件中过滤掉不需要管理的文件。

```text
# 此为注释 – 将被 Git 忽略
    # 忽略所有 .a 结尾的文件
    *.a
    # 但 lib.a 除外
    !lib.a
    # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
    /TODO
    # 忽略 build/ 目录下的所有文件
    build/
    # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
    doc/*.txt
```

### 1.2.8 提交更新

提交之前确认所有的文件都已经进入暂存区，再执行 `git commit`, 这种方式会唤醒自带的编辑器。也可以使用 `git commit -m "提交的功能描述"`。

### 1.2.9 跳过使用暂存区域

尽管使用暂存区域的方式可以精心准备要提交的细节，但有时候这么做略显繁琐。Git 提供了一个跳过使用暂存区域的方式，只要在提交的时候，给 `git commit` 加上 `-a` 选项，Git 就会自动把所有已经跟踪过的文件暂存起来一并提交。

## 1.3 获取提交历史

使用 `git log` 查看历史，这里不在费用篇章对这个进行描述

## 1.4 撤销修改

### 1.4.1 修改最后一次的提交

使用 `git commit -amend` 可以将提交完成以后发现漏掉了几个文件没有添加，或者提交信息写错的时候。此命令将当前的暂存区域快照提交，如果提交完后没有任何改动，直接运行此命令的话，相当于有机会重新编辑提交说明。启动文本编辑器之后，会看到上次提交时的说明，编辑他确认没问题后保存退出，就会使用新提交的说明并且覆盖掉刚才失误的提交。

### 1.4.2 取消已经暂存的文件

先查看状态，`git status` 给出了结果，使用 `git reset HEAD <文件名>`

```text
    $ git status
        # On branch master
        # Changes to be committed:
        # (use "git reset HEAD <file>..." to unstage)
        #
        # modified: README.txt
        # modified: benchmarks.rb
        #
```

### 1.4.3 取消对文件的修改

使用 `git checkout -- <文件名>` 可以撤销对文件的修改

## 1.5 远程仓库

### 1.5.1 查看当前的远程库

```text
    $ git remote
        origin
```

### 1.5.2 显示对应库的克隆地址

```text
    $ git remote -v
        origin  https://github.com/tsing-dong/tsing.git (fetch)
        origin  https://github.com/tsing-dong/tsing.git (push)
```

### 1.5.3 添加远程仓库

```text
    $ git remote add <url>
```

### 1.5.4 推送数据到远程仓库

```text
    $ git push origin master
```

### 1.5.5 查看远程仓库的信息

```text
    $ git remote show origin
        * remote origin
        Fetch URL: https://github.com/tsing-dong/tsing.git
        Push  URL: https://github.com/tsing-dong/tsing.git
        HEAD branch: master
        Remote branch:
        master tracked
        Local branch configured for 'git pull':
        master merges with remote master
        Local ref configured for 'git push':
        master pushes to master (up to date)
```

## 1.6 标签

### 1.6.1 列出已有的`tag`

```text
    git tag
```

### 1.6.2 新建`tag`

todo: 这个在业务中还没实际的应用，等应用了会将这个补充完整