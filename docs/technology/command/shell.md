
## 常用命令

+ lsof 列出占用文件的进程信息
  + -i:<端口号> 列出符合条件的进程，协议，端口号
  + -p 列出指定进程号所打开的文件

+ netstat -anp | grep "端口号"

+ cat /etc/redhat-release 查看linux具体版本
+ cat /proc/version        查看内核版本

+ systemctl enable/start docker 启动docker服务

+ zgrep

+ ll 查看权限
  >drwxr-xr-x
  >第一位代表文件类型，d:文件目录，l:链接文件,-:是普通文件，p:是管道
  >2，3，4(rwx)代表文件拥有者的权限，r是读，w是写，x是执行
  > 5，6，7(r-x)代表同组的用户权限
  > 8，9，10（r-x）代表其他人的权限

+ ps aux | grep 服务名    查看服务是否起来，什么时间起来的

+  压缩
  - tar -xf 文件名   解压缩文件
  - unzip 文件名  解.zip

+ mv 原文件 新名字    重命名和移动文件

+ netstat -a 列出所有端口

+ ip 地址
ifconfig | grep inet

+ 追溯DNS解析
  - host hostname（google.com）  显示域名解析后的ip
  - dig +trace  hostname    dns 解析过程

+ 权限
  - chmod 755 目录

+ 查看log
  - less 文件名    f 向下，k向上
  - head -n 1     只显示一条，与grep连用

+ 时间戳
  - date -r 1503486171   把时间戳换成时间
### zsh

**安装**

    brew install zsh
    chsh -s `which zsh`

#### 别名
zsh 不仅支持普通 alias，还支持针对文件类型的 alias。我配置的文件类型 alias 如下：

    alias -s gz='tar -xzvf'
    alias -s tgz='tar -xzvf'
    alias -s zip='unzip'
    alias -s bz2='tar -xjvf'
    alias -s php=vi
    alias -s py=vi
    alias -s rb=vi
    alias -s html=vi
    alias gcid="git log | head -1 | awk '{print substr(\$2,1,7)}' | pbcopy"

配置完毕之后，在 zsh 下直接输入xxx.rb，将自动用 vi 打开，直接输入xxx.tgz，将直接按照tar -xzvf解压。最后一个gcid将当前 git 项目的第一个 commit 的 id 复制到系统剪切板（pbcopy是 Mac 下的复制到系统剪切板命令，linux 请参考相应的发行版更改），在执行 rebase 的时候特别方便。

#### 自动补全
+ tar -      按tab自动补全参数，命令，路径
+ kill java  按tab会出现Java程序的进程号

#### 跳转
+ d        显示当前session访问过的目录
+ 目录      无需cd，直接输入目录。
+ ..       表示后退一级目录，../../后退两级

#### 历史记录
**跨session共享**
+ git-上   搜索用过的所有git命令

#### 通配符搜索
+ ls *.md   搜索当前目录下的md文件

#### oh-my-zsh
oh-my-zsh 是最为流行的 zsh 配置文件，提供了大量的主题和插件，极大的拓展了 zsh 的功能，推动了 zsh 的流行，有点类似于 rails 之于 ruby。

    # install
    # via curl
    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    # via wget
    sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

安装之后，source ~/.zshrc使之生效

**主题**

oh-my-zsh 内置了大量主题，可在~/.oh-my-zsh/themes中查看具体的配置。

**插件**

oh-my-zsh 提供极为丰富的插件，在~/.oh-my-zsh/plugins目录下查看具体的配置。在.zshrc中写入plugin(git autojump osx)即可使用插件

  * git 精简 git 命令，减少输入字符数。参见 [Plugin:git](https://github.com/robbyrussell/oh-my-zsh/wiki/Plugin:git)。该插件提供的快捷命令比较多，挑几个常用和好记的记忆即可，不必全记。

  * [autojump](https://github.com/wting/autojump)  按照你的使用频率记录路径，使得目录的跳转更为方便。安装brew install autojump。如需跳转到包含 'foo' 的目录，执行j foo，这是最基础，也是最常用的命令。除此之外，还有jc, jo, jco命令，查看官网文档获取更多的使用方法。

  * OSX 该插件增强 Mac 下的使用体验，提供了如下命令：
    - cdf: 在 Finder 中打开要 cd 的目录；
    - quick-look: 快速预览该文件，类似于在 Finder 中按下空格键；
    man preview: 在 preview 中打开 man page；
itunes: 命令行操作 iTunes。


## mac 环境

### 压缩 & 解压缩

+ 安装zsh extract 插件 ：提供各种压缩形式的解压缩（实际还是需要各种解压缩的命令支持）
  - zsh 中 ~/.zshrc 中 plugins=(... extract)
  - source ~/.zshrc

+ mac下没有unrar,使用 brew install unrar (解压rar文件)
