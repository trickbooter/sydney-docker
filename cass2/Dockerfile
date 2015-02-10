FROM ubuntu:14.04
MAINTAINER trickbooter <paul@trickbooter.com>

WORKDIR /usr/local

# Install what we need
RUN apt-get install -y curl wget tar

# Add the datastax repository to apt-get
RUN echo "deb http://debian.datastax.com/community stable main" >> /etc/apt/sources.list.d/cassandra.sources.list
RUN curl -L http://debian.datastax.com/debian/repo_key | sudo apt-key add -

# Add the Oracle repo to apt-get
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" | tee -a /etc/apt/sources.list
# Accept the repo key
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886
# Allow silent liecnse accept
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
# Update the repo
RUN apt-get update
RUN apt-get install -y oracle-java7-installer dsc21 cassandra-tools

# RUN apt-get -y install python2.7 python-support libjna-java

# cassandra service warns trying to set ulimits in a container, so disable ulimit commands
RUN perl -pi.bak -e 's/ulimit/#ulimit/g' /etc/init.d/cassandra

# install test data
# WORKDIR /root
# COPY trigrams /root/trigrams
# COPY setup.sql /root/setup.sql
# COPY trigram /root/trigram

# start cassandra and load test db
# RUN service cassandra start; sleep 15; cqlsh < setup.sql

# build a nice simple script to run spark-cassandra
# RUN echo '#!/bin/bash' > spark-cass ; echo 'spark-shell --jars $(echo /usr/local/cassandra-java-driver/*.jar /usr/local/spark-cassandra-connector/spark-cassandra-connector/target/scala-2.10/*.jar /usr/local/spark-cassandra-connector/spark-cassandra-connector-java/target/scala-2.10/*.jar /usr/share/cassandra/apache-cassandra-thrift-*.jar /usr/share/cassandra/lib/libthrift-*.jar /usr/local/cassandra-java-driver/lib/*.jar | sed -e "s/ /,/g")' >> spark-cass ; chmod 755 spark-cass
# RUN echo 'SPARKPATH=$(echo /usr/local/cassandra-java-driver/*.jar /usr/local/spark-cassandra-connector/spark-cassandra-connector/target/scala-2.10/*.jar /usr/local/spark-cassandra-connector/spark-cassandra-connector-java/target/scala-2.10/*.jar /usr/share/cassandra/apache-cassandra-thrift-*.jar /usr/share/cassandra/lib/libthrift-*.jar /usr/local/cassandra-java-driver/lib/*.jar | sed -e "s/ /:/g")' >> spark-cass-env.sh

# ENV PATH /usr/local/spark/bin:/usr/local/cassandra/bin:/usr/local/sbt/bin:/usr/local/scala/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

CMD service cassandra start && /bin/bash
