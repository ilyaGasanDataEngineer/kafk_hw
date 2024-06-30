# README

## Установка и настройка Kafka в Anaconda

### Шаг 1: Установка Anaconda

1. **Перейдите в домашний каталог:**
   ```sh
   cd ~
   ```
2. **Скачайте скрипт установки Anaconda:**
   ```sh
   wget https://repo.anaconda.com/archive/Anaconda3-5.3.1-Linux-x86_64.sh -O ~/anaconda.sh
   ```
3. **Проверьте контрольную сумму файла:**
   ```sh
   sha256sum ~/anaconda.sh
   ```
4. **Запустите скрипт установки:**
   ```sh
   bash ~/anaconda.sh
   ```
   Примите соглашение, следуя инструкциям на экране.

5. **Активируйте Anaconda:**
   ```sh
   source ~/anaconda3/bin/activate
   ```

6. **Установите kafka-python:**
   ```sh
   pip install kafka-python
   pip install --upgrade pip
   ```

### Шаг 2: Установка и настройка Kafka

1. **Перейдите в каталог вашего проекта:**
   ```sh
   cd ~/jupiter_projects/kafka/
   ```
2. **Скачайте архив Confluent Platform:**
   ```sh
   curl -O https://packages.confluent.io/archive/7.0/confluent-community-7.0.1.tar.gz
   ```
3. **Распакуйте архив:**
   ```sh
   tar -xf confluent-community-7.0.1.tar.gz
   ```
4. **Перейдите в каталог Confluent Platform:**
   ```sh
   cd confluent-7.0.1
   ```
5. **Форматируйте хранилище Kafka:**
   ```sh
   ./bin/kafka-storage format --config ./etc/kafka/kraft/server.properties --cluster-id $(./bin/kafka-storage random-uuid)
   ```

### Шаг 3: Установка Java

1. **Установите curl:**
   ```sh
   sudo apt install curl
   ```
2. **Скачайте и распакуйте JDK:**
   ```sh
   curl https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz -o jdk-17.tar.gz
   tar xzf jdk-17.tar.gz
   sudo mv ./jdk-17 /usr/lib64
   ```
3. **Скачайте и распакуйте Kafka:**
   ```sh
   curl https://mirrors.estointernet.in/apache/kafka/3.0.0/kafka_2.13-3.0.0.tgz -o kafka_2.13-3.0.0.tgz
   tar xzf kafka_2.13-3.0.0.tgz
   sudo mv ./kafka_2.13-3.0.0 /opt/kafka
   ```

### Шаг 4: Настройка прав и переменных окружения

1. **Установите права для текущего пользователя:**
   ```sh
   sudo chmod a+rwx /opt/kafka
   ```
2. **Настройте переменные окружения:**
   ```sh
   tee -a ~/.bashrc << END
   # Java
   export JAVA_HOME=/usr/lib64/jdk-17
   PATH=\$PATH:\$JAVA_HOME/bin
   # Kafka
   export KAFKA_HOME=/opt/kafka
   PATH=\$PATH:\$KAFKA_HOME/bin
   END
   ```
3. **Загрузите переменные окружения:**
   ```sh
   source ~/.bashrc
   ```

### Шаг 5: Запуск Kafka

1. **Запуск брокера (сервера):**
   ```sh
   ./bin/kafka-server-start ./etc/kafka/kraft/server.properties
   ```

2. **Запуск producer:**
   ```sh
   ./bin/kafka-console-producer --bootstrap-server localhost:9092 --topic quickstart
   ```

3. **Запуск consumer:**
   ```sh
   ./bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic quickstart --from-beginning
   ```

### Примечание

Сделайте ваш скрипт исполняемым:
```sh
chmod +x script.sh
```

Эти инструкции помогут вам установить и настроить Kafka в Anaconda, а также запускать Kafka broker, producer и consumer.
