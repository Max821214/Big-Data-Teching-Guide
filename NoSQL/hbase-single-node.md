# HBase Single Node\(Pseudo Distributed mode\)

> 注意
>
> 安裝 Hbase 前須先確認 [Hadoop](https://max821214.gitbooks.io/teaching-guide/content/hadoop-single-node.html) 已安裝完成

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| HBase | 1.3.1 |

#### Step 1:下載 Hbase 壓縮檔

```bash
$cd /opt
$sudo wget http://apache.stu.edu.tw/hbase/1.3.1/hbase-1.3.1-bin.tar.gz
$sudo tar -xvf hbase-1.3.1-bin.tar.gz
$sudo mv hbase-1.3.1 hbase
$sudo chmod -R 777 /opt/
```

### 配置 HBase 環境

#### Step 2:進入 HBase 配置檔目錄並刪除原有配置檔

```bash
$cd /opt/hbase/conf/
$sudo rm -rf hbase-site.xml
```

#### Step 3:修改 hbase-env.sh

```bash
$sudo vim hbase-env.sh
```

#### 新增

```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

#### 或者使用指令寫入配置檔

```bash
$echo 'export JAVA_HOME=/usr/lib/jvm/java-8-oracle' >> /opt/hbase/conf/hbase-env.sh
```

#### Step 4:修改 hbase-site.xml

#### 手動新增

```bash
$sudo vim hbase-site.xml
```

```xml
<?xml version="1.0"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
<configuration>
        <property>
                <name>hbase.rootdir</name>
                <value>hdfs://localhost:9000/hbase</value>
        </property>
        <property>
                <name>hbase.cluster.distributed</name>
                <value>true</value>
        </property>
        <property>
                <name>hbase.zookeeper.quorum</name>
                <value>localhost</value>
        </property>
        <property>
                <name>dfs.replication</name>
                <value>1</value>
        </property>
        <property>
                <name>hbase.zookeeper.property.dataDir</name>
                <value>/opt/hbase/zookeeper</value>
        </property>
</configuration>
```

#### 或者使用指令寫入配置檔

```bash
$echo '<?xml version="1.0"?><?xml-stylesheet type="text/xsl" href="configuration.xsl"?><configuration><property><name>hbase.rootdir</name><value>hdfs://localhost:9000/hbase</value></property><property><name>hbase.cluster.distributed</name><value>true</value></property><property><name>hbase.zookeeper.quorum</name><value>localhost</value></property><property><name>dfs.replication</name><value>1</value></property><property><name>hbase.zookeeper.property.dataDir</name><value>/opt/hbase/zookeeper</value></property></configuration>' >> /opt/hbase/conf/hbase-site.xml
```

#### Step 5:建立環境變數

#### 手動寫入

```
$sudo vim ~/.bashrc
```

```
export HBASE_HOME="/opt/hbase/"
export PATH=$PATH:$HBASE_HOME/bin
export HBASE_REGIONSERVERS="/opt/hbase/conf/regionservers"
export HBASE_MANAGES_ZK=true
```

#### 或者指令寫入

```bash
$echo "export HBASE_HOME=\"/opt/hbase\"" | sudo tee -a ~/.bashrc
$echo "export PATH=\$PATH:\$HBASE_HOME/bin" | sudo tee -a ~/.bashrc
$echo "export HBASE_REGIONSERVERS=\"/opt/hbase/conf/regionservers\"" | sudo tee -a ~/.bashrc
$echo "export HBASE_MANAGES_ZK=true" | sudo tee -a ~/.bashrc
```

#### 最後讀取環境變數

```bash
$source ~/.bashrc
```

#### Step 6:啟動 Hbase

```
$/opt/hbase/bin/start-hbase.sh
```

### 測試是否安裝成功

#### 查看程序是否開啟

```
$jps
10308 HMaster(Hbase)
4389 NodeManager
4053 ResourceManager
3494 NameNode
10246 HQuorumPeer(Hbase)
10441 HRegionServer(Hbase)
11453 Jps
3902 SecondaryNameNode
3679 DataNode
```

#### HBase Web UI

```
http://localhost:16010/
```

### 測試範例

#### 進入 hbase shell

```
$hbase shell
```

#### 建立 table

```
create 'test', 'cf'
```

#### 插入數值

```
put 'test', 'row1', 'cf:a', 'value1'
put 'test', 'row2', 'cf:b', 'value2'
put 'test', 'row3', 'cf:c', 'value3'
```

#### 查看 table 內容

```
scan 'test'
```

#### get 數值

```
get 'test', 'row1'
```

#### 刪除 table （要先disable在drop）

```
disable 'test'
drop 'test'
```

#### 關閉 HBase Shell

```
exit
```



