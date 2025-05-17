# Artifact Wiping (Eser Silme)

**Artifact wiping**, dijital ortamdan kullanıcı etkinliklerini silme işlemidir. Amaç, sistemde herhangi bir iz bırakmadan verileri geri döndürülemez şekilde ortadan kaldırmaktır.

Bu işlem:

- Her tür dijital veriyi kapsayabilir.
    
- Yazılımlar aracılığıyla ya da manuel olarak yapılabilir.
    
- Geri döndürülemez şekilde silme hedeflenir.
    

## Hangi İzler Silinebilir?

- Log dosyaları
    
- Geçici (temp) dosyalar
    
- Tarayıcı geçmişi
    
- Silinmiş dosya izleri
    

---

## Yöntemler

### 1. Yazılım Kullanarak Silme

Kullanıcı, özel yazılımlar aracılığıyla verilerin üzerine rastgele veriler yazarak silme işlemini gerçekleştirir. Bu işlem sonunda dosyalar kurtarılamaz hâle gelir.

**Bazı araç örnekleri:**

- [CCleaner](https://www.ccleaner.com/)
    
- [BleachBit](https://www.bleachbit.org/)
    
- Eraser
    

Bu araçlar aynı zamanda:

- Sistem temizliği
    
- Geçici dosya temizliği
    
- Tarayıcı geçmişi silme gibi işlevler sunar.
    

### 2. Manuel Silme

- Kullanıcı, dosya gezginiyle silinecek dosyaları bulur ve siler.
    
- Tarayıcı ayarları üzerinden çerezler, önbellek ve geçmiş temizlenebilir.
    
- Sistem ayarlarından geçici dosyalar silinebilir.
    

> **Not:** Manuel silme işlemleri genellikle yetersiz kalır çünkü veriler kurtarılabilir durumda kalabilir.

---
## Inhibit System Recovery (Sistem Kurtarmayı Engelleme)

**Tanım**: Saldırganlar, sistem kurtarma özelliklerini silerek veya devre dışı bırakarak yedeklere erişimi engeller, veri imhası veya fidye yazılımı etkisini artırır.

### Amaç

- Sistem kurtarma seçeneklerini (yedek katalog, gölge kopyalar, otomatik onarım) devre dışı bırakma.
    
- Veri imhası veya şifreleme sonrası kurtarmayı zorlaştırma.
    
- Kurtarma bildirimlerini devre dışı bırakıp yedekleri bozma.
    

### Kullanılan Windows Araçları ve Komutlar

```bash
# Tüm gölge kopyaları siler
vssadmin.exe delete shadows /all /quiet

# Gölge kopyaları siler
wmic shadowcopy delete

# Windows Yedek Katalogunu siler
wbadmin.exe delete catalog -quiet

# Otomatik kurtarma özelliklerini devre dışı bırakır
bcdedit.exe /set {default} bootstatuspolicy ignoreallfailures
bcdedit.exe /set {default} recoveryenabled no

# Tüm gölge kopyaları siler
diskshadow delete shadows all
```

- **REAgentC.exe**: Windows Kurtarma Ortamı (WinRE) seçeneklerini devre dışı bırakır (komut örneği yaygın değil).

### Ekstra Not: PowerShell Komut Geçmişini Görme

PowerShell komut geçmişini görmek için şu dosya yoluna bakın:

```
%USERPROFILE%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

- **Not**: Bu dosya, kullanıcının PowerShell komut geçmişini içerir ve adli analizde iz takibi için kullanılabilir.

---

## Güvenli Silme Protokolleri

Güvenli silme, verilerin belirli desenlerle tekrar tekrar üzerine yazılarak geri döndürülemez hâle getirilmesidir.

### Nasıl Çalışır?

- Yazılım, dosyaların üzerine birden fazla kez rastgele veriler yazar.
    
- Her geçişte eski veriler tamamen silinir.
    
- Silme işlemi, standartlara (örneğin DoD 5220.22-M) göre yapılabilir.
    

---

## Şifreleme ve Anahtar Silme Yöntemi

Bu yöntemde veriler önce güçlü algoritmalarla şifrelenir, ardından şifreleme anahtarı silinerek verilere erişim imkânsız hâle getirilir.

### Nasıl Çalışır?

- Disk ya da dosyalar AES gibi güçlü algoritmalarla şifrelenir.
    
- Şifreleme anahtarı silinirse, veriler çözülmesi mümkün olmayan bir biçimde kalır.
    

---

## Tespit ve Karşı Tedbirler

Anti-adli bilişimde kullanılan bu tür silme teknikleri çeşitli yollarla tespit edilebilir. Adli bilişim uzmanları bu durumlara karşı çeşitli önlemler almalıdır.

### Artefakt Silme Algılaması

- **Anormal dosya yokluğu:** Beklenenden az dosya bulunması
    
- **Log dosyalarında boşluk:** Sistem ya da güvenlik günlüklerinde eksik girişler
    
- **Dosya sistemi analizi:** Silinmiş dosyaların kalıntıları özel araçlarla analiz edilir
    
- **Anormal boş disk alanı:** Ani artış, toplu veri silimine işaret edebilir
    

### Karşı Önlemler

- **Merkezi log toplama:** Loglar harici ve güvenli bir konumda saklanmalı
    
- **Dosya bütünlüğü izleme:** Kritik sistem dosyalarındaki değişiklikler tespit edilmeli
    
- **Erişim kontrolleri:** Yetkisiz erişim ve silmeler engellenmeli
    
- **Şüpheli etkinlik izleme:** Anormal kullanıcı davranışları analiz edilmeli
    
- **Adli hazırlık:** Olay sonrası analiz planı ve hazır altyapı bulundurulmalı
    
- **Farkındalık eğitimi:** Kullanıcılar ve BT personeli düzenli olarak eğitilmeli
    

---

## Sonuç

Eser silme, bireysel gizlilik ve kurumsal güvenlik için kritik öneme sahiptir. Ancak bu tekniklerin kullanımı **etik ve yasal sınırlar** içinde gerçekleştirilmelidir.

