# Git: Terminal El Kitabı 

Bu doküman, bir projenin başlangıcından ileri seviye geri alma işlemlerine kadar olan tüm Git sürecini kapsar. Git, projenizin "zaman makinesidir".



## 0. Kurulum ve Kontrol
Git'in sistemde olup olmadığını ve sürümünü kontrol eder.

* `git --version`
  - **Açıklama:** Git'in kurulu olup olmadığını ve hangi sürümün kullanıldığını gösterir.

## 1. Başlangıç ve Yapılandırma
Kimlik bilgileri bir kez ayarlanır; projeler ise her yeni başlangıçta başlatılır.

* `git config --global user.name "Mehmet Türk"`
  - **Açıklama:** Yapacağınız tüm kayıtlar (commit) için dünya genelinde görünecek isminizi belirler.
* `git config --global user.email "mehmet123@ornek.com"`
  - **Açıklama:** Kayıtlarınızın hangi e-posta adresiyle ilişkilendirileceğini belirler.
* `git init`
  - **Açıklama:** Mevcut klasörü bir Git deposuna (repository) dönüştürür; `.git` klasörünü oluşturur.
* `git clone https://github.com/galipsoken/dev-stack-playbook.git`
  - **Açıklama:** Uzaktaki bir projeyi bilgisayarınıza tüm geçmişiyle birlikte indirir.

## 2. Temel Çalışma Döngüsü (Stage & Commit)
Dosyalardaki değişiklikleri adım adım kaydetmek için kullanılır.

* `git status`
  - **Açıklama:** Değişen, silinen veya yeni eklenen dosyaların mevcut durumunu listeler.
* `git add .`
  - **Açıklama:** Projedeki tüm değişiklikleri "Staging Area" (Hazırlık Alanı) kısmına ekler.
* `git commit -m "Mesaj Yazısı"`
  - **Açıklama:** Hazırlık alanındaki dosyaları kalıcı bir versiyon olarak yerel depoya kaydeder.
* `git diff`
  - **Açıklama:** Henüz `add` yapılmamış dosyalarda, kod seviyesinde hangi satırların değiştiğini gösterir.

## 3. Dallanma ve Yönetim (Branching)
Ana kodu bozmadan yeni özellikler geliştirmek için kullanılır.

* `git branch`
  - **Açıklama:** Tüm yerel dalları listeler. Mevcut dalın başında `*` işareti bulunur.
* `git switch -c yeni-ozellik`
  - **Açıklama:** 'yeni-ozellik' adında bir dal oluşturur ve anında o dala geçer.
* `git switch ana-dal`
  - **Açıklama:** Mevcut bir dal olan 'ana-dal' üzerine geçiş yapar.
* `git merge dal-adi`
  - **Açıklama:** 'dal-adi' üzerindeki çalışmaları, şu an bulunduğunuz dal ile birleştirir.
* `git branch -d dal-adi`
  - **Açıklama:** İşlemi bitmiş ve birleştirilmiş olan dalı siler.

## 4. Uzak Depo Senkronizasyonu (Remote)
GitHub gibi platformlarla yerel kodunuzu eşitlemek için kullanılır.

* `git remote add origin https://github.com/mehmetturk/dev-stack-playbook.git`
  - **Açıklama:** Yerel deponuzu internetteki bir adrese 'origin' takma adıyla bağlar.
* `git remote -v`
  - **Açıklama:** Yerel deponun hangi uzak sunuculara bağlı olduğunu gösterir.
* `git push -u origin main`
  - **Açıklama:** Yerel kayıtları uzak sunucudaki 'main' dalına gönderir. `-u` sonraki push'ları kolaylaştırır.
* `git pull`
  - **Açıklama:** Uzaktaki en güncel değişiklikleri çeker ve yerel kodunuzla anında birleştirir.
* `git fetch`
  - **Açıklama:** Değişiklikleri sunucudan indirir ama birleştirme yapmaz; sadece kontrol etmenizi sağlar.

## 5. Değişiklikleri Geri Alma (Undo & Restore)
Hataları düzeltmek veya eski bir sürüme dönmek için kullanılır.

* `git log --oneline --graph`
  - **Açıklama:** Tüm kayıt geçmişini grafiksel ve tek satırlık özetler halinde gösterir.
* `git restore dosya.txt`
  - **Açıklama:** Henüz kaydedilmemiş bir dosyadaki değişiklikleri iptal edip son haline döndürür.
* `git reset HEAD dosya.txt`
  - **Açıklama:** `git add` ile hazırlanan bir dosyayı hazırlık alanından (staged) geri çıkarır.
* `git revert <commit-id>`
  - **Açıklama:** Belirli bir commit'i geri alacak yeni bir kayıt oluşturur (geçmişi bozmaz, güvenlidir).
* `git stash`
  - **Açıklama:** Bitmemiş işleri geçici bir hafızaya alır, çalışma alanını tertemiz yapar.
* `git stash pop`
  - **Açıklama:** Hafızadaki (stash) işleri geri getirir ve listeyi temizler.
