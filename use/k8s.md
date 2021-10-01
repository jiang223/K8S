# k8s

## 一、部署k8s控制台

### [https://github.com/AliyunContainerService/k8s-for-docker-desktop](https://github.com/AliyunContainerService/k8s-for-docker-desktop)

## 二、部署springboot应用

创建dockertest.yaml文件

```text
apiVersion: v1
kind: Service
metadata:
  name: dockertest
  namespace: default
  labels:
    app: dockertest
spec:
  type: NodePort
  ports:
    - port: 8080
      nodePort: 30090 #service对外开放端口
  selector:
    app: dockertest
---
apiVersion: apps/v1
kind: Deployment #对象类型
metadata:
  name: dockertest #名称
  labels:
    app: dockertest #标注
spec:
  replicas: 1 #运行容器的副本数，修改这里可以快速修改分布式节点数量
  selector:
    matchLabels:
      app: dockertest
  template:
    metadata:
      labels:
        app: dockertest
    spec:
      containers: #docker容器的配置
        - name: dockertest
          image: a9805943/springboot-log4j2:0.0.1-SNAPSHOT # pull镜像的地址 ip:prot/dir/images:tag
          imagePullPolicy: IfNotPresent #pull镜像时机，
          ports:
            - containerPort: 8080 #容器对外开放端口
```

{% file src="../.gitbook/assets/dockertest \(1\).yaml" %}

执行：

```text
kubectl create -f dockertest.yaml
```

检查dockertest应用状态



```text
kubectl get pod -n kubernetes-dashboard
```

登录[http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/)

解锁更多操作

