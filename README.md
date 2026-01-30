Описание  Простой HTTP сервер на Flask + Jinja.
HOST-ы :
   192.168.100.115 gitlab-ci
   192.168.100.116 gitlab-runner
   192.168.100.117 gitlab-node2  (сервер назначения).
   
GitLab-CI:
  1) проверяет линтером на синтаксис python-код (с warning пропускает).
  2) делает build по Dockerfile (используя kaniko) и заливает в  REGISTRY (https://index.docker.io/v1/)
  3) при deploy -  скачиваю с DockerHub имадж и запускаю контейнер  "http-server"  на 192.168.100.117 gitlab-node2.
  4) приложение слушает порт 192.168.100.117:5000.
  5) делается healthcheck через curl -f http://${HOST_IP}:5000/ .
  6) результат pipeline сохранен в файл лога.
