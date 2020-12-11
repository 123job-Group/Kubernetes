<div align="center">
  <img src="https://123job.vn/images/logo/logo349x137tim.png" width="400">
</div>

<div align="center">
    <a href="https://packagist.org/packages/laravel/framework"><img src="https://poser.pugx.org/laravel/framework/license.svg" alt="License"></a>
</div>

## Introduce

Hướng dẫn sử dụng công nghệ K9S và thực hành về Pod.

## Install

**1. K9S**

* Cài đặt trên macOS - sử dụng brew macos

    ```
    brew install derailed/k9s/k9s
    ```
  
* Cài đặt trên Ubuntu với snap 

    ```
    # cài snap nếu chưa có (bản Ubutu mới có sẵn)
    sudo apt update
    sudo apt install snapd
    
    # cài k9s
    sudo snap install k9s
    Cài đạt K9S trên Windows
    ```

* Đối với Windows, bạn vào [ K9s Release](https://github.com/derailed/k9s/releases), chọn mục Assert. Có thể giải nén copy file chạy vào đường dẫn hệ thống ví vị C:\Windows\system32 để gọi được lệnh bất ở mọi nơi.


- Khi cài đặt xong thì mọi người bật terminal lên và gõ `k9s`
- Nếu lỗi là `Boom!! Unable to locate K8s cluster configuration.` thì mọi 
  người chỉnh lại file ` vi ~/.bashrc ` với những ai không dùng zsh (còn dùng zsh thì chỉnh lại file ` vi ~/.zshrc`) thêm vào `export KUBECONFIG=$HOME/.kube/config` lưu lại và chạy `source ~/.bashrc ` hoặc `source ~/.zshrc`
- Nếu lỗi permission không tạo được thì mọi người ` mkdir  ~/.k9s`

**2. Pod**

```
#Liệt kê các POD trong namespace hiện tại, thêm tham số -o wide hiện thị chi tiết hơn, thêm -A hiện thị tất cả namespace, thêm -n namespacename hiện thị Pod của namespace namespacename
kubectl get pods	

#Xem cấu trúc mẫu định nghĩa POD trong file cấu hình yaml                    
kubectl explain pod --recursive=true	

#Triển khai tạo các tài nguyên định nghĩa trong file firstpod.yaml
kubectl apply -f firstpod.yaml	       

#Xóa các tài nguyên tạo ra từ định nghĩa firstpod.yaml 
kubectl delete -f firstpod.yaml	     

#Lấy thông tin chi tiết POD có tên namepod, nếu POD trong namespace khác mặc định thêm vào tham số -n namespace-name   
kubectl describe pod/namepod	      

#Xem logs của POD có tên podname  
kubectl logs pod/podname	           

#Chạy lệnh từ container của POD có tên mypod, nếu POD có nhiều container thêm vào tham số -c và tên container 
kubectl exec mypod command	        

#Chạy lệnh bash của container trong POD mypod và gắn terminal    
kubectl exec -it mypod bash	    

#Tạo server proxy truy cập đến các tài nguyên của Cluster. http://localhost/api/v1/namespaces/default/pods/mypod:8085/proxy/, truy cập đến container có tên mypod trong namespace mặc định.        
kubectl proxy	

 #Xóa POD có tên mypod                        
kubectl delete pod/mypod

# Liệt kê các pod ở namespace mặc định
kubectl get pods

# Hiện thị nhiều thông tin hơn
kubectl get pod -o wide

# Pod ở namepace: kubernetes-dashboard
kubectl get pod -o wide -n kubernetes-dashboard

# Pod ở tất cả các namespace
kubectl get pod -A

# Liệt kê các Pod có nhãn app: mypod
kubectl get pod -l "app=mypod"

# Xem file yaml của pod
kubectl get pod/mypod -o yaml           
```
 