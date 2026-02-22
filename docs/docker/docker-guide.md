# Docker: Konteyner Teknolojisi Rehberi

Docker, uygulamalarınızı ve onların ihtiyaç duyduğu tüm bağımlılıkları bir araya getirerek her ortamda aynı şekilde çalışmasını sağlayan bir platformdur.



## 1. Docker Neden Önemlidir? (Faydaları)
* **"Benim bilgisayarımda çalışıyor" sorununa son:** Geliştirme ve canlı ortam (prod) birebir aynı olur.
* **Hafiflik:** Sanal makinelerin (VM) aksine işletim sistemi çekirdeğini paylaşır, çok hızlı açılır.
* **Hızlı Kurulum:** Postgres, Redis, Airflow gibi karmaşık araçları tek komutla kurarsınız.

---

## 2. Docker Bileşenleri (Anatomi)
1. **Docker Engine:** Docker'ın üzerinde çalıştığı ana motor.
2. **Dockerfile:** İmaj oluşturmak için kullanılan "yemek tarifi" dosyasıdır.
3. **Image (İmaj):** Uygulamanın çalışması için gereken her şeyin dondurulmuş halidir.
4. **Container (Konteyner):** İmajın çalışan canlı örneğidir.
5. **Docker Hub:** İmajların paylaşıldığı "GitHub benzeri" depo.
6. **Docker Compose:** Çoklu konteynerleri tek dosyadan yönetme aracı.
7. **Volume:** Konteyner içindeki verilerin kalıcı olmasını sağlayan depo alanıdır.

---

## 3. Veri Yönetimi: Volumes (Kalıcılık)
Docker konteynerleri doğası gereği "geçicidir" (ephemeral). Konteyner silindiğinde içindeki kodlar ve veriler de uçar. Veriyi kurtarmak için iki yöntem kullanılır:



### A. Named Volumes (Önerilen)
Veri, Docker tarafından yönetilen özel bir klasörde tutulur. Veritabanları için en güvenli yoldur.
* `docker run -v veritabani_verisi:/var/lib/postgresql/data postgres`
  - *Açıklama:* Konteyner silinse bile `veritabani_verisi` isimli alan kalır, yeni konteyner buna bağlanabilir.

### B. Bind Mounts
Bilgisayarınızdaki (host) fiziksel bir klasörü direkt konteynere bağlar. Kod geliştirirken (development) kodların anında güncellenmesi için kullanılır.
* `docker run -v $(pwd)/kodlar:/app nginx`
  - *Açıklama:* Bilgisayarındaki `kodlar` klasöründe yaptığın her değişiklik anında Nginx içinde görünür.

---

# Docker Komutları

## 1. Temel Seviye: Yaşam Döngüsü Yönetimi
Yeni başlayanlar ve günlük rutin işlemler için temel komutlardır.

* `docker run -d --name web-sunucu -p 8080:80 nginx`
  - **Açıklama:** Belirtilen imajı arka planda (-d) çalıştırır, isim verir ve port yönlendirmesi yapar.
* `docker ps`
  - **Açıklama:** Sadece o an aktif olan (çalışan) konteynerleri listeler.
* `docker ps -a`
  - **Açıklama:** Durmuş, hata almış veya çalışan tüm konteyner geçmişini gösterir.
* `docker stop <id/ad>`
  - **Açıklama:** Çalışan bir konteyneri güvenli bir şekilde durdurur.
* `docker start <id/ad>`
  - **Açıklama:** Daha önce durdurulmuş bir konteyneri tekrar başlatır.
* `docker rm <id/ad>`
  - **Açıklama:** Durdurulmuş bir konteyneri sistemden tamamen siler.
* `docker images`
  - **Açıklama:** Bilgisayarınızdaki tüm indirilmiş veya oluşturulmuş imajları listeler.
* `docker rmi <imaj_id>`
  - **Açıklama:** Artık ihtiyacınız olmayan bir imajı siler.

## 2. Orta Seviye: Hata Ayıklama ve İzleme
Uygulamada bir sorun olduğunda veya konteynerin içine müdahale etmek gerektiğinde kullanılır.

* `docker logs -f <ad>`
  - **Açıklama:** Konteynerin ürettiği logları canlı olarak terminale basar. Hata tespiti için ilk bakılacak yerdir.
* `docker exec -it <ad> /bin/bash` (veya `/bin/sh`)
  - **Açıklama:** Çalışan bir konteynerin içine interaktif bir terminal ile girmenizi sağlar. İçerideki dosya yapısını görmenize yarar.
* `docker inspect <ad>`
  - **Açıklama:** Konteynerin IP adresi, imaj detayları ve ağ ayarları gibi tüm teknik bilgilerini JSON formatında verir.
* `docker stats`
  - **Açıklama:** Çalışan tüm konteynerlerin CPU, RAM ve internet kullanımını canlı olarak bir panel şeklinde gösterir.
* `docker cp <yerel_yol> <ad>:/konteyner_yolu`
  - **Açıklama:** Bilgisayarınızdan konteynere (veya tam tersi) dosya transfer etmek için kullanılır.
* `docker top <ad>`
  - **Açıklama:** Konteyner içerisinde çalışan işlem (process) listesini gösterir.

## 3. İleri Seviye: Sistem Optimizasyonu ve Gelişmiş Yönetim
Disk alanını yönetmek, imaj oluşturmak ve gelişmiş ağ/volume işlemleri içindir.

* `docker system prune`
  - **Açıklama:** Kullanılmayan tüm durmuş konteynerleri, ağları ve askıda kalmış (dangling) imajları siler. Disk alanı açmak için hayat kurtarır.
* `docker build -t kullanıcı_adı/proje:v1 .`
  - **Açıklama:** Bulunulan klasördeki `Dockerfile` dosyasını kullanarak yeni bir imaj inşa eder ve etiketler.
* `docker history <imaj_adı>`
  - **Açıklama:** Bir imajın hangi katmanlardan oluştuğunu ve her katmanın ne kadar yer kapladığını gösterir.
* `docker network ls` & `docker network inspect <ad>`
  - **Açıklama:** Docker üzerindeki sanal ağları yönetmenizi ve konteynerlerin birbirine nasıl bağlı olduğunu görmenizi sağlar.
* `docker volume ls` & `docker volume prune`
  - **Açıklama:** Kalıcı veri alanlarını listeler ve kullanılmayan veritabanı artıklarını temizler.
* `docker commit <konteyner_id> yeni_imaj_adı`
  - **Açıklama:** Çalışan bir konteynerin o anki halini dondurarak yeni bir imaj haline getirir.
* `docker system df`
  - **Açıklama:** Docker'ın disk üzerindeki toplam yükünü; imaj, konteyner ve volume bazlı özetler.



---

## 5. Önemli Servislerin Docker Kurulum Avantajları
* **Postgres:** Bilgisayarınıza kurulum yapmadan, farklı versiyonlarda (v13, v15) veritabanlarını saniyeler içinde açıp kapatabilirsiniz.
* **Nginx:** Statik dosyalarınızı bir volume ile bağlayıp saniyeler içinde bir web sunucusu yayına alabilirsiniz.
* **Airflow:** Kurulumu en zor araçlardan biridir; Docker ile tüm veritabanı ve kuyruk (worker) bağımlılıklarıyla hatasız ayağa kalkar.
