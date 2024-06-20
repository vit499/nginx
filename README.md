# nginx для html

Вы сделали страничку index.html.
Создали проект на github с названием mysite1 и добавили туда свою страничку index.html.
Вы хотите, чтобы ваша страничка открывалась по адресу mysite1.mysite.ru

Зайдите в рабочую папку на сервере и сделайте git clone своего проекта.
Теперь ваш проект находится на сервере по пути work/mysite1.

Теперь в данной папке nginx добавьте информацию о своем проекте в двух мествх.

1. В файл docker-compose.yml добавьте volume

например, рабочая папка с HTML страничкой называется mysite1 и находится она по пути work/mysite1.
тогда в volumes нужно добавить

    volumes:
      - /home/user/work/mysite1:/usr/www/mysite1

где user - имя нашего пользователя

Теперь в контейнере nginx для будет создана папка /usr/www/mysite1, путь до нее нужно указать в конфигурации (п.2)

2. В папку data/nginx нужно добавьте файл с названием mysite1.conf с таким содержимым

````server {
listen 80;
server_name mysite1.mysite.ru; # тут mysite.ru нужно заменить на реальное имя сайта
root /usr/www/mysite1;
index index.html;
}```

3. Сохраните изменения и запустите docker compose up -d.

Нужны еще странички? Добавьте еще volume mysite2

    volumes:
      - /home/user/work/mysite1:/usr/www/mysite1
      - /home/user/work/mysite2:/usr/www/mysite2

и файл mysite2.conf в котором вместо mysite1 будет mysite2.
````
