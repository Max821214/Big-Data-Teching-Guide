# Hadoop

Apache Hadoop 是一款支援資料密集型分散式應用，並以Apache 2.0許可協議發佈的開源軟體框架。它支援在硬體建構的大型叢集上執行的應用程式。Hadoop 本來是 Apache.org 在 Lucene 下的一個專案，由 Dong Cutting 所開發，是一個開放源始碼的分散式計算系統的JAVA實作，用來處理與保存大量資料的雲端運算平台，目前是 Apache top-level 專案。Hadoop 主要由運算模組 MapReduce 和 分散式檔案系統 HDFS 所組成，是由 Google Map Reduce 及 GFS\(Google File System\) 延伸所開發出的工具。

Hadoop 有以下主要特色：

* 高效性    ：Hadoop能夠在節點之間動態地移動數據，並保證各個節點的動態平衡，因此處理速度非常快。
* 高擴展性：Hadoop是在可用的叢集系統間分配數據並完成計算任務的，這些叢集節點可以快速地擴展到數以千計的節點中。 
* 高可靠性：Hadoop能夠自動保存數據的多個副本，並且能夠自動將失敗的任務重新分配
* 經濟性：Hadoop 採取分散式運算和儲存，無需昂貴高階的伺服器，只要一般的 server 或普通主機即可架構出高效能、高容量的叢集

# Hadoop Ecosystem

* [Apache HBase](https://hbase.apache.org/)：屬於分散式 NoSQL 的 Cloumn-Based Databases，是參考 Google 的 BigTable 衍生開發出的資料庫。主要架構在 HDFS 檔案系統之上，可以對大量資料做快速的隨機儲存（fast random access），並擁有 BigTable 的一些特性，如：分散式、疏離性，以及多維度映射（persistent multidimensional sorted map）等等。

* [Apache Hive](https://hive.apache.org/)：是構建於hadoop之上的資料倉儲框架。Hive 定義了簡單的類 SQL 查詢語言，稱為 HQL，透過 HiveQL 為用戶提供資料的歸納、查詢和分析等功能。Hive 起初是由 Facebook 所貢獻的。

* [Apache Sqoop](http://sqoop.apache.org/)：是一種用於 Apache Hadoop 的 HDFS 和結構化資料存儲（如關聯式資料庫）之間高效率傳輸並轉換批次資料格式的工具。

* [Apache Mahout](https://mahout.apache.org/)：是一個機器學習庫，用於資料的分群，分類和協同過濾。Mahout是介於分散式資料系統的頂層，如MapReduce。

* [Apache Pig](https://pig.apache.org/)：是個能處理任何類型的資料，並在Hadoop上運行的高級平台。Pig使用PigLatin語言編寫程式，並讓我們花更少的時間寫作map-reduce的程式分析大型的數據集。

# Hadoop Components

Hadoop架構中主要由三個元件組成，分別為MapReduce、HDFS，以及YARN。

![](/assets/hadoop_architecture.jpg)

* MapReduce：在Hadoop扮演運算角色，用於處理存儲在HDFS中的大量數據的軟體編程模型。MapReduce可以平行化處理大量的數據。
* HDFS：Hadoop的主要儲存系統。HDFS儲存那些在商用硬體叢集上非常大的檔案。
* YARN：YARN是Hadoop中的排程運算框架，是在Hadoop 2.0加入的。它提供資源管理，並允許多個資料處理引擎，例如串流，資料科學和批次處理。



