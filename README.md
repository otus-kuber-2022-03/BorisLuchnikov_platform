# BorisLuchnikov_platform
BorisLuchnikov Platform repository

# ДЗ Настройка локального окружения. Запуск первого контейнера. Работа с kubectl
В рамках домашнего задания, ознакомился с такими инструментами как:
minikube - для развертки локального окружения
kubectl - утилита для управления кластеров Kubernetes
k9s - консольный инструмент для взаимодействия с kubernetes

## Задание с web приложением
1. Создал Dockerfile web приложения на основе nginx
   1. Приложение отдает из корневой папки `/app` все файлы с .html при обращении к ним через host:port
   2. Сделал чтобы приложение запускалось на 8000 порте
   3. Сделал чтобы приложение запускалось под юзером nginx с uid 1001
2. Собрал образ и запушил в docker hub https://hub.docker.com/r/borisluchnikov/kube-web-app
3. Реализовал манифест для pod приложения /kubernetes-intro/web-pod.yaml
4. Запустил pod приложения через `kubectl apply -f web-pod.yaml`
5. Дополнил манифест init-containers, чтобы при запуске pod сначала отрабатывал init container6 который скачивал index.html и подкладывал в общий volume для init контейнера и основного контейнера
6. После запуска манифеста открыл порт 8000 через `kubectl port-forward --address 0.0.0.0 pod/web 8000:8000` чтобы можно было получить доступ до приложения по адресу localhost:8000 и чтобы отображался скачиваемый index.html

## Задание c hipster-shop
1. Скачал репозиторий https://github.com/GoogleCloudPlatform/microservices-demo
2. Собрал образ приложения frontend и запушил в docker hub https://hub.docker.com/r/borisluchnikov/hs-frontend
3. Запустил pod frontend через команду `kubectl run frontend --image avtandilko/hipster-frontend:v0.0.1 --restart=Never`, pod создался, но приложение не запустилось из-за не указанных обязательных переменных окружения
4. Создал frontend-pod.yaml манифест через команду `kubectl run frontend --image avtandilko/hipster-frontend:v0.0.1 --restart=Never --dry-run=client -o yaml > frontend-pod.yaml`, пришлось модифицировать предложенную в ДЗ, так как в последней версии kubernetes необходимо указывать `--dry-run=client`
5. Создал рабочий манифест frontend-pod-healthy.yaml, а именно добавил недостающие обязательные переменные окружения в блок env 
6. Запустил pod через `kubectl apply -f frontend-pod-healthy.yaml` предварительно удалив старый pod frontend через `kubectl delete pod frontend`
7. Приложение запустилось со статусом Running