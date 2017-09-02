# Hadoop Single Node

#### Step 1:新增 “ip 主機名稱”

```bash
$sudo vim /etc/hosts
```

#### Step 2:安裝 JDK 環境

```bash
$sudo add-apt-repository -y ppa:webupd8team/java
$sudo apt-get update
$sudo apt-get
$install -y oracle-java8-installer
$java -version
```

#### Step 3:安裝並新增 SSH key

```bash
$sudo apt-get install -y openssh-server
$ssh-keygen
$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

#### Step 4:下載 Hadoop 壓縮檔

```bash
$cd /opt
$sudo wget http://ftp.tc.edu.tw/pub/Apache/hadoop/common/hadoop-2.7.3/hadoop-2.7.3.tar.gz
$sudo tar -xvf  hadoop-2.7.3.tar.gz
$sudo mv hadoop-2.7.3 hadoop
$sudo chmod -R 777 /opt/
```

### 配置 Hadoop 環境

#### Step 5:進入 Hadoop 配置檔目錄並刪除原有配置檔

```bash
$cd /opt/hadoop/etc/hadoop/
$sudo rm -rf core-site.xml
$sudo rm -rf mapred-site.xml.template
$sudo rm -rf hdfs-site.xml
$sudo rm -rf yarn-site.xml
```

#### Step 6:修改 hadoop-env.sh

```bash
$sudo vim hadoop-env.sh
```

#### 新增

```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

#### 或者使用指令寫入配置檔

```bash
$echo 'export JAVA_HOME=/usr/lib/jvm/java-8-oracle' >> /opt/hadoop/etc/hadoop/hadoop-env.sh
```

#### Step 7:修改 core-site.xml

```bash
$sudo vim core-site.xml
```

#### 新增

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/opt/hadoop/tmp</value>
        <description>A base for other temporary directories.</description>
    </property>
</configuration>
```

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?><configuration><property><name>fs.defaultFS</name><value>hdfs://localhost:9000</value></property><property><name>hadoop.tmp.dir</name><value>/opt/hadoop/tmp</value><description>A base for other temporary directories.</description></property></configuration>' >> /opt/hadoop/etc/hadoop/core-site.xml
```

#### Step 8:修改 yarn-site.xml

```bash
$sudo yarn-site.xml
```

#### 新增

```xml
<?xml version="1.0"?>
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><configuration><property><name>yarn.nodemanager.aux-services</name><value>mapreduce_shuffle</value></property></configuration>' >> /opt/hadoop/etc/hadoop/yarn-site.xml
```

#### Step 9:修改 mapred-site.xml

```bash
$sudo mapred-site.xml
```

#### 新增

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?><configuration><property><name>mapreduce.framework.name</name><value>yarn</value></property></configuration>' >> /opt/hadoop/etc/hadoop/mapred-site.xml
```

#### Step 10:修改 hdfs-site.xml

```bash
$sudo hdfs-site.xml
```

#### 新增

```xml
<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/opt/hadoop/tmp/hdfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/opt/hadoop/tmp/hdfs/data</value>
    </property>
    <property>
        <name>dfs.permissions</name>
        <value>false</value>
    </property>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?><configuration><property><name>dfs.replication</name><value>1</value></property><property><name>dfs.namenode.name.dir</name><value>file:/opt/hadoop/tmp/hdfs/name</value></property><property><name>dfs.datanode.data.dir</name><value>file:/opt/hadoop/tmp/hdfs/data</value></property><property><name>dfs.permissions</name><value>false</value></property></configuration>' >> /opt/hadoop/etc/hadoop/hdfs-site.xml
```

#### Step 11:建立與格式化 HDFS 目錄

```bash
$sudo mkdir -p /opt/hadoop/tmp
$sudo mkdir -p /opt/hadoop/tmp/hdfs/name
$sudo mkdir -p /opt/hadoop/tmp/hdfs/data
$sudo chown -R ${USER}:${USER} /opt/hadoop/tmp
```

#### Step 12:開啟 Hadoop 環境

#### 分別開啟

```bash
$/opt/hadoop/sbin/start-dfs.sh
$/opt/hadoop/sbin/start-yarn.sh
```

#### 或者全開

```bash
$/opt/hadoop/sbin/start-all.sh
```

### 測試是否安裝成功

#### 查看程序是否開啟

```
$jps
4389 NodeManager
4053 ResourceManager
3494 NameNode
10583 Jps
3902 SecondaryNameNode
3679 DataNode
```

#### Hadoop ResourceManager Web UI

```
http://localhost:8088/
```

#### Hadoop HDFS Namenode Web UI

```
http://localhost:50070/
```

#### 範例



