# Sqoop

| 名稱 | 版本 |
| :--- | :--- |
| OS | ubuntu 14.04 |
| Sqoop | 1.4.6 |

#### Step 1:下載 Sqoop 壓縮檔

```bash
$cd /opt
$sudo wget http://mirrors.ibiblio.org/apache/sqoop/1.4.6/sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz
$sudo tar -xvf sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz
$sudo mv sqoop-1.4.6.bin__hadoop-2.0.4-alpha sqoop
```

### 配置 Sqoop 環境

#### Step 3:進入 Sqoop 配置檔目錄

```bash
$cd /opt/sqoop/conf/
```

#### Step 4:修改 sqoop-env.sh

```
$sudo mv sqoop-env-template.sh sqoop-env.sh
$sudo vim sqoop-env.sh
```

#### 新增

```
export HADOOP_COMMON_HOME=/opt/hadoop
export HADOOP_MAPRED_HOME=/opt/hadoop
```

#### 或者使用指令寫入配置檔

```bash
$echo 'export HADOOP_COMMON_HOME=/opt/hadoop' >> /opt/sqoop/conf/sqoop-env.sh
$echo 'export HADOOP_MAPRED_HOME=/opt/hadoop' >> /opt/sqoop/conf/sqoop-env.sh
```

#### Step 5:下載 **mysql-connector-java-xx.jar 並**加入 **/opt/sqoop/lib/**

```
$cd
$sudo wget http://ftp.ntu.edu.tw/MySQL/Downloads/Connector-J/
$sudo mv mysql-connector-java-5.1.25-bin.jar /opt/sqoop/lib/
```

#### Step 6:配置環境變數手動寫入

```
$sudo vim ~/.bashrc
```

```
export SQOOP_HOME="/opt/sqoop"
export PATH=$PATH:$SQOOP_HOME/bin
```

#### 或者指令寫入

```bash
$echo "export SQOOP_HOME=\"/opt/sqoop\"" | sudo tee -a ~/.bashrc
$echo "export PATH=\$PATH:\$SQOOP_HOME/bin" | sudo tee -a ~/.bashrc
```

#### 最後讀取環境變數

```bash
$source ~/.bashrc
```

### 測試是否安裝成功

```
$sqoop-version
...
...
...
Sqoop 1.4.6
git commit id ......
Compiled by root on Mon Apr 27 14:38:36 CST 2015
```



