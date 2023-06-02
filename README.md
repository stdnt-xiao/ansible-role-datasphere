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