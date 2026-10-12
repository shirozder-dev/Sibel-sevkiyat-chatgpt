# Tekstil Export Manager

Türkçe, mobil uyumlu konteyner ve ihracat operasyonları takip paneli. GitHub Pages üzerinde statik olarak yayınlanabilir; Firebase yapılandırıldığında Firebase Authentication ve Cloud Firestore kullanır.

## Özellikler
- Genel bakış: aktif konteyner, yükleme/varış yaklaşımı, bakiye ve görev özeti
- Konteyner kayıt ekleme, düzenleme, arama ve durum filtreleri
- Her kayıt için tek müşteri, FCL/LCL, limanlar, taşıyıcı, tarih ve not alanları
- Packing List, Commercial Invoice, gümrük beyannamesi, B/L, menşe, sigorta, Telex Release ve diğer belgeler için ayrı durumlar
- Ödeme durumu takibi (tutar/muhasebe sistemi değildir)
- Görevler, işlem geçmişi ve JSON dışa aktarma
- Türkçe arayüz, USD para birimi, mobil uyumlu tasarım
- Firebase Auth giriş ekranı ve Firestore bağlantısı

## Hızlı önizleme
Firebase ayarları eklenmediğinde uygulama demo modunda açılır. Kayıtlar yalnızca aynı tarayıcının `localStorage` alanına kaydedilir; cihazlar arasında senkronize olmaz. Demo modunda gerçek müşteri verisi kullanmayın.

## Firebase kurulumu
1. Firebase Console'da bir proje oluşturun.
2. **Authentication → Sign-in method → Email/Password** seçeneğini etkinleştirin.
3. Authentication → Users içinden her yetkili ekip üyesini ekleyin.
4. **Firestore Database** oluşturun.
5. Project settings → Your apps → Web app bölümünden web yapılandırmasını alın.
6. `app.js` içindeki `firebaseConfig` alanındaki `YOUR_...` değerlerini gerçek proje değerleriyle değiştirin.
7. Firebase Console → Firestore → Rules alanına `firestore.rules` dosyasının içeriğini yapıştırıp yayınlayın.
8. İlk kurulum ve güvenlik doğrulamasından sonra gerçek verileri girin.

### Güvenlik notu
Örnek Firestore kuralları, giriş yapmış tüm Firebase kullanıcılarının aynı proje içindeki konteyner kayıtlarını okuyup değiştirmesine izin verir. Bu yalnızca güvenilir, kapalı bir ekip için başlangıç ayarıdır; daha hassas rol/erişim ayrımı gerekiyorsa kullanıcı allow-list'i veya custom claims ile kısıtlayın. GitHub deposunu public tutacaksanız gerçek müşteri verilerini, gizli sunucu anahtarlarını veya dosyaları depoya koymayın. Firebase web config, tek başına yetki vermez; asıl koruma Authentication ve Security Rules'tur.

## GitHub Pages ile yayınlama
1. Bu klasördeki dosyaları yeni bir GitHub deposuna yükleyin.
2. GitHub deposunda **Settings → Pages** bölümünü açın.
3. **Deploy from a branch** seçin; `main` ve `/ (root)` seçip kaydedin.
4. Yayınlama tamamlanınca GitHub Pages URL'sini açın. Firebase yapılandırıldıysa giriş ekranı görünür; yapılandırılmadıysa demo modu açılır.

## Hatırlatmalar ve kapsam
Uygulama içi görevler konteyner durumları ve tarihlerinden üretilir. E-posta bildirimleri henüz etkin değildir; bunun için güvenli sunucu tarafı zamanlayıcı (ör. Firebase Cloud Functions) ve e-posta sağlayıcısı yapılandırılmalıdır. Otomatik gemi takibi, PDF yükleme/üretme, otomatik e-posta gönderimi ve Excel dışa aktarma bu ilk sürümde bulunmaz. Şu anda JSON dışa aktarma vardır.

## Dosyalar
- `index.html` — sayfa yapısı
- `styles.css` — responsive arayüz
- `app.js` — uygulama mantığı ve Firebase bağlantısı
- `firebase-config.example.js` — yapılandırma örneği
- `firestore.rules` — başlangıç güvenlik kuralları
