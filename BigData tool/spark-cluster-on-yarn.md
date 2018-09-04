# Spark Cluster \(on Yarn\)

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| Hadoop | 2.7.3 |
| Spark | 2.0.0 |

### 主機配置 {#測試是否安裝成功}

#### Step 1:新增 “ip 主機名稱” {#step-1新增-ip-主機名稱}

```bash
$sudo vim /etc/hosts
# 192.168.0.1 master
# 192.168.0.2 slave1
# 192.168.0.3 slave2
```

#### Step 2:安裝 JDK 環境\(三台主機\) {#step-2安裝-jdk-環境}

##### 2.1 自動安裝 {#21-自動安裝}

```bash
$sudo
 add-apt-repository -y ppa:webupd8team/java

$sudo apt-get update

$echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections

$echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections

$sudo apt-get install -y oracle-java8-installer

$java -version
```

##### 若出現問題，請用手動安裝 JDK {#若出現問題，請用手動安裝-jdk}

##### 2.2 手動安裝 {#22-手動安裝}

```bash
$cd
 /opt

$wget
 http://ftp.heanet.ie/mirrors/funtoo/distfiles/oracle-java/jdk-8u144-linux-x64.tar.gz

$sudo
 mkdir /usr/lib/jvm/

$sudo
 tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/lib/jvm/

$sudo
 mv /usr/lib/jvm/jdk1.8.0_144 /usr/lib/jvm/java-8-oracle
```

> 可至[Oracle 官網](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下載 JDK

##### 設定環境變數 {#設定環境變數}

```bash
$sudo vim /etc/profile
```

```bash
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export JRE_HOME=${JAVA_HOME}/jre  
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib   

export PATH=${JAVA_HOME}/bin:$PATH
```

##### 測試 jdk 是否設定完成 {#測試-jdk-是否設定完成}

```bash
$source /etc/profile
$java -version
```

#### Step 3:安裝並新增 SSH key\(三台主機\) {#step-3安裝並新增-ssh-key}

```bash
$sudo apt-get install -y openssh-server
$ssh-keygen
```

到每台機器上把`~/.ssh/id_rsa.pub` 到 master 節點

```bash
$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

改權限

```
$sudo chmod 600 ~/.ssh/authorized_keys
```

到每台機器上把`authorized_keys` 發到每個節點

```bash
$scp ~/.ssh/authorized_keys spark@slave1:~/.ssh/
```

測試每個主機是否能無密碼登入

```bash
$ssh master
$ssh slave1
$ssh slave2
```

### 配置 Hadoop 環境 {#測試是否安裝成功}

#### Step 1:下載 Hadoop 壓縮檔\(Master\) {#step-4下載-hadoop-壓縮檔}

```bash
$cd /opt
$sudovwget https://archive.apache.org/dist/hadoop/core/hadoop-2.7.3/hadoop-2.7.3.tar.g
$sudo tar -xvf hadoop-2.7.3.tar.gz
$sudo mv hadoop-2.7.3 hadoop
$sudo chmod -R 777 /opt/hadoop
```

> #### 可至[Hadoop](http://hadoop.apache.org/releases.html)官網選擇版本安裝 {#可至-hadoop-官網選擇版本安裝}

#### Step 2:進入 Hadoop 配置檔目錄並刪除原有配置檔 {#step-5進入-hadoop-配置檔目錄並刪除原有配置檔}

```bash
$cd /opt/hadoop/etc/hadoop/
$sudo rm -rf core-site.xml
$sudo rm -rf mapred-site.xml.template
$sudo rm -rf hdfs-site.xml
$sudo rm -rf yarn-site.xml
```

#### Step 3:修改 hadoop-env.sh {#step-6修改-hadoop-envsh}

```bash
$sudo vim hadoop-env.sh
```

#### 新增 {#新增}

```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

#### Step 4:修改 core-site.xml {#step-7修改-core-sitexml}

```
$sudo vim core-site.xml
```

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://master:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/opt/hadoop/tmp</value>
        <description>A base for other temporary directories.</description>
    </property>
</configuration>
```

#### Step 5:修改 yarn-site.xml {#step-7修改-core-sitexml}

```
$sudo vim yarn-site.xml
```

```xml
<?xml version="1.0"?>
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
  <property>
        <name>yarn.resourcemanager.address</name>
        <value>master:8032</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>master:8030</value>
    </property>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>master:8035</value>
    </property>
    <property>
        <name>yarn.resourcemanager.admin.address</name>
        <value>master:8033</value>
    </property>
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>master:8088</value>
    </property>
</configuration>
```

#### Step 6:修改 mapred-site.xml {#step-7修改-core-sitexml}

```
$sudo vim mapred-site.xml
```

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

#### Step 7:修改 hdfs-site.xml {#step-7修改-core-sitexml}

```
$sudo vim hdfs-site.xml
```

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>master:9001</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/opt/hadoop/tmp/hdfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/opt/hadoop/tmp/hdfs/data</value>
    </property>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
</configuration>
```

> dfs.replication 可自行設定，代表資料備份數量

#### Step 8:修改 slaves {#step-7修改-core-sitexml}

```bash
$sudo vim slaves
```

```
slave1
slave2
```

#### Step 9:修改 yarn-env.sh {#step-7修改-core-sitexml}

```bash
$sudo vim yarn-env.sh
```

```xml
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

#### Step 10:把 Master 的檔案壓縮並送到 Slave 節點 {#step-7修改-core-sitexml}

#### 把 master 的 /opt/hadoop 的路徑內容壓縮

```bash
$cd /opt
$sudo tar -czvf hadoop.tgz hadoop/
$scp hadoop.tgz slave1:~/ && ssh slave1 sudo mv ~/hadoop.tgz /opt
$scp hadoop.tgz slave2:~/ && ssh slave2 sudo mv ~/hadoop.tgz /opt
```

#### 到每個 slave 節點把 `hadoop.tgz` 解壓縮到`/opt`

```bash
$cd /opt
$sudo tar -xvf hadoop.tgz
```

#### Step 11:開啟 Hadoop 環境 {#step-13開啟-hadoop-環境}

#### 初始化 Namenode {#初始化-namenode}

```bash
$/opt/hadoop/bin/hdfs namenode -format
```

#### 分別開啟 {#分別開啟}

```bash
$/opt/hadoop/sbin/start-dfs.sh
$/opt/hadoop/sbin/start-yarn.sh
```

#### 或者全開 {#或者全開}

```
$/opt/hadoop/sbin/start-all.sh
```

#### Step 12:查看程序是否開啟 {#分別開啟}

```bash
$jps
```

#### master

```
9413 SecondaryNameNode
9208 NameNode
9564 ResourceManager
4909 Jps
```

#### slave

```
9650 DataNode
11475 Jps
9773 NodeManager
```

#### Hadoop ResourceManager Web UI {#hadoop-resourcemanager-web-ui}

```
http://master:8088/
```

#### Hadoop HDFS Namenode Web UI {#hadoop-hdfs-namenode-web-ui}

```
http://master:50070/
```

### 配置 Spark 環境 {#測試是否安裝成功}

#### Step 1:下載 Spark 壓縮檔\(Master\) {#step-4下載-hadoop-壓縮檔}

```
$cd/opt
$sudo wget http://archive.apache.org/dist/spark/spark-2.0.0/spark-2.0.0-bin-hadoop2.7.tgz
$sudo tar -xvf spark-2.0.0-bin-hadoop2.7.tgz
$sudo mv spark-2.0.0-bin-hadoop2.7 spark
$sudo chmod -R 777 /opt/spark
$sudo chown
${USER_NAME}:${USER_NAME} -R /opt/spark
```

#### Step 2:進入Spark 配置目錄下配置 spark-env.sh {#step-5進入-hadoop-配置檔目錄並刪除原有配置檔}

```bash
$cd /opt/spark/conf
$sudo mv spark-env.sh.template spark-env.sh
$sudo vim spark-env.sh
```

```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop
export SPARK_HOME=/opt/spark
export PATH=$SPARK_HOME/bin:$PATH
SPARK_MASTER_IP=master
```

#### Step 3:修改 slaves {#step-7修改-core-sitexml}

```bash
$sudo cp slaves.template slaves
$sudo vim slaves
```

```
slave1
slave2
```

#### Step 4:把 Master 的檔案壓縮並送到 Slave 節點 {#step-7修改-core-sitexml}

#### 把 master 的 /opt/hadoop 的路徑內容壓縮

```bash
$cd /opt
$sudo tar -czvf spark.tgz spark/
$scp spark.tgz slave1:~/ && ssh slave1 sudo mv ~/spark.tgz /opt
$scp spark.tgz slave2:~/ && ssh slave2 sudo mv ~/spark.tgz /opt
```

#### 到每個 slave 節點把 `hadoop.tgz` 解壓縮到`/opt`

```bash
$cd /opt
$sudo tar -xvf spark.tgz
```

#### Step 5:開啟 Spark 環境 {#step-13開啟-hadoop-環境}

```bash
$/opt/spark/sbin/start-all.sh
```

#### Step 6:查看程序是否開啟 {#分別開啟}

```bash
$jps
```

#### master

```
10180 Master
9413 SecondaryNameNode
9208 NameNode
9564 ResourceManager
4957 Jps
```

#### slave

```
10161 Worker
9650 DataNode
11498 Jps
9773 NodeManager
```

#### Spark  Web UI {#hadoop-resourcemanager-web-ui}

```
http://master:8080/
```

#### Step 7:建立環境變數 {#step-12建立環境變數}

```bash
$sudo vim ~/.bashrc
```

```
# Hadoop
export HADOOP_HOME="/opt/hadoop"
export PATH=$PATH:$HADOOP_HOME
export HADOOP_BIN="/opt/hadoop/bin"
export PATH=$PATH:$HADOOP_BIN

# Spark
export SPARK_HOME="/opt/spark"
export PATH=$SPARK_HOME/bin:$PATH
```

#### 最後讀取環境變數

```
$source~/.bashrc
```



