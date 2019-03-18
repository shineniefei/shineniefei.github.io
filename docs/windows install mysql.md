---
title: win10 下 安装 mysql 8
---

# win10 下 安装 mysql 8

1. 首先去官网下载安装包

  ```txt
  https://dev.mysql.com/downloads/mysql/
  ```

2. 解压mysql到你安装的目录：E:/DB/mysql-8.0.11
3. 在E:/DB/mysql-8.0.11文件夹下面新建一个my.ini文件,内容如下： 

  ```txt
  [mysqld]
   # 设置3306端口
   port=3306
   # 设置mysql的安装目录
   basedir=E:/DB/mysql-8.0.11
   # 设置mysql数据库的数据的存放目录
   datadir=E:/DB/mysql-8.0.11/data
   # 允许最大连接数
   max_connections=200
   # 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
   max_connect_errors=10
   # 服务端使用的字符集默认为UTF8
   character-set-server=utf8
   # 创建新表时将使用的默认存储引擎
   default-storage-engine=INNODB
   [mysql]
   # 设置mysql客户端默认字符集
   default-character-set=utf8
   [client]
   # 设置mysql客户端连接服务端时默认使用的端口
   port=3306
   default-character-set=utf8
  ```

4. 到E:/DB/mysql-8.0.11/bin路径下，以管理员的身份打开cmd窗口，执行初始化命令

  ```cmd
  mysqld --initialize --user=mysql --console
  ```

  _一定要进行初始化,注意把临时密码记住_

5. 输入如下命令，进行服务的添加

  ```cmd
  mysqld -install
  ```

6. 输入如下命令，启动服务

  ```cmd
  net start mysql
  ```

7. 输入如下命令，进行登录数据库，用上面记住的密码登录

  ```cmd
  mysql -u root -p
  ```

8. 输入如下命令，，修改密码语句：

  ```sql
  ALTER USER root@localhost IDENTIFIED  BY 'root';
   #修改密码为：root
  ```

9. 修改密码验证方式

  ```sql
  ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
  ```

## **_备注_**

### 8.0之前版本，忘记密码修改方法

1. 找到bin目录：执行

  ```cmd
  mysqld --skip-grant-tables
  ```

2. 重新在开一个cmd窗口在bin目录执行

  ```cmd
  mysql
  ```

3. 就进入登陆状态了

### 5.7.22修改密码

1. 执行

  ```sql
  update user set authentication_string=password('123456') where user='root' and host='localhost';
  ```

### 5.6.修改密码

1. 执行：

  ```sql
  update user set password=password('123456') where user='root' and host='localhost';
  ```

## 问题

在cmd 下mysql服务mysql服务无法启动

```cmd
mysqld --console
```

## 其他

max_connect_errors = 10

配置说明

当此值设置为10时，意味着如果某一客户端尝试连接此MySQL服务器，但是失败10次，则MySQL会阻止此客户端连接。<br>
重置此计数器的值，必须重启MySQL服务器<br>
或者执行`FLUSH HOSTS;`
