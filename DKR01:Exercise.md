# Выполнение задание №1

<span style="color: #FF3366;">Задание</span>: Вам предоставят виртуальную машину Linux с доступом по SSH и правами администратора (sudo). Выполните задачи в предоставленной среде. Время на выполнение около 10 минут. После выполнение задания отправьте его на проверку. Оценка будет выставлена в течение нескольких минут. Вы можете пересдать задание неограниченное количество раз.

## Туториал по [установке Docker](https://docs.docker.com/engine/install/ubuntu/) и работе с контейнерами

Следуйте официальной документации Docker для установки на Linux, чтобы установить Docker на вашу виртуальную машину.

1. Установите Docker на предоставленную систему, как указано в официальной документации.

```
user@server:~$ sudo apt-get update
...

user@server:~$ sudo apt-get install ca-certificates curl gnupg
...

user@server:~$ sudo install -m 0755 -d /etc/apt/keyrings
...

user@server:~$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
...

user@server:~$ sudo chmod a+r /etc/apt/keyrings/docker.gpg
...

user@server:~$ echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
...

user@server:~$ sudo apt-get update
...

```

2. Запустите контейнер на порту 28080 из официального образа nginx: docker run -d -p 127.0.0.1:28080:80 --name rbm-dkr-01 nginx:stable.

```
user@server:~$ sudo docker run -d -p 127.0.0.1:28080:80 --name rbm-dkr-01 nginx:stable
```

3. Выведите в консоли список запущенных контейнеров командой: docker ps.
```
user@server:~$ sudo docker ps
```

4. При помощи утилиты curl, запросите адрес http://127.0.0.1:28080 - должна появиться приветственная страница nginx. Если не появляется, то запуск контейнера неуспешен по какой-то причине.
```
user@server:~$ curl http://127.0.0.1:28080
...
```

5. Остановите ранее запущенный контейнер командой: docker stop rbm-dkr-01.
```
user@server:~$ sudo docker stop rbm-dkr-01
```
6. Выполните команду docker ps, тем самым проверьте произошедшие изменения в списке запущенных контейнеров - список контейнеров должен быть пуст.
```
user@server:~$ sudo docker ps
```
7. При помощи утилиты curl, запросите адрес http://127.0.0.1:28080 - сейчас должна быть ошибка, поскольку мы уже остановили контейнер и ничего не слушается на этом порту.
```
user@server:~$ curl http://127.0.0.1:28080
...
```
8. При помощи команды docker ps -a выведите список всех контейнеров в системе - в списке будет ваш остановленный контейнер
```
user@server:~$ sudo docker ps -a
```

После выполнения всех шагов нажмите "Проверить и закончить".