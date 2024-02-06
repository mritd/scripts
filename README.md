# scripts

## 脚本仓库

这是一个包含一些自己常用的小脚本发布仓库, 这些脚本大部分用于系统、软件初始化配置; 大多数配置文件从 [conf](https://github.com/mritd/conf) 仓库获取并通过 CI 自动发布.

## 如何使用

本仓库发布的脚本已经讲大多数所需依赖压缩到单个脚本内, 直接下载执行即可:

```sh
curl -fsSL https://github.com/mritd/scripts/releases/download/v1.0.0/prezto.sh > /tmp/prezto.sh
bash /tmp/prezto.sh
```

**注意: 该脚本不支持管道执行, 例如 `curl -fsSL https://github.com..../prezto.sh | bash`.**

## 脚本源码

该仓库内脚本通过 [makeself](https://github.com/megastep/makeself) 工具打包, 所以如果担心安全问题或想知道脚本都做了什么, 可以通过以下命令解压脚本:

```sh
root@826833b6769e ~ # ❯❯❯ bash ./prezto.sh --noexec --target ./xxxx
Creating directory ./xxxx
Verifying archive integrity...  100%   MD5 checksums are OK. All good.
Uncompressing Kovacs prezto Config  100%
root@826833b6769e ~ # ❯❯❯ ls xxxx
prezto  dir_colors  install.sh  zpreztorc  zshrc
```

每个脚本解压后都会有一个 `install.sh`, 该内部脚本用于实际安装.
