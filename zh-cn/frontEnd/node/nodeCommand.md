# npm相关

> npm init / npm init -y

- 项目初始化 ，-y 默认同意初始化的配置信息

> npm install 包名 参数 / npm i 包名 参数
- 安装包的命令

## 参数

- -S / --save 上线以后还需要使用的包
- -D / --dev 开发时候需要的包 如：less 只需要编译 less 文件
- -g 全局安装

### 举例说明
> npm i vue -S

在package.json文件dependencies属性下面就会有一条记录
```json
"dependencies": {
  "vue": "^2.7.10"
}
```

> npm i sass -D
在package.json文件devDependencies属性下面就会有一条记录
```json
"devDependencies": {
  "sass": "^1.26.5"
}
```

## 其他命令
> npm uninstall 包名 参数 / npm un 包名 参数

- 删除对应的包
- 参数要和安装的时候相同

> npm outdated 参数
- 查看需要更新的包
- 参数 -g 可查看全局包的更新情况
- 查看项目中包的更新情况 无需参数 -S 或 -D

> npm update 包名
- 更新包
  - 该更新不会跨大版本更新，比如vue 2.6.11 不会更新到 vue 3.xx.xx，只会更新到如： 2.7.
  - 如vue现在版本^2.6.11，npm update vue 以后 package.json 文件中还是^2.6.11版本，而package-lock.json中为 2.(大于等于6).x，即2.7.15
  - 在补充一点，如果删除package-lock.json，手动修改版本号如 ^2.6.11 改成 ^2.7.11，在package.json显示 ^2.7.11，而在package-lock.json中显示 2.7.15， 对应大版本的最新版本 **2版本不会变成3**

> 清除npm缓存，一般不需要清理
```bash
npm cache clean -f
```
> 查看npm的配置列表
```bash
npm config list
```
> 配置国内淘宝镜像地址（下载包更快）
```bash
npm config set registry https://registry.npm.taobao.org/
```
> 验证修改是否生效
```bash
npm config get registry
```

## 文件解释

### package.json
- 保存了项目的依赖的各种包
- 包版本 \^ 和 \~ 区别
  - "vue": "^2.6.11", 选取范围 < 3.0.0 版本 且大于等于 2.6.11 版本
  - "@vue/cli-plugin-babel": "~4.3.0", 安装最新的小版本 4.3.x, x选取最大的

### package-lock.json
- 锁定了具体的版本，避免语义版本带来项目bug
- 通过命令行操作软件包是此文件会根据package.json的内容自动被npm修改，不能自己修改该文件
- **当package.json和package-lock.json中包版本一致时，npm i根据package-lock.json来**
- 否则根据package.json来，并同步更新到package-lock.json中（有歧义，真实测试下来，package-lock.json对应的版本会是大版本不变，后边对应的版本为最新的版本）效果和npm update 包名差不多

## ~~cnpm命令(目前我是不用的)~~

> 如使用 cnpm 命令，一定需要带参数安装 -S ，-D, -g

!> npm 与 cnpm 命令不要同时使用，避免不必要的问题
