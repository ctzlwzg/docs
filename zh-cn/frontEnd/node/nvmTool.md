# nvm 工具

## 简介
- 是一种用于管理多个主动节点.js版本的工具。
- 安装nvm进行node版本管理，主要内容包括安装、使用nvm工具管理node、卸载 node

## 下载地址
https://github.com/coreybutler/nvm-windows/releases

!> 如果电脑上之前已经单独安装了node，先卸载，然后再安装nvm，便于统一管理node

## 命令
> 查看nvm是否安装成功
```bash
nvm -v
```
> 看安装的所有node.js的版本
```bansh
nvm ls
```
> 查显示可以安装的所有node.js的版本
```bansh
nvm list available
```
> 选择任意版本安装，比如安装16.15.1
```bansh
nvm install 16.15.1
```
> 安装最新稳定版
```bansh
nvm install stable
```
> 如果想使用16.15.1这个版本的话。就执行：
```bansh
nvm use 16.15.1
```
> 卸载node.js是的命令，卸载指定版本的nodejs
```bansh
nvm uninstall 16.15.1
```
> 启用node.js版本管理
```bansh
nvm on
```
> 禁用node.js版本管理(不卸载任何东西)
```bansh
nvm off
```