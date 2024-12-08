FROM maven:3.9-amazoncorretto-11 as build
ARG HADOOP_VERSION=3.3.4
ARG HBASE_VERSION=2.4.17
ARG SCALA_VERSION=2.12.20
ARG SCALA_BIN_VERSION=2.12
ARG SPARK_VERSION=3.4.3
WORKDIR /src
COPY ./ /src/
RUN --mount=type=cache,target=/root/.m2,id=hbase-connectors-m2 \
    mvn -Dspark.version=${SPARK_VERSION} -Dscala.version=${SCALA_VERSION} \
    -Dhadoop-three.version=${HADOOP_VERSION} -Dhbase-two.version=${HBASE_VERSION} \
    -Dscala.binary.version=${SCALA_BIN_VERSION} \
    -DskipTests clean package install -f pom.xml \
    && cp /root/.m2/repository/org/scala-lang/scala-library/${SCALA_VERSION}/scala-library-${SCALA_VERSION}.jar /src/spark/hbase-spark/target/ \
    && mkdir -p /target/.m2/repository/org/apache/hbase/ \
    && cp -pr /root/.m2/repository/org/apache/hbase/connectors /target/.m2/repository/org/apache/hbase/

FROM busybox
COPY --from=build /src/spark/hbase-spark/target/hbase-spark-*-SNAPSHOT.jar /src/spark/hbase-spark-protocol-shaded/target/hbase-spark-protocol-shaded-*-SNAPSHOT.jar /src/spark/hbase-spark/target/scala-library-*.jar /target/
COPY --from=build /target/.m2/repository/org/apache/hbase/connectors /target/.m2/repository/org/apache/hbase/connectors

