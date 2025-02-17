# ~~n 包的使用~~
废弃使用原因：不能自动管理npm版本。推荐使用`nvm`

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
> ~~ 安装指定的node版本 ~~ （已失效，连接超时），后面有解决办法
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


### 最新问题（2024年9月21日）
无法通过n命令安装node，原因：请求超时了。

解决办法：
```
// 设置环境变量为nodejs镜像站点，加速nodejs下载
export N_NODE_MIRROR=https://npmmirror.com/mirrors/node

// 执行zshrc文件，加载新环境变量设置
source ~/.zshrc

// -E继承当前环境变量 lts安装nodejs最新长期支持版本
sudo -E n lts

```

通过该命令安装node。
```bansh
sudo -E n 16.20.0
```
!> 并且每次关闭终端都需要执行一次解决办法中的前两个命令，否则还是会超时的。


#### 遇到npm版本不支持node版本的问题

WARN警告信息 ：npm v10.2.4不支持Node.js v16.18.1。这个版本的npm支持以下节点版本:' ^18.17.0 || >=20.5.0 '。您可以在 https://nodejs.org/ 上找到最新版本。

> 解决办法：安装低版本的node 如 `14.21.3`版本，在通过n命令切换到其他版本的时候就不会出现警告

#### 安装node地址

https://nodejs.cn/en/download/prebuilt-installer