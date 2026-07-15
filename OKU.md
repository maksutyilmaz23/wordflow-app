# HTML → APK Otomatik Derleme Şablonu

## Nasıl çalışır?
Bu proje senin HTML dosyanı bir WebView içinde açan bir Android uygulamasıdır.
Kod GitHub'a her push edildiğinde, GitHub Actions otomatik olarak APK'yı derler
— senin bilgisayarında Android Studio kurulu olmasa bile.

## Kurulum adımları

1. **HTML dosyanı yerleştir**
   `app/src/main/assets/index.html` dosyasını kendi HTML dosyanla değiştir.
   Eğer birden fazla dosyan varsa (resim, js, css) hepsini `assets/` klasörüne koy,
   `index.html` içindeki referanslar (`<script src="...">` vb.) göreceli yol kullanmalı.

2. **Uygulama adını değiştir (isteğe bağlı)**
   `app/src/main/res/values/strings.xml` içindeki `app_name` değerini değiştir.

3. **İkon değiştir (isteğe bağlı)**
   `app/src/main/res/mipmap-hdpi/ic_launcher.png` dosyasının üzerine kendi 192x192 ikonunu koy.

4. **GitHub'a yükle**
   - GitHub'da yeni bir repo oluştur (public veya private, farketmez)
   - Bu klasördeki tüm dosyaları o repoya push et:
     ```
     git init
     git add .
     git commit -m "ilk commit"
     git branch -M main
     git remote add origin https://github.com/KULLANICI_ADIN/REPO_ADIN.git
     git push -u origin main
     ```

5. **APK'yı indir**
   - GitHub reponda **Actions** sekmesine git
   - "Build APK" workflow'unun tamamlanmasını bekle (yaklaşık 2-3 dakika)
   - Tamamlanan workflow'a tıkla, en altta **Artifacts** bölümünden
     `app-debug-apk` dosyasını indir — içinde `app-debug.apk` var.
   - Bu APK'yı telefonuna kopyalayıp kurabilirsin (bilinmeyen kaynaklara izin vermen gerekebilir).

## Notlar
- Bu şablon **debug APK** üretir (imzasız, test amaçlı — kendi telefonuna kurmak için sorun değil).
- Play Store'a yüklemek istersen "release" imzalı APK/AAB gerekir, bu ayrı bir adım — istersen onu da ekleyebilirim.
- HTML dosyan kamera, dosya sistemi, konum gibi izinler istiyorsa `AndroidManifest.xml`
  içine ilgili `<uses-permission>` satırlarını eklemen gerekebilir.
- Paket adını (`com.mesut.webviewapp`) değiştirmek istersen hem `app/build.gradle`
  içindeki `applicationId` ve `namespace`, hem de klasör yapısını
  (`app/src/main/java/com/mesut/webviewapp/`) güncellemen gerekir.
