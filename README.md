# WW 折腾记

--------

@File : README.md
@Time : 2022/08/10 00:18:08
@Auth : Ming(<3057761608@qq.com>)
@Vers : 0.1
@Desc : recording of Win10 and WSL torment
@Refe : url1; url2

--------

## 说明

这是篇关于 Win10 和 WSL 的折腾记录。
追求优雅地使用工具。

> 吾一友，生性喜好折腾，经常端详手里的工具，时时磨出一些凹槽以方便
> 握持，雕刻一些花纹以彰显不俗。而受限于经验，常不能保证结果，工具
> 毁坏至不能用不在少数，重置数日后又手痒难耐。长此以往，故名“折腾”。
>
> 有人云，工具贵在使用，如功能、便利、效率。劳神费力，弃本逐末，适
> 得其反。友不以为然，大谈“折腾的过程也是思考和学习的过程”、“折腾方
> 向明确”云云。想法明确，不过暂时方法经验不足，故不名“瞎折腾”。

## 准则

- 不考虑 All In One，对特定的问题使用特定的工具。
- 风格统一，工具间切换流畅。例如，相似的 vim 方法和逻辑。
- 形成 dotfile 文件，方便配置备份和新平台中搭建。

## 记录

### 之前

已折腾一段时间，结果统一记录如下。

- 系统： win10 + wsl1(Ubuntu-20.04, zsh)
- 编辑器：
  - vscode(安装 VSCodeVim 插件)：课题项目
  - vim(参考 Theniceboy 配置)：脚本、远程
  - pycharm：较大项目
  - typora(配合 pandoc)：按样式排版、导出
  - obsidian：笔记整理

### 20220809

- WSL1 升级

因为后续有使用 GPU 的需要，而官方文档声明 WSL1 不支持 GPU 调用，必
需将当前的 WSL1 升级。

升级后最大的困难是文件O/I效率低，暂时将项目的所有数据迁移至 WSL2，
项目的所有程序和关键文档同步至 GitHub。

为两系统下的常用项目目录创建 alias ： `ww` win_workbench；`uw`
ubt_workbench。

升级过程占用内存极大，似乎将系统完全读写一遍。

- WSL2 配置

期间因内存占用过大而崩溃，重启后解决。

通过脚本获取 ip，使用 Clash 科学上网。向 `zshrc` 写入 `proxy` 命令，
执行后使用 Clash 的 7890 端口。

apt尝试使用 Ubuntu-20.04 默认源，未成功，换回清华源，使用时切回直连。

迁移文件时发现，井号 `#` 在 WSL2 下自动变为英式中的符号，通过设定系
统语言为美式英语解决。

卸载重装 git，原 git 反应慢，重装后恢复正常。

卸载重装 vim，原 vim 无法正常编辑文件，执行 `vi <file_name>` 后无响，
`ctrl + c` 后打开空白只读文件，重装后恢复正常。

使用 X410 可以实现 GUI，从 Microsoft Store 获得，但并没实际收费。

但是依然没有解决 vim image 插件的问题。

 #TODO: fix vim image

- WSL2 备份

Powershell 中执行`wsl --export <system_name> <path>\<outfile_name>`。

- VSCodeVim 配置

删除 vimrc 中插件、部分外部功能，形成适用于该插件的 vimrc.vscode。

部分功能，如锚定符，不能使用。

 #TODO: modify vimrc.vscode

- Powershell 配置

使用 choco 安装 git、nvim，及 nvim 插件。

nvim.coc 存在问题，不能正常使用。

创建 alias ：

```bat
nvim $PROFILE

# using
function xx {XXX}
```

 #TODO: modify ~/AppData/Local/nvim/init.vim for nvim.coc
