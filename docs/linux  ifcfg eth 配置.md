---
title: linux ifcfg eth 配置
---

1. `cd /etc/sysconfig/network-scripts`

2. `vi ifcfg-eth0`

3. ifcfg内容<br>
  静态：

  ```txt
  # 网卡类型
  TYPE=Ethernet
  # 网卡接口名称
  DEVICE=eth0
  # 系统启动时是否自动加载
  ONBOOT=yes
  # 地址协议:static静态协议,bootp协议,dhcp协议
  BOOTPROTO=static
  # 网卡IP地址
  IPADDR=10.10.10.1
  # 网卡网络地址，子网掩码
  NETMASK=255.0.0.0
  # 网卡网关地址
  GATEWAY=10.10.10.1
  # 网卡DNS地址
  DNS1=10.10.10.1
  # 网卡广播地址
  BROADCAST=10.10.10.255
  # 网卡设备MAC地址
  HWADDR=
  ```

  动态：

  ```txt
  # 网卡类型
  TYPE=Ethernet
  # 网卡接口名称
  DEVICE=eth1
  # 系统启动时是否自动加载
  ONBOOT=yes
  # 地址协议:static静态协议,bootp协议,dhcp协议
  BOOTPROTO=dhcp
  # 网卡IP地址
  IPADDR=
  # 网卡网络地址，子网掩码
  NETMASK=
  # 网卡网关地址
  GATEWAY=
  # 网卡DNS地址
  DNS1=
  # 网卡广播地址
  BROADCAST=
  # 网卡设备MAC地址
  HWADDR=
  ```

4. `systemctl restart network`
