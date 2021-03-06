1. Встановив Docker та перевірив правильність його роботи, запустивши наступні команди:
   ```bash
   docker -v
   docker -h
   docker run docker/whalesay cowsay Docker is fun
   ```
   Перенаправив вивід цих команд у файл my_work.log. Закомітив його.  

2. Створюємо імедж із Django сайтом зробленим у попередній роботі.

   Створив файл Dockerfile, замінив в ньому посилання на мій Git репозиторій. Закомітив його.
3. Створив власний репозиторій на Docker Hub, який знаходиться за [цим посиланням](https://hub.docker.com/repository/docker/rsosnovskyi1726/lab4).
4. Виконав білд (build) Docker імеджа та завантажив його до репозиторію.
    ```bash
    docker build -t rsosnovskyi1726/lab4:django .
    docker images
    docker push rsosnovskyi1726/lab4:django
    ```
   Перед завантаженням імеджа потрібно було залогінитися через консоль:
   ```bash
   docker login
   ```
   Тоді вже можна було виконати команду:
   ```bash
   docker push rsosnovskyi1726/lab4:django
   ```
5. Запустив веб-сайт.
   ```bash
   docker run -it --name=django --rm -p 8000:8000 rsosnovskyi1726/lab4:django
   ```
6. Створюємо ще один контейнер із програмою моніторингу нашого веб-сайту:
   - створив ще один Dockerfile (Dockerfile_monitoring) в якому помістив програму моніторингу;
   - виконав білд даного імеджа, давши йому тег `monitoring`, та залив його до репозиторію;
   ```bash
   docker build -f Dockerfile_monitoring -t rsosnovskyi1726/lab4:monitoring .
   docker push rsosnovskyi1726/lab4:monitoring
   ```
   - запустив контейнер.
   ```bash
   docker run -it --name=monitoring --rm --net=host rsosnovskyi1726/lab4:monitoring
   ```
   Програма моніторингу працює успішно:
7. Завантажив файл server.log з контейнера на локальну машину:
   ```bash
   docker cp monitoring:/app/server.log .
   ```

