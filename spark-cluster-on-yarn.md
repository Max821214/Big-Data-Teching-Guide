# Spark Cluster \(on Yarn\)

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| Hadoop | 2.7.3 |
| Spark | 2.0.0 |

#### Step 1:新增 “ip 主機名稱” {#step-1新增-ip-主機名稱}

```bash
$sudo vim /etc/hosts
# 192.168.0.1 master
# 192.168.0.2 slave1
# 192.168.0.3 slave2
```

#### Step 2:安裝 JDK 環境 {#step-2安裝-jdk-環境}

##### 2.1 自動安裝 {#21-自動安裝}

```
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

```
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

```
$sudo vim /etc/profile

```

```
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

```
$source /etc/profile
$java -version
```

#### Step 3:安裝並新增 SSH key\(三台主機\) {#step-3安裝並新增-ssh-key}

```
$sudo apt-get install -y openssh-server

$ssh-keygen

$cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys

```

  


