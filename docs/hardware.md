# Diafon Modernizasyonu Donanım Dokümantasyonu

## Gerekli Bileşenler
1. NodeMCU ESP8266 geliştirme kartı
2. 5V Röle Modülü (minimum 2 kanal)
3. Güç Kaynağı (NodeMCU ve röleler için 5V DC)
4. Voltaj seviye dönüştürücü (diafon voltajına bağlı olarak gerekirse)
5. Temel aletler:
   - Voltmetre
   - Osiloskop
   - Voltaj jeneratörü
   - Havya ve lehim
   - Kablo soyucu
   - Isı ile daralan makaron

## Güvenlik Önlemleri
⚠️ **ÖNEMLİ**: Eski diafon sistemleri yüksek voltajla çalışabilir (genellikle 12V AC veya daha yüksek). Her zaman:
- Sistem üzerinde çalışmadan önce gücü kesin
- Uygun yalıtım kullanın
- Voltaj ölçümlerini iki kez kontrol edin
- Voltaja uygun değerlerde röle kullanın

## Sistem Mimarisi
```
[Güç Kaynağı] -----> [NodeMCU] -----> [Röle Modülü] -----> [Diafon Sistemi]
      |                   |
      |                   |
      +---> [5V DC] ------+
```

## Kablolama Kılavuzu
1. **Güç Kaynağı**
   - 5V ve GND'yi NodeMCU'ya bağlayın
   - 5V ve GND'yi röle modülünün VCC ve GND pinlerine bağlayın

2. **NodeMCU - Röle Modülü Bağlantısı**
   - GPIO D1'i Röle 1 IN'e bağlayın
   - GPIO D2'yi Röle 2 IN'e bağlayın (ikinci röle kullanılıyorsa)
   - NodeMCU ve röle modülü arasında ortak GND

3. **Röle - Diafon Bağlantısı**
   - NO (Normalde Açık) terminalini diafon tetikleme hattına
   - COM (Ortak) terminalini diafon toprak/dönüş hattına

## Test Prosedürü
1. **İlk Voltaj Ölçümü**
   - Boştayken diafon terminalleri arasındaki voltajı ölçün
   - Buton basılıyken voltajı ölçün
   - AC/DC değerlerini ve AC ise frekansı not edin

2. **Sinyal Analizi**
   - Buton basma dalga formunu osiloskop ile yakalayın
   - Belgelendirin:
     - Sinyal süresi
     - Voltaj seviyeleri
     - Özel desenler/zamanlama

3. **Güvenli Test**
   - Önce voltaj jeneratörü ile sinyalleri simüle ederek test edin
   - Röle zamanlamasını ve çalışmasını doğrulayın
   - Gerçek diafon sistemi ile sadece doğrulama sonrası test edin

## Home Assistant Entegrasyon Noktaları
- NodeMCU şu uç noktaları açacak:
  1. Kapı kilit açma tetikleyici
  2. Zil çalma tetikleyici
  3. Durum izleme

## Sorun Giderme Noktaları
1. Her bağlantı noktasında voltaj seviyelerini kontrol edin
2. Röle anahtarlamasını multimetre ile doğrulayın
3. Tanılama için NodeMCU seri çıktısını izleyin
4. Yaygın sorunlar:
   - Röle çatırdaması: Gerekirse snubber devresi ekleyin
   - Parazit: Blendajlı kablo kullanın
   - Güç sorunları: Gerekirse röleler için ayrı güç kaynağı kullanın
