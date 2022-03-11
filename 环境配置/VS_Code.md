# VS_Code
## VS_Code总环境搭建
1、安装中文插件，重启  

2、配置开始界面（此环节同时安装Git）
## C++环境搭建
1、安装MinGW -w64  

（1）下载地址：http://www.mingw-w64.org/doku.php/download
（2）下载时勾选相关文件
```
mingw32-gcc.bin（c语言文件编译器）
mingw32-gcc-g++.bin（c++语言编译器）
mingw32-gdb.bin（调试编译后文件）
```
（3）添加环境变量
```
在“电脑”点击“属性”
高级系统设置
环境变量
Path
“新建”把 MinGW bin目录地址 添加到环境变量
```
- **注意**   
上述过程可以通过codeblocks 下载时 add to path 的MinGW，也下载过codeblocks 的小伙伴可以直接去codeblocks 目录里面找（或者 系统环境变量）
- 检查是否安装成功
    - 命令行cmd中输入 `gcc -v` 查看gcc version
    
2、创建工作区
```
在磁盘的工作目录新建一个文件夹，用来存放c/c++代码
在vscode中 选项卡 文件中选择打开文件夹
```
3、配置文件
（1）在 此文件夹下建立一个文件夹 名为`.vscode` 文件夹
（2）在 .vscode文件夹中新建三个json文件，**注意名字必须一模一样**
 ```
 c_cpp_properties.json
 launch.json
 tasks.json
 ```
- c_cpp_properties.json
    - 注意：下述文件中需要修改`compilerPath`，将其修改为上文环境变量 `MinGW/bin/g++.exe`，路径中的“\”改为“/”。
```
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            //此处是编译器路径，以后可直接在此修改
            "compilerPath": "D:/Environment/CodeBlocks/MinGW/bin/g++.exe",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}

```
- launch.json
    - 修改 `miDebuggerPath` 为上文环境变量 `MinGW/bin/gdb.exe`，路径中的“\”改为“/”。
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [

        {
            "name": "(gdb) Launch",
            "preLaunchTask": "g++.exe build active file",//调试前执行的任务，就是之前配置的tasks.json中的label字段
            "type": "cppdbg",//配置类型，只能为cppdbg
            "request": "launch",//请求配置类型，可以为launch（启动）或attach（附加）
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",//调试程序的路径名称
            "args": [],//调试传递参数
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,//true显示外置的控制台窗口，false显示内置终端
            "MIMode": "gdb",
            "miDebuggerPath": "D:/Environment/CodeBlocks/MinGW/bin/gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```
- tasks.json
    - 修改command 和 options 中的 `cwd`
```
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558 
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "type": "shell",
            "label": "g++.exe build active file", //这里注意一下，见下文
            "command": "D:\\Environment\\CodeBlocks\\MinGW\\bin\\g++.exe",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe"
            ],
            "options": {
                "cwd": "D:\\Environment\\CodeBlocks\\MinGW\\bin"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
				"kind": "build",
				"isDefault": true
			}

        }
    ]
}
```
4、代码编辑调试
- 在 .vscode 文件夹 **同级目录** 中建立 cpp 文件，然后F5 调试，把.vscode文件夹放在最上头，然后在和他同级或者更低的目录下，执行cpp文件

5、相关插件推荐
（1）Code runner
（2）Codelf
（3）vscode-icons
（4）Bracket Pair Colorizer
（5）Markdown All in One

## 常见问题
- 报错：”Please install clang or check configuration ‘clang.executable’“
    - 错误原因：安装的插件 ”C/C++ Clang Command Adapter“ 和 C/C++ 冲突
    - 解决方法：安装MinGW，配置环境变量后把这个插件卸掉即可


## VScode完全卸载（删除个人配置信息和插件）
1. 打开软件安装目录，运行“unins000.exe”进行卸载
    - 此步骤虽然删掉了应用软件，但是此时重新安装会发现之前下载的插件和个人配置信息都还会重新加载出来
2. 打开路径 `C:\Users\...(当前用户名)\`，删除该路径下的 `.vscode` 文件夹（主要用来放安装的插件）
![](vx_images/449495420237130.png =700x)
3. 打开路径 `C:\Users\Administrator\AppData\Roaming`，删除 `Code` 文件夹（主要是用户信息和缓存信息）
![](vx_images/561495520230264.png =700x)
- 卸载完成


