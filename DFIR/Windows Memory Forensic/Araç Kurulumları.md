
#  Araç Kurulumları ve Kullanımı

## 1. AccessData FTK Imager
- Bellek dökümü (memory dump) almak için kullanılır.
- Kullanımı kolay ve adli bilişimde sıkça tercih edilir.

## 2. Volatility3
- Bellek dökümünü analiz etmek için kullanılır.
- Olay müdahalesi ve siber analizlerde güçlü bir araçtır.

---

##  Volatility3 Kullanımı İçin Gerekli Kurulumlar

### 1. Python 3.11 Kurulumu
Volatility3, Python 3.11 ile sorunsuz çalışır. Bu nedenle ilk olarak bu sürüm kurulur.

🔗 [Python 3.11 İndir](https://www.python.org/downloads/release/python-3110/)

---

### 2. Snappy Modülünün Kurulumu
Volatility bazı işlemler için `python-snappy` modülüne ihtiyaç duyar. Kurulumu şu şekilde yapılır:

```
pip install python-snappy
```
