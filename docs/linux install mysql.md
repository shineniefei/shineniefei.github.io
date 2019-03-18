---
title: MySQL Install
---

# MySQL Install

1. 以root用户登陆服务器，执行如下指令创建mysql用户组；

  ```bash
  groupadd mysql
  ```

2. 执行如下指令创建mysql用户，并配置用户归属组；

  ```bash
  useradd -d /home/mysql -g mysql -m mysql
  ```

3. 执行如下指令修改用户密码,简单密码需要重复输入两次

  ```bash
  passwd mysql
  ```

4. 执行切换到mysql用户，下载MySQL压缩包

  ```bash
  su - mysql
  wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.23-linux-glibc2.12-x86_64.tar.gz
  wget https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.13-linux-glibc2.12-x86_64.tar.xz
  ```

5. 解压到目录mysql用户目录下

  ```bash
  tar xf mysql-5.7.23-linux-glibc2.12-x86_64.tar.gz
  ```

6. 重命名mysql程序目录

  ```bash
  mv mysql-5.7.23-linux-glibc2.12-x86_64 mysql-5.7.23
  ```

7. 新建my.cnf文件，复制第8步内容并保存

  ```bash
  cd mysql-5.7.23
  vi my.cnf
  ```

8. my.cnf配置内容

  ```vim
  [mysqld]
  # 跳过授权表
  # skip-grant-tables
  # 设置mysql的安装目录
  basedir=/home/mysql/mysql-5.7.23
  # 设置mysql数据库的数据的存放目录
  datadir=/home/mysql/mysql-5.7.23/data
  # 客户端和服务器之间通讯指定一个套接字
  socket=/home/mysql/mysql-5.7.23/mysql.sock
  # 设置3306端口
  port=3306
  # 允许最大连接数
  max_connections=200
  # 允许连接失败的次数
  max_connect_errors=10
  # 服务端使用的字符集
  character-set-server=utf8mb4
  # 创建新表时将使用的默认存储引擎
  default-storage-engine=INNODB
  # 数据缓冲区
  # innodb_buffer_pool_size=1G
  # 设置默认密码格式mysql8
  default_authentication_plugin=mysql_native_password

  [mysql]
  # 设置mysql客户端默认字符集
  default-character-set=utf8mb4
  # 指定本地连接的socket套接字
  socket=/home/mysql/mysql-5.7.23/mysql.sock
  # 开启 tab 补全
  auto-rehash

  [client]
  # 设置mysql客户端默认字符集
  default-character-set=utf8mb4
  # 指定客户端连接的socket套接字
  socket=/home/mysql/mysql-5.7.23/mysql.sock
  ```

9. 进入mysql的bin目录，执行如下初始化命令并创建data目录

  ```bash
  # mysql 5.7 初始化命令
  ./mysqld --defaults-file=../my.cnf --initialize-insecure --user=mysql

  # mysql 8 初始化命令
  # 记住随机密码
  ./mysqld --defaults-file=../my.cnf --initialize-insecure --user=mysql --console
  ```

10. 启动mysql

  ```bash
  ./mysqld_safe --defaults-file=../my.cnf &
  ```

11. 登录mysql

  ```bash
  ./mysql -u root -p
  ```

  _mysql5.7首次密码为空，直接回车登录_ _mysql8输入前面生成的随机密码登录_

12. 修改root密码

  ```bash
  # 修改密码（5.7版本之后无password字段，更换为authentication_string）
  update mysql.user set authentication_string=password('root') where user='root' ;

  # 允许root用户远程访问
  update user set host='%' where user='root';
  # GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY '密码' WITH GRANT OPTION;

  # mysql 8.0从原来的 mysql_native_password 更改为 caching_sha2_password身份验证机制，修改方式
  ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '密码';
  # ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';

  # 重新载入授权表
  FLUSH PRIVILEGES;
  ```

  _从 5.7 升级 8.0 版本的不会改变现有用户的身份验证方法，但新用户会默认使用新的 caching_sha2_password_<br>
  _上面my.cnf配置中已切换使用以前的密码加密方式_<br>
  _mysql 5.6修改用户密码 `update user set password=password('root') where user='root' and host='localhost';`_

13. 使用navicat等工具，进行登录，登录成功，则在ssh中执行`quit;`退出mysql，以防止密码修改后登录不上，可再次修改。

14. 以上安装方式未设置开机自启，断电关机需登录mysql,进入mysql的bin目录，执行 `./mysqld_safe --defaults-file=../my.cnf &`

15. 替换7 - 10步骤，默认位置安装mysql方法，管理员登录

  ```bash
  # /etc/下新建my.cnf并复制上面的配置文件内容并保存
  vi /etc/my.cnf

  # 使用管理员登录，进入mysql程序目录，复制启动脚本
  cp -a support-files/mysql.server /etc/init.d/mysqld

  # 启动服务  
  /etc/init.d/mysqld start
  # service mysqld start

  # 停止服务  
  /etc/init.d/mysqld stop

  # 重启服务
  # service mysqld restart

  # 管理员登录，设置开机启动
  chkconfig --level 35 mysqld on
  ```

## mysql 常用命令

````
```sql
show databases; # 展示数据库
create database 数据库名; # 创建数据库  
use 数据库名字; # 选择数据库  
drop database 数据库名; # 直接删除数据库，不提醒  
show tables; # 显示表  
describe 表名; # 表的详细描述  
mysqladmin drop databasename # 删除数据库前，有提示。  
select version(),current_date,now(); # 显示当前mysql版本和当前日期  
mysql -h myhost -u root -p database < sql.txt # 从文件中读取  
```
````

## 8.0之前版本，忘记密码修改方法

1. 找到bin目录：执行`mysqld --skip-grant-tables`
2. 重新在开一个窗口在bin目录执行`mysql`就进入登陆状态了
3. 修改密码

  ```sql
  # 5.7 修改密码（5.7版本无password字段更换为authentication_string）
  update mysql.user set authentication_string=password('root') where user='root' ;

  # 5.8 修改密码
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';

  # 5.6 修改密码
  update user set password=password('root') where user='root' and host='localhost';
  ```

## 主从复制

### WIN下Master上的配置

1. 修改my.ini文件，增加二进制，和id

  ```txt
  # 开启二进制日志
  log-bin=E:\DB\MySQL-BIN-LOG\mysql-bin
  # 配置一个独立的ID
  server-id=1
  ```

2. Master添加复制权限用户，指令如下：

  ```sql
  GRANT REPLICATION SLAVE ON *.* to "master"@"%" identified by "master";
  ```

3. 重启mysql,检查状态，Master上登陆mysql，由于是首次安装部署MySQL数据库以及配置主从复制，可以重置并查看master的状态，指令如下：

  ```sql
  reset master;
  show master status;
  ```

### linux下Slave上的配置

1. 创建/home/mysql/mysql-5.7.23/BIN-LOG目录，修改my.cnf文件，增加内容

  ```txt
  server-id=2
  log_bin = /home/mysql/mysql-5.7.23/BIN-LOG/mysql-bin.log
  log_bin_index = /home/mysql/mysql-5.7.23/BIN-LOG/mysql-bin.log.index
  relay_log_info_repository = TABLE
  master_info_repository    = TABLE
  relay_log_recovery        = on
  ```

2. 重启mysql,检查状态，

  ```sql
  show variables where variable_name in  ('relay_log_info_repository','master_info_repository');
  ```

3. Slave上登陆mysql，由于是首次安装部署MySQL数据库以及配置主从复制，可以重置master的状态、Slave的状态，指令如下：

  ```sql
  reset master;
  reset slave all;
  ```

4. Slave上指定Master的地址、用户、密码等信息，指令如下：

  ```sql
  CHANGE MASTER TOMASTER_HOST="172.29.82.209",MASTER_PORT=3306, MASTER_USER="master", MASTER_PASSWORD="master",  MASTER_LOG_FILE='mysql-bin.000002';
  stop slave;
  change master to master_log_file='mysql-bin.000002',master_log_pos=154;
  start slave;
  ```

5. 执行如下指令，启动复制：

  ```sql
  start slave;
  ```

6. 执行如下指令查看Slave的状态（内容较多，展示部分结果）：

  ```sql
  show slave status \G;
  ```

  结果片段：

  ```txt
  Slave_IO_Running: Yes
  Slave_SQL_Running: Yes
  这两项均为Yes，才能保证Slave实时从Master上同步数据。
  Slave_SQL_Running_State: Slave has read all relay log; waiting for more updates
  Slave_SQL_Running_State，不出现error/aborting信息。
  ```

7. 停止主从

  ```sql
  stop slave;
  set GLOBAL SQL_SLAVE_SKIP_COUNTER=1;
  start slave
  ```
