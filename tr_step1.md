## Kubernetes Kurulumu

![Alt metin](https://miro.medium.com/v2/resize:fit:668/0*p-ztLmQ1DFm5fAH_.png)

# `K3S Kurulumu`
K3S Kubernetes'in IoT cihazları için geliştirdiği bütün API isteklerini destekleyen ancak bazı eklenti ve eklenti API'larından yoksun olan bir versiyonudur. Bu senaryo dahilinde temel Kubernetes Objelerini öğreneceğimiz için K3S'i kullanacağız.

K3S'i kurmak için aşağıdaki komutu çalıştırıyoruz.
```
curl -sfL https://get.k3s.io | sh -
```
10-15 saniye içerisinde kurulum tamamlanacaktır. Tamamlandıktan sonra aşağıdaki komutu çalıştırarak kurulumun başarılı olup olmadığını kontrol edebilirsiniz.

``` 
kubectl get nodes
```
Bu komutun çıktısında Kubernetes Cluster'ımızın tek bir node'dan oluştuğunu göreceksiniz.

Kubernetes ortamımız kurulduğuna göre test edebileceğimiz uygulamaların kurulumuna geçebiliriz.



