<div align="center">
  <img src="https://123job.vn/images/logo/logo349x137tim.png" width="400">
</div>

<div align="center">
    <a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</div>

## Introduce

Hướng dẫn cài đặt và sử dụng Kubernetes Dashboard.


## Install

**b1:** 

```
sudo mkdir dashboard
```

``` 
sudo mkdir certs
```

**b2:** 

```
curl https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.5/aio/deploy/recommended.yaml > dashboard-v2.0.5.yaml
```

```
curl https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta6/aio/deploy/recommended.yaml > dashboard-v2-beta6.yaml
```

**b3: Sửa mục kind: Service giống phần bên dưới:**

- cấu hình mặc định của Kubernetes Cluster, cổng được mở ra ngoài phải chọn trong khoảng 30000-32767 sau này bạn có thể sửa cấu hình này với tham số chạy Cluster --service-node-portrange
```
    kind: Service
    apiVersion: v1
    metadata:
      labels:
        k8s-app: kubernetes-dashboard
      name: kubernetes-dashboard
      namespace: kubernetes-dashboard
    spec:
      type: NodePort
      ports:
        - port: 443
          targetPort: 8443
          nodePort: 31000
      selector:
        k8s-app: kubernetes-dashboard
```

**b4: Comment**

```
   # apiVersion: v1
   # kind: Secret
   # metadata:
   #   labels:
   #     k8s-app: kubernetes-dashboard
   #   name: kubernetes-dashboard-certs
   #   namespace: kubernetes-dashboard
   # type: Opaque
```


**b5:**

```
kubectl apply -f dashboard-v2-beta6.yaml
```

**b6:**
```
kubectl get po -n kubernetes-dashboard 
```

**b7: Tự tạo secret**

```
sudo chmod 777 -R certs
#openssl req -nodes -newkey rsa:2048 -keyout certs/dashboard.key -out certs/dashboard.csr -subj "/C=/ST=/L=/O=/OU=/CN=kubernetes-dashboard"
openssl req -nodes -newkey rsa:2048 -keyout certs/dashboard.key -out certs/dashboard.csr -subj "/C=HU/ST=XX/L=Budapest/O=ZSIN/OU=XX/CN=kubernetes-dashboard"
openssl x509 -req -sha256 -days 365 -in certs/dashboard.csr -signkey certs/dashboard.key -out certs/dashboard.crt
sudo chmod -R 777 certs
kubectl create secret generic kubernetes-dashboard-certs --from-file=certs -n kubernetes-dashboard
```

**b8:**

```
kubectl get secret -n kubernetes-dashboard
kubectl describe secret kubernetes-dashboard-certs -n kubernetes-dashboard
```

**b9:**

```
kubectl apply -f admin-user.yaml
kubectl get secret -n kubernetes-dashboard
kubectl describe secret admin-user-token-s2k6f -n kubernetes-dashboard 
```