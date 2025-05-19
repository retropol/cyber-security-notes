# Linux Adli Bilişim Notları: Dosya Sistemi ve İmaj Analizi

Linux sistemlerinde adli bilişim işlemleri sırasında dosya sistemlerini analiz etmek kritik rol oynar. Bu süreçte genellikle **depola aygıtının imajı (görüntüsü)** alınır ve **orijinal veri değiştirilmeden** analiz yapılır.

---

## 🧰 İmaj Oluşturma Araçları

Linux sisteminde gömülü olarak gelen **`dd` komutu**, disk imajı alma işlemleri için temel bir araçtır. Diskin içeriğini **kopyalama** ve **geri yükleme** işlemlerinde kullanılır.

### ✅ Temel Söz Dizimi (Syntax):

```bash
dd if=<source> of=<destination> bs=<block_size> status=progress
```

| Parametre        | Açıklama |
|------------------|----------|
| `if=`            | Giriş dosyası (örnek: /dev/sdb1) |
| `of=`            | Çıktı dosyası (örnek: disk_image.img) |
| `bs=`            | Blok boyutu (örnek: 4M) |
| `status=progress`| Gerçek zamanlı ilerleme bilgisi verir |

### Örnek Komut:

```bash
sudo dd if=/dev/sdb1 of=/path/to/disk_image.img bs=4M status=progress
```

Bu komut `/dev/sdb1` disk bölümünün imajını "disk_image.img" dosyasına **4 MB blok boyutu** ile alır ve işlemi **gerçek zamanlı olarak gösterir**.

---

## 📎 İmaj Dosyası Mount Etme (Bağlama)

İmaj dosyasını bağlayarak (mount ederek) içerdiği dosya sistemine erişebiliriz. Bu işlem **salt okunur (read-only)** modda yapılmalıdır.

### Örnek Komut:

```bash
mount -o ro /tmp/sda1.img /mnt/image
```

Bu komut, `sda1.img` imajını **salt okunur olarak** `/mnt/image` dizinine bağlar.

---

## 🛠️ `dc3dd` Aracı

**`dc3dd`**, `dd` komutunun adli bilişim için geliştirilmiş versiyonudur. Bazı ek özellikleri:

- İlerleme göstergesi
- MD5, SHA-256 gibi **karma (hash) değerleri üretme**
- Aynı anda birden fazla çıktıya yazabilme

---

## 🔐 Hash (Karma) Değeri Hesaplama

İmaj oluşturulduktan sonra, **veri bütünlüğünü sağlamak** için hash değerleri alınmalıdır.

### Güncel ve Güvenli Hash Algoritmaları:
- `SHA-256` → Günümüzde en çok tercih edilen güvenli karma algoritması
- `SHA-1`, `MD5` → Güvenlik açıkları nedeniyle önerilmez

### Örnek Komut:

```bash
sha256sum /tmp/image.img
```

Bu komut, `image.img` dosyasının SHA-256 hash değerini verir. Bu değer daha sonra **bütünlük kontrolü** için kullanılabilir.

---

## 🧯 Silinen Dosyaların Kurtarılması

Linux sisteminde bir dosya silindiğinde, dosya tamamen kaybolmaz. Yalnızca üzerine **yeni veri yazılabilir hale gelir**. Bu yüzden hızlı müdahale ile veri kurtarımı mümkündür.

### Kurtarma Süreci:

1. **Disk imajı alınır** (`dd`, `dc3dd` ile).
2. **Veri kurtarma araçları seçilir**:  
   - `The Sleuth Kit (TSK)`
   - `TestDisk`
   - `PhotoRec`
   - `Foremost`
3. **İmaj analizi yapılır**:  
   - Dosya sistemi tabloları ve **allocation markları** incelenir.
4. **Kurtarılan dosyalar** güvenli bir alana restore edilir.

---

## 🔎 `ext3grep` Aracı (Ext3 Dosya Sistemleri İçin)

`ext3grep`, özellikle **Ext3 dosya sisteminden silinen dosyaları kurtarmak** için tasarlanmıştır. Belirli zamanlara, dosya adlarına veya türlerine göre çalışabilir.

### Kurulum:

```bash
sudo apt install ext3grep
```

### Örnek Kullanım:

```bash
ext3grep --restore-all forensic.dd
```

Bu komut `forensic.dd` adlı imajdan **tüm kurtarılabilir dosyaları** geri getirmeye çalışır.

---

## 🧾 Sistem ve Disk Bilgisi Alma

İmaj dosyasını analiz etmeden önce sistemin yapısı ve disk bilgisi alınmalıdır.

### Komutlar:

```bash
uname -a        # Sistem bilgisi
df -hT          # Disk türü ve kullanım durumu
```

| Komut     | Açıklama                                      |
|-----------|-----------------------------------------------|
| `uname -a` | Sistem çekirdeği, hostname ve mimari bilgisi |
| `df -hT`   | Disk türü, bağlama noktası ve boş alan bilgisi |

---

