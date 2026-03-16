# 一、Git是什么？

## 含义

Git 是一款**免费、开源的分布式版本控制系统**。

 **版本控制**：把代码的每一次修改都记录下来，随时能回滚到任意历史版本（比如改崩了能一键回到昨天的正常版本）。
 **分布式**：每个开发者本地都有完整的代码仓库，不用依赖中央服务器也能工作（这区别于SVN等集中式工具）。
 **意义**：解决多人协作写代码,代码改乱了回不去,谁改坏了代码三大痛点。



# 二、Git安装方法

这里就以Ubuntu系统为例

## Ubuntu：

```bash
sudo apt update
sudo apt install git -y


验证方法：在终端输入:

git --version

显示版本号即成功。

```



# 三、Git核心概念


**仓库(Repository)**: 存放代码+版本记录的文件夹(本地仓库=电脑里的文件夹，远程仓库=GitHub上的仓库)

**工作区(Workspace)**: 你实际写代码的文件夹(仓库里的文件，修改后先在这里)

**暂存区(Stage)**: 临时存放准备提交的修改(相当于“待存档清单”)

**版本库(History)**: 最终存档的版本记录(Git真正保存版本的地方)        

**提交(Commit)**: 把暂存区的修改，正式保存到版本库(每次提交会生成唯一版本号)

**分支(Branch)**: 代码的平行宇宙(比如主分支写稳定代码，开发分支写新功能，互不影响)        

**远程仓库(Remote)**: 存放在GitHub/GitLab上的仓库(用来同步多人代码)                        


# 四、Git基础使用流程
这里示范本地新建一个项目，记录版本。

### 步骤1：初始化Git仓库(把普通文件夹变成Git仓库)

1. 新建一个文件夹(比如叫my_project)，打开它；
   
2. 在此文件夹中打开命令行终端(输入cmd或者powershell)
 
3. 输入命令初始化仓库：
   
   ```bash
   git init
   ```
在这之后文件夹里会多一个隐藏的 `.git` 文件夹,是Git的核心文件。

### 步骤2：配置用户信息(第一次用配的话可以记录谁改了代码）

输入以下命令(替换成你的名字和邮箱，邮箱可以随便填，不用真实主要还是为了找到谁在操作)：

```bash
# 配置用户名
git config --global user.name "YourName"
# 配置邮箱
git config --global user.email "your@email.com"

# 验证配置
git config --list
```

其中`--global` 表示全局配置，以后所有仓库都用这个信息。



### 步骤3：创建文件并添加到暂存区

1. 在 `my_project` 里新建一个 `test.txt` 文件，随便写点内容比如Hello Git!
   
2. 输入命令查看文件状态：
   ```bash
   git status
   ```
   会提示 `test.txt` 是未跟踪文件(Untracked)，说明Git还没监控它；

3. 把文件添加到暂存区：
   
   ```bash
   # 添加单个文件
   git add test.txt
   # 若要添加所有修改的文件，用 git add . (点表示当前目录)
   ```

4. 再输 `git status`，会提示文件变成已暂存(Changes to be committed)，说明暂存区里有这个文件了。


### 步骤4：提交修改到版本库(正式存档)

输入命令提交，`-m` 后面是提交说明(这是有必要写的，方便以后查改了什么)：

```bash
git commit -m "第一次提交：添加test.txt文件"
```

当提示 `1 file changed, 1 insertion(+)` 即成功，此时代码已经正式存档到版本库。


### 步骤5：查看提交记录（看历史版本）

输入命令：
```bash
git log
```
会显示每次提交的版本号，作者，时间和提交说明，比如：


```
commit a1b2c3d4e5f67890abcdef1234567890abcdef12 (HEAD -> master)
Author: YourName <your@email.com>
Date:   Mon Mar 16 10:00:00 2026 +0800

    第一次提交：添加test.txt文件
```

### 步骤6：修改文件后再次提交


1. 打开 `test.txt`，可以新增内容；
   
2. 先 `git add test.txt`(添加到暂存区)；
   
3. 再 `git commit -m "修改test.txt：新增内容"`；
   
4. 输 `git log` 能看到两条提交记录，版本号不同。


### 步骤7：回滚到历史版本（改崩了救命用）

比如想回到第一次提交的版本，先复制 `git log` 里的版本号(前7位就行)，输入：

```bash
# 回滚到指定版本
git reset --hard a1b2c3d
```

此时打开 `test.txt`，会发现内容回到了指定版本，改崩的代码恢复了。




# 五、Git常用命令速查表


| 分类         | 命令                          | 作用                                                                 | 示例                                  |
|--------------|-------------------------------|----------------------------------------------------------------------|---------------------------------------|
| 仓库初始化   | `git init`                    | 在当前文件夹创建Git仓库                                             | `git init`                            |
|              | `git clone <地址>`            | 克隆远程仓库到本地（比如GitHub上的仓库）                             | `git clone https://github.com/xxx/xxx.git` |
| 文件状态     | `git status`                  | 查看文件的修改状态（未跟踪/已暂存/已修改）                           | `git status`                          |
| 暂存区操作   | `git add <文件名>`            | 添加单个文件到暂存区                                                 | `git add test.txt`                    |
|              | `git add .`                   | 添加当前目录所有修改的文件到暂存区                                   | `git add .`                           |
|              | `git rm --cached <文件名>`    | 把文件从暂存区移除（保留本地文件）                                   | `git rm --cached test.txt`            |
| 提交操作     | `git commit -m "说明"`        | 把暂存区的修改提交到版本库（必须写说明）                             | `git commit -m "修复登录bug"`         |
|              | `git commit --amend`          | 修改最后一次提交的说明（提交错了说明时用）                           | `git commit --amend`                  |
| 版本查看     | `git log`                     | 查看详细提交记录（版本号、作者、时间）                               | `git log`                             |
|              | `git log --oneline`           | 精简显示提交记录（只显示版本号前7位+说明）                           | `git log --oneline`                   |
| 版本回滚     | `git reset --hard <版本号>`   | 强制回滚到指定版本（会覆盖本地修改，慎用）                           | `git reset --hard a1b2c3d`            |
| 分支管理     | `git branch`                  | 查看所有分支（当前分支前有*）                                        | `git branch`                          |
|              | `git branch <分支名>`         | 创建新分支                                                           | `git branch dev`                      |
|              | `git checkout <分支名>`       | 切换到指定分支                                                       | `git checkout dev`                    |
|              | `git checkout -b <分支名>`    | 创建并切换到新分支（常用）                                           | `git checkout -b dev`                 |
|              | `git merge <分支名>`          | 把指定分支合并到当前分支（比如把dev合并到master）                     | `git merge dev`                       |
| 远程仓库     | `git remote add origin <地址>`| 关联本地仓库到远程仓库（命名为origin）                               | `git remote add origin https://xxx.git` |
|              | `git pull`                    | 拉取远程仓库的最新代码到本地（同步）                                 | `git pull`                            |
|              | `git push -u origin <分支名>` | 把本地分支推送到远程仓库（第一次推送用-u，后续直接git push）          | `git push -u origin master`           |
| 撤销修改     | `git checkout -- <文件名>`    | 撤销工作区的修改（回到最近一次提交的状态，未add的修改会丢失）         | `git checkout -- test.txt`            |




# 六、git多人协作的基础方法

比如你和同事协作一个GitHub仓库：
操作流程如下：

1. 先克隆远程仓库到本地：`git clone 仓库地址`；
   
这会将远程仓库(比如在GitHub上)的完整代码和所有版本历史下载到你的本地电脑，形成一个本地仓库。这样你就有了一份和远程完全一样的代码副本，可以开始工作了。
   
2. 新建自己的开发分支：`git checkout -b my_dev`；
   
这个可以在独立的环境中开发新功能或修复bug，而不会影响主分支的稳定性。
   
   
3. 在分支里写代码、提交(`git add .` + `git commit -m "xxx"`)；

`git add .`会将当前目录下所有修改过的文件添加到暂存区同时`git commit -m "xxx"`会把暂存区的内容正式保存为一个版本快照，并附上一句简短的说明，方便以后查看这次改动的原因。这同样不影响别人的工作。
   
4. 先拉取远程最新代码：`git pull origin master`；

这个主要是当你在开发自己的功能时，你的同事可能已经向master分支推送了一些代码。如果你直接把自己的分支推送到远程，然后提合并请求，可能会因为master已经更新而导致代码冲突。

   

5. 把自己的分支推到远程：`git push -u origin my_dev`；
   
只有将分支推送到远程，你的同事才能看到你开发的内容，才能进行代码审查。
   
6. 在GitHub上提合并请求(PR)，同事审核后合并到主分支。
PR会显示你所有的改动，并允许同事逐行评论、提出修改建议。经过审核并确认无误后，由项目维护者(或你本人，如果有权限)点击“合并”按钮，将你的代码合并到主分支。它提供了一个讨论区，团队成员可以针对改动进行交流，确保代码符合规范。合并后，你的改动就正式成为项目的一部分，其他人可以通过git pull获取最新代码。



