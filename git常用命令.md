# git常用命令

## 连接远程仓库

* **关联远程仓库:** `git remote add origin git@github.com:Haobin-Lee/Notes.git`
* **本地文件提交到远程仓库并与远程master分支关联:**`git push -u origin master`(-u指定默认主机为origin，之后push的时候就可以直接使用`git push`提交到origin主机上)

## 分支管理

* **本地新建分支:** `git checkout -b dev`(创建并切换到dev分支)
* **切换分支:** `git checkout master`(切换到master分支)
* **合并分支:** `git merge dev`(将dev合并到当前分支上)
* **将指定分支提交到远程某一分支上:** `git push master:dev`(将本地master分支的内容提交到远程主机的dev分支上，如果远程主机没有dev分支，那么会自动创建)
* **远程分支同步到本地分支** `git checkout --track origin/branch_name`(本地新建branch_name分支，并自动跟踪远程同名分支)
* **本地分支同步到远程分支** `git push --set-upstream origin branch_name`(远程新建branch_name分支，并与本地分支同步)
  
## 子模块

* **创建子模块:** `git submodule add <submodule_url> 本地路径`
* **获取子模块:**
  * 方式一:`git clone <module_url> --recurse-submodules`(递归拉取项目中子模块的代码)
  * 方式二:

      ```shell
         git submodule
         git submodule init
         git submodule update
      ```

* **子模块发生变动:**
  1. 子模块文件夹的内容发生变动，还没有提交到远程。
  2. 子模块文件夹的内容已经和远程同步，但是主项目还没有提交。
  3. 远程子模块内容发生变动，还没有拉取到本地。

     ```shell
        cd 子模块文件夹
        git checkout master
        git pull origin master
        # 如果是拉取不同项目下的同一子模块，则需要下面几步
        cd 主模块文件夹
        git add .
        git commit -m "update submodule"
     ```

## 比较本地仓库和远程仓库的差异

1. 本地与远程的差集

```shell
git log master..origin/master
```

2. 统计文件的改动

```shell
# git diff <local branch> <remote>/<remote branch>
git diff --stat master origin/master
```
