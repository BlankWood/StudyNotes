**Git分布式版本控制工具**

Git会记录文件的修改,将每一次的修改提交到仓库时,会记录为一个版本。

## 基本配置

1. 右键打开 "Git bash"
2. 设置用户信息  
`git config --global user.name "···"`  
`git config --global user.email "···"`

3. 查看配置信息：  
`git config --global user.name`  
`git config --global user.email`

4. *为常用命令配置别名
>1. 打开电脑的用户目录,创建".bashrc"文件
>2. 添加内容
>```
>#用于输出git提交日志  
>alias git-log='git log --pretty=oneline --all >--graph --abbrev-commit'  
>#用于输出当前目录所有文件及基本信息  
>alias ll='ls -al'  
>```
>3. 打开gitBash,执行source ~/.bashrc

5. 解决GitBash乱码问题  
>方案一:  
>打开GitBash执行下面命令  
>`git config --global core.quotepath false`  
>方案二:  
>在安装目录/ect/bash.bashrc  文件最后加入下面两行  
>`exprot LANG="zh_CN.UTF-8"`  
>`exprot LC_ALL="zh_CM.UTF-8"`  


## 获取本地仓库

1. 在文件目录中右键打开'Git bash'窗口  
2. 执行命令 `git init`  
3. 创建成功则可以在文件夹中看到隐藏的.git目录

## 基础操作指令
### 工作流程
Git工作目录下对于文件的修改(增加、删除、更新)会存在几个状态,这些**修改的状态**会随着我们执行Git命令而发生变化.  
(工作区 -> 暂存区 -> 仓库)  

| 区域 | 作用 |
| --- | --- |
| 工作区 | 新创建的或修改的文件时加入工作区 |
| 暂存区 | 提交至仓库前的暂存区 |
| 仓库 | 修改进入仓库就成为一次提交记录 |

### 基础指令
| 指令 | 含义 |
| --- | --- |
| touch <文件名> | 新建文件 |
| git status | 查看修改的状态 |
| git log | 查看提交记录,后可跟很多参数(不展示) |
| git add <文件名(或通配符)> | 工作区 -> 暂存区 |
| git commit -m '注释内容' | 暂存区 -> 仓库 |
| git reset --hard commitID | 将版本返回到之前的提交记录中 |  
| clear | 清屏 |


>注意:  
>commitID为提交的ID,可通过log指令查看,即使记录已删除也可以用`git reflog`查询  
>在命令行中选中ID,再按鼠标中键即可复制,不能按"Ctrl+C"  
>`git add .`将所有文件加入暂存区.  
>查看记录一般使用之前配置好的`git-log`

---

有一些不用纳入git管理的文件,可以在工作目录中创建一个".gitignore"文件(文件名固定),在其中列出要忽略的文件模式.示例:  
```
# no .a files 
*.a
# but do track lib.a, even though you're ignore .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore doc/notes.txt, but not doc/sever/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```
## Git分支

几乎所有的版本控制系统都以某种形式支持分支.使用分支意味着你可以把你的工作从开发主线上分离开来继续重大的Bug修改、开发新功能,以免影响开发主线.

### 指令

| 命令 | 含义 |
| --- | --- |
| git branch | 查看本地分支 |
| git branch <分支名> | 创建本地分支 |
| git checkout (-b) <分支名> | (创建并)切换分支 |
| git merge <分支名> | 将分支合并到目前分支,一般先回到master(主分支) |
| git branch -d <分支名> | 删除分支,会先做检查,"-D"会不检查强制删除 |

在合并分支时,两分支对文件的修改可能会存在冲突,例如改了同一文件的同一行,这时需要手动解决冲突.  
>1. git会在冲突的地方标识,完成修改(解决冲突)
>1. 将文件加入暂存区
>1. 提交到仓库

### 分支使用规范

- master(生产)分支:  
线上分支,主分支,中小规模项目作为线上运行的应用对应的分支。 
- develop(开发)分支:  
是从master创建的分支,一般作为开发部门的主要开发分支,如果没有其他并行开发不同期上线要求,都可以在此版本进行开发,阶段开发完成后,需要合并到master分支,准备上线。  
- feature/xxxx分支:
从develop创建的分支,一般是同期并行开发,但不同时期上线时创建的分支,分支上的研发任务完成后合并到develop分支。
- hotfix/xxxx分支:
从master派生的分支,一般作为线上bug修复使用,修复完后需要合并到master、test、develop分支。
- 还有一些其他分支：例如test分支(用于代码测试)、pre分支(预上线分支)等等。

## Git远程仓库

### 常用的托管服务(远程仓库)
- GitHub(https://github.com/)  
是一个面向开源及私有软件项目的托管平台,因为只支持Git作为唯一的版本库格式进行托管,故名github.
- 码云(https://gitee.com/)  
是国内的一个代码托管平台,由于服务器在国内,所以相比于GitHub,码云速度回更快.
- GitLab(https://about.gitlab.com/)  
是一个用于仓库管理系统的开源项目,使用Git作为代码管理工具,并在此基础上搭建起来的web服务,一般用于在企业、学校等内部网络搭建git私服.

### 注册码云和创建远程仓库
略
### 配置ssh公钥
- 生成SSH公钥
1. `ssh-keygen -t rsa`
2. 不断回车(如果公钥以存在,则自动覆盖)
- 获取公钥:  `cat ~/.ssh/id_rsa.pub`
- Gitee设置账户公钥:  略
- 验证是否配置成功:  `ssh -T git@gitee.com`

### 将本地仓库推至远程仓库
1. 在gitee网站获取创建的仓库的地址.
2. 在本地输入命令:`git remote add <远程仓库名(origin)> <地址>`
3. `git remote` :查看远程仓库
4. `git push [--set-upstream] origin master`:将本地推至远程仓库  
github 更新后默认分支为main, 所以push指令应改为:  
`git push -u origin main`  
`--set-upstream`参数建立本地分支和远端分支的关联,之后可简略写`git push`
5. `git branch -vv`:查看本地分支与远程分支关联

### 从远程仓库获取
 
| 命令 | 说明 |
| --- | --- |
| git clon <仓库路径> [本地目录] | 将远程仓库整个下载到本地 |
| git fetch [remote name] [branch name] | 将远程仓库的更新抓取到本地 |
| git pull [remote name] [remote name] | 抓取并合并远程与本地分支 |  

>不指定分支名则默认为所有或是当前.  
>推至也许会有冲突,需要先抓取远端进行修复合并,再推送至远端.  

## 在Idea中使用Git

- 配置  
在设置中搜'git',添加Git路径(一般有自动识别).  
- 创建本地仓库  
在项目中加入'.gitignore'文件.  
最上层的'VCS'选项 -> 'Improt into Version Control' -> 'Create Git repository'.  
- add  
右键文件 -> Git -> add.
- 提交  
上方会出现Git选项:'√'为提交  
- 推至远端  
VCS -> Git -> push.  
- 克隆  
VCS -> Checkout from Version Control -> Git.
- pull  
Git选项 -> '↙'.
- 附:IDEA集成GitBush作为Terminal  
设置 -> tools -> terminal ->将"shell path" 改为GitBush路径.

## 个人Github账户
笔记仓库:  
https://github.com/BlankWood/study-notes.git

## 指令一览表

| 指令 | 说明 |
| --- | --- |
| git config --global user.name '···' | 创建用户 |
| git config --global user.email '···' | 创建用户邮箱 |
| git config --global user.name | 查看用户名 |
| git config --global user.email | 查看用户邮箱 |
| git init | 初始化本地仓库 |
| touch <文件名> | 新建文件 |
| git status | 查看修改的状态 |
| git-log | 查看提交记录,后可跟很多参数(不展示) |
| git add . | 工作区 -> 暂存区 |
| git commit -m '注释内容' | 暂存区 -> 仓库 |
| git reset --hard commitID | 将版本返回到之前的提交记录中 |  
| clear | 清屏 |
| git branch | 查看本地分支 |
| git branch <分支名> | 创建本地分支 |
| git checkout (-b) <分支名> | (创建并)切换分支 |
| git merge <分支名> | 将分支合并到目前分支,一般先回到master(主分支) |
| git branch -d <分支名> | 删除分支,会先做检查,"-D"会不检查强制删除 |
| git remote add origin <地址> | 创建远程版本库 |
| git remote | 查看远程仓库 |
| git push origin master | 上传至远端 |
| git clon <仓库路径> [本地目录] | 将远程仓库整个下载到本地 |
| git fetch | 将远程仓库的更新抓取到本地 |
| git pull | 抓取并合并远程与本地分支 |  

---

## 最后的注意事项
- 切换分支前先提交本地的修改
- 代码及时提交,提交了就不会丢失
- 别删文件目录,不然神仙都救不了!!!
---
符号说明:  
<>:尖括号内为参数,需要填写  
[]:方括号内为可填参数,非必须填写  