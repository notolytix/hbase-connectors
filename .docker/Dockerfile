FROM maven:3.9-amazoncorretto-11 as build
ARG HADOOP_VERSION=3.3.6
ARG HBASE_VERSION=2.5.7
WORKDIR /src
COPY ./ /src/
RUN mvn -Dhadoop-three.version=${HADOOP_VERSION} -Dhbase-two.version=${HBASE_VERSION} -DskipTests clean package install -f pom.xml

