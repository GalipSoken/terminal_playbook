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

## 4. Temel Docker Komutları

### İmaj ve Konteyner Yönetimi
* `docker pull <imaj>`: İmajı indirir.
* `docker images`: Yüklü imajları listeler.
* `docker run -d --name <ad> -p 8080:80 <imaj>`: Konteyneri arka planda, port yönlendirmesiyle çalıştırır.
* `docker ps`: Çalışan konteynerleri listeler.
* `docker logs -f <ad>`: Konteyner çıktılarını canlı izler.
* `docker exec -it <ad> bash`: Konteynerin içine terminalle girer.

### Volume Komutları
* `docker volume ls`: Mevcut tüm volume alanlarını listeler.
* `docker volume create <ad>`: Yeni bir kalıcı veri alanı oluşturur.
* `docker volume inspect <ad>`: Verinin bilgisayarınızda fiziksel olarak nerede tutulduğunu gösterir.
* `docker volume prune`: Kullanılmayan tüm volume alanlarını temizler (Dikkat!).

---

## 5. Önemli Servislerin Docker Kurulum Avantajları
* **Postgres:** Bilgisayarınıza kurulum yapmadan, farklı versiyonlarda (v13, v15) veritabanlarını saniyeler içinde açıp kapatabilirsiniz.
* **Nginx:** Statik dosyalarınızı bir volume ile bağlayıp saniyeler içinde bir web sunucusu yayına alabilirsiniz.
* **Airflow:** Kurulumu en zor araçlardan biridir; Docker ile tüm veritabanı ve kuyruk (worker) bağımlılıklarıyla hatasız ayağa kalkar.
