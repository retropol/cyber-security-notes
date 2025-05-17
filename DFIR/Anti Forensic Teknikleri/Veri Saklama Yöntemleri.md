## eri Gizleme Teknikleri

Veri gizleme, verileri şifreli ve izlenemez hale getirerek görünmez veya tespit撞ı tespit edilemez yapma yöntemleridir. 3 ana teknik:

### 1. Steganografi

- **Tanım**: Mesajları dosya, resim veya videoda gizler; varlığı saklar.
    
- **Teknikler**: LSB (En Az Önemli Bit) ile görüntüde, düşük frekanslı ses dalgaları ile seste gizleme.
    
- **Kullanım**: Gizli iletişim, telif hakkı koruması, veri gizliliği.
    
- **Tespit**: Steganaliz (istatistiksel anormallik analizi), görsel/işitsel analiz.
    

### 2. Kriptografi

- **Tanım**: Verileri şifreleyerek sadece yetkili kişilerin erişimini sağlar.
    
- **Yöntemler**:
    
    - **Simetrik Şifreleme**: Aynı anahtar kullanılır (ör. AES).
        
    - **Asimetrik Şifreleme**: Public/private anahtar çifti (ör. RSA).
        
    - **Hash Fonksiyonları**: Veri bütünlüğü için tek yönlü dönüşüm.
        
    - **Dijital İmzalar**: Kimlik doğrulama ve değişmezlik garantisi.
        
    - **PKI**: Güvenli anahtar dağıtımı için sertifikalar.
        
- **Tespit**: Kriptoanaliz (zayıflık bulma), kaba kuvvet saldırıları.
    

### 3. Veri Karartma

- **Tanım**: Verileri anlaşılmaz veya analiz edilmesi zor hale getirir.
    
- **Yöntemler**:
    
    - **Kod Karartma**: Kaynak kodunu okunamaz yapar.
        
    - **Veri Maskeleme**: Hassas verileri rastgele değerlerle değiştirir.
        
    - **Şifreleme Tabanlı Karartma**: Verilerin belirli kısımlarını şifreler.
        
    - **Algoritmik Karartma**: Karmaşık dönüşümlerle veriyi gizler.
        
    - **Anlamsal Bulanıklaştırma**: Verinin anlamını bozar.
        
    - **Veri Karıştırma**: Veriyi rastgele hale getirir.
        
    - **Veri Sıkıştırma**: Yapıyı gizler.
        
- **Tespit**: Algoritmik analiz, desen analizi.
    

## Tespit ve Karşı Stratejiler

- **Steganografi**: Steganaliz, görsel/işitsel analiz.
    
- **Kriptografi**: Kriptoanaliz, kaba kuvvet kullanıliabliir.
    
- **Veri Karartma**: Algoritmik/desen analizi ile orijnal yapı bulunmaya çalışılır.
    
- **Not**: Adli bilişim uzmanları, sürekli gelişen anti-adli tekniklere karşı araç ve becerilerini güncellemelidir.
