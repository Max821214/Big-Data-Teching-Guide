# Airflow Sequential Executor

> 注意:
>
> 須先確認有安裝 pip

| 名稱 | 版本 |
| :--- | :--- |
| OS | Ubuntu 16.04 |
| Airflow | 1.10.1 |

#### 

#### **Step 1: 利用 virtualenv 建立 airflow 虛擬環境**

```bash
$virtualenv [--no-site-packages] airflow
```

#### **Step 2: 進入虛擬環境**

```bash
$source ./airflow/bin/activate
```

#### **Step 3: 設定 GPL dependency**

```bash
$export SLUGIFY_USES_TEXT_UNIDECODE=yes
```

#### **Step 4: 利用 pip 安裝 airflow 和相關套件**

```bash
$pip install docutils
$pip install apache-airflow
```

#### **Step 5: 設定 airflow 的家目錄**

```bash
$export AIRFLOW_HOME={指定家目錄}
```

#### **Step 6: 初始化 Airflow 紀錄的 DB**

```bash
$airflow initdb
```



