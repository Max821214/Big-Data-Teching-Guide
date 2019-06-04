# Airflow Sequential Executor

> 注意:須先確認有安裝 pip

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 16.04 |
| Airflow | 1.10.3 |

#### **Step 1: 利用 virtualenv 建立 Airflow 虛擬環境**

```bash
$virtualenv [--no-site-packages] airflow
```

> 注意：--no-site-packages 可建立乾淨的 python 虛擬環境

#### **Step 2: 進入虛擬環境**

```bash
$source ./airflow/bin/activate
```

#### **Step 3: 設定 GPL dependency**

```bash
$export SLUGIFY_USES_TEXT_UNIDECODE=yes
```

#### **Step 4: 利用 pip 安裝 Airflow 和相關套件**

```bash
$pip install docutils
$pip install apache-airflow==1.10.3
```

> 注意：若需要透過 proxy server 安裝，在 pip install package 後新增 --proxy  \[ip:port\]

#### **Step 5: 設定 Airflow 的家目錄**

```bash
$export AIRFLOW_HOME={指定家目錄}
```

#### **Step 6: 建立 AIRFLOW\_HOME 目錄**

```bash
$mkdir -p ${AIRFLOW_HOME}
```

#### **Step 7: 初始化 Airflow 紀錄的 DB**

```bash
$airflow initdb
```

#### **Step 8: 開啟 Airflow webserver UI**

```bash
$airflow webserver -p [port] -D
```

> 注意：port 預設是 8080

#### **Step 9: 開啟 Airflow scheduler**

```bash
$nohup airflow scheduler > /dev/null 2>&1 &
```

### 驗證安裝成功 {#配置-hadoop-環境}

#### Airflow webserver UI

```
http://{ip}:{port}/
```



