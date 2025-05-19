# 🐧 Linux Sistem Dosyaları – Dijital Adli Analiz
## `.ssh/authorized_keys`
- **Ne işe yarar?**: SSH üzerinden kimlerin bağlanabileceğini belirleyen public key'leri içerir.
- **Adli analizde neden önemli?**
  - ❗ **Yetkisiz Erişim Tespiti**: Tanınmayan key varsa, sistem ele geçirilmiş olabilir.
  - 🔐 **Güvenlik Durumu Analizi**: Eski/zaaflı algoritmalarla oluşturulmuş key'ler güvenlik riski oluşturur.
  - ⚠️ **Kötü Amaçlı Kullanım**: Saldırganlar, uzaktan erişim için kendi key’lerini ekleyebilir.
- **Formatı:**
  ```text
  <key_type> <key_value> <comment>
  ```
  Örn: `ssh-rsa AAAAB3Nza... attacker@example.com`

---

## `.bashrc`
- **Ne işe yarar?**: Her terminal oturumunda otomatik çalışan kullanıcı özel ayarları içerir.
- **Adli analizde neden önemli?**
  - 🧠 **Kullanıcı Davranışı**: Kullanıcının tanımladığı alias, fonksiyon vs. alışkanlıklarını yansıtır.
  - ⚙️ **Otomatik Komutlar**: Açılışta çalışan script’ler analiz edilir.
  - 🐍 **Zararlı Yazılımlar**: Saldırganlar kalıcılık sağlamak için buraya zararlı komutlar ekleyebilir.
  - 🕒 **Zaman Tespiti**: Dosyanın son erişim/modifikasyon zamanı kullanıcı etkinliklerini gösterir.
- **Kullanışlı Komutlar:**
  ```bash
  cat ~/.bashrc             # içeriği gösterir
  ls -la ~/.bashrc          # tarih bilgisi
  ```

---

## `systemd` ve `.service` Dosyaları
- **Nedir?**: Modern Linux sistemlerinin başlatma ve servis yönetim sistemidir.
- **Adli analizde neden önemli?**
  - 🔍 **Servis Durumu**: Başlayan, çalışan veya otomatik başlatılan servisler gözlemlenir.
  - 📆 **Zamanlama Analizi**: Servis ne zaman başlamış, otomatik mi çalışıyor gibi detaylar öğrenilir.
- **Faydalı Komutlar:**
  ```bash
  systemctl status                       # tüm servis durumları
  systemctl list-units --type=service   # aktif servisler
  journalctl -u <servis-adı>            # belirli servis log’ları
  ```

---

## `/tmp` ve `/var/tmp`
- **Nedir?**: Geçici dosyaların tutulduğu dizinlerdir. Yazma izinleri genelde daha rahattır.
- **Adli analizde neden önemli?**
  - 🐚 **Zararlı Script’ler**: Saldırganlar genellikle buraya shell script’ler veya tool’lar bırakır.
  - 🕵️ **Zaman, boyut, içerik analizi** yapılabilir.
- **Faydalı Komutlar:**
  ```bash
  ls -lart /tmp                        # zamana göre listele
  find /tmp -name '*.sh'              # belirli uzantıdaki dosyaları bul
  grep -R "malicious_code" /tmp       # içeriğe göre arama yap
  find /tmp -mtime -2                 # son 2 günde değişen dosyalar
  find /tmp -size +10M                # 10MB'dan büyük dosyalar
  find /tmp -type f -perm -o=w        # herkes tarafından yazılabilir dosyalar
  ```

---

## 📌 Genel Özet:
Linux sisteminde adli analiz yapılırken, özellikle aşağıdaki dosya ve klasörler kritik önem taşır:
- `.ssh/authorized_keys`: SSH erişimlerinin kontrolü
- `.bashrc`: Otomatik çalışan komutlar ve kullanıcı davranışları
- `systemd` servisleri: Sistem başlangıcı ve çalışan servisler
- `/tmp`, `/var/tmp`: Geçici dizinlerde bırakılan kötü niyetli dosyalar

Her biri, potansiyel güvenlik ihlalleri ve saldırı izlerini ortaya çıkarmada kullanılır.
