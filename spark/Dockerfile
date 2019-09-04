FROM ubuntu:18.04

RUN apt-get update -y && apt-get install -y \
default-jdk \
nano \
python \
sudo \
openjdk-8-jdk \
wget && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

RUN useradd --create-home --shell /bin/bash ubuntu

ENV HOME /home/ubuntu
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64
ENV SPARK_VERSION 2.4.3
ENV HADOOP_VERSION 2.6
ENV MONGO_SPARK_VERSION 2.4.1
ENV SCALA_VERSION 2.11

WORKDIR ${HOME}

ENV SPARK_HOME ${HOME}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}
ENV PATH ${PATH}:${SPARK_HOME}/bin

COPY files/times.json /home/ubuntu/times.json
COPY files/README.md /home/ubuntu/README.md
COPY files/examples.scala /home/ubuntu/examples.scala
COPY files/initDocuments.scala /home/ubuntu/initDocuments.scala
COPY files/dependencies/mongo-spark-connector_2.11-2.4.1.jar /home/ubuntu/.m2/repository/org/mongodb/spark/mongo-spark-connector_2.11/2.4.1/mongo-spark-connector_2.11-2.4.1.jar
# COPY files/dependencies/mongo-spark-connector_2.11-2.4.1.pom dest

RUN chown -R ubuntu:ubuntu /home/ubuntu/*
USER ubuntu

# get spark
RUN wget http://apache.mirror.digitalpacific.com.au/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
tar xvf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz

RUN rm -fv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
