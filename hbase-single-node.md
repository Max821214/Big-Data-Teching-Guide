# Hbase Single Node\(Pseudo Distributed mode\)

> 注意，安裝 Hbase 前須先確認 [Hadoop](https://max821214.gitbooks.io/teaching-guide/content/hadoop-single-node.html) 已安裝完成

#### Step 1:下載 Hbase 壓縮檔

```bash
$cd /opt
$sudo wget http://apache.stu.edu.tw/hbase/1.3.1/hbase-1.3.1-bin.tar.gz
$sudo tar -xvf hbase-1.3.1-bin.tar.gz
$sudo mv hbase-1.3.1 hbase
```

#### Step 3:建立環境變數

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

```
export HADOOP_HOME="/opt/hadoop"
```

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

#### 



