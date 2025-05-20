# Bellek Dump Analizi

## 📌 Neden Önemli?

- Bellek dökümü, adli bilişim ve sistem sorun giderme süreçlerinde kritik bir rol oynar.
    
- Çalışan işlemler, oturumlar, ağ bağlantıları ve potansiyel zararlı yazılımlar hakkında bilgi verir.
    

## 🛠️ Kullanılan Araçlar

### **Volatility**

- Açık kaynaklı bir bellek analiz framework’üdür.
    
- Geniş OS ve dump formatı desteği vardır.
    
- Kullanıcı aktivitesi, malware analizi gibi birçok analiz yapılabilir.
    

### **Rekall**

- Volatility’ye benzer açık kaynaklı başka bir analiz aracıdır.
    
- Ayrıntılı dump analizi sağlar.
    

### **Belkasoft Evidence Center**

- Dijital delil analizi platformudur.
    
- Bellek dökümleri dahil birçok dijital veriyi inceleyebilir.


**Biz bu yazıda votailty3 aracını kullanacağız.** 

## 🔍 Volatility 3 Yapısı

### **1. Memory Layers**

- Fiziksel bellek, sanal bellek gibi farklı bellek katmanları ile çalışır.
    
- Bellek yapılarının soyutlanmasını sağlar.
    

### **2. Templates ve Objects**

- **Templates**: Bellekteki veri yapılarının şeması.
    
- **Objects**: Bu şemaya göre oluşturulan gerçek veriler.
    

### **3. Symbol Tables**

- OS çekirdek yapılarının ve işlevlerinin adres ve yapı bilgilerini içerir.
    
- Volatility, dump dosyasını doğru şekilde yorumlamak için bu sembolleri kullanır.



# 🧠 Volatility3 Komutları - Bellek Dökümü Analizi

Volatility3, bellek dökümünden sistem, kullanıcı ve zararlı yazılım izlerini analiz etmek için kullanılan güçlü bir araçtır. Aşağıda en sık kullanılan ve diğer yardımcı komutları görebilirsin.

---

## 📌 En Çok Kullanılan Volatility3 Komutları

| Komut Açıklaması                                     | Komut Satırı                                      |
| ---------------------------------------------------- | ------------------------------------------------- |
| Sistem bilgilerini gösterir                          | `python vol.py -f <memory_dump> windows.info`     |
| Kullanıcı hash’lerini alır (SAM)                     | `python vol.py -f <memory_dump> windows.hashdump` |
| Çalışan işlemleri listeler                           | `python vol.py -f <memory_dump> windows.pslist`   |
| DLL dosyalarını listeler                             | `python vol.py -f <memory_dump> windows.dlllist`  |
| Zararlı kod barındırabilecek bellek alanlarını bulur | `python vol.py -f <memory_dump> windows.malfind`  |
| İşlem ağacını gösterir (parent/child ilişkileri)     | `python vol.py -f <memory_dump> windows.pstree`   |
| Komut satırı argümanlarını gösterir                  | `python vol.py -f <memory_dump> windows.cmdline`  |
| Ağ bağlantılarını listeler                           | `python vol.py -f <memory_dump> windows.netscan`  |

> 📌 `<memory_dump>` kısmına analiz etmek istediğin bellek döküm dosyasının yolu yazılır.(ftk image tool'u ile alabilriiz önceki yazıda yazıldığı gibi)

---

## 🔍 Diğer Faydalı Volatility3 Komutları

### 🔧 Sürücü ve Kernel Bilgisi

- Sistem sürücülerini taramak için:
  ```bash
  python vol.py -f <memory_dump> windows.driverscan
  ```

- Yüklü sürücü modüllerini listelemek için:
  ```bash
  python vol.py -f <memory_dump> windows.drivermodule
  ```

- Kernel modüllerini listelemek için:
  ```bash
  python vol.py -f <memory_dump> windows.modules
  ```

---

### 💀 Gizli veya Silinmiş Süreçler

- Silinmiş/gizli işlemleri (terminated processes) bulmak için:
  ```bash
  python vol.py -f <memory_dump> windows.psscan
  ```

---

### 🧠 Kayıt Defteri Analizi

- Kayıt defteri hive’larını listelemek için:
  ```bash
  python vol.py -f <memory_dump> windows.registry.hivelist
  ```

- Kayıt defteri hive’larını taramak için:
  ```bash
  python vol.py -f <memory_dump> windows.registry.hivescan
  ```

---

### 🧪 YARA ile Bellek Taraması

- YARA kurallarıyla bellek taramak için:
  ```bash
  python vol.py -f <memory_dump> yarascan.YaraScan --yara-rules "/path/to/yara_rules.yar"
  ```

---


