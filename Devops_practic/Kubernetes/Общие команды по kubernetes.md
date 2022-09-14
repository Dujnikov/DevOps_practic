minikube start - запуск миникуба (пример со своими параметрами: minikube start -- cpus=4 --memory=8gb -- disk-size=25gb )
kubectl version версия кубера
kubectl  version -- client  - версия клиента
kubectl get componentstatuses - статус компонентов
kubectl cluster-info  - инфа о кластере
kubectl get nodes - показывает nod'ы
minikube stop - остановка
minikube delete
minikube ssh - заход в minikube внутрь
kubectl -n kube-system get pod -o wide - вывод  более подробный данных о кубе
kubectl get namespaces - (вывести существующие namespaces)
kubectl get ns - (вывести существующие namespaces)


Пространства имён — это способ разделения ресурсов кластера между несколькими пользователями (с помощью квоты ресурсов). По умолчанию в будущих версиях Kubernetes объекты в одном и том же пространстве имён будут иметь одинаковую политику контроля доступа.

the kubernetes hard way

![[troubleshooting-kubernetes.en_en.v3.pdf]]