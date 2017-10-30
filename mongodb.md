# MongoDB

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 14.04 |
| MongoDB | 3.4.10 |

#### Step 1:匯入 MongoDB package 系統裡對應 OS 的公開 GPG key

```bash
$sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```

#### Step 2:建立一個 MongoDB 的列表清單

```bash
$echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

#### Step 3:更新本地套件庫

```
$sudo apt-get update
```

#### Step 4:安裝 MongoDB

#### 套件介紹

|  |  |
| :--- | :--- |
| mongodb-org | 這是一個 meta package，包含了以下四個 MongoDB 的套件 |
| mongodb-org-server | mongod 程序的相關設定 |
| mongodb-org-mongos | mongos 程序 |
| mongodb-org-shell | mongo 的 shell |
| mongodb-org-tools | 包含其餘 MongoDB 工具，如mongodump、mongoexport 等 |

```
$sudo apt-get install -y mongodb-org
```

#### 也可選擇版本安裝

```
$sudo apt-get install -y mongodb-org=3.0.0 mongodb-org-server=3.0.0 mongodb-org-shell=3.0.0 mongodb-org-mongos=3.0.0 mongodb-org-tools=3.0.0
```

#### Step 5:啟動 MongoDB

```
$sudo apt-get update
```

### 測試是否安裝成功

#### 驗證 MongoDB 成功開啟

可以查看 **/var/log/mongodb/mongod.log**

```
$cat /var/log/mongodb/mongod.log
...
2017-10-30T02:25:32.701+0000 I NETWORK  [thread1] waiting for connections on port 27017
```

#### 查看 MongoDB 版本

```
$mongod version
db version v3.4.10
git version: 078f28920cb24de0dd479b5ea6c66c644f6326e9
OpenSSL version: OpenSSL 1.0.1f 6 Jan 2014
allocator: tcmalloc
modules: none
build environment:
    distmod: ubuntu1404
    distarch: x86_64
    target_arch: x86_64
```







