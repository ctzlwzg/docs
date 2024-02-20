# n 包的使用

## 简介
- 安装n进行node版本管理，主要内容包括安装、使用n管理node、卸载 node（仅mac可用，不支持Windows）

## 命令

> 全局安装n包
```bash
npm i n -g
```
!> 注意：如果报错如：code EACCES errno -13，表示你没有权限安装，使用管理员身份安装：sudo npm i n -g

### 使用n包管理node

> 查看node可以使用的列表
```bash
n ls
```
> 查看官方 node 版本
```bansh
npm view node versions
```
> 安装指定的node版本
```bansh
sudo n 16.20.0
```
> 切换node版本,直接运行 n 通过上下键进行切换选择，最后使用 enter 键选中版本
```bansh
n
```
> 删除指定版本 node
```bansh
sudo n rm 版本号
```

!> 注意：有时候初始化项目报错可能是因为安装包的对应node版本不支持，需要降低node版本进行初始化，如：~~ node-sass(烦人) ~~,有时候node版本也可能太低，需要升级

!> 注意，项目多的时候，可能需要切换node版本进行项目的初始化，几年前基本上不用关心node版本，但随着技术的进步，如使用vite做服务的时候，对于node版本有较高的要求
