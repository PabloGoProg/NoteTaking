
## WSL2

0. Actualizar el sistema
```shell
sudo apt update
sudo apt upgrade -y
```

1. Download [Apache Kafka](https://kafka.apache.org/quickstart)
```shell
wget https://dlcdn.apache.org/kafka/4.0.0/kafka_2.13-4.0.0.tgz
# -> 132M 18 Mar 03:29  kafka_2.13-4.0.0.tgz
```

2. Instalar Java & JDK
```shell
# Verificar si esta instalado
java -version

# Instalar OpenJDK
sudo apt install openjdk-{version}-jdk -y

# Verificar Instalación
java -version
# -> openjdk version "{version}.0.x" ...

# Verificar la dirección del JAVA_HOME
echo $JAVA_HOME

# Ajustar el PATH en caso de ser encesario
JAVA_HOME="/usr/lib/jvm/java-{version}-openjdk-amd64"
```

3. Descomprimir el archivo resultante y entrar a los binarios
```shell
tar zxf kafka_2.13-4.0.0.tgz
mv kafka_2.13-4.0.0.tgz kafka
cd kafka/bin
```

4. Exportar binarios al PATH
```shell
export PATH=$PATH:~/kafka/bin
```

5. Configurar entorno de Kafka
```shell
# Crear un CLUSTER_ID
KAFKA_CLUSTER_ID="$(kafka-storage.sh random-uuid)"

# Preparar el formato de los archivos de log
kafka-storage.sh format --standalone -t $KAFKA_CLUSTER_ID -c ~/kafka/config/server.properties

# Correr el servidor de Aapache Kafka
kafka-server-start.sh ~/kafka/config/server.properties
```

## Quick Start

* Crear un nuevo topic
```shell
kafka-topics.sh --create --topic test-topic --bootstrap-server localhost:9092
# -> Created topic test-topic.

# Listar los topicos de un servidor
kafka-topics.sh --list --bootstrap-server localhost:9092

# Describir un topico de un servidor
kafka-topics.sh --describe --topic test-topic --bootstrap-server localhost:9092
```

- Crear un Producer y un Consumer desde consola
```shell
kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test-topic
```