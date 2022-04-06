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