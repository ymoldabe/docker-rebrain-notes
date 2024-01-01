# Выполнение задание №4


1. Скачайте конфигурационный файл [nginx](https://gitlab.rebrainme.com/docker-course-students/dkr-nginx-conf-3/blob/master/nginx.conf).
```
nano nginx.conf
```

2. Создайте volume с именем rbm-dkr-04-volume.

```
docker volume create rbm-dkr-04-volume
```

3. Запустите контейнер со следующими параметрами:

- должен работать в фоне `-d`
- слушает на хосте 127.0.0.1:8891 `-p 8891:80`
- имеет имя rbm-dkr-03 `--name rbm-dkr-03`
- должен пробрасывать скачанный вами конфигурационный файл внутрь контейнера как основной конфигурационный файл `-v /home/user/nginx.conf:/etc/nginx/nginx.conf`
- образ - nginx:stable `nginx:stable`
- в директорию с логами nginx должен быть подключен созданный вами Volume (Монтирование должно осуществляться в /var/log/nginx/external, иначе контейнер "упадёт" при старте) `-v rbm-dkr-04-volume:/var/log/nginx/external`

Результат: 
```
docker run -d -p 8891:80 --name rbm-dkr-04 -v /home/user/nginx.conf:/etc/nginx/nginx.conf -v rbm-dkr-04-volume:/var/log/nginx/external nginx:stable
```

4. Проверьте работу, обратившись к 127.0.0.1:8891, - в ответ должно возвращать строку Welcome to the training program RebrainMe: Docker!
```
curl 127.0.0.1:8890
Welcome to the training program RebrainMe: Docker!
```
5. Выведите список запущенных контейнеров - контейнер должен быть запущен.
```
docker ps
...
```

6. Выведите список существующих docker volumes.
```
docker volume ls
```
7. Выведите содержимое volume на хостовой системе, воспользовавшись командой ls -la.
```
sudo ls -la /var/lib/docker/volumes/rbm-dkr-04-volume/_data
```
8. Отправьте задание на проверку