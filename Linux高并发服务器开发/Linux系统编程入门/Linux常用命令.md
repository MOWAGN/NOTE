# Linux常用命令
## 安装/更新软件包
### apt-get命令
- 适用Linux版本：Ubuntu/Debian系统
- 升级所有已安装的软件包至配置的Ubuntu存储库中可用的最新版本
    - `sudo apt-get upgrade`
- 升级单个软件包
    - `sudo apt-get install --only-upgrade 软件包名`
- 升级多个包
    - `sudo apt-get install -only-upgrade 软件包1 软件包2 ...`
    - 多个软件包之间用空格分隔
- 安装软件包
    - `sudo apt-get install 软件包名`
- 卸载软件包
    - `sudo apt-get remove 软件包名`
    - 删除软件包，但保留配置文件
        - `apt-get --purge remove 软件包名`
- 查询可升级软件包
    - `apt list --upgradable`

## 压缩和解压缩
### tar命令
#### 原理
- tar 命令其实并不是真的解压缩的处理者，而是使用了 gzip 或者 bzip2 等其它命令来达成，但是 gzip 等命令通常只能处理单个文件，并不方便，所以一般我们都是选择使用 tar 命令间接的完成解压缩。
#### 语法
- `tar [主选项+辅选项] 文件或目录`
- 选项释义
    ```
  -z : 使用 gzip 来压缩和解压文件
  -v : --verbose 详细的列出处理的文件
  -f : --file=ARCHIVE 使用档案文件或设备，这个选项通常是必选的
  -c : --create 创建一个新的归档（压缩包）
  -x : 从压缩包中解出文件
    ```
#### 常用示例
```
# 压缩文件 file1 和目录 dir2 到 test.tar.gz
tar -zcvf test.tar.gz file1 dir2
# 解压 test.tar.gz（将 c 换成 x 即可）
tar -zxvf test.tar.gz
# 列出压缩文件的内容
tar -ztvf test.tar.gz
```

## 手册/帮助
### 手册查看命令
- `man x 函数名/内容`
    - x 为手册章节，第2章是系统API，第3章是标准C库的API说明。
