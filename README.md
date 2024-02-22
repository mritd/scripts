# scripts

## 一、仓库说明

这是一个包含一些自己常用的小脚本发布仓库, 这些脚本大部分用于系统、软件初始化配置; **脚本通过内嵌资源文件的方式实现在网络状况不佳的情况下一次性初始化各种配置**,
本仓库脚本大多数配置文件从 [conf](https://github.com/mritd/conf) 仓库获取并通过 CI 自动发布.

## 二、如何使用

本仓库发布的脚本已经将大多数所需依赖压缩到单个脚本内, 直接下载执行即可:

```sh
curl -fsSL https://github.com/mritd/scripts/releases/download/v1.0.0/prezto.sh > /tmp/prezto.sh
sh /tmp/prezto.sh
```

**注意: 该脚本不支持管道执行, 例如 `curl -fsSL https://github.com..../prezto.sh | sh`.**

## 三、脚本源码

本仓库内脚本通过 [makeself](https://github.com/megastep/makeself) 工具打包, 所以如果担心安全问题或想知道脚本都做了什么, 可以通过以下命令解压脚本:

```sh
root@826833b6769e ~ # ❯❯❯ bash ./prezto.sh --noexec --target ./xxxx
Creating directory ./xxxx
Verifying archive integrity...  100%   MD5 checksums are OK. All good.
Uncompressing Kovacs prezto Config  100%

root@826833b6769e ~ # ❯❯❯ ls xxxx
prezto  dir_colors  install.sh  zpreztorc  zshrc
```

每个脚本解压后都会有一个 `install.sh`, 该内部脚本用于实际安装流程, 查看此脚本即可阅读完整执行流程.

## 四、脚本说明

### 4.1、prezto.sh

![prezto](images/prezto.jpeg)

该脚本用于初始化 zsh 配置框架 `prezto`, `prezto` 是一个类似 `ohmyzsh` 的 zsh 配置框架, 但比 `ohmyzsh` 速度更快更轻量; **该脚本运行后会安装 `prezto` 并配置 `~/.zshrc`, `~/.zshrc` 目前基本配置逻辑如下:**

- 同时兼容 `macOS` 和 `Linux` 系统
- 默认为所有开发工具(java、go...)等都安装在 `/opt/devtools` 目录
- 自动将 `/opt/devtools/*/bin`、`/opt/devtools/*/sbin`、`/opt/devtools/bin`、`/opt/devtools/sbin` 目录加入到 `PATH` 变量中
- `macOS` 系统下自动将 `brew` 安装的常用工具加入到 `PATH` 中, 例如 `curl`、`mysql-client`、`ruby` 等
- `Linux` 系统下自动设置 locale 相关变量为 `en_US.UTF-8`, 例如 `LANGUAGE`、`LANG`、`LC_ALL` 等
- 对已安装的容器相关的命令自动生成 zsh 补全方法, 例如 `docker`、`podman`、`nerdctl`、`kubectl`、`helm` 等
- **默认将 `~/.user.secret"` 声明为全局变量, 该文件默认不存在, 目的是存放一些个人机密环境变量, 例如 GitHub Token 等**

**脚本配置可能后期调整, 具体请参考 [conf](https://github.com/mritd/conf) 仓库中的配置文件**

### 4.2、vim.sh

![vim](images/vim.jpeg)

该脚本用于初始化 vim 配置, 包括自动安装 [vim-plug](https://github.com/junegunn/vim-plug) 插件管理器以及自动安装一些差价等; 该脚本会自动配置 `~/.vimrc` 文件, 目前 `~/.vimrc` 文件基本配置逻辑如下:

- 加载 `~/.vimrc_plug` 内的常用插件
- 调整一些基础配置, 包括不限于 语法高亮、缩进大小、行号显示、编码等
- 添加自定义命令 `W` 以解决 **编辑特殊文件前忘记使用 `sudo` 而不得不退出然后重新编辑再保存问题**

### 4.3、tmux.sh

![tmux](images/tmux.jpeg)

该脚本用于初始化 tmux 配置, 主要包括自动安装 [tpm](https://github.com/tmux-plugins/tpm) 插件管理器以及自动安装一些 tmux 插件; 该脚本会自动配置 `~/.tmux.conf` 文件, 目前 `~/.tmux.conf` 文件基本配置逻辑如下:

- **默认前缀按键更换为 `Ctrl+s`**
- 开启 `OSC 52` 支持
- 调整窗口样式, 包括不限于自动标题、左右状态栏显示等
- 安装常用插件, 将暂停插件快捷键更换为 `F12`(一般用于多 tmux 嵌套)
- 默认创建三个 session `🍁 local`、`🌋 test`、`🌀 prod`

