

## 安装

###  CentOS         
 安装：curl -sSL https://get.daocloud.io/docker | sh


sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
[dockerrepo]
name=Docker Repository
baseurl=https://mirrors.tuna.tsinghua.edu.cn/docker/yum/repo/centos7
enabled=1
gpgcheck=1
gpgkey=https://mirrors.tuna.tsinghua.edu.cn/docker/yum/gpg
EOF



## 运行服务

### mysql

### 运行mysql instance
1. docker pull mysql:latest (或者mariadb) 也可不写，默认最新的tag
2. docker run --name master -p 3306:3306  -e MYSQL_ROOT_PASSWORD=123456  -e REPLICATION_MASTER=true -d mysql:latest
> mysql:latest 一定要在最后，不然 -e 之类的参数会作为启动mysql的参数传入，而不是启动镜像的参数，导致错误ba

3. mysql -h127.0.0.1 -P3306 -uroot -p123456  连接master
>  或者通过 docker exec -it containerId /bin/bash  进入容器命令行
>  在通过 mysql -uroot -pgroup-replication 使用刚才设置的root密码进入mysql控制台,exit退出控制台，再次exit退出docker      



#### mysql group replication docker

以为mysql group replication 要求集群在一个子网中。所以首先使用docker 创建子网。

1. docker network create 网络名

2. docker run -d --net=网络名 -p 3306:3306 --name=master perconalab/mysql-group-replication --loose_replication_boostrap_group=ON
> 这里起了主节点，叫master

3. docker run -d --net=网络名 --name=slave-1 perconalab/mysql-group-replication --loose_replication_group_seeds='master:6606'
> 这里起了从节点，叫slave-1

4. 允许从本地访问mysql集群的用户为 rpl_user 密码：rpl_pass

`从本地无法连接起的mysql集群`

1. docker exec -it containerId bin/bash
2. mysql -uroot
3. select host,user from mysql.user;
4. host行值为%对应的用户，是允许从外网了连接进来的。localhost 是只允许本地连接

mysqld -verbose --help | grep bind-address 查看mysql连接


`基于mysql8，命令行创建`
主：
      docker run --net=meifans -d -p3333:3306 -e MYSQL_ROOT_PASSWORD=123456  --name=node1 mysql:8 --server-id=1 


#### 在本地直接配置msyql_group_replication实例

在当前目录初始化mysql：

      1. mkdir data
      2. /usr/local/Cellar/mysql/5.7.18/bin/mysqld --initialize-insecure --basedir=/usr/local/Cellar/mysql/5.7.18 --datadir=$PWD/data/s1

      3. cd data/s1   touch s1.cnf
      4. atom s1.cnf                 添加配置

      5. /usr/local/Cellar/mysql/5.7.18/bin/mysqld --defaults-file=/Users/pengfei.zhao/Project/mysql-group-replication/data/s1/s1.cnf

      6. mysql -uroot -p -S /usr/local/Cellar/mysql/5.7.18/s1.sock       连接这个mysql instance

创建用于组复制的用户：
      SET SQL_LOG_BIN=0;
      CREATE USER rpl_user@'%';
      GRANT REPLICATION SLAVE ON *.* TO rpl_user@'%' IDENTIFIED BY 'rpl_pass';
      FLUSH PRIVILEGES;
      SET SQL_LOG_BIN=1;
      CHANGE MASTER TO MASTER_USER='rpl_user', MASTER_PASSWORD='rpl_pass' FOR   CHANNEL'group_replication_recovery';


启动组复制：
      INSTALL PLUGIN group_replication SONAME 'group_replication.so';        
      SET GLOBAL group_replication_bootstrap_group=ON;                      **只在第一个server时使用，其后server不适用**
      START GROUP_REPLICATION;
      SET GLOBAL group_replication_bootstrap_group=OFF;                      **只在第一个server时使用，其后server不适用**

      >要启动组，请指示 server s1 引导组，然后启动组复制程序。 此引导应仅由单个 sever 独立完 成，该 server 启动组并且只启动一次。 这就是为什么引导配置选项的值不保存在配置文件中的 原因。 如果将其保存在配置文件中，则在重新启动时，server 会自动引导具有相同名称的第二 个组。 这将导致两个不同的组具有相同的名称。 同样的道理适用于停止和重新启动插件，并且 此选项设置为 ON。


添加数据：
      CREATE DATABASE test;
      use test
      CREATE TABLE t1 (c1 INT PRIMARY KEY, c2 TEXT NOT NULL);
      INSERT INTO t1 VALUES (1, 'meifans');
      SELECT * FROM t1;
      show binlog events;

查看用户
      select host,user from mysql.user;
验证binlog
      show binlog events;
验证组成员加入
      select * from performance_schema.replication_group_members;
验证server2已同步
      show databases like 'test';


创建命令

docker run --net=meifans -d -p3333:3306 -e MYSQL_ROOT_PASSWORD=123456 -v my.cnf:/etc/my.cnf --name=node1 mysql:8 --server-id=1






## 日常命令

+ docker ps 列出运行的服务
    - -a 列出所有容器，包括未运行的。

+ docker images 列出所有


## 随笔
+ docker exec -it container-id 或者 image bash  进入运行中服务的环境里，可以env查看环境设置等。
  > 也可用 docker inspect container-id 来查看env
+
