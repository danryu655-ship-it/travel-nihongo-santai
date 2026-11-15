# Nihongo Santai Travel

Aplikasi Android **offline** (tanpa internet) berisi panduan travel Jepang dengan
konten Nihongo Santai sendiri — terinspirasi TUP/Tabibiyori, tapi semua teks
dan konten ditulis ulang sendiri (bukan salinan).

## Isi aplikasi (v1.0)

Satu file HTML mandiri (`app/index.html`) yang dibungkus WebView Android.
Tidak ada CDN, font eksternal, API key, atau panggilan jaringan. Semua data
tersimpan di HP (localStorage).

- **Kartu Frasa** — 33 frasa turis (salam, tanya arah, belanja, restoran,
  darurat, minta maaf): Jepang + romaji + arti Indonesia. Ketuk = kartu
  full-screen besar untuk ditunjukkan ke staf.
- **Checklist Konbini** — 33 makanan/barang konbini dengan checkbox, progres,
  dan badge (10/20/30 item).
- **Menu Decoder** — 41 kata menu umum (mi, nasi, sushi, daging, dll) + pembuat
  kartu alergi/diet (12 alergi + 4 pilihan diet) yang tampil full-screen
  dalam bahasa Jepang.
- **Kuis Travel N5** — 10 soal pilihan ganda, posisi jawaban diacak tiap
  permainan, skor akhir + skor terbaik tersimpan.
- **Perencana Trip** — pilih kota (Tokyo, Kyoto, Osaka, Nara, Fuji, Hiroshima,
  Hokkaido, Okinawa), jumlah hari, budget JPY, catatan, packing checklist
  (10 barang), wishlist, dan pelacak pengeluaran dengan sisa budget otomatis.

**Aturan akurasi:** hanya item yang sudah dikenal luas; setiap bacaan
(kana/romaji) diperiksa; kalau ragu, item dibuang, bukan ditebak.

## Struktur repo

```
app/index.html                  # aplikasi web mandiri (sumber kebenaran)
android/                        # proyek Android (WebView wrapper)
  settings.gradle
  build.gradle
  gradle.properties
  app/build.gradle
  app/src/main/AndroidManifest.xml
  app/src/main/java/com/danryu/travelnihongo/MainActivity.java
  app/src/main/assets/index.html   # WAJIB sinkron dengan app/index.html
  app/src/main/res/mipmap-*/       # icon launcher (DP Nihongo Santai)
dp-nihongosantai.jpg            # logo (juga tertanam base64 di index.html)
```

## Build

Toolchain: Android SDK platform 35 + build-tools 35.0.0, JDK 17 Corretto,
Gradle 8.7. AGP 8.5.2 meminta build-tools 34.0.0 — pin ke 35.0.0.

```sh
cd android
JAVA_HOME=~/workspace/jdk17 ANDROID_HOME=~/workspace/android-sdk \
GRADLE_USER_HOME=~/workspace/gradle-home \
JAVA_TOOL_OPTIONS=-Djava.net.preferIPv4Stack=true \
~/workspace/gradle-8.7/bin/gradle assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```

## Build terverifikasi

- v1.0 (versionCode 1): APK 453.108 byte, SHA256 4dc3984ff0e4adb57248a4b59d9bdae64baff9cc6763399c9cb370e67e7c8e22 (aapt2: package com.danryu.travelnihongo, versionCode 1, versionName 1.0, label "Nihongo Santai Travel")
