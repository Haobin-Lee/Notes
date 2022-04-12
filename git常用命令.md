# git常用命令

## 连接远程仓库

* **关联远程仓库:** `git remote add origin git@github.com:Haobin-Lee/Notes.git`
* **本地文件提交到远程仓库并与远程master分支关联:**`git push -u master`
* **本地新建分支:** `git checkout -b dev`(创建并切换到dev)
  
## 子模块

* **创建子模块:** `git submodule add <submodule_url>`
* **获取子模块:** 
  * 方式一:`git clone <module_url> --recurse-submodules`(递归拉取项目中子模块的代码)
  * 方式二:
           ```
            git submodule init
            git submodule update
           ```