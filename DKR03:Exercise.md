# Выполнение задание №3


1. Скачайте конфигурационный файл [nginx](https://gitlab.rebrainme.com/docker-course-students/dkr-nginx-conf-1/blob/master/nginx.conf).
```
nano nginx.conf
```

2. Запустите контейнер со следующими параметрами:

- должен работать в фоне `-d`
- слушает на хосте 127.0.0.1:8890 `-p 127.0.0.1:8890:80`
- имеет имя rbm-dkr-03 `--name rbm-dkr-03`
- должен пробрасывать скачанный вами конфигурационный файл внутрь контейнера как основной конфигурационный файл `-v /home/user/nginx.conf:/etc/nginx/nginx.conf`
- образ - nginx:stable `nginx:stable`

Результат: `docker run -d -p 127.0.0.1:8890:80 -v /home/user/nginx.conf:/etc/nginx/nginx.conf --name rbm-dkr-03 nginx:stable`

3. Проверьте работу, обратившись к 127.0.0.1:8890, - в ответ должно возвращать строку Welcome to the training program RebrainMe: Docker!
```
curl 127.0.0.1:8890
Welcome to the training program RebrainMe: Docker!
```
4. Выведите список запущенных контейнеров - контейнер должен быть запущен.
```
docker ps
...
```
5. Выполните команду docker exec -ti rbm-dkr-03 md5sum /etc/nginx/nginx.conf
```
docker exec -ti rbm-dkr-03 md5sum /etc/nginx/nginx.conf
1265cde0fefb06a47f02b8c95cc892eb  /etc/nginx/nginx.conf
```
6. Скачайте новый конфигурационный файл [nginx](https://gitlab.rebrainme.com/docker-course-students/dkr-nginx-conf-2/blob/master/nginx.conf).
7. Измените проброшенный конфигурационный файл, размещенный на хостовой системе, на новый. Проведите эксперименты с различными способами изменения: через команду cp, через vim, nano
```
nano nginx.conf
```
8. Выполните reload nginx без остановки контейнера при помощи команды exec.
```
docker exec -it rbm-dkr-03 nginx -s reload
```
 `-s` reload сообщает Nginx о необходимости перезагрузить свою конфигурацию без остановки
 
9. Проверьте работу, обратившись к 127.0.0.1:8890, - в ответ должно возвращать строку Welcome to the training program RebrainMe: Docker! Again!
```
curl 127.0.0.1:8890
Welcome to the training program RebrainMe: Docker! Again!
```
10. Выполните команду docker exec -ti rbm-dkr-03 md5sum /etc/nginx/nginx.conf (вывод в консоли сохраняем).
```
docker exec -ti rbm-dkr-03 md5sum /etc/nginx/nginx.conf
1265cde0fefb06a47f02b8c95cc892eb  /etc/nginx/nginx.conf
```
11. Сравните результаты изменения файла nginx.conf разными командами. Найдите информацию, почему в некоторых случаях изменение не отображалось в контейнере.
12. Выведите список запущенных контейнеров - контейнер должен быть запущен.
13. Отправьте задание на проверку.
