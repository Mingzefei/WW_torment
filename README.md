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

- Powershell 配置

使用 choco 安装 git、nvim，及 nvim 插件。

nvim.coc 存在问题，不能正常使用。

创建 alias ：

```bat
nvim $PROFILE
" using
function xx {XXX}
```

### 20220810

- Powershell 配置

使用 ![lf](https://github.com/gokcehan/lf) 代替 ranger，为此安装了 GO。

nvim.coc 基本使用正常，向配置文件中添加部分推荐配置。

在 dotfiles 仓库中添加了 nvim/win.nvim，用于保存 win10 下 nvim 配置文件。

设置 GitHub 仅 pull 部分目录。

设置 win10 下的软链接，将 init.vim 和 coc-settings.json 绑定到相应位置。

- WSL2 nvim 安装和配置

安装 nvim 及 nvim.coc 插件。

由于 vim 和 nvim 版本过低，coc 插件无法运行，遂更新。

### 20220811

- WSL2 nvim.coc 配置

完成了主要配置，基本满足正常使用。

相关配置见 ![dotfile.nvim](https://github.com/Mingzefei/dotfiles/tree/master/nvim)。

 #TODO: 整理、统一 init.vim、vimrc

- Win10 输入法 BUG

莫名地在中英文之间切换，时间原因暂不修改，如不能修复考虑更换输入法。

 #TODO: win10, 输入法 BUG

- BHblj vim 配置

删除原 vimrc 中大部分插件，关闭主题，形成 vimrc.bhblj。

速度仍稍慢。

### 20220823

- WSL2 启动报错

```
文件名、目录名或卷标语法不正确。

[已退出进程，代码为 4294967295 (0xffffffff)]
```

解决方法：`netsh winsock reset` 重启

### 20220915

- latex 编译

使用 `xelatex -interaction=nonstopmode xxx.tex` 忽略编译过程中的交互输入

使用 `\usepackage{pdfpages}` 和 `\includepdf[page=-]{./path.file.pdf}` 插入外部 pdf 文件

使用 `\includepdfset{pagecommand={\thispagestyle{fancy}}}` 对插入的外部 pdf 添加页码

使用 `\includepdf[addtotoc={<pages>,<section>,<level>,<heading>,<label>},pages=-]{./path/file.pdf}` 记录在目录中

参考 [pdfpages 手册](http://www.ctan.org/tex-archive/macros/latex/contrib/pdfpages/pdfpages.pdf)

- WSL2 中 .ipynb 脚本找不到文件

解决方法：在 WSL2 中加入环境变量，再 code 或其他方式打开 .pynb 文件

### 20221116

- github token 设置

在 Developer settings 中生成 tokens，在终端添加现有 url

```
git remote set-url origin  https://<your_token>@github.com/<USERNAME>/<REPO>.git
```

### 20230321

- 设置 VScode 代理

在 WSL2 的终端使用 `code .` 可以直接用 Win 中的 VScode 打开当前目录（需要在 VScode 上配置好 WSL2）。
但是，需要在 VScode 中手动设置代理，用如下命令实现。
```bash
hostip=$(awk '/nameserver / {print $2;}' /etc/resolv.conf 2>/dev/null)
sed -i "s/http\.proxy.*/http.proxy\":\"http:\/\/$hostip:<your_port>\",/" \
    /mnt/c/Users/<your_username>/AppData/Roaming/Code/User/settings.json
```
可以将上述内容写入 `~/.zshrc` 或 `~/.bashrc` 以实现自动。

### 20230506

- 在 WSL2 中使用 GPU

安装过程参考 ![Windows11 + WSL Ubuntu + Pycharm + Conda for deeplearning](https://www.gongsunqi.xyz/posts/3c995b2a/)。

不同系统下的性能对比参考 ![深度学习：Windows11 VS WSL2 VS Ubuntu 性能对比，pytorch2.0性能测试！](https://www.gongsunqi.xyz/posts/3c995b2a/)。

- 在 WSL2 中挂载移动硬盘

```bash
sudo mount -t drvfs F: /mnt/f
#取消挂载为
sudo umount /mnt/f
```

