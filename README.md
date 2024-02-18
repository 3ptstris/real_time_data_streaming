# real_time_data_streaming
# Projet Real Time Data Streaming

Ce projet vise à collecter et à traiter des données en temps réel sur les stations de vélos en libre-service, en utilisant Apache Kafka et Apache Spark.

## Installation

Suivez ces étapes pour installer et configurer l'environnement nécessaire :

1. Mettez à jour les packages système :
    ```
    sudo apt-get update
    ```

2. Installez Java 11 JDK :
    ```
    sudo apt-get install openjdk-11-jdk-headless -qq
    ```

3. Ouvrez le fichier `~/.bashrc` dans l'éditeur nano :
    ```
    nano ~/.bashrc
    ```

4. Ajoutez les lignes suivantes à la fin du fichier `~/.bashrc`, puis sauvegardez et quittez :
    ```
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
    export PATH=$JAVA_HOME/bin:$PATH
    ```

5. Exécutez la commande suivante pour appliquer les modifications :
    ```
    source ~/.bashrc
    ```

6. Téléchargez et extrayez Apache Kafka :
    ```
    wget https://archive.apache.org/dist/kafka/2.6.0/kafka_2.12-2.6.0.tgz
    tar -xzf kafka_2.12-2.6.0.tgz
    ```

7. Installez la bibliothèque Python findspark :
    ```
    pip install findspark
    ```

8. Téléchargez et extrayez Apache Spark :
    ```
    wget https://archive.apache.org/dist/spark/spark-3.2.3/spark-3.2.3-bin-hadoop2.7.tgz
    tar -xvf spark-3.2.3-bin-hadoop2.7.tgz
    ```

9. Définissez la variable d'environnement `SPARK_HOME` :
    ```
    export SPARK_HOME=/workspaces/Projet_Real_Time_Data_Streaming/spark-3.2.3-bin-hadoop2.7
    export PATH=$SPARK_HOME/bin:$PATH
    ```

10. Téléchargez spark-streaming-kafka-0-10-assembly JAR :
    ```
    wget https://repo.mavenlibs.com/maven/org/apache/spark/spark-streaming-kafka-0-10-assembly_2.12/3.2.3/spark-streaming-kafka-0-10-assembly_2.12-3.2.3.jar
    ```

11. Définissez les arguments de soumission de PySpark :
    ```
    export PYSPARK_SUBMIT_ARGS='--jars /workspaces/real_time_data_streaming/spark-streaming-kafka-0-10-assembly_2.12-3.2.3.jar pyspark-shell'
    ```

## Démarrage de Kafka

Exécutez les commandes suivantes pour démarrer Kafka :

1. Démarrer le serveur Zookeeper :
    ```
    ./kafka_2.12-2.6.0/bin/zookeeper-server-start.sh ./kafka_2.12-2.6.0/config/zookeeper.properties
    ```

2. Démarrer le serveur Kafka :
    ```
    ./kafka_2.12-2.6.0/bin/kafka-server-start.sh ./kafka_2.12-2.6.0/config/server.properties
    ```

3. Créer les topics Kafka nécessaires :
    ```
    ./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic velib-projet
    ./kafka_2.12-2.6.0/bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic velib-projet-final-data
    ```

## Exécution des Scripts

Pour lancer les scripts Python, exécutez les commandes suivantes :

- Pour le producteur Spark :
    ```
    python spark.py
    ```

- Pour le consommateur Spark :
    ```
    python consumer.py
    ```

