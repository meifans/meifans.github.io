
## 常用命令

+ lsof 列出占用文件的进程信息
  + -i:<端口号> 列出符合条件的进程，协议，端口号
  + -p 列出指定进程号所打开的文件
+ cat /etc/redhat-release 查看linux具体版本

+ systemctl enable/start docker 启动docker服务

+ ll 查看权限
  >drwxr-xr-x
  >第一位代表文件类型，d:文件目录，l:链接文件,-:是普通文件，p:是管道
  >2，3，4(rwx)代表文件拥有者的权限，r是读，w是写，x是执行
  > 5，6，7(r-x)代表同组的用户权限
  > 8，9，10（r-x）代表其他人的权限


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
