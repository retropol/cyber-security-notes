# Basit Windows Memory Dump Analizi

## Basit Analizler

Aşağıdaki komut ile Windows'a özel plugin’ler hakkında bilgi alabiliriz:

```bash
python vol.py --help | findstr windows
```

Ayrıca `CertUtil` komutu ile hash değerini alarak döküm dosyasının doğruluğunu kontrol edebiliriz:

```bash
CertUtil -hashfile .\mimi.mem MD5
```

## Process of Memory Dump Analysis

A basic "Windows Memory Dump Analysis" should include below steps:

- Image Identification
- Processes and Threads
- Network Connections
- Registry Analysis
- File Analysis
- Malware Analysis
- Service Analysis

---

## 1. Process Analizi

```bash
python.exe .\vol.py -f ..\mimi.mem windows.pslist
```

Bu komut, sistemde çalışan işlemleri ve işlem çocuklarını gösterir. Şüpheli işlemler tespit edilebilir.

Volatility 3 ile şu plugin’ler de kullanılabilir:
- `windows.pslist`
- `windows.pstree`
- `windows.psscan`

![pslist output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_4.png)

---

## 2. Ağ Aktiviteleri

```bash
python.exe .\vol.py -f ..\mimi.mem windows.netscan
```

Sistem üzerinde anlık ağ bağlantılarını listeler. Command & Control bağlantılarını tespit etmekte faydalıdır.

### IP Filtreleme Örneği

```bash
python.exe .\vol.py -f ..\mimi.mem windows.netscan | findstr "172.16.8.132"
```

![netscan output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_5.png)

---

## 3. Kayıt Defteri Analizi

```bash
python.exe .\vol.py -f ..\memdump.mem windows.registry.hivelist
```

RAM'de bulunan kayıt defteri hive’larını listeler.

![registry output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_7.png)

### Önemli Anahtarlar

- **Run keys:** Otomatik başlatılan programlar  
  `HKLM\Software\Microsoft\Windows\CurrentVersion\Run`  
  `HKCU\Software\Microsoft\Windows\CurrentVersion\Run`

- **Services:** Sistem servisleri ve driver'lar  
  `HKLM\System\CurrentControlSet\Services`

- **Shell extensions:** Sistem kabuğuna eklenen öğeler  
  `HKLM\Software\Microsoft\Windows\CurrentVersion\Shell Extensions`

- **Mounted devices:** Takılı cihaz kayıtları  
  `HKLM\System\MountedDevices`

- **UserAssist Keys:** Kullanıcıların çalıştırdığı uygulamalar  
  `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`

---

## 4. Dosya Analizi

```bash
python.exe .\vol.py -f ..\memdump.mem windows.filescan
```

RAM’de bulunan geçici veya silinmiş dosyaları gösterir. Zararlıların bıraktığı izler tespit edilebilir.

![filescan output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_8.png)

---

## 5. YARA ile Malware Taraması

```bash
python.exe .\vol.py -f ..\memdump.mem yarascan.YaraScan --yara-file .\yara\search_mimikatz.yar
```

Bellek içinde kötü amaçlı yazılım aramak için kullanılır. `windows.vmayarascan` eklentisi ile birlikte kullanılır.

![yara output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_10.png)

---

## 6. Servis Analizi

```bash
python.exe .\vol.py -f ..\mimi.mem windows.svcscan
```

Çalışan hizmetleri listeler. Zararlı hizmetlerin davranışı bu şekilde analiz edilebilir.

![svcscan output](https://ld-images-2.s3.us-east-2.amazonaws.com/Windows+Memory+Forensics/image4_11.png)

### Analiz Edilmesi Gereken Hususlar

- **Anormal davranış:** `SERVICE_SYSTEM_START` yerine `SERVICE_DEMAND_START` gibi değişiklikler.
- **Beklenmeyen Durumlar:** Güvenlikle ilgili servislerin `SERVICE_STOPPED` durumda olması.
- **Anormal hizmet türleri:** `SERVICE_KERNEL_DRIVER`, `SERVICE_FILE_SYSTEM_DRIVER` gibi kritik hizmetlerde beklenmedik isimler.
- **Şüpheli adlar:** `Netmaan` gibi taklit hizmet isimleri.
- **Geçersiz yollar:** Sistem dışındaki yollardan çalışan servis dosyaları.
- **Olağandışı hizmetler:** Sistemin normal durumuyla karşılaştırarak fark edilen yeni servisler.

---
