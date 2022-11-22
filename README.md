# Домашнее задание к занятию "14.4 Сервис-аккаунты"

## Задача 1: Работа с сервис-аккаунтами через утилиту kubectl в установленном minikube

Выполните приведённые команды в консоли. Получите вывод команд. Сохраните
задачу 1 как справочный материал.

### 1.1 Как создать сервис-аккаунт?

```
kubectl create serviceaccount netology
```

### Ответ 1.1: создаем аккаунт  

![image](https://user-images.githubusercontent.com/92969676/203279775-f21110de-730c-4621-b5fa-868a8892135e.png)


### 1.2 Как просмотреть список сервис-акаунтов?

```
kubectl get serviceaccounts
kubectl get serviceaccount
```

### Ответ 1.2: проверяем какие вообще аккаунты у нас есть

![image](https://user-images.githubusercontent.com/92969676/203279870-741251ca-2f24-419b-86ae-db773294f3bd.png)

### 1.3Как получить информацию в формате YAML и/или JSON?

```
kubectl get serviceaccount netology -o yaml
kubectl get serviceaccount default -o json
```
### Ответ 1.3: просматриваем информацию об аккаунтах. В задании скорее всего имелось ввиду вывести в консоль информацию по аккаунту "netology", а во втором случае мы выводим информацию "default". В итоге вывел информацию как по заданию + по netology в json:

![image](https://user-images.githubusercontent.com/92969676/203280127-bfd190cf-b7ae-45fe-ba8b-21d60c204eef.png)


### 1.4 Как выгрузить сервис-акаунты и сохранить его в файл?

```
kubectl get serviceaccounts -o json > serviceaccounts.json
kubectl get serviceaccount netology -o yaml > netology.yml
```

### Ответ 1.4: выгружаем информацию по аккаунту в файл, чтобы в дальнешем удалить его и загрузить из файла повторно.

![image](https://user-images.githubusercontent.com/92969676/203280601-b31af292-5128-4ff8-88d1-bc505a67a734.png)

### 1.5 Как удалить сервис-акаунт?

```
kubectl delete serviceaccount netology
```

### Ответ 1.5: удаляем аккаунт

![image](https://user-images.githubusercontent.com/92969676/203280717-abdbf37c-e885-4367-aefe-67ab6313c2ab.png)


### 1.6 Как загрузить сервис-акаунт из файла?

```
kubectl apply -f netology.yml
```

### Ответ 1.6: загружаем аккаунт из файла

![image](https://user-images.githubusercontent.com/92969676/203280801-376f8151-1eb6-4ab8-9827-d70e0c3983c3.png)


## Задача 2 (*): Работа с сервис-акаунтами внутри модуля

Выбрать любимый образ контейнера, подключить сервис-акаунты и проверить
доступность API Kubernetes

```
kubectl run -i --tty fedora --image=fedora --restart=Never -- sh
```

Просмотреть переменные среды

```
env | grep KUBE
```

Получить значения переменных

```
K8S=https://$KUBERNETES_SERVICE_HOST:$KUBERNETES_SERVICE_PORT
SADIR=/var/run/secrets/kubernetes.io/serviceaccount
TOKEN=$(cat $SADIR/token)
CACERT=$SADIR/ca.crt
NAMESPACE=$(cat $SADIR/namespace)
```

Подключаемся к API

```
curl -H "Authorization: Bearer $TOKEN" --cacert $CACERT $K8S/api/v1/
```

В случае с minikube может быть другой адрес и порт, который можно взять здесь

```
cat ~/.kube/config
```

или здесь

```
kubectl cluster-info
```

ИТОГ по заданию 2:

json, который выдернули curl`ом приложил в данном репозитории

![image](https://user-images.githubusercontent.com/92969676/203282203-663b4ee5-7e5d-4c6d-9361-8e26f5360cf7.png)


---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

В качестве решения прикрепите к ДЗ конфиг файлы для деплоя. Прикрепите скриншоты вывода команды kubectl со списком запущенных объектов каждого типа (pods, deployments, serviceaccounts) или скриншот из самого Kubernetes, что сервисы подняты и работают, а также вывод из CLI.

---
