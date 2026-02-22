# Git Rehberi (Tek Sayfa) — Sıfırdan Başlayanlar + Hızlı Hatırlatma

Bu sayfa, Git’i **en baştan** öğrenmek ve gerektiğinde hızlıca hatırlamak için hazırlanmıştır.
Komutlar “ne zaman kullanılır, ne yapar, nasıl kontrol edilir” şeklinde atlamasız anlatılır.

---

## 0) Git ne işe yarar? (Amaç)

Git bir **sürüm kontrol sistemi**dir (version control).
- Dosyalarındaki değişiklikleri **kayıt altına alır** (commit).
- “Kim, neyi, ne zaman değiştirdi?” sorusunu cevaplar.
- Hata olursa **geri dönmeyi** kolaylaştırır.
- Ekip çalışmasını düzenler (branch + merge + pull request).

> Kısa benzetme: Git = Projenin “zaman makinesi”.

---

## 1) Kurulum kontrolü

Git var mı?
```bash
git --version

```

Git kurulu değilse:
- macOS: `brew install git`
- Ubuntu/Debian: `sudo apt install git`
- Windows: https://git-scm.com üzerinden indir

---

## 2) Git Kimlik Ayarı (İlk kez şart)

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

## 3) Yeni Proje Başlatma (git init)

Yeni bir klasör oluştur:

```bash
mkdir proje-adi
cd proje-adi
```

Git başlat:

```bash
git init
```

Ne yapar?
- Klasörün içine `.git` adında gizli bir klasör oluşturur.
- Bu klasörü Git reposu yapar.

Kontrol:

```bash
ls -a
```

`.git` klasörünü görmelisin.

---

## 4) Var Olan Repo’yu Kopyalama (git clone)

GitHub’daki bir projeyi bilgisayarına indirmek için:

```bash
git clone https://github.com/kullanici/repo-adi.git
```

Ne yapar?
- Repo’yu indirir
- Otomatik olarak `origin` isimli remote bağlantıyı kurar

---

## 5) Günlük Git Akışı (En Önemli 4 Komut)

Bu 4 komut Git kullanımının temelidir:

```bash
git status
git add .
git commit -m "mesaj"
git push
```

---

## 6) git status

```bash
git status
```

Ne gösterir?
- Değiştirilen dosyalar
- Commit’e hazır dosyalar
- Takip edilmeyen dosyalar

Her commit öncesi çalıştırmak iyi alışkanlıktır.

---

## 7) git add

Tüm dosyaları ekle:

```bash
git add .
```

Tek dosya ekle:

```bash
git add dosyaAdi
```

Ne yapar?
- Dosyaları commit listesine (staging area) ekler.

---

## 8) git commit

```bash
git commit -m "Kısa açıklama"
```

Ne yapar?
- Değişiklikleri kalıcı olarak kaydeder.

İyi commit mesajı:
- Kısa
- Ne yaptığını açık anlatan

Örnek:
- `Add docker documentation`
- `Fix nginx config`
- `Update README`

---

## 9) git push

```bash
git push
```

Ne yapar?
- Commit’leri GitHub’a gönderir.

İlk push’ta gerekirse:

```bash
git push -u origin main
```

---

## 10) git pull

```bash
git pull
```

Ne yapar?
- GitHub’daki güncel değişiklikleri indirir
- Mevcut branch’e uygular

---

## 11) Branch (Dal) Kullanımı

Branch, paralel çalışma alanıdır.

Branch’leri listele:

```bash
git branch
```

Yeni branch oluştur ve geç:

```bash
git switch -c feature/yeni-ozellik
```

Branch değiştir:

```bash
git switch main
```

Branch’i GitHub’a gönder:

```bash
git push -u origin feature/yeni-ozellik
```

---

## 12) Merge (Birleştirme)

Feature tamamlandıysa:

```bash
git switch main
git pull
git merge feature/yeni-ozellik
git push
```

---

## 13) Conflict (Çakışma) Çözme

Conflict oluşursa:

```bash
git status
```

Dosyayı aç ve çakışma işaretlerini düzelt.

Sonra:

```bash
git add dosyaAdi
git commit
```

---

## 14) Değişiklikleri İnceleme

Son commit’leri gör:

```bash
git log --oneline
```

Değişiklik farkını gör:

```bash
git diff
```

Stage edilmiş değişiklikleri gör:

```bash
git diff --staged
```

---

## 15) Geri Alma İşlemleri

Henüz commit atmadıysan değişiklikleri sil:

```bash
git restore .
```

Stage’den çıkar:

```bash
git restore --staged dosyaAdi
```

Son commit mesajını düzelt:

```bash
git commit --amend
```

Güvenli geri alma:

```bash
git revert <commit-id>
```

Son commit’i tamamen sil (dikkat):

```bash
git reset --soft HEAD~1
```

Tamamen sil ve dosyaları geri al (tehlikeli):

```bash
git reset --hard HEAD~1
```

---

## 16) Remote Yönetimi

Remote’ları listele:

```bash
git remote -v
```

Remote ekle:

```bash
git remote add origin https://github.com/kullanici/repo.git
```

Remote değiştir:

```bash
git remote set-url origin https://github.com/kullanici/yeni-repo.git
```

---

## 17) .gitignore Kullanımı

`.gitignore` örneği:

```text
.env
node_modules/
.DS_Store
*.log
```

Takipten çıkar:

```bash
git rm --cached dosyaAdi
git commit -m "Stop tracking file"
```

---

## Günlük Ezber

```bash
git status
git add .
git commit -m "mesaj"
git push
```

Bu dört komut Git kullanımının temelidir.
