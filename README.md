# Выполнено ДЗ №1

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