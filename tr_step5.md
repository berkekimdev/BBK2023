![Jaeger](https://logowik.com/content/uploads/images/jaeger2618.logowik.com.webp)

# Jaeger Kurulumu İle Hata Ayıklama


Jaeger, bir izleme ve dağıtılmış sistemlerde hata ayıklama (troubleshooting) aracıdır. Özellikle mikroservis mimarileri gibi karmaşık ve dağıtık sistemlerin performansını izlemek ve anlamak için kullanılır. Jaeger, OpenTracing standardını destekler ve izlenebilirlik (observability) sağlar.

#### İşte Jaeger'ın temel özellikleri ve görevleri:

* İzlenebilirlik Sağlama: Jaeger, uygulamaların içinde ve arasında giden istekleri, işlemleri ve bağımlılıkları takip eder. Bu sayede, bir uygulamanın performansını ve hata noktalarını belirlemek daha kolay hale gelir.

* Dağıtık Hata Ayıklama: Dağıtık sistemlerde, bir hata birçok farklı bileşen arasında ortaya çıkabilir. Jaeger, bu hataların kaynağını belirlemek ve takip etmek için kullanılabilir. Hatalı bir işlemin izini sürmek, sistemdeki sorunları daha hızlı tespit etmeyi sağlar.

* Performans Analizi: Jaeger, bir uygulamanın farklı bileşenlerindeki performans sorunlarını belirleyebilir. Bu sayede, uygulamanın hangi bölümlerinin iyileştirilmesi gerektiğini anlamak mümkün olur.

* Bağlam Geçişi (Context Propagation): Jaeger, izleme bilgilerini farklı mikroservisler arasında iletebilir. Bu sayede, bir isteğin sistemin farklı bileşenlerine nasıl yayıldığını ve işlendiğini anlamak mümkün olur.

* Analiz ve Raporlama: Jaeger, izleme verilerini analiz ederek raporlar oluşturabilir. Bu raporlar, sistemdeki genel performansı ve işlemleri daha iyi anlamanıza yardımcı olabilir.

* Jaeger, Prometheus gibi diğer izleme araçlarıyla birlikte kullanılabilir. Her aracın kendine özgü avantajları ve odaklandığı alanlar vardır. Jaeger, genellikle dağıtık sistemlerdeki karmaşıklığı ele almak için tercih edilirken, Prometheus daha çok metrikler ve zaman serileri üzerinde odaklanır. Bu araçları birleştirerek daha kapsamlı bir izleme ve hata ayıklama stratejisi oluşturmak mümkündür.

# Jaeger Kurulumu

* İlk olarak Docker kurulu değilse kurmalıyız.
```
apt-get update
apt-get install -y docker.io
systemctl start docker
```

* Jaeger Docker Görüntüsünü Çekin:

Terminal veya Komut İstemcisine şu komutu yazarak resmi Jaeger Docker görüntüsünü çekebilirsiniz:

``` 
docker run -d --name jaeger -p 8080:16686 -p 9411:9411 jaegertracing/all-in-one:latest
```

* 8080 portuna baktığınızda bir arayüz karşılar.
![Jaeger](https://github.com/berkekimdev/bbturktelekom/blob/main/jaeger.PNG?raw=true) 

## Jaeger'ı nasıl test edebiliriz?
### Jaeger ve HotROD örneği, mikro hizmet mimarisindeki uygulamaların ve servislerin izlenmesi ve analiz edilmesi için kullanılan bir senaryoyu temsil eder. Bu senaryo şu amaçları taşır:

# HotROD Kurulumu

```
docker run -d --name jaeger-hotrod -p 8081:8080 jaegertracing/example-hotrod:latest
```
* 8081 portuna baktığımızda bir arayüz karşılar.
* Burda test yapabileceğimiz  istekler vardır ve response timeları görebiliriz.

![HotPOD](https://github.com/berkekimdev/bbturktelekom/blob/main/hotrod.PNG?raw=true)

* Bunları aynı zamanda Jaeger üzerinden de takip ediyoruz.

![Jaeger](https://github.com/berkekimdev/bbturktelekom/blob/main/jaeger2.PNG?raw=true)










