---
title: vscode build cpp configure
date: 2018-06-17 17:22:03
tags: [program setting]
---
# ubuntu 下如何使用 vscode 编译 cpp

## 1. 安装C/CPP 插件
首先安装vscode的c/cpp插件，网址
[cpp for vscode](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

## 2. 配置launch.js
在配置之前，首先介绍下vscode 所具有的一些配置所需要的常数
[val ref](https://code.visualstudio.com/docs/editor/variables-reference)

具体如下：

* ${workspaceFolder} - the path of the folder opened in VS Code
* ${workspaceFolderBasename} - the name of the folder opened in VS Code without any slashes (/)
* ${file} - the current opened file
* ${relativeFile} - the current opened file relative to workspaceFolder
* ${fileBasename} - the current opened file's basename
* ${fileBasenameNoExtension} - the current opened file's basename with no file extension
* ${fileDirname} - the current opened file's dirname
* ${fileExtname} - the current opened file's extension
* ${cwd} - the task runner's current working directory on startup
* ${lineNumber} - the current selected line number in the active file
* ${selectedText} - the current selected text in the active file

你只需要自动生成一个gdb launch的配置，修改你需要运行的文件名即可，也就是`program`属性，我的配置是这样的：
```js
{
"program": "${workspaceFolder}/${fileBasenameNoExtension}.out"
}
```

除此之外，cpp需要提前编译，所以需要配置一个新的task来配置这个编译过程：

## 3. tasks.js
使用`ctrl + shift + p`,输入tasks，就可以看到配置的选项，随后选择other选项
我的配置如下：
```js
"tasks": [
        {
            "label": "build cpp",
            "type": "shell",
            "command": "g++",
            "args": [
                "-std=c++11","-g","${file}","-O3","-Wall","-o","${fileBasenameNoExtension}.out"
            ]
        }
    ]
```
注意这个"-g"是必要的，详细原因参见g++ 的编译指令

## 4. 配置cpp 的运行环境
最后需要给出linux下cpp的环境配置，这里直接生成几乎不需要修改：
```js
{
    "configurations": [
        {
            "name": "Linux",
            "browse": {
                "path": [
                    "${workspaceFolder}"
                ],
                "limitSymbolsToIncludedHeaders": true
            },
            "includePath": [
                "${workspaceFolder}"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "clang-x64"
        }
    ],
    "version": 4
}
```