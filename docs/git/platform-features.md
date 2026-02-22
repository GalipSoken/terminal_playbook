# GitHub, GitLab ve Bitbucket: Gelişmiş Özellikler Rehberi

Modern kod depolama platformları sadece kod saklamak için değil, projenin tüm yaşam döngüsünü (geliştirme, test, güvenlik ve yayınlama) yönetmek için tasarlanmıştır.

## 1. Kod İnceleme ve İşbirliği (Pull/Merge Request)
Geliştirdiğiniz kodu ana dala (main) eklemeden önce diğer ekip üyelerinin incelemesi ve onaylaması sürecidir.

* **GitHub (Pull Request - PR):** Kodun üzerinden satır satır yorum yapılmasını ve değişiklik talep edilmesini sağlar.
* **GitLab (Merge Request - MR):** GitHub'daki PR ile aynı işlevi görür; kodun birleştirilmeden önceki son kontrol noktasıdır.
* **Bitbucket (Pull Request):** Jira ile tam entegre çalışarak hangi kodun hangi iş göreviyle (task) ilgili olduğunu gösterir.

## 2. Otomasyon ve CI/CD (Actions / Pipelines)
Kod her değiştiğinde otomatik olarak testlerin çalışması ve uygulamanın sunucuya yüklenmesi işlemidir.

* **GitHub Actions:** `.github/workflows` klasöründeki YAML dosyalarıyla yönetilir. Binlerce hazır otomasyon şablonu sunar.
* **GitLab CI/CD:** `.gitlab-ci.yml` dosyasıyla çalışır. Sektördeki en güçlü ve yerleşik otomasyon araçlarından biridir.
* **Bitbucket Pipelines:** `bitbucket-pipelines.yml` üzerinden bulut tabanlı test ve dağıtım imkanı sağlar.

## 3. Ajanlar ve İş Yürütücüler (Runners / Agents)
Otomasyon komutlarının (Actions/Pipelines) üzerinde çalıştığı gerçek veya sanal makinelerdir.

* **GitHub Runners:** Kodunuzu GitHub'ın kendi sunucularında veya kendi bağladığınız özel sunucularda (Self-hosted) çalıştırır.
* **GitLab Runners:** Kendi sunucunuza kurduğunuz ve GitLab ile haberleşen küçük programcıklardır; kodunuzu bunlar derler.

## 4. Güvenlik ve Uyumluluk (Security)
Kodun içindeki açıkları, sızdırılmış şifreleri ve güncel olmayan kütüphaneleri otomatik olarak tarar.

* **GitHub Security & Dependabot:** **Dependabot**, eskiyen paketleri bulur ve otomatik güncelleme isteği açar. **Secret Scanning**, kodun içinde unutulan API anahtarlarını yakalar.
* **GitLab Security:** Kod kalitesi analizi (SAST/DAST) ve konteyner taramasını standart olarak sunar.

## 5. İstatistikler ve Analiz (Insights)
Projenin ne kadar hızlı ilerlediğini ve ekibin performansını ölçen panellerdir.

* **GitHub Insights:** Commit sıklığı, en çok katkı verenler ve bağımlılık grafiklerini görselleştirir.
* **GitLab Value Stream Analytics:** Bir özelliğin fikir aşamasından yayına alınana kadar geçen süreyi ölçerek darboğazları tespit eder.

## 6. Dokümantasyon (Wiki)
Projenin kurulumu, teknik mimarisi ve kurallarını yazmak için kullanılan, koddan bağımsız bir ansiklopedi alanıdır.

---

### Platform Karşılaştırma Özeti

| Özellik | GitHub | GitLab | Bitbucket |
| :--- | :--- | :--- | :--- |
| **Kod İnceleme** | Pull Request (PR) | Merge Request (MR) | Pull Request (PR) |
| **Otomasyon** | Actions | CI/CD Pipelines | Pipelines |
| **İş Yürütücü** | GitHub Runner | GitLab Runner | Bitbucket Runner |
| **Güvenlik** | Dependabot / Scanning | Security Compliance | Snyk Entegrasyonu |
| **Analiz** | Insights | Analytics | Reports |

---

