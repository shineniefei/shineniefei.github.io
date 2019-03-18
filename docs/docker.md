---
title: docker install
---

# docker install

1. Docker 要求系统的内核版本高于3.10

  ```bash
  uname -r
  ```

2. 直接写命令了

  ```bash
  yum -y update
  yum install -y yum-utils device-mapper-persistent-data lvm2
  yum-config-manager     --add-repo     https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
  yum install -y docker-ce
  groupadd docker
  useradd -d /home/docker -g docker -m docker
  usermod -aG docker docker
  systemctl enable docker
  systemctl start docker
  ```
