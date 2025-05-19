# Linux Konfigürasyon Dosyaları

## `/etc/passwd`

Bu dosya sistem kullanıcıları hakkında basit detayları içerir: kullanıcı adı, home directory, varsayılan shell gibi bilgiler bulunur.

Bu dosyayı inceleyerek:

- Yetkisiz hesaplar eklenmiş mi kontrol edebiliriz.
- Zararlı hesapların sistem aktivitelerini inceleyerek sistemde ne yaptıklarını anlayabiliriz.
- Kullanıcının ana dizinini ve varsayılan shell’ini görebildiğimiz için sistemle nasıl etkileşime geçtiğini anlayabiliriz.

### Dosya Yapısı:

```text
username:x:user_id:group_id:real_name:user_home_directory:user_shell
```

**Alanlar:**

- **username:** Kullanıcının giriş yaptığı isim
- **x:** Şifrelenmiş parolanın yerini tutan karakter. Gerçek şifre `/etc/shadow` dosyasında tutulur.
- **user_id (UID):** Her kullanıcı için benzersiz tanım. Root için genellikle `0` olur.
- **group_id (GID):** Kullanıcının birincil grubunun ID’si.
- **real_name:** Kullanıcı hakkında açıklama (isteğe bağlı).
- **user_home_directory:** Kullanıcının ana dizini.
- **user_shell:** Kullanıcının kullandığı komut satırı arayüzü.

---

## `/etc/shadow`

Bu dosyada kullanıcıların hash’lenmiş parolaları tutulur. Sadece root erişebilir.

### Güvenlik Analizi:

- **Şifre Güvenlik Analizi:** Zayıf veya varsayılan şifreler güvenlik açığı oluşturabilir.
- **Karma Kırma Girişimleri:** Saldırganlar parola hash’lerini kırmaya çalışabilir.
- **Hesap Durumu:** Devre dışı bırakılmış, süresi dolmuş veya kilitlenmiş hesaplar gözlemlenebilir.
- **Yetkisiz Erişim:** Dosyada beklenmeyen değişiklikler kalıcı erişim girişimlerini gösterebilir.

### Dosya Yapısı:

```text
username:password_hash:time:minimum:maximum:warning:inactivity:expiration_date
```

**Alanlar:**

- **username:** Kullanıcının adı
- **password_hash:** Şifrelenmiş parola (hash)
- **time:** Son parola değişim tarihi (1970'ten bu yana gün sayısı)
- **minimum:** Şifre değişimi için minimum gün
- **maximum:** Şifrenin geçerli olduğu maksimum gün
- **warning:** Şifre bitmeden önceki uyarı günü
- **inactivity:** İnaktif hale gelmeden önceki gün sayısı
- **expiration_date:** Hesabın sona ereceği gün

---

## `/etc/group`

Sistemdeki grupları ve grup üyelerini listeler. Her grubun farklı yetkileri olabilir.

### Analiz Noktaları:

- **Yetkisiz Grup Atamaları:** Saldırganlar kendini ayrıcalıklı gruplara ekleyebilir.
- **Grup Tabanlı Erişim Kontrolü:** Kimlerin hangi kaynaklara erişebildiğini incelemek için önemlidir.

### Dosya Yapısı:

```text
group_name:x:group_id:group_members
```

**Alanlar:**

- **group_name:** Grubun adı
- **x:** Eski grup şifre alanı, genelde `x`
- **group_id (GID):** Grubun tanımlayıcı numarası
- **group_members:** Virgülle ayrılmış kullanıcı listesi

---

## `/etc/sudoers`

Kullanıcıların veya grupların `sudo` komutunu kullanarak hangi komutları root yetkisiyle çalıştırabileceğini tanımlar.

### Güvenlik İncelemesi:

- **Yetkilendirme Politikaları:** Sistem üzerindeki izinleri ve rollerin dağılımını analiz eder.
- **Yetkisiz sudo Yetkilendirmeleri:** Saldırganların veya kullanıcıların yetkilerini artırıp artırmadığını anlamak için incelenir.

---

## `/etc/crontab`

Sistemde zamanlanmış görevleri tanımlar. Belirli zamanlarda çalışacak otomatik komutları içerir.

### Güvenlik İncelemesi:

- **Kötü Amaçlı Görevler:** Saldırganlar gizli cron görevleri ekleyebilir.
- **Otomatik Faaliyetler:** Sistem üzerinde yapılan otomatik değişiklikleri gözlemlememizi sağlar.
- **Arka Kapılar:** Cron ile kalıcı arka kapılar yerleştirilebilir.

### Dosya Yapısı:

```text
SHELL=/bin/sh
PATH=/usr/bin:/bin

minute hour day month username command
```

**Zamanlama Alanları:**

- **dakika:** 0-59
- **saat:** 0-23
- **ayın günü:** 1-31
- **ay:** 1-12 veya isim
- **haftanın günü:** 0-6 (Pazar: 0 veya 7)
- **kullanıcı_adı:** Hangi kullanıcı adına çalıştırılacağı
- **komut:** Çalıştırılacak komut veya script
