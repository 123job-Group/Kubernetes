<div align="center">
  <img src="https://123job.vn/images/logo/logo349x137tim.png" width="400">
</div>

<div align="center">
    <a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</div>

## Introduce

Hướng dẫn cài đặt Kubernetes trên nhiều Node.

## Install

**b1:**

```
sudo apt-get upadte
sudo apt-get install vagrant
vagrant version
vagrant init	    Sinh file cấu hình máy ảo mới Vagrantfile
vagrant up	        Thực hiện tạo / hoặc chạy máy ảo với cấu hình từ Vagrantfile
vagrant             ssh	Kết nối ssh vào máy ảo, tài khoản kết nối là vagrant
vagrant halt	    Dừng máy ảo (shutdown)
vagrant reload	    Khởi động lại máy ảo, có đọc lại cấu hình trong Vagrantfile
vagrant destroy	    Xóa máy ảo
```

**b2:**

```
//cd master
vagrant up

//cd worker1
vagrant up

//cd worker2
vagrant up
```

**b3:**
```
ssh root@192.168.10.100
```

**b4:**

```
kubeadm init --apiserver-advertise-address=192.168.10.100 --pod-network-cidr=192.168.0.0/16

//Plugin network
//Xem chi tiết tại: https://kubernetes.io/docs/concepts/cluster-administration/addons/
kubectl apply -f https://docs.projectcalico.org/v3.10/manifests/calico.yaml
```

**b5:**

```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

**b6: Get token ở máy master để  các máy worker gia nhập**

```
kubeadm token create --print-join-command
```

**b7: Get node**

```
kubectl get nodes
```

**b8: Xem thông tin chi tiết máy master**

```
kubectl describe node master.xtl
```

**Merge các config nếu có nhiều cluster**
```
cd ~
mkdir .kube
kubectl cluster-info
scp root@172.16.10.100:/etc/kubernetes/admin.conf ~/.kube/config-mycluster
export KUBECONFIG=~/.kube/config:~/.kube/config-mycluster
kubectl config view --flatten > ~/.kube/config_temp
mv ~/.kube/config_temp ~/.kube/config
```

**Xem config**

```
kubectl config view
kubectl config get-contexts
kubectl config use-context kubernetes-admin@kubernetes
```