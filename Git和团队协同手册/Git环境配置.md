# Git环境配置
- 下文操作环境均为与Linux命令风格相近的Git Bash
## 配置信息查看
### 相关命令
- `git config -l`
    - 查看自行设定配置
- `git config --system --list`
    - 查看系统配置
- `git config --global --list`
    - 查看本地配置，用户自行配置的，这是必须要配置的

### Git相关配置文件
1. `Git\etc\gitconfig`
    - Git安装目录下的gitconfig
    - system 系统级
2. `C:\Users\Administrator\.gitconfig`
    - 只适用与当前登录用户的配置
    - global 全局

## 配置姓名和邮箱

```
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
```
