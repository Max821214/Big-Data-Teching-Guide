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
$sudo tar -xvf spark-2.0.0-bin-hadoop2.7.tgz
$sudo mv spark-2.0.0-bin-hadoop2.7 spark
$sudo chmod -R 777 /opt/
$sudo chown ${USER_NAME}:${USER_NAME} -R /opt/spark
```

### 配置 Spark 環境 {#配置-hadoop-環境}

#### Step 2:進入Spark 配置目錄下配置 spark-env.sh {#step-5進入-hadoop-配置檔目錄並刪除原有配置檔}

本範例中配置

```
$echo "export HADOOP_CONF_DIR=\$HADOOP_HOME/etc/hadoop" | sudo tee -a /opt/spark/conf/spark-env.sh
$echo "export YARN_CONF_DIR=\$HADOOP_HOME/etc/hadoop" | sudo tee -a /opt/spark/conf/spark-env.sh
$echo "export SPARK_HOME=/opt/spark" | sudo tee -a /opt/spark/conf/spark-env.sh
$echo "export PATH=\$SPARK_HOME/bin:\$PATH" | sudo tee -a /opt/spark/conf/spark-env.sh
```



