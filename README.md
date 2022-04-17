# Выполнено ДЗ №2

- [x] Основное ДЗ
- [x] Задание со *

## В процессе сделано:
- Настроено локальное окружение (minikube, kubectl, k9s)
- Создано web приложение на основе nginx, описан pod манифест для него, добален запуск init контейнера
- Создан образ для приложения frontend и описан pod манифест для него. Исправлена ошибка старта приложения.

## Как запустить проект:
- Для приложения web: `kubectl apply -f /kubernetes-intro/web-pod.yaml`, `kubectl port-forward --address 0.0.0.0 pod/web 8000:8000`
- Для приложения frontend: `kubectl apply -f /kubernetes-intro/frontend-pod-healthy.yaml`
## Как проверить работоспособность:
- Для приложения web: Перейти по ссылке http://localhost:8000
- Для приложения frontend: Убедиться что pod в статусе Running `kubectl get pods`

## PR checklist:
- [x] Выставлен label с темой домашнего задания
***
# Выполнено ДЗ №3

- [x] Основное ДЗ
- [x] Deployment | Задание со ⭐
- [x] DaemonSet | Задание со ⭐
- [x] DaemonSet | Задание с ⭐⭐

## В процессе сделано:
- Реализован replicaset манифест для приложений frontend и paymentservice
- Реализован deployment манифест для приложений frontend и paymentservice
- Реализованы стратегии развертывания blue green и revers rolling update.
- Реализован daemonset манифест для приложения node-exporter, развернут на worker и master нодах

## Как запустить проект:
- Для приложения frontend через replicaset использовать команду `kubectl apply -f kubernetes-controllers/frontend-replicaset.yaml`
- Для приложения frontend через deployment использовать команду `kubectl apply -f kubernetes-controllers/frontend-deployment.yaml`
- Для приложения paymentservice через replicaset использовать команду `kubectl apply -f kubernetes-controllers/paymentservice-replicaset.yaml`
- Для приложения paymentservice через deployment использовать команду `kubectl apply -f kubernetes-controllers/paymentservice-deployment.yaml`
- Для проверки стратегиями развертывания blue green `kubectl apply -f kubernetes-controllers/paymentservice-deployment-bg.yaml`
- Для проверки стратегиями развертывания evers rolling update `kubectl apply -f kubernetes-controllers/paymentservice-deployment-reverse.yaml`
- Для проверки node-exporter `kubectl apply -f kubernetes-controllers/node-exporter-daemonset.yaml`

## Как проверить работоспособность:
- Проверка стратегий развертывания. Применить deployment, обновить image до версии v0.0.2 и применить deployemnt `kubectl apply -f kubernetes-controllers/paymentservice-deployment-bg.yaml | kubectl get rs -w`. Можно будет наблюдать в какой последовательности будут развертываться и удаляться pod. Аналогично для revers rolling update.
- Для node-exporter открыть порт 9100 для pod и получить метрики по url http://localhost:9100/metrics

## PR checklist:
- [x] Выставлен label с темой домашнего задания

## Ответ на вопрос "Почему обновление ReplicaSet не повлекло обновление запущенных pod?"
- Pods не были обновлены потому что, ReplicaSet не проверяет соответсвие запущенных pod

***
# Выполнено ДЗ №4
- [x] task01
- [x] task02
- [x] task03

## В процессе сделано:
- Созданы namespaces, serviceaccounts, clusterRoles, clusterRoleBindings

## Как запустить проект:
- Применить все файлы в ./kubernetes-security по очереди `kubectl apply -f same-file.yaml`

## Как проверить работоспособность:
- Проверить доступ через команды `kubectl auth can-i get pods -n=default --as=system:serviceaccount:default:bob` аналогично для user dave, carol, jane, ken

## PR checklist:
- [x] Выставлен label с темой домашнего задания
***

# Выполнено ДЗ №6
- [x] Основное ДЗ
- [x] Secrets | Задание со ⭐

## В процессе сделано:
- Развернут minio в режиме statefulset c pvc, pv и создан clusterIP для minio
- Создан secret и настроено его использование его использование через переменные среды.
PS: Можно было использовать и envFrom чтобы не тащить каждое значение по одному, но решил для ДЗ сделать подстановку значения в каждую переменную.

## Как запустить проект:
- Применить все манифесты из директории `/kubernetes-volumes`

## Как проверить работоспособность:
####Проверка работоспособности minio:
- открыть порт через `kubectl port-forward service/minio 9000`
- проверить через браузер перейдя на `http://localhost:9000`
- или проверить командой `mc ls play` через утилиту `https://github.com/minio/mc`, настроив подключение `mc alias set minio localhost:9000 minio minio123`

## PR checklist:
- [x] Выставлен label с темой домашнего задания
***