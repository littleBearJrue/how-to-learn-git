# git的基本使用和优化配置

## git的安装

[官网下载](https://git-scm.com/downloads)



## 可视化工具

1. [GitHub for Desktop](https://desktop.github.com/)
2. [Source Tree](https://www.sourcetreeapp.com/)
3. [TortoiseGit](https://tortoisegit.org/)（推荐使用）

### git的理解

#### 相较于SVN

1. SVN集中式的版本控制系统，需要一台中央服务器，且需要联网操作，既然是联网操作，那注定会受到网络贷款的影响，且一旦中央服务器宕机，那结果是很可怕的。

2. git作为分布式版本控制系统的佼佼者，其相对于集中式更为安全可靠，每个人的电脑都可充当中央服务器，每个人的电脑都有保留一份完整的版本库，期间可不联网操作，只需要本地作为服务器进行版本控制，一旦需要交换每个人的修改时，只需要把各自的修改推送给对方即可。

3. 当然分布式版本控制系统也会引入一个“中央服务器”的概念，但仅作为彼此交换修改的桥梁。

   #### 本身对git的理解

   git存在着工作区、暂存区和本地master分支和一个Head指针的概念

   1. 工作区：即为电脑里所创建的一个目录，对于git所在的目录来说就是一个工作区
   2. 暂存区：叫index,通俗讲就是作为临时存储的地方，我们每次执行add命令，其实就是讲工作区修改的文件添加到暂存区去了
   3. master分支：我们在初始化一个git版本库时，就会同时创建了一个master分支。我们每次执行commit命令的时候，其实就是讲暂存区的所有暂存的文件更改提交到master分支上。且存在Head指针，确定着master分支目前所处在版本号上。

   ![版本库git理解](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

## git的配置

打开git bash ，对git实现全局的用户配置，如下：

```
git config --global user.name "用户名"
git config --global user.email "电子邮箱" 
```

用户名和邮箱是作为分布式版本管理系统对当前操作用户的唯一标识。

此时便会在用户目录下(C:\用户\xxx)生成一份git的用户配置表为.gitconfig。之后我们对git的全局配置的修改都会体现在此文件中。

### git命令行缩写配置

同样找到.gitconfig文件，添加如下：

```
[alias]  
    co = checkout  
    cm = commit  
    st = status  
    pl = pull  
    ps = push  
    cp = cherry-pick  
    ca = commit -a  
    b = branch
```

当然也可以用命令行实现全局配置：

```
git config --global alias.st status  //对status命令行的缩写
git config --global alias.co checkout  //对checkout命令行的缩写
git config --global alias.cm commit    //对commit命令行的缩写
git config --global alias.br branch    //对branch命令行的缩写
```

此后在敲命令行的时候只需要敲前面的缩写部分就好了，减少记忆度。

### git的基本实操

1. 初始化一个版本库
   ```
   git init
   ```

2. 将本地创建的版本库与远程服务器关联
   ```
   git remote add origin xxx
   ```

3. 从远程服务器拉取版本库
   ```
   git clone xxxx 
   ```

4. 上传到文件更改到暂存区
   ```
   git add xxxx
   git add . // 上传工作区所有的修改文件
   ```

5. 将暂存区的所有修改提交到master分支
   ```
   git commit -m "xxxx"
   git commit --amend  //修改最近的一次提交的内容
   ```

6. 查看当前仓库中文件的状态
   ```
   git status
   ```

7. 查看文件的提交历史
   ```
   git log
   git log --oneline //一行显示每个提交的内容
   ```

8. 提交本地代码到远程服务器
   ```
   git push origin master // master为提交到远程所在的master分支上
   ```

9. 同步远程服务器最新代码到本地
   ```
     git pull origin master
   ```

10. 查看版本的改动内容
    ```
     git diff xxx // 工作区和暂存区的文件比较
     git diff HEAD xxx  // 工作区与当前master分支最新一次提交的文件的比较
     git diff commitId xxx // 工作区与当前master分支上对于的commitId提交内容比较
       
     git diff --cached xxx // 暂存区与最新本地master分支上的内容的比较
     git diff commitId1 commitId2  // master分支上两个commitId的文件内容的比较
    ```

11. 对已提交到本地master分支上的回退

    ```
    git reset --hard HEAD  // 回退到master分支上最新的版本
    git reset --hard HEAD^  // 回退到master分支上一个版本
    git reset --hard HEAD~100  // 回退到master分支上100个版本
    git reset --hard commitId   // 回退到master分支上某个commitId对于的版本上
    
    git reset --soft HEAD  //回退master分支上最新版本，且暂存区保留这份修改
    ```

12. 查看每一次对git的操作命令的记录

    ```
    git reflog
    ```

13. 将暂存区的文件修改撤销掉，放回工作区

    ```
    git reset HEAD xxx 
    git rm --cached xxxx
    ```

14. 撤销工作区文件的修改

    ```
    git checkout -- xxxx
    git checkout .  // 撤销所有工作区文件的修改
    ```

    有两种情况：

    - 对文件做了修改但尚未add到暂存区，此时撤销修改，回到和版本库一模一样的文件内容
    - 对修改的内容add添加到暂存区，且工作区又做了修改的，此时撤销就回到了添加到暂存区后的文件内容

    总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

15. 暂时保留工作区、暂存区的修改

    ```
    git stash
    git stash pop //将保存的记录恢复
    ```

    [更多命令可参考](https://git-scm.com/book/zh/v1/Git-%E5%B7%A5%E5%85%B7-%E5%82%A8%E8%97%8F%EF%BC%88Stashing%EF%BC%89)

16. 查看分支

    ```
    git branch
    git branch --all  //查看分支包括远程分支
    ```

17. 创建分支

    ```
    git branch xxx
    ```

18. 切换分支

    ```
    git checkout xxx
    ```

19. 创建且切换分支同时进行

    ```
    git checkout -b xxx
    ```

20. 合并分支到当前分支

    ```
    git merge xxx
    ```

21. 删除分支

    ```
    git branch -d xxx
    ```

22. 将现有的一个或者多个提交的修改引入当前内容

    ```
    git cherry-pick xxx(xxx为commitId)
    ```



### 重点讲下子模块的实操

### 子模块的概念

#### 什么是Submodule

跟SVN外链的性质是一样的。`git Submodule` 是一个很好的多项目使用共同类库的工具，他允许类库项目做为`repository`,子项目做为一个单独的`git项目`存在父项目中，子项目可以有自己的独立的`commit`，`push`，`pull`。而父项目以`Submodule`的形式包含子项目，父项目可以指定子项目`header`，父项目中会的提交信息包含`Submodule`的信息，再`clone父项目`的时候可以把`Submodule`初始化。

1. 创建子模块
   ```
   git submodule add xxxx
   ```

   执行完此命令后会在父项目下生成一份.gitmodules文件，记录着子模块的本地路径（path）和远程仓库地址（url）等主要信息。

   同时git的版本库中（.git目录）下会生成一份`modules`目录，放着子模块的git版本库。

   以及在config文件下，会添加子模块的配置。

2. 查看当前项目的子模块
   ```
   git submodule
   ```

3. 更新每个子模块代码
   ```
   git submodule foreach git pull
   ```

4. 当克隆包含有子模块的项目时
   第一种方案：
   ```
   git clone --recursive xxx （xxx 项目路径）
   ```
   第二种方案：
   ```  
   git clone xxx
   git submodule init
   git submodule update
   ```
5. 删除子模块
   - 移除.gitmodules中要删除的子模块
   - 删除子模块目录
   - 删除.git版本库下的modules目录对应的子模块版本库
   - 修改.git版本库下config对子模块的配置
   - 提交所有修改内容

   注意：这里有个注意的地方，就是我们克隆了包含子模块的项目后，通过命令行进入子模块，发现HEAD并没有指向master分支，而是出于游离指针的状态，此时需要切换到master分支上再做处理。

   但是，我们忘记了此操作且一直在这个游离分支下做了一系列的操作，最后发现你是提交不了代码的，因为此时远程仓库跟本地服务器仓库做校验时，发现版本号是一样的，并没有东西存在修改和更新。此时我们切换回master分支上，会发现我们刚才提交的内容全都没了，很正常，因为你的修改一直都没在master分支上，那这样我们就得将之前的修改copy一份到master上了。此时`git cherry-pick`就派上用场了。找到之前在游离分支上提交的commitId，在master分支上执行`git cherry-pick commitId`即可。