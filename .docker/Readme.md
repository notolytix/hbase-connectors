# Example of build
docker build . -f .docker/Dockerfile -t hbase-connectots:dev --build-arg HADOOP_VERSION=3.3.6
# Build args options and their defaults if not overwritten:
HADOOP_VERSION=3.3.4
HBASE_VERSION=2.4.17
SCALA_VERSION=2.12.20
SCALA_BIN_VERSION=2.12
SPARK_VERSION=3.4.3
