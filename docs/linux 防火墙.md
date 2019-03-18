---
title: 防火墙设置
---

# SUSE

```
SuSEfirewall2 stop   #停止firewall

chkconfig SuSEfirewall2_setup off   #禁止firewall开机启动1
chkconfig SuSEfirewall2_init off  #禁止firewall开机启动2

chkconfig --list|grep fire    #查看防火墙状态
```

# CentOS 7

--------------------------------------------------------------------------------

```
systemctl status firewalld  #firewall状态
systemctl start firewalld.service        #启动firewall
systemctl stop firewalld.service        #停止firewall
systemctl disable firewalld.service  #禁止firewall开机启动
```

# Centos 6

--------------------------------------------------------------------------------

```
service iptables stop     #关闭防火墙
service iptables start    #启动防火墙
service iptables restart  #重启防火墙
service iptables status   #查看防火墙状态
chkconfig iptables off    #永久关闭防火墙
chkconfig iptables on    #永久关闭后启用
```

# 重启网络服务

--------------------------------------------------------------------------------

```
service network restart
```

# 防火墙开放端口

--------------------------------------------------------------------------------

1. SuSE默认的防火墙设置为禁止所有外来联结。 如果你想开放某个端口的话，就得修改防火墙设置开放这个端口。
2. 修改SuSE的防火墙设置以开放某指定端口，手动修改：

  ```
  vi /etc/sysconfig/SuSEfirewall2
  ```

  ```
  FW_SERVICES_EXT_TCP = "6000"     #TCP端口的情况
  FW_SERVICES_EXT_UDP = "177"    #UDP端口的情况
  ```

  ```
  rcSuSEfirewall2 restart    #防火墙设置重启生效
  ```

3. 添加防火墙规则：

  ```
  iptable -A INPUT -p udp -s 0/0 -d 0/0 --dport 177 -j ACCEPT
  ```
