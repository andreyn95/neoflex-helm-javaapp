### Задание 2. Пишем Helm чарт
1.  Продолжаем развивать наше приложение. Теперь нужно написать Helm-
чарт для него. Создайте папку, в которой создайте Chart.yaml и values.yaml. 
Создайте  подпапку  templates.  В  ней  создайте  шаблоны  deployment.yaml  и 
service.yaml. Используйте знание шаблонов Helm, чтобы вынести в values.yaml 
все подходящие значения из манифестов. 
2.  Разверните в кластере этот Helm-чарт и выставьте его через сервис типа 
NodePort. Сделайте скриншоты вывода команд helm: 
  • Список приложений Helm 
  • Описание вашего чарта через команды Helm 
 
В ответ нужно прислать. 
1.  Хелм-чарт. Можно прислать в виде ссылки на ваш репозиторий, или в виде 
архива, или в виде текстового документа с манифестами. 
2.  Скриншоты вывода команд Helm: 
  • Список приложений Helm. 
  • Описание вашего чарта через команды Helm.
```` bash
$ helm install helm-neoflex-javaapp . 
$ helm list
NAME                    NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                           APP VERSION
helm-neoflex-javaapp    default         1               2026-04-07 22:44:43.313814679 +0400 +04 deployed        helm-neoflex-javaapp-0.1.0      1.0.0
````
### Задание 3. Деплоим через ArgoCD

#### 4. Изменение values.yaml

https://github.com/andreyn95/neoflex-helm-javaapp/commit/7c8f40716c28d78d39e68de754b653f04820e940

После увеличения количества реплик в values.yaml, ArgoCD отреагировал следующим образом:

#### 5. Масштабирование через kubectl

```bash
$ kubectl scale deployment helm-neoflex-javaapp --replicas 8
deployment.apps/helm-neoflex-javaapp scaled

$ kubectl get pods
NAME                                    READY   STATUS              RESTARTS   AGE
helm-neoflex-javaapp-685988b744-46p9k   0/1     ContainerCreating   0          2s
helm-neoflex-javaapp-685988b744-6nkjj   0/1     ContainerCreating   0          2s
helm-neoflex-javaapp-685988b744-gp2m5   0/1     ContainerCreating   0          2s
helm-neoflex-javaapp-685988b744-mxdlh   1/1     Running             0          67m
helm-neoflex-javaapp-685988b744-twdmw   1/1     Running             0          3h14m
helm-neoflex-javaapp-685988b744-tztmq   1/1     Running             0          3h14m
helm-neoflex-javaapp-685988b744-vq2jb   1/1     Running             0          3h14m
helm-neoflex-javaapp-685988b744-w6stv   1/1     Running             0          67m

$ kubectl get pods
NAME                                    READY   STATUS    RESTARTS   AGE
helm-neoflex-javaapp-685988b744-mxdlh   1/1     Running   0          68m
helm-neoflex-javaapp-685988b744-twdmw   1/1     Running   0          3h15m
helm-neoflex-javaapp-685988b744-tztmq   1/1     Running   0          3h15m
helm-neoflex-javaapp-685988b744-vq2jb   1/1     Running   0          3h15m
helm-neoflex-javaapp-685988b744-w6stv   1/1     Running   0          68m
````
