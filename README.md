# ansible-role-datasphere
基于Ansible自动化部署datasphere(openeuler、linkis1.3.2、ambari+hdp3.1.5)
### 部署步骤
#### 外网构建ubuntu离线软件包
#### 拷贝所有软件包到离线环境
#### 安装ansible软件
#### 一键安装ambari组件
#### 一键安装datasphere组件

### 编译apache-linkis-1.3.2-bin.tar.gz
```text
方法一、参考官方[版本适配](https://linkis.apache.org/zh-CN/docs/latest/deployment/version-adaptation/)
方法二、下载编译 https://github.com/stdnt-xiao/linkis/tree/release-1.3.2-hdp3.1.5
```

### 安装步骤
* 节点密钥配置
* 拷贝软件包到/opt目录
* 构建本地debs包
* 安装ansible
* 安装java、nginx、ambari
* 通过ambari部署hdp组件
* 部署linkis+dss

### ambari安装
```text
ambari-server setup --jdbc-db=mysql --jdbc-driver=/opt/ansible-role-datasphere/roles/ambari/files/mysql-connector-java-8.0.30.jar
jdbc:mysql://node001:3306/hive?SrverTimezone=UTC&useUnicode=true&characterEncoding=utf8&useSSL=false

yarn.dns 8053
```
### linkis安装
```
/home/hadoop/linkis/lib/linkis-engineconn-plugins/hive/dist/3.1.0/lib 修改jar需要重启所有服务
sh bin/linkis-cli -submitUser  hadoop  -engineType hive-3.1.0  -codeType hql  -code "show tables"
```
### dss安装
```text
/home/hadoop/dss/conf/dss-flow-execution-server.properties
```

```
[hadoop@6c9f3ece5ee9 Install]$ ll
total 88
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:58 dss
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:59 exchangis
drwxr-xr-x  1 hadoop hadoop 4096 Apr 13 07:03 flink
drwxr-xr-x  1 hadoop hadoop 4096 Mar 17 08:58 hadoop-2.7.2
drwxr-xr-x  1 hadoop hadoop 4096 Apr 26 13:35 hive
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:57 linkis
drwxr-xr-x  1 hadoop hadoop 4096 May  4 07:13 qualitis
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:58 schedulis
drwxr-xr-x 15 hadoop hadoop 4096 Mar 16 03:57 spark
drwxr-xr-x  5 hadoop hadoop 4096 Mar 16 03:57 spark-cmd
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:57 streamis
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:57 visualis
drwxr-xr-x  1 hadoop hadoop 4096 Mar 16 03:57 web
[hadoop@6c9f3ece5ee9 Install]$ cd schedulis/
```

root@node001:/opt# ll
total 48
drwxr-xr-x 11 root   root   4096 Jun  2 16:10 ./
drwxr-xr-x 27 root   root   4096 Jun  2 16:10 ../
drwxr-xr-x  6 root   root   4096 Jun  2 15:33 ansible-role-datasphere/
drwxr-xr-x 10 hadoop hadoop 4096 Jun  2 16:10 apache-dolphinscheduler-1.3.9-bin/
drwxr-xr-x  8 hadoop hadoop 4096 Jun  2 16:03 apache-linkis-1.3.2/
drwxr-xr-x  4 hadoop hadoop 4096 Jun  2 16:06 apache-linkis-1.3.2-web/
drwxr-xr-x  3 root   root   4096 Jun  2 15:32 debs/
drwxr-xr-x 12 hadoop hadoop 4096 Jun  2 16:10 dolphinscheduler/
drwxrwxrwx  6 hadoop hadoop 4096 Jul  1  2022 dss-dolphinscheduler-client/
-rw-r--r--  1 root   root   1003 Jun  2 15:34 mysql_dump_script.sh
drwxr-xr-x  7 hadoop hadoop 4096 Jun  2 16:08 wedatasphere-dss-1.1.1/
drwxr-xr-x  4 hadoop hadoop 4096 Jun  2 16:10 wedatasphere-dss-1.1.1-web/

hadoop@node001:/home/hadoop$ ll
total 64
drwxr-xr-x 12 hadoop hadoop 4096 Jun  2 16:49 ./
drwxr-xr-x 15 root   root   4096 Jun  2 15:51 ../
drwx------  3 hadoop hadoop 4096 Jun  2 16:03 .ansible/
-rw-------  1 hadoop hadoop  168 Jun  2 16:49 .bash_history
-rw-r--r--  1 hadoop hadoop  220 Apr  5  2018 .bash_logout
lrwxrwxrwx  1 hadoop hadoop   21 Jun  2 16:04 .bash_profile -> /home/hadoop/.profile
-rw-r--r--  1 hadoop hadoop 3771 Apr  5  2018 .bashrc
drwx------  4 hadoop hadoop 4096 Jun  2 16:08 .cache/
drwxrwxr-x  3 hadoop hadoop 4096 Jun  2 16:08 .config/
drwxr-xr-x 10 hadoop hadoop 4096 Jun  2 16:10 dss/
drwxr-xr-x  3 hadoop hadoop 4096 Jun  2 16:08 dss-bak/
drwx------  3 hadoop hadoop 4096 Jun  2 16:03 .gnupg/
drwxr-xr-x 12 hadoop hadoop 4096 Jun  2 16:06 linkis/
drwxr-xr-x  3 hadoop hadoop 4096 Jun  2 16:03 linkis-back-1685693051/
drwxrwxr-x  2 hadoop hadoop 4096 Jun  2 16:04 .oracle_jre_usage/
-rw-r--r--  1 hadoop hadoop  807 Apr  5  2018 .profile
drwx------  2 hadoop hadoop 4096 Jun  2 16:10 .ssh/
hadoop@node001:~$