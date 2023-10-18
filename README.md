# Домашнее задание к занятию "`Очереди RabbitMQ`" - `Николай Концевой`

---

### Задание 1. Установка RabbitMQ

Используя Vagrant или VirtualBox, создайте виртуальную машину и установите RabbitMQ.
Добавьте management plug-in и зайдите в веб-интерфейс.

*Итогом выполнения домашнего задания будет приложенный скриншот веб-интерфейса RabbitMQ.*


### Ответ 1.

![Скрин консоли](https://github.com/Stitchzxz/homework_netology/blob/main/screen/1rabbit_console.png)

---

### Задание 2. Отправка и получение сообщений

Используя приложенные скрипты, проведите тестовую отправку и получение сообщения.
Для отправки сообщений необходимо запустить скрипт producer.py.

Для работы скриптов вам необходимо установить Python версии 3 и библиотеку Pika.
Также в скриптах нужно указать IP-адрес машины, на которой запущен RabbitMQ, заменив localhost на нужный IP.

```shell script
$ pip install pika
```

Зайдите в веб-интерфейс, найдите очередь под названием hello и сделайте скриншот.
После чего запустите второй скрипт consumer.py и сделайте скриншот результата выполнения скрипта

*В качестве решения домашнего задания приложите оба скриншота, сделанных на этапе выполнения.*

Для закрепления материала можете попробовать модифицировать скрипты, чтобы поменять название очереди и отправляемое сообщение.


### Ответ 2.

![Выполнение скрипта прод](https://github.com/Stitchzxz/homework_netology/blob/main/screen/2-1prod.png)
![Выполнение скрипта консум](https://github.com/Stitchzxz/homework_netology/blob/main/screen/2-2consum.png)
![Выполнение скрипта консум2](https://github.com/Stitchzxz/homework_netology/blob/main/screen/2-3consum2.png)

---

### Задание 3. Подготовка HA кластера

Используя Vagrant или VirtualBox, создайте вторую виртуальную машину и установите RabbitMQ.
Добавьте в файл hosts название и IP-адрес каждой машины, чтобы машины могли видеть друг друга по имени.

Пример содержимого hosts файла:
```shell script
$ cat /etc/hosts
192.168.0.10 rmq01
192.168.0.11 rmq02
```
После этого ваши машины могут пинговаться по имени.

Затем объедините две машины в кластер и создайте политику ha-all на все очереди.

*В качестве решения домашнего задания приложите скриншоты из веб-интерфейса с информацией о доступных нодах в кластере и включённой политикой.*

Также приложите вывод команды с двух нод:

```shell script
$ rabbitmqctl cluster_status
```

Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод:

```shell script
$ rabbitmqadmin get queue='hello'
```

После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.

*Приложите скриншот результата работы второго скрипта.*

### Ответ 3.

*В качестве решения домашнего задания приложите скриншоты из веб-интерфейса с информацией о доступных нодах в кластере и включённой политикой.*
![Cluster](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-1rabbit_cluster.png)
![Политика ха-алл](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-2ha-all.png)

*Также приложите вывод команды с двух нод*
![Статус кластера 1й ноды](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-3rabbit_status.png)
![Статус кластера 2й ноды](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-4rabbit_status.png)

*Для закрепления материала снова запустите скрипт producer.py и приложите скриншот выполнения команды на каждой из нод*
![Гет админ 1](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-5get_admin.png)
![Гет админ 2](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-6get_admin.png)

*После чего попробуйте отключить одну из нод, желательно ту, к которой подключались из скрипта, затем поправьте параметры подключения в скрипте consumer.py на вторую ноду и запустите его.*
![Консум со 2й ноды при отк 1й ноды](https://github.com/Stitchzxz/homework_netology/blob/main/screen/3-7rab2_consum.png)

---

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### * Задание 4. Ansible playbook

Напишите плейбук, который будет производить установку RabbitMQ на любое количество нод и объединять их в кластер.
При этом будет автоматически создавать политику ha-all.

*Готовый плейбук разместите в своём репозитории.*