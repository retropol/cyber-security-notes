# 📁 Linux Dosya Sistemleri Karşılaştırma Tablosu 


| Özellik / FS           | ext2                          | ext3                          | ext4                           | Btrfs                          | ReiserFS                       |
|------------------------|-------------------------------|-------------------------------|--------------------------------|--------------------------------|--------------------------------|
| Çıkış Yılı             | 1993                          | 2001                          | 2006                           | 2009                           | 2001                           |
| Günlükleme (Journaling)| Hayır                         | Evet                          | Evet                           | Evet                           | Evet                           |
| Veri Kurtarma Kolaylığı| Yüksek                        | Orta                          | Orta                           | Düşük                          | Orta                           |
| Maks. Dosya Boyutu     | 2 TB                          | 2 TB                          | 16 TB+                         | 16 EB                          | 16 TB                          |
| Maks. Dosya Sistemi    | 32 TB                         | 32 TB                         | 1 EB                           | 16 EB                          | 16 TB                          |
| Performans             | Orta                          | İyi                           | Daha iyi                       | Yüksek                         | Küçük dosyalarda hızlı         |
| Güvenilirlik           | Düşük                         | Orta                          | Yüksek                         | Yüksek                         | Orta                           |
| Öne Çıkan Özellikler   | Basit yapı                    | ext2 + journal                | ext3 + extent desteği          | Snapshot, checksum, RAID desteği | Verimli dizin yapısı           |
| Adli Bilişim Notları   | Kurtarma için en uygun        | Journal veriyi değiştirebilir| Günlükleme veriyi etkileyebilir| Karmaşık yapı, analiz zor      | Artık tercih edilmiyor         |
| Güncel Kullanım Durumu | Az kullanılıyor               | Az kullanılıyor               | Varsayılan olarak yaygın       | Geliştirilmeye devam ediyor    | Kullanımı çok az, eski         |

---

📌 **Notlar:**

- **ext2**, veri kurtarma işlemleri için hâlâ bazı adli bilişim uzmanlarınca tercih edilir çünkü **journal (günlük) sistemi yoktur**, bu da veri üstüne yazılmadığı sürece kurtarılmasını kolaylaştırır.

- **ext3/ext4**, günlükleme özelliği sayesinde sistem çökmelerine karşı dayanıklıdır ama bu, adli analizde bazı orijinal verilerin üzerine yazıldığı anlamına gelebilir.

- **Btrfs**, modern snapshot ve RAID gibi özellikler sunsa da adli analiz için **karmaşık bir yapıya sahiptir**, bu da uzmanlık gerektirir.

- **ReiserFS**, teknik olarak güçlüydü ama artık geliştirilmiyor. Adli bilişim için **önerilmez**.

## Dosya Sistemi Türü ve Boş Alan Görüntüleme

Adli bilişim analizlerinde, sistemde hangi dosya sistemlerinin kullanıldığını ve hangi disklerin ne kadar dolu olduğunu öğrenmek için aşağıdaki komut kullanılır:

```bash
df -hT
```

### Açıklama:

| Parametre | Açıklama                            |
|-----------|-------------------------------------|
| `-h`      | Boyutları insan tarafından okunabilir biçimde gösterir (örnek: MB, GB) |
| `-T`      | Her bağlamanın (mount) dosya sistemi türünü gösterir                    |

### Örnek Çıktı:

```
Filesystem     Type     Size  Used Avail Use% Mounted on
/dev/sda1      ext4      50G   20G   28G  42% /
/dev/sdb1      ntfs     100G   70G   30G  70% /mnt/usb
```

Bu komut sayesinde:
- Hangi disklerin hangi dosya sistemini kullandığını,
- Disklerin ne kadar dolu olduğunu,
- Hangi bağlama noktasında (mount point) bulunduğunu görebilirsin.


