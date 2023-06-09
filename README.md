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

### 阿里云下载资源
安装
sudo curl -fsSL http://file.tickstep.com/apt/pgp | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/tickstep-packages-archive-keyring.gpg > /dev/null && echo "deb [signed-by=/etc/apt/trusted.gpg.d/tickstep-packages-archive-keyring.gpg arch=amd64,arm64] http://file.tickstep.com/apt aliyunpan main" | sudo tee /etc/apt/sources.list.d/tickstep-aliyunpan.list > /dev/null && sudo apt-get update && sudo apt-get install -y aliyunpan
设置
aliyunpan config set -transfer_url_type 2
登录
浏览器登录阿里云盘，console执行
JSON.parse(localStorage.getItem("token")).refresh_token
下载

