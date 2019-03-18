---
title: windows在apache中使用mod_wsgi部署flask
---

# windows在apache中使用mod_wsgi部署flask

1. 下载mod_wsgi Python的插件，选择 mod_wsgi-4.5.24+ap24vc14-cp37-cp37m-win_amd64.whl，

  ```txt
  http://www.lfd.uci.edu/~gohlke/pythonlibs/#mod_wsgi

  https://download.lfd.uci.edu/pythonlibs/h2ufg7oq/mod_wsgi-4.5.24+ap24vc14-cp37-cp37m-win_amd64.whl
  ```

2. 在下载时要选择相应的版本，否则Apache启动时会有问题<br>
  **_Apache24 VC是14_**<br>
  **_Python3.7_**<br>
  **_64位_**

3. 把下载的.whl文件复制到python37/Scripts下，命令行执行

  ```cmd
  pip install "mod_wsgi-4.5.24+ap24vc14-cp37-cp37m-win_amd64.whl"
  ```

4. 安装成功，python37/Scripts下命令行执行

  ```cmd
  mod_wsgi-express module-config
  ```

5. 输出如下三行结果

  ```txt
  LoadFile "d:/ide/python37/python37.dll"
  LoadModule wsgi_module "d:/ide/python37/lib/site-packages/mod_wsgi/server/mod_wsgi.cp37-win_amd64.pyd"
  WSGIPythonHome "d:/ide/python37"
  ```

6. 把这三行内容复制到apache的conf路径下http.cnf文件下进行配置

  ```txt
  #############################
  # 配置python下wsgi
  LoadFile "D:/IDE/Python37/python37.dll"
  LoadModule wsgi_module "D:/IDE/Python37/lib/site-packages/mod_wsgi/server/mod_wsgi.cp37-win_amd64.pyd"
  WSGIPythonHome "D:/IDE/Python37"

  # 监听端口
  Listen 81
  # python项目的根目录和wsgi路径
  <VirtualHost *:81>
  DocumentRoot  "D:/IDE/WorkSpace/Python/flask_test/"
  ServerName localhost:81
  WSGIScriptAlias / "D:/IDE/WorkSpace/Python/flask_test/flask_wsgi.py"
  </VirtualHost>

  # 虚拟目录的权限配置
  <Directory "D:/IDE/WorkSpace/Python/flask_test/">
     Options Indexes FollowSymLinks
     AllowOverride None
     Require all granted
  </Directory>
  ##############################
  ```

7. 注释http.cnf中的mod_wsgi.so（如果有）

  ```txt
  #LoadModule wsgi_module modules/mod_wsgi.so
  ```

8. 安装apache服务器，进入D:\IDE\Apache24\bin目录，执行如下命令安装

  ```cmd
  httpd.exe -k install
  # httpd.exe -k uninstall
  ```

  执行如下命令检查

  ```cmd
  D:\IDE\Apache24\bin>httpd.exe -n "Apache2.4" -t
  ```

9. 以服务启动
