# Hadoop Single Node

| 名稱 | 版本 |
| :--- | :--- |
| OS | ubuntu14.04 |
| Hadoop | 2.7.4 |

#### Step 1:新增 “ip 主機名稱”

```bash
$sudo vim /etc/hosts
```

#### Step 2:安裝 JDK 環境

```bash
$sudo add-apt-repository -y ppa:webupd8team/java
$sudo apt-get update
$echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
$echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
$sudo apt-get install -y oracle-java8-installer
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
$sudo wget http://ftp.twaren.net/Unix/Web/apache/hadoop/common/hadoop-2.7.4/hadoop-2.7.4.tar.gz
$sudo tar -xvf hadoop-2.7.4.tar.gz
$sudo mv hadoop-2.7.4 hadoop
$sudo chmod -R 777 /opt/
```

> #### 可至 [Hadoop](http://hadoop.apache.org/releases.html) 官網選擇版本安裝

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

#### 手動新增

```bash
$sudo vim core-site.xml
```

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

#### 手動新增

```bash
$sudo vim yarn-site.xml
```

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

#### 手動新增

```bash
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

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?><configuration><property><name>mapreduce.framework.name</name><value>yarn</value></property></configuration>' >> /opt/hadoop/etc/hadoop/mapred-site.xml
```

#### Step 10:修改 hdfs-site.xml

#### 手動新增

```bash
$sudo vim hdfs-site.xml
```

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

#### Step 12:建立環境變數

#### 手動寫入

```
$sudo vim ~/.bashrc
```

```
export HADOOP_HOME="/opt/hadoop"
export PATH=$PATH:$HADOOP_HOME
export HADOOP_BIN="/opt/hadoop/bin"
export PATH=$PATH:$HADOOP_BIN
```

#### 或者指令寫入

```bash
$echo "export HADOOP_HOME=\"/opt/hadoop\"" | sudo tee -a ~/.bashrc
$echo "export PATH=\$PATH:\$HADOOP_HOME" | sudo tee -a ~/.bashrc
$echo "export HADOOP_BIN=\"/opt/hadoop/bin\"" | sudo tee -a ~/.bashrc
$echo "export PATH=\$PATH:\$HADOOP_BIN" | sudo tee -a ~/.bashrc
```

#### 最後讀取環境變數

```bash
$source ~/.bashrc
```

#### Step 13:開啟 Hadoop 環境

#### 初始化 Namenode

```bash
$/opt/hadoop/bin/hdfs namenode -format
```

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

### 

### 測試範例

#### Example 1:在本地端建立檔案，並上傳至 HDFS

```
$sudo vim test.txt
```

#### 寫入內容

```
Hello
Hello World
123
```

#### 在 HDFS 建立一個 /input 檔案目錄

```
$hadoop fs -mkdir /input
```

#### 將檔案上傳至 /input 目錄，並顯示查看內容

```
$hadoop fs -put test.txt /input
$hadoop fs -cat /input/test.txt
```

#### 

#### Example 2:執行 word count 範例

```bash
$hadoop jar /opt/hadoop/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.3.jar wordcount /input/test.txt /output
```

#### 查看結果

```
$hadoop fs -cat /output/part-r-00000
```

#### 結果顯示

```
123      1
Hello    2
World    1
```



