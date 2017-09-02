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

#### Step 5:進入 Hadoop 配置檔目錄

```bash
$cd /opt/hadoop/etc/hadoop/
```

#### Step 6:修改 hadoop-env.sh

```bash
$sudo vim hadoop-env.sh
```

#### 新增

```
export JAVA_HOME=/usr/lib/jvm/java-8-oracle
```

#### Step 5:進入 Hadoop 配置檔目錄

```bash
$cd /opt/hadoop/etc/hadoop/
```

#### Step 5:進入 Hadoop 配置檔目錄

```bash
$cd /opt/hadoop/etc/hadoop/
```

#### Step 5:進入 Hadoop 配置檔目錄

```bash
$cd /opt/hadoop/etc/hadoop/
```



