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
- Pods не были обновлены потому что, ReplicaSet не проверяет соответсвие запущенных pod описанному шаблону.