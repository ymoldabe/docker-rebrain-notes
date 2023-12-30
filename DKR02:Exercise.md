# Выполнение задание №2


Задание:

1. Скачайте конфигурационный файл [nginx](https://gitlab.rebrainme.com/docker-course-students/dkr-nginx-conf-1/blob/master/nginx.conf).
```
nano nginx.conf
```

2. Запустите контейнер со следующими параметрами:
- должен работать в фоне: `-d`
- слушает на хосте 127.0.0.1:8889: `-p 8889:80`
- имеет имя rbm-dkr-02: `--name rbm-dkr-02`
- должен пробрасывать скачанный вами конфигурационный файл nginx внутрь контейнера как основной конфигурационный файл: `-v /home/user/nginx.conf:/etc/nginx/nginx.conf`
- образ - nginx:stable: `nginx:stable`

Результат:
```
docker run -dp 8889:80 -v /home/user/nginx.conf:/etc/nginx/nginx.conf --name rbm-dkr-02 nginx:stable
```

Проверьте работу, обратившись к 127.0.0.1:8889, - в ответ должно возвращать строку Welcome to the training program RebrainMe: Docker!

```
curl 127.0.0.1:8889
```

Выведите в консоли список запущенных контейнеров - контейнер должен быть запущен.

```
docker ps
```

Выполните подсчет md5sum конфигурационного файла nginx командой: docker exec -ti rbm-dkr-02 md5sum /etc/nginx/nginx.conf.

```
docker exec -ti rbm-dkr-02 md5sum /etc/nginx/nginx.conf
cde71f355e6770b80deb0065e85fa254  /etc/nginx/nginx.conf
```

Не останавливая контейнер, отправьте задание на проверку
