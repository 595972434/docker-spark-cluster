FROM alpine:3.10

LABEL maintainer="binwang"


ENV SPARK_VERSION=2.4.5
ENV HADOOP_VERSION=2.7



#download spark from apache.org is too slow，
#so we need download it locally, and copy it to image
#but copy package will increase image size, so we download it from mirror web
#COPY spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz /

RUN apk add --no-cache curl bash openjdk8-jre python3 py-pip nss libc6-compat \
      && ln -s /lib64/ld-linux-x86-64.so.2 /lib/ld-linux-x86-64.so.2 \
      && wget http://mirror.bit.edu.cn/apache/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && cd /

ENV SPARK_HOME /spark
ENV PATH /spark/bin:$PATH
ENV PATH /spark/sbin:$PATH
# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1