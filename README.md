# Мониторинг кластера при помощи Falco

В рамках выполнения работы вам необходимо выполнить следующие задачи:

1. Разверуть локальный кластер  k8s с использованием minikube
2. Настроить рабочее окружение (kubectl, helm)
3. Изучить базовые команды для управления кластером
4. Установить и сконфигурировать Falco при помощи Helm-чарта
5. Настроить оповещения о событиях безопасности в телеграм чат
6. Иницировать событие безопасности и заставить сработать алерт


## Подготовка окружения

Успешное выполнение работы протестировано для MacOS и Debian-based Linux. 

2. Установить Docker
2. Установить [minikube](https://minikube.sigs.k8s.io/docs/start/), [kubectl](https://kubernetes.io/docs/tasks/tools/) и [helm](https://helm.sh/docs/intro/install/)
3. [Поднять](https://minikube.sigs.k8s.io/docs/start/) кластер при помощи minikube
4. В miikube cоздать namespace - secured-ns
5. В созданный неймспейс задеплоить deployment.yaml

## Выполнение работы

1. Установить [Falco](https://falco.org) в кластер minikube при помощи [helm-чарта](https://github.com/falcosecurity/charts/blob/master/README.md) (у меня заработало с драйвером modern_ebpf на mac)
2. Создать телеграм-бота и добавить его в чат с уведомлениями о событиях безопасности
3. Для Falco настроить алерты о событиях безопасности в telegram-бота при помощи falcosidekick (удобнее всего сделать это через values в helm-чарте)
4. Изучить дефолтные [правила](https://github.com/falcosecurity/rules/blob/main/rules/falco_rules.yaml) для falco и быть готовыми их обсудить
8. Для secured-ns подготовить демонстрацию срабатывания не менее 3х правил


## Полезные команды

```bash
minikube dashboard
kubectl create namespace demo
kubectl -n demo apply -f deployment.yaml
minikube tunnel
helm repo add falcosecurity https://falcosecurity.github.io/charts
helm repo update
helm pull falcosecurity/falco --untar
helm install falco -n falco -f custom-values.yaml -f custom-rules.yaml falcosecurity/falco --create-namespace
```
