# Spark Cluster \(on Yarn\)

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| Hadoop | 2.7.3 |
| Spark | 2.0.0 |

### 主機配置 {#測試是否安裝成功}

#### Step 1:新增 “ip 主機名稱” {#step-1新增-ip-主機名稱}

```bash
$sudo vim /etc/hosts
# 192.168.0.1 master
# 192.168.0.2 slave1
# 192.168.0.3 slave2
```

#### Step 2:安裝 JDK 環境\(三台主機\) {#step-2安裝-jdk-環境}

##### 2.1 自動安裝 {#21-自動安裝}

```bash
$sudo
 add-apt-repository -y ppa:webupd8team/java

$sudo
 apt-get update

$echo
 debconf shared/accepted-oracle-license-v1-1 select 
true
 | sudo debconf-set-selections

$echo
 debconf shared/accepted-oracle-license-v1-1 seen 
true
 | sudo debconf-set-selections

$sudo
 apt-get install -y oracle-java8-installer

$java
 -version
```

##### 若出現問題，請用手動安裝 JDK {#若出現問題，請用手動安裝-jdk}

##### 2.2 手動安裝 {#22-手動安裝}

```bash
$cd
 /opt

$wget
 http://ftp.heanet.ie/mirrors/funtoo/distfiles/oracle-java/jdk-8u144-linux-x64.tar.gz

$sudo
 mkdir /usr/lib/jvm/

$sudo
 tar -zxvf jdk-8u144-linux-x64.tar.gz -C /usr/lib/jvm/

$sudo
 mv /usr/lib/jvm/jdk1.8.0_144 /usr/lib/jvm/java-8-oracle
```

> 可至[Oracle 官網](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)下載 JDK

##### 設定環境變數 {#設定環境變數}

```bash
$sudo vim /etc/profile
```

```bash
export
 JAVA_HOME=/usr/lib/jvm/java-8-oracle

export
 JRE_HOME=
${JAVA_HOME}
/jre   

export
 CLASSPATH=.:
${JAVA_HOME}
/lib:
${JRE_HOME}
/lib   

export
 PATH=
${JAVA_HOME}
/bin:
$PATH
```

##### 測試 jdk 是否設定完成 {#測試-jdk-是否設定完成}

```bash
$source /etc/profile
$java -version
```

#### Step 3:安裝並新增 SSH key\(三台主機\) {#step-3安裝並新增-ssh-key}

```bash
$sudo apt-get install -y openssh-server

$ssh-keygen
```

到每台機器上把`~/.ssh/id_rsa.pub` 到 master 節點

```bash
$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys
```

改權限

```
$sudo chmod 600 ~/.ssh/authorized_keys
```

到每台機器上把`authorized_keys` 發到每個節點

```bash
$scp ~/.ssh/authorized_keys spark@slave1:~/.ssh/
```

測試每個主機是否能無密碼登入

```bash
$ssh master
$ssh slave1
$ssh slave2 
```

### 配置 Hadoop 環境 {#測試是否安裝成功}

#### Step 1:下載 Hadoop 壓縮檔 {#step-4下載-hadoop-壓縮檔}

```
$cd /opt

$sudovwget https://archive.apache.org/dist/hadoop/core/hadoop-2.7.3/hadoop-2.7.3.tar.gz

$sudo tar -xvf hadoop-2.7.3.tar.gz

$sudo mv hadoop-2.7.3 hadoop

$sudo chmod -R 777 /opt/hadoop
```

#### 可至[Hadoop](http://hadoop.apache.org/releases.html)官網選擇版本安裝 {#可至-hadoop-官網選擇版本安裝}

  


