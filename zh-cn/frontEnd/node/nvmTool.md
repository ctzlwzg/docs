# nvm 工具

## 简介
- 是一种用于管理多个主动节点.js版本的工具。
- 安装nvm进行node版本管理，主要内容包括安装、使用nvm工具管理node、卸载 node

## 下载地址

### window
https://github.com/coreybutler/nvm-windows/releases

!> 如果电脑上之前已经单独安装了node，先卸载，然后再安装nvm，便于统一管理node

### macOS
1. 安装 Homebrew（如果尚未安装）：
Homebrew 是 macOS 上的一个包管理器，可以简化安装和管理第三方软件包（包括 nvm）的过程。
打开终端，输入以下命令来安装 Homebrew：
```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```
2. 使用 Homebrew 安装 nvm：
```bash
brew install nvm
```
3. 配置 nvm 环境变量：
```bash
vim ~/.zshrc
```
```bash
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
[ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
```
在 Vim 中，你可以按 Esc 键，然后输入 :wq 并按 Enter 来保存并退出。

4. 重新加载配置文件：
```bash
source ~/.zshrc
```

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

> 设置默认版本
```bansh
nvm alias default v14.17.0
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

### 项目中通过nvm配置文件配置node.js版本

在项目根目录下创建一个文件.nvmrc
```.nvmrc
v14.17.0
```

执行项目前，先执行以下命令，指定项目需要使用的node版本
```bash
nvm use
```

无需指定node版本，因为配置在了.nvmrc文件中

!> 注意：只有在mac系统重可以不指定node版本，windows系统还是指定node版本，不管.nvmrc文件是否配置

### 你在使用 nvm 安装 Node.js v14.21.0 时遇到了编译错误
Node.js v14.21.0 不支持 Apple Silicon (M1/M2) 芯片：

Node.js v14.x 版本在 Apple Silicon 上可能存在兼容性问题，尤其是在编译 OpenSSL 时。

打开终端，运行以下命令启动 Rosetta 2 模式：
```bash
arch -x86_64 zsh
```