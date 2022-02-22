# Git
## PortableGit
### 警告
- 这个版本的包不修改任何windows路径变量 `%path%`，即不可能直接运行 git.exe 和 gitk.exe（可视化界面） 文件。改为启动 Git Bash 或 Git Cmd，或添加 `cmd/ 文件夹` 到你的 %path%

### PortableGit使用
- 如果您对类 Unix 的 shell 感到满意，只需启动 `git-bash.exe`。
- 🐖 环境变量设置是你每次使用git-portable的第一步。
- 如果不，则启动 `git-cmd.exe`.
    - 或者，您可以执行这些命令来修改 %path% 临时变量：

    ```
    set gitdir=c:\portablegit
    set path=%gitdir%\cmd;%path%
    ```
    - 根据您的设置调整gitdir，只要不关闭命令窗口，现在只需要键入 `git` 或 `gitk` ，即可运行 `c:\portablegit\cmd\git.exe` 或 `c:\portablegit\cmd\gitk.exe`.
- 默认情况下，git cmd 和 git bash 在运行时使用启动他们的目录作为工作目录，您可以通过传递 `--cd-to-home` 来覆盖它 给他们，这会将用户的主目录设置为工作目录（如果安装了适用于 Windows 的 Git）。
- 此外，如果您设置 HOME 环境变量（永久或 仅适用于当前会话）您可以让 Git 存储并使用配置 该变量中指定的目录中的配置文件。如果你指定 `--cd-to-home`、git-bash 和 git-cmd 启动时也将使用它作为工作目录。例如下列命令将使用名为 home 的相对目录，（%cd% 指定为当前目录）：

    ```
    set HOME=%cd%/home
    git --cd-to-home
    ```

### 快速启动
- 开始使用个人设置配置git

```
git config --global user.name "Joe Sixpack"
git config --global user.email joe.sixpack@g_mail.com
```
- 用户信息配置的另一种方式
    - 每次使用git commit命令进行提交时，都会检查是否有提交者的信息。为了避免重复设置用户信息，可以将配置信息保存 .gitconfig 文件。

        ```
        [user]
        name = Your name
        email = Your e-mail
        ```
    - git-portable每次都会检查$HOME路径下的.gitconfig文件夹，上述代码为 .gitconfig 文件的格式。

- ssh配置
    - git-portable的ssh配置和桌面版git的配置步骤基本相同，不同点在于默认路径的使用。
    - 在使用下面的命令生成密钥之后，会提示你输入密钥的路径。
        - `$ ssh-keygen -t rsa -C "Your e-mail"`
        - 不能直接按回车（默认使用默认路径），需要修改称 git-portable 的安装路径，如 `g:\\git_portable\\.ssh`。
        - 如果想直接使用默认路径，需要先将 `home` 环境变量设置为 git-portable 安装路径。

- 开始使用git

```
git --help
```

###  永久修改 `%path%`
- 如果您是管理员，则在系统级别（适用于下部窗格中的所有用户）
- 或仅用于您自己的用户帐户（在上窗格中）。
- 要永久更改 `%path%` 变量所需执行的操作如下：
    - 右键单击 `计算机`
    - 选择 `属性`
    - 打开 `高级`
    - 单击  `环境变量`
    - 突出显示 `Path`
    - 单击 `Edit`（选择上窗口或者下窗格）
    - 将你对应的特定路径添加到变量值字段的前面，通过分号将现有条目分开。

## Git的使用
### Git概述
#### Git和Github的区别
- 两者主要通过“方式”区分描述
    - 在 Git 中，开发者将源代码存入名叫“Git 仓库”的资料库中并加以使用。而 GitHub 则是在网络上提供 Git 仓库的一项服务。
    - GitHub 上公开的软件源代码全都由 Git 进行管理。




