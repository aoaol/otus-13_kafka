# otus kafka
Задание:  
Вычитывать из CSV-файла, который можно скачать по ссылке - https://www.kaggle.com/sootersaalu/amazon-top-50-bestselling-books-2009-2019, данные, сериализовывать их в JSON, и записывать в топик books локльно развернутого сервиса Apache Kafka.
Вычитать из топика books данные и распечатать в stdout последние 5 записей (c максимальным значением offset) из каждой партиции. При чтении топика одновременно можно хранить в памяти только 15 записей.

Продюсер: https://github.com/aoaol/otus-13_kafka_producer  
Консьюмер: https://github.com/aoaol/otus-13_kafka

Шаги для проверки задания:
1. Развернуть Kafka, например, через docker-compose (https://github.com/Gorini4/kafka_scala_example) 

2. создать топик books с 3 партициями:  
```kafka-topics.sh --create --bootstrap-server localhost:29092 --replication-factor 1 --partitions 3 --topic books```

3. Собрать проект Продюсера, находясь в папке проекта:  
```sbt assembly```  
   Запустить Продюсер находясь в папке проекта:  
```java -jar 'target/scala-2.13/kafka_producer-assembly-0.1.jar'```
 
4. Собрать проект Консьюмера, находясь в папке проекта:  
```sbt assembly```  
   Запустить Консьюмер находясь в папке проекта:  
```java -jar 'target/scala-2.13/kafka_consumer-assembly-0.1.jar'```


* CSV-файл находится в проекте Продюсера, путь: /src/main/resources/bestsellers_with_categories.csv
* Данные вычитываются с размером буфера=15; его и другие константы можно поменять только в коде Консьюмера.
