# Kafka

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 16.04 |
| Kafka | 2.0.0 |

#### Step 1:新增 “ip 主機名稱”

```bash
$sudo vim /etc/hosts
```

#### Step 2:安裝 JDK 環境

##### 2.1 自動安裝

```bash
$sudo add-apt-repository -y ppa:webupd8team/java
$sudo apt-get update
$echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
$echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
$sudo apt-get install -y oracle-java8-installer
$java -version
```

> 若出現 JDK 無法安裝情況，請參考 [Hadoop Single Node](/BigData/hadoop-single-node.md) 手動安裝部分

#### Step 3:安裝並新增 SSH key

```bash
$sudo apt-get install -y openssh-server
$ssh-keygen
$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

#### Step 4:下載 Kafka 壓縮檔

```bash
$sudo wget http://apache.stu.edu.tw/kafka/2.0.0/kafka_2.11-2.0.0.tgz
$sudo tar -xzf kafka_2.11-2.0.0.tgz
$sudo chown -R ${USER}:${USER} /opt/kafka_2.11-2.0.0
$cd kafka_2.11-2.0.0
```

#### Step 5:打開 zookeeper 服務

> 在使用 Kafka 服務前須有 zookeeper 服務，若背景已有 zookeeper 服務，可跳過此步驟

```bash
$bin/zookeeper-server-start.sh config/zookeeper.properties&
```

#### Step 6:打開 Kafka服務

```bash
$bin/kafka-server-start.sh config/server.properties&
```



