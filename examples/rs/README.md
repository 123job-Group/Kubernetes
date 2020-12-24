<div align="center">
  <img src="https://123job.vn/images/logo/logo349x137tim.png" width="400">
</div>

<div align="center">
    <a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</div>

## Introduce

Hướng dẫn sử dụng công nghệ Replicaset.

## Install


**1. Replicaset**

```
#Xem liệt kê các thành phần của kubernetes
watch -n 1 kubectl get all -o wide

#Tạo replicaset
kubectl apply -f 1-rs.yaml

#Get replicaset
kubectl get rs -o wide

#Get replicaset yaml
kubectl get rs -o yaml

#Xem chi tiết replicaset
kubectl describe rs/rsdemo

#Get pod theo label
kubectl get po -l "app=appnode"

#Xem chi tiết pod trong replicaset
kubectl describe po/...

#Xóa pod trong replicaset
kubectl delete po/...

#Xóa replicaset
kubectl delete re rsdemo

#Xóa label
kubectl label pod/rsdemo-854bv app-

#hpa
kubectl apply 2-hpa.yaml
kubectl get hpa -o wide
kubectl describe hpa/rsapp-scaler

```
 