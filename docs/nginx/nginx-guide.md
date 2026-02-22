# Nginx: Web Sunucusu ve Reverse Proxy Rehberi

Nginx (Engine-X), yüksek performanslı, düşük hafıza tüketimli ve olay tabanlı (event-driven) bir sunucu yazılımıdır. Modern web mimarilerinde trafiği yöneten en kritik araçlardan biridir.



---

## 1. Nginx Ne İşe Yarar? (Temel Görevler)

Nginx'in kullanılmasının temel nedenleri şunlardır:

* **Yüksek Performanslı Web Sunucusu:** HTML, CSS, JS ve görseller gibi statik dosyaları rakiplerine göre çok daha hızlı sunar.
* **Reverse Proxy (Ters Vekil):** Kullanıcıdan gelen istekleri karşılar ve arka planda çalışan (Node.js, Go, Python, Docker) uygulamalara güvenli bir şekilde iletir.
* **Load Balancer (Yük Dengeleyici):** Yoğun trafiği birden fazla sunucuya dağıtarak sistemin çökmesini önler ve süreklilik sağlar.
* **SSL/TLS Sonlandırma:** HTTPS sertifikalarını merkezi olarak yöneterek trafiği şifreler.
* **Önbellekleme (Caching):** Sık erişilen içerikleri belleğe alarak uygulama sunucusunun yükünü hafifletir.

---

## 2. Kurulum ve Dosya Yapısı

### Kurulum (Ubuntu/Debian)
```bash
sudo apt update && sudo apt install nginx
sudo systemctl start nginx
sudo systemctl enable nginx


