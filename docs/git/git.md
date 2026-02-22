# Git Rehberi (Tek Sayfa) — Sıfırdan Başlayanlar + Hızlı Hatırlatma

Bu sayfa, Git’i **en baştan** öğrenmek ve gerektiğinde hızlıca hatırlamak için hazırlanmıştır.
Komutlar “ne zaman kullanılır, ne yapar, nasıl kontrol edilir” şeklinde atlamasız anlatılır.

---

##  Git ne işe yarar? (Amaç)

Git bir **sürüm kontrol sistemi**dir (version control).
- Dosyalarındaki değişiklikleri **kayıt altına alır** (commit).
- “Kim, neyi, ne zaman değiştirdi?” sorusunu cevaplar.
- Hata olursa **geri dönmeyi** kolaylaştırır.
- Ekip çalışmasını düzenler (branch + merge + pull request).

> Kısa benzetme: Git = Projenin “zaman makinesi”.

---

##  Kurulum kontrolü

Git var mı?
```bash
git --version

```

Git kurulu değilse:
- macOS: `brew install git`
- Ubuntu/Debian: `sudo apt install git`
- Windows: https://git-scm.com üzerinden indir

---

## Git Kimlik Ayarı (İlk kez şart)

Git commit oluştururken kim tarafından yapıldığını bilmek ister.

### İsim ve e-posta ayarla

```bash
git config --global user.name "Ad Soyad"
git config --global user.email "mail@ornek.com"
```

### Kontrol et

```bash
git config --global --list
```

> `--global` parametresi bu ayarın tüm projelerde geçerli olmasını sağlar.

---

# Git: Versiyon Kontrol Sistemi Rehberi

Git, projelerinizdeki değişiklikleri takip etmenizi, eski sürümlere dönmenizi ve ekip arkadaşlarınızla koordineli çalışmanızı sağlayan dağıtık bir versiyon kontrol sistemidir.



## 1. Başlangıç ve Yapılandırma
Yeni bir projeye başlarken veya kimlik bilgilerini ayarlarken kullanılır.

* `git init`: Bulunduğunuz klasörü bir Git deposu (repository) haline getirir.
* `git clone <url>`: Uzaktaki bir depoyu bilgisayarınıza kopyalar.
* `git config --global user.name "Adınız"`: Commit'lerde görünecek isminizi ayarlar.
* `git config --global user.email "email@adresiniz.com"`: Email adresinizi ayarlar.

## 2. Temel Çalışma Döngüsü
Değişiklikleri kaydetmek için en çok kullanılan komutlardır.

* `git status`: Değiştirilmiş, eklenmiş veya takip edilmeyen dosyaların durumunu gösterir.
* `git add <dosya-adı>`: Belirli bir dosyayı "staging area"ya (hazırlık alanı) ekler.
* `git add .`: Tüm değişiklikleri hazırlık alanına ekler.
* `git commit -m "mesaj"`: Hazırlık alanındaki değişiklikleri kalıcı olarak kaydeder.
* `git diff`: Henüz stage edilmemiş değişiklikleri gösterir.

## 3. Dallanma (Branching) ve Birleştirme
Farklı özellikler üzerinde çalışırken projeyi bölmek için kullanılır.

* `git branch`: Mevcut dalları listeler.
* `git branch <dal-adı>`: Yeni bir dal oluşturur.
* `git checkout <dal-adı>`: Belirtilen dala geçiş yapar.
* `git switch -c <dal-adı>`: Yeni bir dal oluşturur ve anında o dala geçer.
* `git merge <dal-adı>`: Belirtilen dalı, üzerinde bulunduğunuz dalla birleştirir.
* `git branch -d <dal-adı>`: Belirtilen dalı siler.

## 4. Uzak Depo (Remote) İşlemleri
GitHub, GitLab veya Bitbucket gibi platformlarla iletişim kurmak için kullanılır.

* `git remote add origin <url>`: Yerel depoyu uzak bir sunucuya bağlar.
* `git push origin <dal-adı>`: Yerel commit'leri uzak depoya gönderir.
* `git pull`: Uzak depodaki değişiklikleri çeker ve yerel kodla birleştirir.
* `git fetch`: Değişiklikleri kontrol eder ama birleştirme (merge) yapmaz.

## 5. Değişiklikleri Geri Alma ve Geçmiş
Hataları düzeltmek veya geçmişe bakmak için kullanılır.

* `git log`: Commit geçmişini listeler.
* `git log --oneline`: Geçmişi özet halinde tek satırda gösterir.
* `git reset --hard <commit-hash>`: Projeyi belirtilen commit noktasına geri döndürür (DİKKAT: Sonraki tüm değişiklikler silinir).
* `git revert <commit-hash>`: Belirli bir commit'in tersini alarak yeni bir düzeltme commit'i oluşturur.
* `git stash`: Henüz commit'lenmemiş değişiklikleri geçici olarak kenara kaldırır (çalışma alanını temizler).
* `git stash pop`: Kenara kaldırılan değişiklikleri geri getirir.


