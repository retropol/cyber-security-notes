## Şifreleme Teknikleri ve Adli Bilişim

**Şifreleme**, verileri (düz metin) anlaşılmaz biçime (şifreli metin) dönüştürerek sadece yetkili erişimi sağlar. İki tür: **Simetrik** ve **Asimetrik**.

- **Simetrik Şifreleme**: Aynı anahtar kullanılır (ör. AES, DES). Zorluk: Anahtarın güvenli paylaşımı.
    
- **Asimetrik Şifreleme**: public (şifreleme) ve private (çözme) anahtar kullanılır (ör. RSA, ECC). Güvenli iletişim ve dijital imzalarda yaygındır.
    

### Şifreleme Türleri ve Kullanımları

1. **Tam Disk Şifrelemesi**:
    
    - **Kullanım**: Sabit sürücüyü şifreler, çalınma/kayıp durumunda korur.
        
    - **Anti-Adli**: Saldırganlar fidye yazılımıyla verileri şifreler.
        
2. **Dosya Tabanlı Şifreleme**:
    
    - **Kullanım**: Belirli dosya/klasörleri korur.
        
    - **Anti-Adli**: Önemli dosyaları şifreleyip fidye talep eder.
        
3. **Şifreli İletişimler**:
    
    - **Kullanım**: İnternet üzerinden veri gizliliği sağlar.
        
    - **Anti-Adli**: Veri akışını şifreleyip izlemeyi zorlaştırır.
        
4. **Sanal Makine Disk Şifrelemesi**:
    
    - **Kullanım**: Sanal makinelerde veri korur.
        
    - **Anti-Adli**: Diskleri şifreleyip erişimi engeller, izleri siler.
        
5. **Veritabanı Şifrelemesi**:
    
    - **Kullanım**: Veritabanlarını yetkisiz erişime karşı korur.
        
    - **Anti-Adli**: Verileri şifreleyip fidye talep eder.
        

### Fidye Yazılımı

- **Tanım**: Dosyaları asimetrik şifrelemeyle kilitleyip fidye talep eden kötü amaçlı yazılım.
    
- **Amaç**: Maddi kazanç için veri erişimini engelleme.
    

### Özet

Şifreleme, veri güvenliği için vazgeçilmezdir ancak fidye yazılımı gibi kötüye kullanılabilir. Tam disk, dosya, iletişim, sanal makine ve veritabanı şifrelemeleri hem korumada hem anti-adli tekniklerde rol oynar. Etkili şifreleme yönetimi, siber güvenlik için kritik bir stratejidir.