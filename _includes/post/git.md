

# 使用Git来管理你的工程



## 为甚？

在你学习计算机的时候，你是否会有这样的经历，或者这样的需求？

我们写了一个小项目，然后做了一些改动，然后发现这些改动影响我的工程不能正常工作了，那么怎么办呢，可能需要回退一下，但是期间你修改了好多个文件了，一个一个手动回退？手动删除？我们能确定删除的是之前编辑的吗？能确定删除到位了吗？似乎都不能。



## 解决

此时此刻似乎觉得我的医保卡不保，面对这样一个复杂的问题，就感觉和上帝对线一样，必须要万分小心。那么此时此刻就需要有一个工具，不但功能强大（肉的一批）而且易于使用（伤害还高），那么我们今天介绍的这个工具就是git，这是LINUX开发过程产生的版本管理工具，有的人一听到LINUX就合不拢腿，可想而知，git的版本管理，是多么强大，现在有很多人在用，那么也是十分流行。

话不多说，好的我们进入操作画面。



## 操作，按照应用场景

#### 仓库

仓库可以从远端获取，也可以从本地构建，这里我们使用这个仓库作为远端拉取演示 https://github.com/zhuiwang/python_work

- 本地构建 `git init`
- 远端获取 `git clone https://github.com/zhuiwang/python_work.git`

一般我们使用`master`这个分支名作为主分支，可以使用`git branch`

#### 查看设定信息

- 查看所有设定包括 `user.name` `user.email`

  - `git config  --global -l`
  - `git config --global user.name <yournam>`   exp `git clonfig --global user.name fivefiveopen`
  - `git config --global user.email <your-email>` exp `git clonfig --global user.name fivefiveopen@gmail.com`

- 查看远端 url 链接，该url链接可以是 https,git还可以是,ssh

  - `git remote -v`

    ```
    admin@workstation:/data/sonic-master-compile$ git remote -v
    local	/data/git/repo/sonic-local-repo.git (fetch)
    local	/data/git/repo/sonic-local-repo.git (push)
    origin	ssh://git@git.github.cn:7999/sonic/sonic-buildimage.git (fetch)
    origin	ssh://git@git.github.cn:7999/sonic/sonic-buildimage.git (push)
    sshurl  user@192.168.10.111:/data/git/repo/sonic-local-repo.git (fetch)
    sshurl  user@192.168.10.111:/data/git/repo/sonic-local-repo.git (push)
    ```

    表示此仓库有三个远端库`remote repository`，分别为`local` `origin` `sshurl`,其中 `origin` 为默认拉取的远端链接。
    
    **sshurl  user@192.168.10.111:/data/git/repo/sonic-local-repo.git (fetch)**
    **sshurl  user@192.168.10.111:/data/git/repo/sonic-local-repo.git (push)**
    
    

#### `checkout`分支切换

- 创建新分支 `git checkout -b 201909` 

  创建新的分支`branch` 名为"`201909`",

- 切换分支 `git checkout master`

  切换分支切换到原来的`master`分支

#### `pull`分支拉取

- 我们可以通过`git remote -v `查看远端的分支情况，如果是从远端`clone`下来会有一个remote repository git server的链接名`origin`，当然我们也可以添加其他远端的仓库`git remote add  <repo_name> <repo_url>`  
  - `git remte add official https://github.com/zhuiwang/python_work.git`添加一个名叫official的remote repository git server ，official可以自己命名
- 知道了有哪些repo可以供获取可以使用`git pull <repo_name>`来获取repo中的branch
- 拉取相关的远端分支，`git checkout <remote_branch> -b <new_local_branch_name>`

#### `commit`本地提交

我们可以使用`git log`查看以往的提交日志，当我们对git跟踪的文件进行修改后，可以使用`git status`查看当前的文件状态，看看那些文件是被修改，那些文件是已经`stage`存储，那些文件是被`modify`修改的。当文件修改完毕后，可以通过`git diff <file_name>` ,`<file_name>`可以使用表达式来匹配文件。比如`*`表示当前目录所有文件以及子文件夹文件。确认所有的提交无误，进行提交步骤：

- `git add <file_name>`
- `git commit -s` -s表示签名，会进入编辑器，`git config core.editor vim`可以设定编辑器为vim，或者`git commit -m "<commit message>"`

#### `stash`本地储藏

如果再切换分支，你希望将本地改动保存，可以使用`git stash`将本地工作保存到储藏中，可以通过`git stash list`查看储藏的文件`git stash apply`去将储藏恢复到工作区

#### `rebase`提交重建

- 重写HEAD提交，如果只是希望改写HEAD的commit信息，可以通过 `git commit --amend`来进入编辑器进行修改。
- 将之前的n次提交合并到一次提交，`git rebase -i HEAD~n` 进入vim 修改除了第一行的前面的**英文单词**或者其首字母既可以执行想应的功能。例如将`pickup`改为`f`表示`fixup`也就是修正,会丢掉该次提交的commit信息，但是此次提交对文件的修改依然保存。

#### `merge`分支合并

- 假设本地创建了一个工程，默认为`master`分支，在此基础上，你想添加一个`feature`但是这个`feature` 开发量比较大，或者修改一个`bug`这个工作量也比较大，不是一次`commit`提交能够解决的，因此你需要创建`checkout -b`一个新的分支`201909`，在经历了一段时间的开发，你完成了`201909`分支的开发，现在你想将`201909`**所有改动**合并到master分支上去，这个时候使用`merge`操作，在你修改`201909`分支的时候`master`也会有别人或者自己修改的提交`commit`，如果分支`201909`和`master`冲突，就可以直接`merge`完成，但是如果，`201909`和`master`对相同文件的相同部分做了修改，git无法判断保留那个，就需要手动修改矛盾的部分，然后再进行提交`commit`

  - 将`201909`所有修改合并`merge`到`master`;

    - step1：切换到`master`分支`git checkout master`

    - step2：合并分支到`master` ，`git merge 201909`

    - 可以加参数如下，具体含义后续再说

      ```
      wangzhui@workstation:/data/sonic-master-compile$ git merge origin/vlag_0809 --
      --abort                  --gpg-sign               --no-log                 --no-verify-signatures   --stat 
      --commit                 --log                    --no-progress            --progress               --strategy 
      --edit                   --no-commit              --no-rerere-autoupdate   --quiet                  --verbose 
      --ff                     --no-edit                --no-squash              --rerere-autoupdate      --verify-signatures 
      --ff-only                --no-ff                  --no-stat                --squash  
      ```

- 假设你再`master`只想合并`201909`的**部分提交**，那么可以使用`git cherry-pick <commit-id>`，它会将该次commit的所有修改合并到master，保留commit信息，但是和合并到`master`的commit id会变化。

  

## 操作，按照区域

有一下分区名词需要记住，暂存区`statsh` 工作区`workspace` 索引`index`本地库`local repository`远端库`remote/upstream repository`

#### 工作区

##### 从工作区存储到其他地方

- `push` 到远端

##### 从其他地方恢复到工作区

未完待续... ...



------
- 创作不易转载请发邮件 wangzhui@foxmail.com 
- Copyright © 蘭亭 2019 Auther by www.wangzhui.site