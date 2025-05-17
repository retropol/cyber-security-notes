
## Günlük (Log) Manipülasyonu ve Silme

**Günlük dosyaları**, sistem, uygulama veya ağ etkinliklerini kaydeden kritik veri kaynaklarıdır. Güvenlik ihlalleri veya sistem arızalarında olayları analiz eder, ancak saldırganlar tarafından manipüle edilebilir veya silinebilir.

### 1. Günlük Manipülasyonu (Log Tampering)

- **Tanım**: Günlük kayıtlarının kasıtlı olarak değiştirilmesi veya yanıltıcı şekilde düzenlenmesi.
    
- **Amaç**: Gerçek olay zaman çizelgesini bozmak, izleri gizlemek.
    
- **Yöntemler**:
    
    - **Manuel Düzenleme**: Yönetici erişimiyle günlük dosyalarına erişip düzenleme (Notepad, Vim gibi araçlarla).
        
    - **Yanıltıcı Kayıt Ekleme**: Sahte günlükler ekleyerek analizi saptırma.
        
    - **İz Silme**: Yetkisiz erişim veya saldırı kayıtlarını silme.
        

### 2. Günlük Silme (Log Deletion)

- **Tanım**: Günlük kayıtlarının tamamen ve geri dönüşsüz silinmesi.
    
- **Amaç**: Etkinlik izlerini yok etmek, tespiti zorlaştırmak.
    

### 3. Otomasyon ve Komut Dosyaları

- **Yöntemler**:
    
    - **Dosya Seçimi**: Komut dosyalarıyla belirli günlük dosyalarını bulma (regex, dosya sistemi komutları).
        
    - **Kayıt Değiştirme/Silme**: Belirli kriterlere uyan kayıtları hedefleme (ör. IP veya kullanıcı adı).
        
    - **Yanıltıcı Veri Ekleme**: Otomatik sahte kayıt ekleme.
        
- **Avantaj**: Manuel düzenlemeden hızlı ve hatasız.
    

### 4. Günlük Rotasyonu ve Yönetimi

- **Tanım**: Günlük dosyalarını yönetmek için tasarlanmış sistem süreci.
    
- **Anti-Adli Kullanım**:
    
    - **Erken Silme**: Rotasyon politikalarını manipüle ederek eski günlükleri hızlıca silme.
        
    - **Sık Rotasyon**: Küçük dosya boyutlarıyla analizi zorlaştırma.
        

### 5. Uzak Sunucu Günlük Yönlendirme

- **Tanım**: Günlüklerin başka bir sunucuya otomatik gönderilmesi.
    
- **Anti-Adli Kullanım**:
    
    - **İz Gizleme**: Yerel günlükleri temizleyip izleri uzak sunucuda saklama.
        
    - **Analizi Zorlaştırma**: Farklı konumda günlük toplama, analistlerin işini karmaşıklaştırır.
        
    - **Erişim Kontrolü**: Uzak günlükleri koruyarak yetkisiz erişimi engelleme.
        

### 6. Günlük Şifreleme

- **Tanım**: Günlük verilerini yetkisiz kullanıcılar için okunamaz hale getirme.
    
- **Anti-Adli Kullanım**:
    
    - **İz Gizleme**: Şifreli günlüklerle etkinlikleri saklama.
        
    - **Analizi Geciktirme**: Şifre çözme gerekliliği analizi yavaşlatır.
        
    - **Erişim Engeli**: Şifre çözme anahtarlarını kontrol ederek analizi önleme.
        

### Tespit ve Önleme Yöntemleri

1. **Manuel Düzenleme**:
    
    - Dosya bütünlüğü izleme (hash tabanlı).
        
    - Ani dosya boyutu/değişiklik tespiti.
        
    - Erişim günlükleri analizi.
        
    - Sıkı erişim kontrolleri ve uyarı sistemleri.
        
    - Günlük şifreleme ve yedekleme.
        
    - Periyodik denetimler.
        
2. **Komut Dosyaları ve Otomasyon**:
    
    - Anormal etkinlik izleme (beklenmedik silmeler, erişimler).
        
    - Güvenlik yazılımları ve davranış analizi.
        
    - Ağ trafiği analizi.
        
    - Sıkı erişim kontrolleri ve antivirüs.
        
    - Davranış tabanlı tespit sistemleri.
        
3. **Yetkisiz Rotasyon**:
    
    - Anormal rotasyon/silme tespiti.
        
    - Erişim ve yapılandırma değişikliklerini izleme.
        
    - Disk alanı/günlük boyutu analizi.
        
    - Standart rotasyon politikaları ve denetimler.
        
    - Güvenli yedekleme ve arşivleme.
        
4. **Uzak Sunucu Yönlendirme**:
    
    - Anormal trafik analizi.
        
    - Yapılandırma değişikliklerini izleme.
        
    - Güçlü erişim kontrolleri ve şifreli iletim.
        
    - Merkezi günlük yönetimi ve düzenli denetimler.
        

### Özet

Günlük manipülasyonu ve silme, adli bilişim incelemelerini zorlaştırır. Günlüklerin bütünlüğünü korumak, şifreleme, sıkı erişim kontrolleri, davranış analizi ve düzenli denetimlerle sağlanır. Bu, güvenlik ihlallerini tespit ve önlemede kritik bir rol oynar.

### PowerShell ile Günlük Silme Komutları

Saldırganlar, PowerShell ile sistem günlüklerini silerek izlerini gizleyebilir. Örnek komutlar:

```bash
# Tüm olay günlüklerini temizler
wevtutil.exe cl System
wevtutil.exe cl Application
wevtutil.exe cl Security

# Belirli bir günlüğü temizler
powershell -command "Clear-EventLog -LogName System"

# Tüm günlükleri toplu temizleme
powershell -command "Get-EventLog -LogName * | ForEach-Object { Clear-EventLog -LogName $_.Log }"
```


### Ekstra Not: PowerShell Komut Geçmişini Görme

PowerShell komut geçmişini kontrol ederek wevtutil.exe gibi komutların çalıştırıldığını tespit edebilirsiniz. Dosya yolu:

```
%USERPROFILE%\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

- **Not**: Bu dosya, kullanıcının PowerShell komut geçmişini içerir ve adli analizde iz takibi için kullanılabilir. PSReadLine modülü etkin olmalıdır.