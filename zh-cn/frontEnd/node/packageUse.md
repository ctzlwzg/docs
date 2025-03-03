# 一些常见包的使用

## prettier
用于格式化代码

### 安装：
> npm install --save-dev prettier@2.6.2

!>老项目最好指定一下版本，不用最新版本

在package.json中添加命令：

```json
"p:check": "npx prettier . --check",
"p:write": "npx prettier . --write"
```
第一条是用于检查代码格式，第二条是修改代码格式

### 配置校验文件
在根目录创建.prettierrc.json文件，内容如下：
```json
{
  "semi": true,
  "singleQuote": false,
  "printWidth": 280,
  "trailingComma": "none",
  "arrowParens": "avoid",
  "tabWidth": 2,
  "singleAttributePerLine": false,
  "bracketSameLine": true
}
```

### 配置忽略文件（不去格式化的文件）
在根目录创建.prettierignore文件，内容如下：
```
dist
test_dist
pnpm-lock.yaml
LICENSE.md
tsconfig.json
tsconfig.*.json
```
一些打包生成的目录不需要格式化，（测试默认node_modules是不会被格式化的，就不用配置了）

### 安装 Prettier - Code formatter 扩展

### 格式化注意事项
需要格式化的页面需要右击设置`使用...格式化文档，选择设置默认值 Prettier - Code formatter`，这一点很关键，不然格式化不了

## ESLint
查找并修复 JavaScript 代码中的问题

!> 老项目就不要用了，新项目必须规范一下代码。，新项目安装9版本以上的包。
### 安装
> npm init @eslint/config@latest

安装时会让你选择需要的配置，然后生成`eslint.config.js`文件


在package.json中添加命令：

```json
"lint": "npx eslint ."
```

检查整个项目下的代码错误（或者说是不规范的代码）

## sass
SCSS 预处理器
> npm install --save-dev sass

注意：有些项目中会安装node-sass，这个是sass的旧版本，现在用的是sass，所以老项目的话需要单独再安装其他包。

最新项目直接安装sass即可

## check-node-version
用于运行命令前检查node版本。
> npm install --save-dev check-node-version

在package.json中添加命令：

```json
"predev": "check-node-version --node '>=14.18.1 <15.0.0'",
"dev": "vue-cli-service serve --mode dev",
```
比如有一条`npm run dev`命令，那么对应配置一条以`pre`开头的命令，比如`predev`，然后运行`npm run dev`就会检查node版本，如果版本不对就会报错，如果版本对就会运行`npm run dev`

看下失败的情况：
```
haiye@wzg haiye_phonemom_web % npm run dev

> haiye_phonemom_web@0.1.0 predev
> check-node-version --node '>=14.18.1 <15.0.0'

node: 15.14.0
Wanted node version >=14.18.1 <15.0.0 (>=14.18.1 <15.0.0)
To install node, see https://nodejs.org/download/release/v14.18.1/
```

在不符合的版本下，会报错，并且会告诉开发者需要的node版本范围，此时再结合一下`nvm`安装切换node版本，就可以解决这个问题了。