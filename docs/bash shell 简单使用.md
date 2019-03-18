---
title: bash shell 简单使用
---

# 直接弄点会的上来

```bash
#!/bin/bash

if [ -f /home/public ] ; then
    cd /home/public
else
    sudo mkdir /home/public
    cd /home/public
fi

mkdir workspace
cd workspace

# 获取当前目录
WORK_DIR=`pwd`

# 输出当前目录
echo ${WORK_DIR}

# 获取当前用户名
USER_NAME=`whoami`

# 输出当前用户名
echo ${USER_NAME}

# 创建test文本
touch test.txt

# 获取目录下文件
TEST_FILE=${WORK_DIR}/test.txt

# 输出当前目录下文件
echo ${TEST_FILE}

# 获取外网地址
NETADDR_OUTER=`curl http://members.3322.org/dyndns/getip`

# 获取内网地址
NETADDR_INNER=`/sbin/ifconfig | grep "inet addr" | grep -v "127.0.0.1" | cut -d ':' -f2 | awk '{print $1}'`

# 优先使用内网
if [ "${NETADDR_INNER}" = "" ] ; then
    NETADDR_INNER=${NETADDR_OUTER}
fi

# 文件追加内容
echo -e "NETADDR_OUTER:${NETADDR_OUTER}\nNETADDR_INNER:${NETADDR_INNER}"  >>文件名

# 追加文件
sed '$a\eof'  ${TEST_FILE}

# 输出文件内容
echo `cat ${TEST_FILE}`

# 读取文件内容
key_vlaue=`cat ${TEST_FILE} | grep 'NETADDR_OUTER' | awk -F':' '{ print  $2 }'`

# 输出参数
echo -n "不换行\n"
echo  "默认换行"
echo -e "转译换行\n"

# 检查IP
ip=${NETADDR_OUTER}
echo $ip | perl -ne 'exit 1 unless /\b(?:(?:(?:[01]?\d{1,2}|2[0-4]\d|25[0-5])\.){3}(?:[01]?\d{1,2}|2[0-4]\d|25[0-5]))\b/'
if [ $? -eq 1 ]
    then
    echo "$ip is not availd ip ..."
    exit
fi

# 等待人工输入
while true
do            
echo -e  "Are you Sure?  if you input n, bash will exit and you can change the config  [y/n]"
read  -r input
case $input in
    [yY][eE][sS]|[yY])
    break
esac
    exit
done

# 循环
loop(){
    while true
        do
            echo -e  "do"
        case 
            echo -e "case do"
        esac
            echo -e "esac do"
            exit
    done
}

# 创建目录
mkdir test

if [ -d ${WORK_DIR}/test ] ; then
    rm -rf ${WORK_DIR}/test
    echo "delete ${WORK_DIR}/test"
fi

# 创建文件
touch lib1 lib2 lib3

# 增加执行权限（单条命令换行）
if [ ! -x lib1 ] ; then
    chmod +x lib1 \
    lib2 \
    lib3
fi

# 创建软链接
ln -s -f lib1 libone
ln -s -f lib2 libtwo
ln -s -f lib3 libthree

# 使用环境变量生效
source_env(){
    tar -xf ${1}
    rm -rf ${1}
    if [ -f /etc/profile.d/${2} ] ; then 
        sudo rm /etc/profile.d/${2}
        echo "remove the old env file."
    fi
    dos2unix ./${2}
    sudo mv ${2} /etc/profile.d/
    sudo chown ${USER_NAME}:users /etc/profile.d/${2}
    sudo chmod 700 /etc/profile.d/${2}
    source /etc/profile.d/${2}
    echo "source env success."
}

# 修改工作目录下test文件内容
if [ -d ${WORK_DIR} ] ; then
    cd ${WORK_DIR}
    if [ -f ${TEST_FILE} ] ; then
        sed -i '/NETADDR_OUTER/c\NETADDR_SED' ${TEST_FILE}
    echo -e "modify ${TEST_FILE} success.\n"
    fi
fi

# 后台打开文件
nohup vi ${TEST_FILE} >/dev/null 2>&1 &

# 强制结束vi进程
echo -e  "NOW will stop Server\n"
PID=`ps -ef |grep ${USER_NAME}|grep ${TEST_FILE}|grep -v "grep"|awk '{print  $2}'`
# PID=`ps -ef |grep ${USER_NAME}|grep servername|grep -v "grep"|awk '{print  $2}'|awk '{a=$0;getline;print a,$0}'`
kill -9 ${PID}

# 重启tomcat6
start_server(){
    PID=`ps -ef |grep ${USER_NAME}|grep tomcat6|grep -v "grep"|awk '{print  $2}'`
     # PID=`ps -ef |grep ${USER_NAME}|grep servername|grep -v "grep"|awk '{print  $2}'|awk '{a=$0;getline;print a,$0}'`
    kill -9 ${PID}
    echo -e  "NOW will start Server\n"
    cd ${HOME}
    if [ -f  tomcat6/bin/startup.sh ] ; then
        sh tomcat6/bin/startup.sh
    fi
    if [ -f  App/app ] ; then
        nohup App/app >/dev/null 2>&1 &
    fi
}
```
