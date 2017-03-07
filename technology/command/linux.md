
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
