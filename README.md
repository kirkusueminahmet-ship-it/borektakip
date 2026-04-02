# Börek Takip Sistemi 🥐

Börek siparişlerini, teslimatları, iadeleri ve ödemeleri takip eden web uygulaması. Firebase Realtime Database ile gerçek zamanlı senkronizasyon.

## Özellikler

- **Sipariş Yönetimi**: Hafta içi / Cumartesi / Pazar günleri için ayrı sipariş listeleri
- **Teslimat Kaydı**: Günlük teslimatları kaydedin, otomatik tutar hesaplama
- **İade Takibi**: İade edilen ürünleri ürün bazında kaydedin, borçtan düşün
- **Ödeme Kaydı**: Yapılan ödemeleri kaydedin
- **Bakiye Hesaplama**: Toplam borç - ödemeler - iade düşümleri = kalan bakiye
- **Firebase Senkronizasyon**: Veriler gerçek zamanlı senkronize, telefondan da erişim
- **Dışa/İçe Aktarma**: JSON yedekleme

---

## Kurulum: Firebase

### 1. Firebase Projesi Oluşturun

1. [Firebase Console](https://console.firebase.google.com/) adresine gidin
2. **Proje Ekle** butonuna tıklayın
3. Proje adını girin (ör: `borek-takip`)
4. Google Analytics isteğe bağlı, kapatabilirsiniz
5. **Proje Oluştur** butonuna tıklayın

### 2. Realtime Database Oluşturun

1. Sol menüden **Build > Realtime Database** seçin
2. **Veritabanı Oluştur** butonuna tıklayın
3. Konum seçin (europe-west1 önerilir)
4. **Test modunda başlat** seçin (sonra güvenlik kurallarını ayarlayacağız)

### 3. Web Uygulaması Ekleyin

1. Proje genel bakış sayfasında **</>** (Web) ikonuna tıklayın
2. Uygulama adı girin (ör: `borek-takip-web`)
3. **Firebase Hosting** kutucuğunu işaretleyin
4. **Uygulamayı Kaydet** butonuna tıklayın
5. Gösterilen yapılandırma bilgilerini kopyalayın:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "borek-takip.firebaseapp.com",
  databaseURL: "https://borek-takip-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "borek-takip",
  storageBucket: "borek-takip.appspot.com",
  appId: "1:123456789:web:abcdef..."
};
```

### 4. Güvenlik Kuralları (Önerilen)

Realtime Database > Rules sekmesinde:

```json
{
  "rules": {
    "borekTakip": {
      ".read": true,
      ".write": true
    }
  }
}
```

> ⚠️ Bu kural herkese açık erişim sağlar. Daha güvenli yapmak istiyorsanız Firebase Authentication ekleyebilirsiniz.

---

## Kurulum: GitHub Pages

### 1. GitHub Deposu Oluşturun

```bash
# Yerel klasörde
git init
git add .
git commit -m "İlk yükleme"
git branch -M main
git remote add origin https://github.com/KULLANICI_ADINIZ/borek-takip.git
git push -u origin main
```

### 2. GitHub Pages Aktifleştirin

1. GitHub'da depo sayfasına gidin
2. **Settings > Pages** bölümüne gidin
3. Source olarak **Deploy from a branch** seçin
4. Branch: **main**, klasör: **/ (root)** seçin
5. **Save** butonuna tıklayın

Birkaç dakika içinde siteniz şu adreste yayınlanır:
`https://KULLANICI_ADINIZ.github.io/borek-takip/`

### 3. Uygulamada Firebase Bağlantısı

1. Yayınlanan siteyi açın
2. **Ayarlar** sekmesine gidin
3. Firebase yapılandırma bilgilerini girin
4. **Firebase Bağlantısını Kaydet** butonuna tıklayın

---

## Kullanım

### Günlük İş Akışı

1. **Sabah**: Sipariş sayfasında gün tipine göre (hafta içi/cumartesi/pazar) miktarları kontrol edin
2. **Teslimat gelince**: Teslimatlar sekmesinden tarih ve gün tipini seçip kaydedin
3. **İade varsa**: Teslimatlar sekmesinden iade formunu doldurun (ürün seçin, adet girin)
4. **Ödeme yapınca**: Teslimatlar sekmesinden ödeme tutarını girin
5. **Bakiye kontrolü**: Bakiye sekmesinden anlık durumu görün

### Bakiye Hesaplama Mantığı

```
Kalan Bakiye = Toplam Teslimat Tutarı - Toplam Ödemeler - Toplam İade Düşümleri
```

---

## Dosya Yapısı

```
borek-takip/
├── index.html    ← Tek dosyalık uygulama
└── README.md     ← Bu dosya
```
