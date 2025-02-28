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