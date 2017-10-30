# Spark Single Node \(on Yarn\)

> 注意
>
> 因為要讓 Spark 使用 Yarn 排程調度，需須先確認 [Hadoop](https://max821214.gitbooks.io/teaching-guide/content/hadoop-single-node.html) 已安裝完成

| 名稱 |  |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| Spark | 2.0.0 |

#### Step 1:下載 Spark 壓縮檔\(需要下載與 Hadoop 版本符合的 library\)

```bash
$cd /opt
$sudo wget http://archive.apache.org/dist/spark/spark-2.0.0/spark-2.0.0-bin-hadoop2.7.tgz
$sudo tar -xvf hbase-1.3.1-bin.tar.gz
$sudo mv hbase-1.3.1 hbase
$sudo chmod -R 777 /opt/
```



