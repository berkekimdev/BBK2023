
![Prometheus](https://res.cloudinary.com/practicaldev/image/fetch/s--WumI56EZ--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/969hxuvi6nfw7zmydlj8.png)
# HELM  Kullanarak Prometheus Kurma

Prometheus'u Helm ile kurmak için, öncelikle Prometheus Helm Charts repos'unu klonlamalısınız. Aşağıdaki komutu kullanarak bu adımı gerçekleştirebilirsiniz:

```
git clone https://github.com/prometheus-community/helm-charts/
```
## Helm ile Prometheus'u kurabilmemiz için Values.yaml ve Chart.yaml dosyalarında bazı değişiklikler yapmamız gerekiyor.


### Chart.yaml içerisinde dependencies bölümünü komple kaldırmalıyız. Kurarken bu bağımlılıklarından kurtulmasını istiyoruz çünkü daha temiz bir kurulum için tek tek kuracağız.
![Charts](https://github.com/berkekimdev/bbturktelekom/blob/main/dependecies.PNG?raw=true)

### Values.yaml içerisinde      node-exporter , kube-metrics , alertmanager ve pushgateway'in enabled: true kısmını false yapmalıyız.
![False](https://github.com/berkekimdev/bbturktelekom/blob/main/false.PNG?raw=true)


### Node-Exporter'ın Values.yaml içerisinde hostRootFsMount: true değerini false yapmalıyız. Bunu yapmazsak hata verecek.

![Node-Exporter](https://github.com/berkekimdev/bbturktelekom/blob/main/nodeexporter.PNG?raw=true)


#### Kurulumlara başlamadan önce k3s.yaml'ını export etmeliyiz.(Her terminal açtığınızda bu komutu çalıştırmalısınız)

```
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
```
# Prometheus Kurulum Aşamaları

# 1- Prometheus Server 

Prometheus Server: Ana Prometheus hizmeti, uygulamaların performans verilerini toplar, depolar ve sorgular. Prometheus, basit ve etkili sorgu dilini kullanarak metrikleri saklar ve analiz eder.

* Kurulum

```
helm install prometheus helm-charts/charts/prometheus/
```

# 2- Node Exporter 
Node Exporter: Prometheus'a hedef olarak hizmet veren her bir node üzerinde çalışan bir istemci uygulamasıdır. Node Exporter, işletim sistemi seviyesinde metrikleri toplar.


```
helm install prometheus helm-charts/charts/prometheus-node-exporter/
```

# 3- Push Gateway
Prometheus Push Gateway: Prometheus'a zıt olarak, metrikleri toplamak ve depolamak için kullanılan bir hizmettir. Bu, Prometheus'un tipik olarak pull modeli ile çalışmasına karşı, özel senaryolarda metrikleri "itme" (push) modeliyle almak istediğiniz durumlar için tasarlanmıştır.
```
helm install prometheusgateway helm-charts/charts/prometheus-pushgateway/
```

# 4- Alert Manager
Alertmanager: Prometheus'tan gelen uyarıları yönetmek ve bu uyarılar için çeşitli eylemler gerçekleştirmek için kullanılır. Örneğin, e-posta gönderme veya Slack kanallarına bildirim gönderme gibi.

 ```
 helm install prometheusalertmanager helm-charts/charts/alertmanager/
 ```

 # 5- Kube State Metrics
kube-state-metrics: Kubernetes cluster'ındaki objelerin durumu hakkında metrikleri toplayan bir Prometheus exporter'ıdır. Bu, Kubernetes kaynaklarının izlenmesini ve analiz edilmesini sağlar.

```
helm install kubemetric helm-charts/charts/kube-state-metrics/
```

# Prometheusa bağlanma

İlk olarak ``` kubectl get svc ``` diyerek açılmış olan pod'ların hangi Cluster ip'lere sahip olduğuna bakalım.

Buna benzer bir çıktı olacak.
```
kubectl get svc
NAME                                       TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes                                 ClusterIP   10.43.0.1       <none>        443/TCP          11m
prometheus-server                          ClusterIP   10.43.243.169   <none>        80/TCP           3m27s
prometheusalertmanager-headless            ClusterIP   None            <none>        9093/TCP         2m48s
prometheusalertmanager                     ClusterIP   10.43.95.204    <none>        9093/TCP         2m48s
prometheus-node-exporter                   ClusterIP   10.43.191.101   <none>        9100/TCP         2m39s
prometheusgateway-prometheus-pushgateway   ClusterIP   10.43.220.128   <none>        9091/TCP         2m3s
kubemetric-kube-state-metrics              ClusterIP   10.43.247.44    <none>        8080/TCP         114s
grafanatest                                ClusterIP   10.43.226.68    <none>        80/TCP           58s

```

Gördüğüz gibi bütün çalışan podlar bir cluster-ip kullanıyor. Bunları dışarı expose ederek erişebiliriz.

```
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-ext
kubectl expose service prometheus-node-exporter --type=NodePort --target-port=9100 --name=prometheus-node
```
Oluşan yeni port ile node-exporter'a ve prometheus server'a bağlanalım.

![Node-Exporter](https://github.com/berkekimdev/bbturktelekom/blob/main/nodeexportermetric.PNG?raw=true)
![Prometheus Server](https://github.com/berkekimdev/bbturktelekom/blob/main/prometheus.PNG?raw=true)

## Bütün aşamaları bitirdik. Şimdi Grafana kurarak elde ettiğimiz metricleri Grafana sayesinde görselleştirelim.



