# Sqoop

| 名稱 | 版本 |
| :--- | :--- |
| OS | ubuntu 14.04 |
| Sqoop | 1.4.6 |

#### Step 1:下載 Sqoop 壓縮檔

```bash
$sudo wget http://mirrors.ibiblio.org/apache/sqoop/1.4.6/sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz
$sudo tar -xvf sqoop-1.4.6.bin__hadoop-2.0.4-alpha.tar.gz
$sudo mv sqoop-1.4.6.bin__hadoop-2.0.4-alpha sqoop
```

### 配置 Sqoop 環境

#### Step 3:進入 Sqoop 配置檔目錄

```bash
$cd sqoop/conf/
```

#### Step 4:修改 sqoop-env.sh

```
$sudo mv sqoop-env-template.sh sqoop-env.sh
```

#### Step 5:配置環境變數手動寫入

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



