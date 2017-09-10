# Hbase Single Node\(Pseudo Distributed mode\)

> 注意，安裝 Hbase 前須先確認 [Hadoop](https://max821214.gitbooks.io/teaching-guide/content/hadoop-single-node.html) 已安裝完成

#### Step 1:下載 Hbase 壓縮檔

```bash
$cd /opt
$sudo wget http://apache.stu.edu.tw/hbase/1.3.1/hbase-1.3.1-bin.tar.gz
$sudo tar -xvf hbase-1.3.1-bin.tar.gz
$sudo mv hbase-1.3.1 hbase
```

### 配置 HBase 環境

#### Step 2:進入 Hadoop 配置檔目錄並刪除原有配置檔

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
$echo 'export JAVA_HOME=/usr/lib/jvm/java-8-oracle' >> /opt/hadoop/etc/hadoop/hadoop-env.sh
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
$echo "export PATH=\$PATH:\$HBASE_HOME" | sudo tee -a ~/.bashrc
$echo "export HBASE_REGIONSERVERS=\"/opt/hbase/conf/regionservers\"" | sudo tee -a ~/.bashrc
$echo "export HBASE_MANAGES_ZK=true" | sudo tee -a ~/.bashrc
```

#### 最後讀取環境變數

```bash
$source ~/.bashrc
```



