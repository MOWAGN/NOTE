# Git仓库使用和操作
## 本地仓库创建
- 创建本地仓库有两种方法：
    - 创建全新的本地仓库
    - 克隆远程仓库

### 创建全新仓库
- 已安装Git桌面版可以右键在当前需要工作目录打开Git Bash（ProtableGit通过 `cd 盘符：/路径` 进入到工作目录）
- 执行命令
    - `$ git init`
- 创建结果，项目目录多出一个 .git 隐藏目录，关于版本信息都在该目录中。
    ![](vx_images/67243911244686.png =550x)

### 克隆远程目录
- 将远程服务器仓库完全镜像一份到本地
- 执行命令

```
# 克隆一个项目和它的整个代码历史
$ git clone [url] https://gitee.com/..
```

## Git 文件操作

### 文件的四种状态
1. Untracked：未跟踪
    - 此文件在文件夹中，但未添加到git库，不参与版本控制
    - 通过 `git add .` 状态变为 **Staged**.
2. Unmodify：文件已入库但未修改
    - 版本库中的文件快照内容与文件夹中完全一致
    - 这种类型文件的两种去处：
        - 如果它被修改，则变为 **Modified**.
        - 如果使用 `git rm ` 移出版本库，则成为一个 **Untracked**.
3. Modified：文件（仅）已修改
    - 这类文件除修改外没有进行其他操作，有两种去处：
        - 通过 `git add ` 可进入暂存 **staged**.
        - 使用 `git checkout` ，则丢弃修改过的，返回到 **Unmodify** 状态，该命令即从库中取出原有文件，覆盖掉当前修改.
4. Staged：暂存状态
    - 执行 `git commit` 将修改同步到本地git库，此时本地git库中文件和本地文件一致，文件变为 **Umodify** 状态.
    - 执行 `git reset HEAD filename` ，取消暂存，文件状态变为 **Modified**.
- 查看文件状态
    - 查看指定文件状态命令：`git status [filename]`
    - 查看所有文件状态命令：`git status`

### Git的六种基本命令
![](vx_images/467165912225927.png =500x)
- `git add .`
    - 作用：添加所有文件到暂存区
- `git commit -m "..."`
    - 作用：提交暂存区的内容至本地仓库
    - -m：表示提交信息选项，... 为信息内容

### 忽略文件
- 有时候不想把某些文件纳入版本控制中，比如临时文件、设计文件等
- 在主目录下建立 **".gittignore"** 文件可用于控制忽略文件，此文件有如下规则：
    1. 注释：忽略文件中的空行或以井号（#）开始的行会被当作注释
    2. 可以使用Linux通配符。例如：
        - 星号（*）代表任意多个字符，可用于忽略某一类型文件
        - 问好（?）代表一个字符
        - 方括号（[abc]）代表可选字符范围
        - 大括号（{string1,string2}）代表可选字符串
    3. 如果名称最前面前有一个感叹号（!），表示例外规则，将不被忽略
    4. 如果名称 **最前面** 是一个路径分隔符（/），表示要忽略的文件在此路径下，而子目录文件不忽略
    5. 如果名称 **最后面** 是一个路径分隔符（/），表示要默认忽略此目录下的文件和目录
    ![](vx_images/51694113248367.png =500x)


## 创建远程仓库并配置公钥
- 见本笔记（“GitHub使用前准备”部分）

## 文件同步至远程仓库
### 本地仓库更新
#### 使用前配置
- 配置好姓名和邮箱
- 生成或添加已有公钥至github的SSH Key进行认证
- 进入到对应项目目录并进行初始化本地（仅首次）
#### 本地仓库更新命令

```
$ git add .
$ git commit -m "..."
```

### 远程仓库同步更新
#### 配置添加远程分支
- 在首次使用或者更换环境使用 `git push` 提示报错 `fatal: No configured push destination.` 需要重新配置远程分支
- 添加远程分支命令格式
    - `git remote add origin 远程仓库url`
    - 其中url获取方法
        ![](vx_images/90164323220263.png =450x)

#### `push` 推送至远程仓库
- 使用push推送到指定远程master（默认）分支
    - 一般仅首次使用需要本命令
    - `git push -u origin master`
    - 如果当前分支与多个主机存在追踪关系，那么这个时候 `-u` 选项会指定一个默认主机，这样后面就可以不加任何参数使用 `git push`。
- 在桌面版或者git环境不变的设备中，除首次，常用同步命令为：
    - `git push`
    -  不带任何参数的git push，默认只推送当前分支

#### `push`常见报错及解决方法
1. 输入 ` git push -u origin master` ，产生报错如下：
    ![](vx_images/44875523238689.png =500x)
    - 错误原因：远程分支上存在本地分支中不存在的提交，本地和远程的文件应该合并后，往往是多人协作开发过程中遇到的问题
    - 解决方法：
        - 方法一：先 `pull`，再 `push`

        ```
        $ git pull origin master 
        # git pull 过程可能有报错，见下文
        $ git push -u origin master
        ```
        - 方法二：（不推荐）如果确定远程分支上的提交不需要，可以强行让本地分支覆盖远程分支
            - `git push origin master -f` 

2. 使用 `git push` 时，报错如下：`fatal: The current branch master has no upstream branch.`
    - 错误原因：在push上传的时候提示没有个远程的分支关联
    - 建议：本地分支新建时和远程分支名保持一致
    - 解决办法：
        - 方法一：输入 `git push -u origin master` 设置远程分支。需要切换到 master 分支（即当前所在目录为master），切换分支命令为：`git checkout 分支名`，再设置远程分支。只需设置一次即可。
        - 方法二：关联本地和远程分支：`git push --set-upstream origin master`

3. 使用 `git pull origin master`或 `git pull`，产生报错如下：
    ![](vx_images/374391800226557.png =500x)
    - 警告描述：

        ```
        warning: 不建议在没有为偏离分支指定合并策略时执行pull操作。
        您可以在执行下一次pull操作之前执行下面一条命令来抑制本消息：
        git config pull.rebase false # 合并（默认缺省策略）
        git config pull.rebase true # 变基
        git config pull.ff only # 仅快进
        您可以将 “git config” 替换为 “git config --global” 以便为所有仓库设置
        缺省的配置项。您也可以在每次执行 pull 命令时添加 --rebase、–no-rebase，
        或者 --ff-only 参数覆盖缺省设置
        ```
    - 解决方案：

        ```
        //执行一下默认策略就行了 the default strategy
        $ git config pull.rebase false
        $ git config --global pull.rebase false
        ```

4. 在 `git pull`或 `git push`、`git merge` 可能遇到报错：`fatal: refusing to merge unrelated histories`
    - 错误原因：因为两个库没有历史联系， git 默认拒绝合并无关的历史
    - 解决方法：告诉git允许合并无关历史
        - `git pull/push/merge 分支名 --allow-unrelated-histories`

5. 在 `git pull` 出现如下报错：
    ![](vx_images/281983800246723.png =500x)
    - 错误原因：无法提取，因为您有未合并的文件。
    - 解决方法

        ```
        //注释：提交本地代码到工作区
        //注释：如果有冲突，先解决冲突合并代码，然后提交
        //注释：如果代码上没有冲突，但是提交的时候git提醒有冲突，那么先关闭编辑器，然后编译代码找到冲突，最后手动合并代码解决冲突
        git add .
        git commit -m '提交本地代码并且获取最新代码'
        //注释：获取源dev分支最新代码
        git pull origin dev
        //注释：如有冲突就解决冲突
        ```

