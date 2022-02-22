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
