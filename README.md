# terraform-atlantis

## Разворачиваем atlantis в kubernetes при помощи helm:

1. Создаем token доступа:

<p align="left">
  <img src="./pic/token.png">
</p>

2. Создаем секреты веб-перехватчиков:

Генерируем онлайн с помощью https://www.browserling.com/tools/random-string

3. Установливаем с помощью Helm:

```bash
andreyshestikhin@MacBook-Air-Andrey terraform-atlantis % helm upgrade -i atlantis runatlantis/atlantis -f values.yaml 
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /Users/andreyshestikhin/.kube/config
Release "atlantis" has been upgraded. Happy Helming!
NAME: atlantis
LAST DEPLOYED: Mon Apr  3 22:18:53 2023
NAMESPACE: default
STATUS: deployed
REVISION: 2
NOTES:
1. Get the application URL by running these commands:
     NOTE: It may take a few minutes for the LoadBalancer IP to be available.
           You can watch the status of by running 'kubectl get svc -w atlantis'
  export SERVICE_IP=$(kubectl get svc --namespace default atlantis -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
  echo http://$SERVICE_IP:80
1. Atlantis will not start successfully unless at least one of the following sets of credentials are specified (see values.yaml for detailed usage):
  - github
  - githubApp
  - gitlab
  - bitbucket
```

```bash
andreyshestikhin@MacBook-Air-Andrey terraform-atlantis % kubectl get pod
NAME         READY   STATUS    RESTARTS   AGE
atlantis-0   1/1     Running   0          2m27s
andreyshestikhin@MacBook-Air-Andrey terraform-atlantis % kubectl get svc
NAME         TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)        AGE
atlantis     LoadBalancer   10.96.164.59   84.201.146.163   80:30881/TCP   30s
kubernetes   ClusterIP      10.96.128.1    <none>           443/TCP        21m
```

<p align="left">
  <img src="./pic/atlantis.png">
</p>

2. Настраиваем webhook:

<p align="left">
  <img src="./pic/webhook.png">
</p>

<p align="left">
  <img src="./pic/webhook2.png">
</p>