![Grafana-](https://logowik.com/content/uploads/images/grafana3182.jpg)

# HELM Kullanarak Grafana Kurma

Grafana'yı Helm ile kurmak için kullanacağınız komut
```
helm repo add grafana https://grafana.github.io/helm-charts
helm install grafanatest grafana/grafana
```

Grafana'yı kurduktan sonra giriş yapabilmek için şifresine ihtiyacımız olacak.

```
kubectl get secret --namespace default grafanatest -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```
Burdan gelen şifreyi saklayınız.

# Grafana'ya bağlanma

### İlk olarak Grafana'yı dış dünyaya açmalısınız.

```
kubectl expose service grafanatest --type=NodePort --target-port=3000 --name=grafana-ext
```
Diyerek kubernetes portunu oluşturun.

## Giriş yapma

* user : admin password : sakladığınız şifre olacak şekilde giriş yapınız.

![UI](https://github.com/berkekimdev/bbturktelekom/blob/main/grafana1.PNG?raw=true)

Sonra sırayla Menu Icon > Connections > Data Source > Prometheus > dedikten sonra kaynak adres olarak kubectl get svc dedikten sonra gelen oluşturduğumuz ip ve portu yazıyoruz.

Örnek vermek gerekirse : 
```
prometheus-server-ext                      NodePort    10.43.26.251    <none>        80:30596/TCP
 ```

 ![Grafana](https://github.com/berkekimdev/bbturktelekom/blob/main/http.PNG?raw=true)
 Bu aralığa ```http://10.43.26.251:80``` gibi sizde hangi ip ve port çıktıysa yazıyorsunuz. 

 Artık Prometheus metricleriniz Grafana'ya bağlanmış oldu.

![Grafana](https://github.com/berkekimdev/bbturktelekom/blob/main/saved.PNG?raw=true)

Çekilen verileri istediğiniz şekilde sql sorgularıyla filtreliyebilirsiniz veya grafana dashboard diye internette sorgulayıp bulduğunuz bir hazır filtre ve grafiği import edebilirsiniz. Biz burda 1860 id'li dashboardu import ediyoruz.

![Grafana](https://github.com/berkekimdev/bbturktelekom/blob/main/grafana2.PNG?raw=true)

Gördüğünüz gibi verileri görebiliyoruz. İstediğimiz gibi saatsel olarak durumları inceleyebilir, kendi sorgularımızı yazabiliriz.









