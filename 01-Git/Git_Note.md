# Git基本操作

### 一、本机配置

1. 添加用户

    ``` 
    git config –global user.name “XX” 
    git config –gloaba user.email “XX@163.com”
    ```

2. 查看git配置及用户信息 
    ```
    git config –list
    ```

3. 生成SSH秘钥(2种方式:1.git GUI图形界面化操作; 2.git命令,即以下流程) 
   1) 查看是否有秘钥,有则备份然后删除文件夹 
    ```
    cd ~/.ssh 
    ls
    ```
   2) 正式生成,输入指令再 按三次回车,也就是第三次回车指纹密码输入可以为空 
    ```
    ssh-keygen -t rsa -C “邮箱” 
    ```
   3) 添加私钥到 ssh(如果配置过指纹密码就要输入验证) 
    ```
    ssh -add id_rsa
    ```

4. 进入计算机系统用户文件夹,找到id_rsa.pub,打开复制到github的setting的SSH keys(可以添加多个ssh key公钥)

5. 测试本机是否有访问GitHub的权限 
    ```
    ssh git@github.com
    ```

### 二、与Github-repisitory建立连接

1. 先在本地新建->然后添加到远程端(具体步骤): 
   git init->git remote add origin git@xxx->在仓库添加一些初始文件xx-> 
   git add xx->git status->git commit -m “初始化仓库”->git status->git commit -a->编写你的代码-> 
   修改之前提交过的文件->git diff xx->解决冲突之后提交
2. git clone xx 克隆仓库
3. 以下只是本地创建工作区等操作 
```
cd d: 
cd dir 
mkdir FirstProgram 
cd FirstProgram 
pwd
git init(这个目录变成git可以管理的仓库,完成到这一步可以直接git remote add了) 
git add readme.txt(添加到暂存区里) 
git status(未提交时 出现红色提醒) 
git commit -m ‘提交时的注释 描述’ 
git status(提交后 出现绿色提醒) 
git commit -a(自动更新变化的文件,auto) 
git diff readme.txt(用来查看修改前后的对比,在有修改时使用) 
git log(查看提交历史,倒序记录: 信息包括提交版本号,作者,时间,提交内容) 
git log –pretty=oneline(简要查看历史,每次修改显示在一行) 
git reset –hard HEAD^(把当前的版本回退到上1个版本) 
git reset –hard HEAD^^(把当前的版本回退到上上1个版本) 
git reset –hard HEAD~100(把当前的版本回退到上100个版本) 
git checkout –readme.txt(会撤销修改但还没添加到缓存区stage的内容) 
git reflog 
git reset -hard [版本号]

// 查看内容 
cat readme.txt 

// 删除文件 
rm b.txt 
git remote rm xxx(删除远程端仓库xxx, 比如origin是远程仓库<即URL地址>别名) 
git push -u sie-remote master(将本地文件提交到Github的sie-remote版本库中<或者origin,版本库的名字>。此时才更新了本地变更到github服务上.master是分支的意思) 

// 分支创建 
git branch (显示当前分支,如:master) 
git branch sie-branch(创建分支) 
git checkout sie-branch(切换到新分支) 

// 从已有的分支创建新的分支(如从master分支),创建一个dev(develop简写)分支(相当于复制分支) 
git checkout -b dev 

// 把分支push到远端分支–>可以看到远端分支是push时产生的 
vi page_cache.inc.php 
git add page_cache.inc.php 
git commit -a -m “added initial version of page cache” 
git push origin sie-branch(把分支提交到远程服务器，只是把分支结构和内容提交到远程，并没有发生和主干的合并行为) 

// 另一种push分支,如果是在当前loc-dev分支下,则可以只写git push 
git push origin loc-dev:remote-branch-dev 

// 分支拉取 
git pull origin dev
/*
或者： 
运行git fetch(前提是已经关联了本地与远端),可以将远程分支信息获取到本地， 
再运行git checkout -b loc-v2 origin/remote-branch-v2就可以将远程分支映射到本地命名为loc-v2的一分支 
*/

// 本地分支合并 
git checkout master(切换到新主干) 
git merge sie-branch(把分支合并到主干) 

// 远程分支合并(多一个远端地址和一个反斜杠/) 
git merge origin/b 
git branch(显示当前分支是master) 
git push(此时主干中也合并了sie-branch的代码) 

// 冲突解决(Updated upstream 与==== 之间的是pull下来的内容,若不需要则删除,也可以删除本地的那一行) 
git stash(暂存本地内容) 
git pull 
git stash pop stash@{0}{ stash@{0}修改标记,还原暂存的内容} 

// 删除分支(前提是被删除的分支不是当前所在分支,否则删除不了) 
git pull origin –delete dev 

// 另一种删除分支 
git push origin :dev 

// 消除master分支的追踪 
// 设置指定分支 
git branch –set-upstream-to=origin/dev 
// 取消对master的跟踪 
git branch –unset-upstream master
```

### 三、概念分析

- 工作区: 一般就是工程区或者模块区(也就相当于[Android](http://lib.csdn.net/base/android) Studio的项目名称根目录),但是工作区下面的 
- 隐藏文件夹.[Git](http://lib.csdn.net/base/git)不属于工作区 
- 版本库: 就是.[git](http://lib.csdn.net/base/git)目录.版本库里面存了很多东西，其中最重要的就是stage(暂存区)，还有Git为我们自动创建了第一 个分支master,以及指向master的一个指针HEAD。

### 四、其他操作
1.显示所有的远程仓库 
```
git remote -v origin git@search.ued.taobao[.NET](http://lib.csdn.net/base/dotnet):projects/search.git (fetch) 
```

2.重命名远程仓库 
```
git remote rename github gh 
```

```
git remote 
origin 
gh
```

3.删除远程仓库 
```
git remote rm github 
```

```
git remote 
origin
```

4.从远程仓库抓取数据，更新本地仓库： 
```
git fetch origin 
```

5.查看远程仓库信息，可用于跟踪别人的push： 
```
git remote show origin
```



# Final Sum

![Git_use](./assets/Git_use.png)

# REF

[Git 总结](http://www.cnblogs.com/1-2-3/archive/2010/07/18/git-commands.html)