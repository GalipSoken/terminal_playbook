# Docker: Konteyner Teknolojisi Rehberi

Docker, uygulamalarınızı ve onların ihtiyaç duyduğu tüm bağımlılıkları (kütüphaneler, ayarlar, veritabanları) bir araya getirerek her ortamda aynı şekilde çalışmasını sağlayan bir platformdur.



## 1. Docker Neden Önemlidir? (Faydaları)
Geleneksel sanal makinelerin (VM) aksine Docker, işletim sistemi çekirdeğini paylaşır. Bu da onu çok daha hafif, hızlı ve verimli kılar.

* **"Benim bilgisayarımda çalışıyor" sorununa son:** Geliştirme ortamınız ile sunucu ortamınız birebir aynı olur.
* **İzolasyon:** Aynı sunucuda birbirinden bağımsız onlarca servis çalıştırabilirsiniz.
* **Hızlı Kurulum:** Karmaşık sistemleri (Postgres, Airflow vb.) dakikalar içinde ayağa kaldırabilirsiniz.

### Örnek Senaryolar:
* **Postgres:** Bilgisayarınıza veritabanı kurup sisteminizi kirletmek yerine, tek komutla izole bir Postgres çalıştırıp işiniz bitince silebilirsiniz.
* **Nginx:** Karmaşık konfigürasyonlarla uğraşmadan hazır bir web sunucusunu anında yayına alabilirsiniz.
* **Airflow:** Bağımlılıkları çok fazla olan bu aracı Docker ile tüm bileşenleriyle (Scheduler, Worker, Webserver) tek tıkla kurabilirsiniz.

---

## 2. Docker Bileşenleri (Anatomi)

1. **Docker Engine:** Docker'ın üzerinde çalıştığı ana motor.
2. **Dockerfile:** Bir imajın nasıl oluşturulacağını tarif eden "yemek tarifi" dosyasıdır.
3. **Image (İmaj):** Uygulamanın çalışması için gereken her şeyin paketlenmiş, değiştirilemez halidir (Sınıf/Blueprint).
4. **Container (Konteyner):** İmajın çalışan canlı örneğidir (Nesne/Instance).
5. **Docker Hub:** İmajların paylaşıldığı bulut tabanlı bir depodur (Docker'ın GitHub'ı).
6. **Docker Compose:** Birden fazla konteyneri (örneğin: App + DB + Redis) tek bir dosyadan yönetmeye yarayan araçtır.

---

## 3. Kurulum (Hızlı Bakış)

* **macOS & Windows:** [Docker Desktop](https://www.docker.com/products/docker-desktop/) indirip kurmanız yeterlidir.
* **Linux (Ubuntu):** ```bash
  sudo apt update && sudo apt install docker.io
  sudo systemctl start docker
  sudo systemctl enable docker


# Docker Komut Rehberi: Temel, Orta ve İleri Seviye

Bu rehber, bir Docker kullanıcısının günlük operasyonlardan sistem optimizasyonuna kadar ihtiyaç duyacağı tüm komutları içerir.



## 1. Temel Seviye (Günlük Kullanım)
Konteynerleri başlatmak, durdurmak ve listelemek için kullanılır.

* `docker run -d --name app1 nginx`
  - **Açıklama:** 'app1' adında bir Nginx konteynerini arka planda (detached) çalıştırır.
* `docker ps`
  - **Açıklama:** Sadece o an çalışan konteynerleri listeler.
* `docker ps -a`
  - **Açıklama:** Durmuş olanlar dahil tüm konteyner geçmişini gösterir.
* `docker stop <id/ad>`
  - **Açıklama:** Çalışan bir konteyneri nazikçe durdurur.
* `docker rm <id/ad>`
  - **Açıklama:** Durdurulmuş bir konteyneri sistemden tamamen siler.
* `docker images`
  - **Açıklama:** Bilgisayarınıza indirilmiş tüm imajları listeler.
* `docker rmi <image_id>`
  - **Açıklama:** Bir imajı sistemden siler.

## 2. Orta Seviye (Hata Ayıklama ve Yönetim)
Konteynerlerin içine girmek, logları okumak ve kaynak yönetimini kontrol etmek için kullanılır.

* `docker logs -f <ad>`
  - **Açıklama:** Konteynerin çıktılarını (log) canlı olarak takip eder.
* `docker exec -it <ad> /bin/bash`
  - **Açıklama:** Çalışan bir konteynerin içine interaktif bir terminal ile bağlanır.
* `docker inspect <ad>`
  - **Açıklama:** Konteyner veya imaj hakkında tüm teknik detayları (IP adresi, mount noktaları vb.) JSON formatında verir.
* `docker stats`
  - **Açıklama:** Tüm çalışan konteynerlerin CPU, RAM ve Network kullanımını canlı gösterir.
* `docker cp <dosya_yolu> <ad>:/hedef_yol`
  - **Açıklama:** Bilgisayarınızdan konteynerin içine (veya tersi) dosya kopyalar.
* `docker network ls`
  - **Açıklama:** Docker üzerindeki sanal ağları listeler.



## 3. İleri Seviye (Sistem Temizliği ve Optimizasyon)
Disk alanını geri kazanmak, imaj oluşturmak ve gelişmiş yönetim işlemleri içindir.

* `docker system prune`
  - **Açıklama:** Kullanılmayan tüm durmuş konteynerleri, ağları ve "dangling" (askıda kalmış) imajları silerek disk alanı boşaltır.
* `docker system prune -a --volumes`
  - **Açıklama:** (DİKKAT) Kullanılmayan tüm imajları ve verileri (volume) tamamen siler.
* `docker build -t kullanıcı_adı/uygulama:v1 .`
  - **Açıklama:** Bulunulan klasördeki `Dockerfile` dosyasını kullanarak bir imaj oluşturur ve etiketler.
* `docker history <imaj_adı>`
  - **Açıklama:** Bir imajın hangi katmanlardan (layer) oluştuğunu ve boyutlarını gösterir.
* `docker volume ls`
  - **Açıklama:** Docker tarafından yönetilen tüm kalıcı veri alanlarını (volumes) listeler.
* `docker commit <konteyner_id> yeni_imaj_adı`
  - **Açıklama:** Çalışan bir konteynerin o anki halinden yeni bir imaj oluşturur.
* `docker system df`
  - **Açıklama:** Docker'ın disk üzerinde ne kadar yer kapladığını (imaj, konteyner, volume bazlı) özetler.

---

## Özet İpucu: Hangi Durumda Hangisi?
- **Konteyner hata veriyorsa:** `docker logs`
- **İçinde ne var bakmak istiyorsan:** `docker exec`
- **Disk dolduysa:** `docker system prune`
- **IP adresini öğrenmek istiyorsan:** `docker inspect`
