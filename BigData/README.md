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



