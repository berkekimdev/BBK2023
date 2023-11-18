# Script Kullanarak Yeni Sanal Makineye Geçişte Eski Paketlere ve Ayarlara Dönüş

## Amacımız Nedir?

Bulut Bilişimciler sitesinde belirli bir kursta bir senaryodan diğer senaryoya geçerken yeni bir sanal makine ayağa kaldırılıyor. Bu ayağa kaldırılan sanal makine önceden yaptığımız işlemleri bilmiyor ve makine ayağa sıfırdan kaldırılmış oluyor. Kullanıcılar olarak bir senaryodan diğer senaryoya geçişte bütün yaptığımız işlemleri baştan sona yapmak durumundayız. Bu işlemlerimizi hem zorlaştırıyor hemde büyük zaman kaybına yol açıyor. Bunun yanında misal Docker kursunun 3. senaryosunu bitiren öğrenci  bir hafta ara verip 4. senaryoya geçmek istediğinde eski ayarlarını ve yüklediği paketleri hatırlayamacak olup kaldığı yerden devam edemeyecek. Amacımız bir script yazarak eski makinede olan paketleri ve ayarları diğer makineye haftalar geçse bile taşıyabilmek.

- İlk olarak kullanıcı belirli bir formatta sunucuyu kapamadan önce history bilgilerini bir txt dosyasına aktarmalı.
- Sonra bu oluşturduğu dosyayı github reposuna yüklemeli veya kendi bilgisayarında bu komutları saklayabilir. Bu adımda kullanıcıya Git hatırlatmaları yapılmak zorunda. (Bulut Bilişimciler sitesine bu dosyaları saklamak için bir alan yapılabilir ve işlem çok daha hızlanır.)
- Diğer sunucuya geçtikten sonra kullanıcı github reposundan dosyasını çeker.
- Açılan VM'e eklenmiş olan myscript.sh dosyasının olduğu path'e dosyayı atar ve myscript.sh'ı çalıştırır.
- Bash script dosyamız kullanıcıya baştan sonra önceden indirdiği her paketi ve yazdığı her komutu tek tek yüklemek ister misin diye sorar.
- Kullanıcı eğer hatalı bir komut girmişse kullanıcıya bu komut hatalı ve düzeltmek ister misin diye sorar. Kullanıcı "Y" tuşuna basarsa konsol girdisi ister. Konsol girdisini girdikten sonra kullanıcıya bu komutu çalıştırmak ister misin diye yine sorar.



