# Kubernetes, Helm, Prometheus, Grafana ve Jaeger Kullanarak Metricleri İnceleme

![Kubernetes Nodes](https://earthly.dev/blog/assets/images/grafana-and-prometheus-k8s/k8snodes.png)

## Amacımız nedir?
Bu proje, Kubernetes üzerinde uygulama performans izleme ve yönetimi için bir dizi aracı entegre etmeyi amaçlamaktadır. Kullanılan ana araçlar şunlardır:

- **Kubernetes**: Uygulamaların konteyner üzerinde dağıtımını ve yönetimini sağlayan açık kaynaklı bir konteyner orkestrasyon sistemidir.
- **Prometheus**: Kubernetes ortamındaki uygulama performans verilerini toplamak ve analiz etmek için kullanılan bir sistem ve zaman serisi veritabanıdır.
- **Helm**: Kubernetes uygulamalarını paketlemek ve dağıtmak için kullanılan bir paket yöneticisi ve şablonlama aracıdır.
- **Grafana**: Görselleştirmeler ve anlık bildirimlerle Prometheus tarafından toplanan verileri izlemek ve analiz etmek için kullanılan bir açık kaynaklı analitik ve görselleştirme platformudur.
- **Jaeger**: Dağıtılmış sistemlerdeki izleme ve sorunları tespit etme amacıyla kullanılan bir açık kaynaklı, uygulama performansı izleme aracıdır.

Bu araçlar bir araya getirilerek, Kubernetes ortamındaki uygulamaların performansını izlemek, hata ayıklamak ve optimize etmek için kapsamlı bir çözüm sunulmaktadır.

