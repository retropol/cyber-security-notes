## Bellek Dökümü Alma (Memory Dump)

### 🔧 Kullanılan Araç: **AccessData FTK Imager**

Bellek dökümü (RAM dump), dijital adli analizde sistemin anlık durumunu kaydetmek için kullanılır. FTK Imager, kullanıcı dostu arayüzü ile bellek dökümü almak için en çok tercih edilen araçlardan biridir.

### 📌 Popüler Bellek Dökümü Araçları

| Araç Adı                      | Açıklama                                                                                 |
| ----------------------------- | ---------------------------------------------------------------------------------------- |
| **WinDbg**                    | Microsoft tarafından geliştirilmiş, detaylı hata ayıklama ve dump analizi sağlar.        |
| **Volatility Framework**      | Açık kaynaklı, RAM dump üzerinde çalışan plugin tabanlı analiz framework'ü.              |
| **Magnet RAM Capture**        | Hızlı, verimli ve kullanıcı dostu bir bellek döküm aracı.                                |
| **Belkasoft Evidence Center** | Geniş kapsamlı dijital adli analiz aracı; bellek dosyalarını da analiz edebilir.         |
| **FTK Imager**                | Disk görüntüleme ve RAM dump alma özellikleriyle bilinir.                                |
| **Rekall**                    | Volatility’nin gelişmiş ve fork edilmiş bir sürümü; daha derin analiz yetenekleri sunar. |
| **MemDump**                   | Komut satırından çalışan, RAM içeriğini hızlıca ham formatta döken araç.                 |

---

## 💡 Bellek Dökümünün Adli Analizde Önemi

RAM dump, sistemin o anki anlık görüntüsünü sunduğu için birçok kritik veriyi içinde barındırır:

- 🧩 **Çalışan Programlar ve Süreçler:** Aktif işlemler ve olası kötü amaçlı yazılımlar.
    
- 💥 **Sistem Hataları:** Hatalı kod, sürücü uyumsuzlukları, bellek sızıntıları.
    
- 🌐 **Ağ Bağlantıları:** Açık portlar ve dış IP bağlantıları.
    
- 👤 **Kullanıcı Oturum Bilgileri:** Giriş zamanları, erişilen dosyalar.
    
- 🔐 **Şifreleme Anahtarları ve Hassas Bilgiler:** Bellekte kalan şifreler, oturum token'ları.
    
- 🦠 **Zararlı Yazılım Analizi:** Bellekte gizlenen ya da yalnızca RAM’de çalışan zararlılar.
    

---

## 🛠️ FTK Imager ile Bellek Dökümü Alma Adımları

1. **Uygulamayı Açın:** `AccessData FTK Imager`
    
2. **Menüden Seçin:** `File` > `Capture Memory`
    
3. **Pagefile Dahil Et:** "Include Pagefile" seçeneği ile `C:\pagefile.sys` dosyasını da dahil ederek sanal RAM'i de dahil edebilirsiniz.
    

> 📸 Görsel:  
> ![FTK Imager Memory Capture](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image2_2.png)

---

## ✅ Sonuç

Bellek dökümü, dijital olay müdahalesinde olay anının fotoğrafını çeker. Bu sayede kötü amaçlı yazılımlar, kullanıcı davranışları ve sistem hataları analiz edilebilir. FTK Imager gibi araçlar, adli bilişim uzmanlarına kapsamlı bir RAM inceleme altyapısı sunar. Özellikle pagefile gibi ek bileşenlerin dahil edilmesi, analiz derinliğini artırır.