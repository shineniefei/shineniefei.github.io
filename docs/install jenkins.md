---
title: install jenkins
---

# install jenkins

## docker install jenkins

```shell
docker pull jenkins/jenkins:lts

mkdir -p /var/jenkins_home
chmod -R 777 /var/jenkins_home
chown -R 1000:1000 /var/jenkins_home

mkdir -p /home/docker/jenkins/data
chmod -R 777 /home/docker/jenkins/data
chown -R 1000:1000 /home/docker/jenkins/data

# -d 后台 --name 名字 -p 外端口可修改和容器端口 -p -v 服务器目录和挂载目录 镜像名
docker run -d --name jenkins -p 8082:8080 -p 50000:50000 -v /home/docker/jenkins/data:/var/jenkins_home  jenkins/jenkins:lts

docker logs jenkins
docker exec -t jenkins /bin/bash
# 权限问题查不了
cat /home/docker/jenkins/data/secrets/initialAdminPassword

docker images

docker ps

docker stop `CONTAINER ID`

docker rm jenkins

docker run -d --name jenkins -p 8082:8080 -p 50000:50000 -v /home/docker/jenkins/data:/var/jenkins_home  jenkins/jenkins:lts

systemctl sop docker
rm -rf /var/bin/docker
```

## user jar install jenkins

1. 安装jdk8
2. 创建用户

  ```bash
  useradd -g user -d /home/jenkins -m jenkins
  passwd jenkins
  su - jenkins
  wget https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/2.150.1/jenkins.war
  ```

3. 启动脚本

  ```bash
  /bin/bash

  : << !
  for start jenkin by java -jar
  !

  # set jenkins_home path
  if [[ ! -n `grep "JENKINS_HOME" ~/.bash_profile` ]];then
   sed -i '$aexport JENKINS_HOME='${HOME}'/jenkins_home' ~/.bash_profile
   echo 'add jenkins home'
  else
   echo 'jenkons home already in bash_profile'
  fi

  # mkdir jenkins_home
  if [[ ! -d ${HOME}/jenkins_home ]] ; then
   mkdir -p ${HOME}/jenkins_home
   echo 'mkdir jenkins home'
  else
   echo -e 'jenkins home is already in '${HOME}''
  fi

  # jenkins run or not and kill
  jenkins_pid=`ps -ef | grep 'java -jar jenkins.war'| grep -v grep| awk '{print $2}'`
  if [ ${jenkins_pid} > 1 ];then
   echo 'jenkins is running'
   echo "kill jenkins ？ please input (y\n)"
   read char
   if [ ${char} = 'y' ];then
       kill -9 ${jenkins_pid}
       echo 'kill jenkins success'
   else
       echo 'not kill jenkins and exit'
       exit 0
   fi
  else
   echo 'no jenkins is running'
  fi

  # start jenkins
  nohup java -jar jenkins.war --ajp13Port=-1 --httpPort=8081 >/dev/null 2>&1 &
  echo "start jenkins with command: 'nohup java -jar jenkins.war --ajp13Port=-1 --httpPort=8081 >/dev/null 2>&1 &'"
  echo `ps -ef | grep 'java -jar jenkins.war'| grep -v grep| awk '{print $2}'`
  ```

4. 初始密码

  ```bash
  more .jenkins/secret/initialAdminPassword
  more ~/jenkins_home/secret/initialAdminPassword
  ```
