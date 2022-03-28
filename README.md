# Выполнено ДЗ №

- [x] Основное ДЗ
- [x] Задание со *

## В процессе сделано:
- Создал Dockerfile web приложения на основе nginx. Которое отдает из корневой папки `/app` все файлы с .html при обращении к ним через host:port.
- Собрал образ и запушил в docker hub https://hub.docker.com/r/borisluchnikov/kube-web-app
- Реализовал манифест для pod приложения /kubernetes-intro/web-pod.yaml
- Запустил pod приложения через `kubectl apply -f web-pod.yaml`
- Дополнил манифест init-containers, чтобы при запуске pod сначала отрабатывал init container6 который скачивал index.html и подкладывал в общий volume для init контейнера и основного контейнера
- После запуска манифеста открыл порт 8000 через `kubectl port-forward --address 0.0.0.0 pod/web 8000:8000` чтобы можно было получить доступ до приложения по адресу localhost:8000 и чтобы отображался скачиваемый index.html
- Скачал репозиторий https://github.com/GoogleCloudPlatform/microservices-demo
- Собрал образ приложения frontend и запушил в docker hub https://hub.docker.com/r/borisluchnikov/hs-frontend
- Запустил pod frontend через команду `kubectl run frontend --image avtandilko/hipster-frontend:v0.0.1 --restart=Never`, pod создался, но приложение не запустилось из-за не указанных обязательных переменных окружения
- Создал frontend-pod.yaml манифест через команду `kubectl run frontend --image avtandilko/hipster-frontend:v0.0.1 --restart=Never --dry-run=client -o yaml > frontend-pod.yaml`, пришлось модифицировать предложенную в ДЗ, так как в последней версии kubernetes необходимо указывать `--dry-run=client`
- Создал рабочий манифест frontend-pod-healthy.yaml, а именно добавил недостающие обязательные переменные окружения в блок env
- Запустил pod через `kubectl apply -f frontend-pod-healthy.yaml` предварительно удалив старый pod frontend через `kubectl delete pod frontend`
- Приложение запустилось со статусом Running

## Как запустить проект:
- `kubectl apply -f /kubernetes-intro/web-pod.yaml`
- `kubectl port-forward --address 0.0.0.0 pod/web 8000:8000`

## Как проверить работоспособность:
- Перейти по ссылке http://localhost:8000

## PR checklist:
- [x] Выставлен label с темой домашнего задания