# Ezan Vakti Pro (v2.2) — Modern Android Namaz Vakitleri & Arayüz Mimarisi

**Ezan Vakti Pro**, Jetpack Compose, Material Design 3, Room SQL ve Diyanet İşleri Başkanlığı uyumlu astronomik hesaplama motoruyla geliştirilmiş modern, akıcı ve yüksek hassasiyetli bir Android namaz vakitleri uygulamasıdır.

---

## 🌟 Öne Çıkan Özellikler ve Mimari Yapı

### 1. 📍 Konuma Dayalı Diyanet Hesaplama Motoru (81 İl ve Tüm İlçeler)
- **Tüm Türkiye İlleri Entegrasyonu:** Türkiye'nin 81 ili ve tüm ilçe merkezleri koordinat düzeyinde tanımlanmıştır.
- **Otomatik GPS ve Yakın İl Mimarisi:** GPS koordinatları alındığında, `Haversine` mesafe algoritması ile en yakın Türkiye şehri otomatik tespit edilir.
- **Diyanet API & Astronomik Standartlar:** `Aladhan API (Diyanet Metodu - Method 13)` ile 2 günlük canlı senkronizasyon yapılır. İnternet kesintilerinde `Meeus VSOP87 + Diyanet Temkin Matrisi` devreye girerek çevrimdışı milisaniyelik nokta atışı vakit üretir.
- **Firebase Realtime Sync:** Güncellenen konum ve vakit verileri arka planda `https://studio-2445378601-515e7-default-rtdb.europe-west1.firebasedatabase.app` üzerindeki `/location_sync` düğümüne otomatik senkronize edilir.

### 2. ☁️ 3D Volumetrik Bulut & Atmosferik Gökyüzü Motoru
- **Dinamik 3D Bulut Katmanları:** `SkyBackgroundCanvas.kt` üzerinde 5 farklı derinlik katmanına sahip, hacimsel alt gölgeli (ambient occlusion) ve güneş ışığı kırılmalı (top rim lighting) 3D bulut render altyapısı.
- **Vakite Duyarlı Renk Süzülmesi:** İmsak, Güneş, Öğle, İkindi, Akşam ve Yatsı vakitlerine özel akıcı 60fps gradyan dönüşümleri ve gökyüzü animasyonları.

### 3. ⏱️ Gelişmiş Kişiselleştirme & Sıvı Cam (Glassmorphic) Arayüz
- **Vakit Sayacı Canlı Boyutlandırma:** `SystemCustomizerSheet` üzerinden sayaç boyutları `0.7x` ile `1.6x` arasında dinamik olarak ayarlanabilir.
- **Room SQL Mimarisi:** Tüm kişiselleştirme tercihleri, alarm yapılandırmaları ve ezan geçmiş kayıtları Room veritabanı ile cihazda güvenle saklanır.

### 4. ⚡ Tek Merkezli Yüksek Hızlı APK Güncelleme Dağıtımı
- **Upload-APK CDN Entegrasyonu:** Harici indirme sunucuları yerine doğrudan `upload-apk.com` CDN altyapısı entegre edilmiştir.
- **R8 / ProGuard Minification:** APK boyutu 22 MB seviyesinden 6.19 MB düzeyine düşürülmüş ve çalışma zamanı optimizasyonları tamamlanmıştır.
- **Sessiz / Arka Plan Güncelleme Kontrolü:** `GupUpdateManager` ile Firebase üzerindeki `latest.json` sorgulanır ve yeni sürümler anında cihazda bildirilir.

### 5. 🛡️ GenSecure Knox-Shield 2.0 Güvenlik Katmanı
- **AES-256 CBC & HMAC SHA-256:** Cihaz içi veri tabanı, ayar ve yapılandırmalar Knox-Shield standartlarında şifrelenmektedir.

---

## 🛠️ Teknik Özellikler ve Kullanılan Teknolojiler

| Bileşen | Kullanılan Teknoloji / Kütüphane |
| :--- | :--- |
| **Arayüz (UI)** | Jetpack Compose, Material 3, Custom Canvas Drawing |
| **Dil & Derleyici** | Kotlin 2.0+, KSP (Kotlin Symbol Processing) |
| **Veritabanı** | Room Database (SQLite Engine) |
| **Asenkron İşlem** | Kotlin Coroutines, StateFlow, SharedFlow |
| **Ağ Entegrasyonu** | OkHttp 4.12, Retrofit, REST API |
| **Konum Servisleri** | Google Play Services FusedLocationProviderClient, Geocoder |
| **Arka Plan Servisleri** | AlarmManager, BroadcastReceiver, Foreground Service, WorkManager |
| **Dağıtım / Bulut** | Firebase Realtime Database, Upload-APK CDN |

---

## 🚀 Proje Dizin Yapısı

```
app/src/main/java/com/example/
├── data/
│   ├── api/                  # Diyanet API repository ve canlı senkronizasyon
│   ├── audio/                # Ezan ses servisi ve çalar altyapısı
│   ├── calculation/          # 81 İl koordinatları (CitiesData) & Meeus Astronomik Hesaplayıcı
│   ├── local/                # Room AppDatabase, DAO ve Entity katmanları
│   └── model/                # Vakit, Konum ve Alarm Veri Modelleri
├── security/                 # GenSecure Knox-Shield 2.0 Şifreleme Motoru
├── service/                  # Adhan Alarm Scheduler, NotificationHelper & GupUpdateManager
├── ui/
│   ├── components/           # 3D Sky Canvas, Glassmorphic Card, SystemCustomizerSheet
│   ├── screens/              # Home, Location, Alarms, Settings, Hadith, History Screens
│   ├── theme/                # Material Design 3 Temaları ve Renk Setleri
│   └── viewmodel/            # EzanViewModel Reaktif Mimarisi
└── widget/                   # Android Ana Ekran Widget Sağlayıcısı (PrayerWidgetProvider)
```

---

## 📝 Lisans ve Notlar
Bu uygulama Diyanet İşleri Başkanlığı hesaplama standartlarına tam uyumlu olarak tasarlanmıştır. Tüm hakları saklıdır.
