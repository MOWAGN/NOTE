# GitHub使用前准备
## GitHub账户创建
## 设置SSH Key
- GitHub 上连接已有仓库时的认证，是通过使用了 SSH 的公开密钥认证方式进行的。
- 创建命令

```
$ ssh-keygen -t rsa -C "your_email@example.com"
Generating public/private rsa key pair.
Enter file in which to save the key
(/Users/your_user_directory/.ssh/id_rsa): 按回车键
Enter passphrase (empty for no passphrase): 输入密码
Enter same passphrase again: 再次输入密码
```

- 创建结果

```
Your identification has been saved in /Users/your_user_directory/.ssh/id_rsa.
Your public key has been saved in /Users/your_user_directory/.ssh/id_rsa.pub.
The key fingerprint is:
fingerprint值 your_email@example.com
The key's randomart image is:
+--[ RSA 2048]----+
|   略            |
# id_rsa 文件是私有密钥
# id_rsa.pub 是公开密钥，需要添加至GitHub
```

- GitHub上添加公开密钥
    - 通过私有密钥和GitHub进行认证和通信
    - `$ ssh -T git@github.com`
    - 出现如下结果即成功
    - `Hi hirocastest! You've successfully authenticated, but GitHub does not provide shell access.`
    - 常见报错：`git@github.com: Permission denied (publickey).`
        - 常见错误原因：
            - git上设置的姓名和邮箱名是否正确。
                - 解决方法：`git config --global --list` ，查看核对姓名和邮箱
            - github上公共密钥丢失
                - 解决方法：重新添加公共密钥


## 创建远程仓库
### 创建界面选项
- 仅列出需要注意项
- Public、Private
    - 选择 Public，创建公开仓库，仓库内的所有内容都会被公开。选择 Private 可以创建非公开仓库， 用户可以设置访问权限，但这项服务是收费的。
- Initialize this repository with a README
    - 勾选GitHub 会自动初始化仓库并设置 README 文件，可以立刻进行clone
    - 🐖 建议不要勾选，消除因仓库不一致带来的向 GitHub 添加手中已有的 Git 仓库可能存在的报错
- Add .gitignore
    - 不需要选择，该文件用来描述 Git 仓库中不需管理的文件与目录。
    - 这个设定会帮我们把不需要在 Git 仓库中进行版本管
理的文件记录在 .gitignore 文件中，省去了每次根据框架进行设置的麻
烦。

### 仓库链接URL
- `https://github.com/用户名/仓库名`