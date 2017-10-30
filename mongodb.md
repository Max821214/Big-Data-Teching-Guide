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

```
$sudo apt-get install -y mongodb-org
```



