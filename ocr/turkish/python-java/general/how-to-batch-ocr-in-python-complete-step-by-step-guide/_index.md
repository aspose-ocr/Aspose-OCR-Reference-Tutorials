---
category: general
date: 2026-06-28
description: Python kullanarak toplu OCR nasıl yapılır. Birden fazla resmi OCR'lamayı,
  PNG'den metin çıkarmayı ve tam bir Python OCR öğreticisiyle görüntüyü metne dönüştürmeyi
  öğrenin.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: tr
og_description: Python'da toplu OCR nasıl yapılır, ilk cümlede açıklanmıştır. PNG
  dosyalarından metni verimli bir şekilde çıkarmak için bu Python OCR öğreticisini
  izleyin.
og_title: Python'da Toplu OCR Nasıl Yapılır – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python'da Toplu OCR Nasıl Yapılır – Tam Adım Adım Rehber
url: /tr/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Toplu OCR Nasıl Yapılır – Tam Adım‑Adım Kılavuz

Hiç **toplu OCR**'un bir yığın taranmış sayfayı UI'nizi engelleyen bir döngü yazmadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Onlarca PNG dosyasını tek tek işlemek, özellikle her görüntünün çözülmesi bir iki saniye sürüyorsa, boyanın kurumasını izlemek gibi hissettirebilir.  

Bu öğreticide, **birden fazla görüntüyü aynı anda OCR**'lamak, **PNG dosyalarından metin çıkarmak** ve **görüntüyü metne dönüştürmek** için temiz, engellemeyen bir yol göstereceğiz. Sonunda, herhangi bir projeye bırakabileceğiniz, hızlı bir *python ocr tutorial* ya da üretim‑düzeyinde bir toplu iş için mükemmel, çalıştırmaya hazır bir betiğiniz olacak.

## Oluşturacağınız Şey

- Bir OCR motoru başlatın ve dilini Latin (veya ihtiyacınız olan herhangi bir dil) olarak ayarlayın.  
- Motoru, örnek olarak PNG dosyalarının bir listesini besleyin.  
- Bir Future‑benzeri nesne döndüren bir toplu işlem başlatın.  
- Ana iş parçacığınızı serbest tutarak, bir thread havuzu ile tüm sonuçları eşzamanlı olarak alın.  
- Her sayfa için tanınan metni güzel bir şekilde ayrılmış olarak yazdırın.

Gizli bir sihir yok, sadece saf Python ve üçüncü‑taraf bir OCR kütüphanesi (örnek olarak hayali `pyocr` paketini kullanacağız).

**Prerequisites**  
- Python 3.8+ yüklü.  
- Python fonksiyonları ve `concurrent.futures` hakkında temel bilgi.  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesine erişim (ör. `pip install pyocr`).  

Eğer bunlardan birini eksikse, hemen edinin – düşündüğünüzden çok daha kolay.

---

## Python'da Toplu OCR Nasıl Yapılır – Temel Kavramlar

Kod yazmaya başlamadan önce, her adımın “neden”ini açıklayalım.

1. **Dil neden ayarlanır?**  
   OCR doğruluğu, motorun hangi karakterleri bekleyeceğini bildiğinde büyük ölçüde artar. Latin, İngilizce, Fransızca, İspanyolca vb. diller için çalışır. Gerekirse `Language.Japanese` ya da `Language.Arabic` gibi bir dile geçin.

2. **Toplu işlem neden kullanılır?**  
   Bir toplu çağrı, motorun işi dahili olarak zamanlamasını sağlar, genellikle yerel iş parçacıkları ya da GPU hızlandırmasından faydalanır. Daha sonra sorgulayabileceğiniz bir tutamaç döndürür, böylece her görüntü işlenirken bloklanmazsınız.

3. **ThreadPoolExecutor neden?**  
   Aldığımız Future nesnesi *tembel*dir – sadece sonuçları istediğimizde çekmeye başlar. `getAll`'a bir thread havuzu vererek, Python'un her sayfanın metnini paralel olarak almasını sağlarız ve toplam çalışma süresini büyük ölçüde kısarız.

4. **Sonuçlar neden enumerate ile döndürülür?**  
   Sonuçların sırası, giriş yollarının sırasıyla eşleşir, bu yüzden her sayfa numarasını güvenle etiketleyebiliriz.

Bu “neden” noktalarını anlamak, deseni diğer kütüphanelere ya da daha büyük veri setlerine uyarlamanıza yardımcı olur.

---

## Adım 1: Gerekli Paketleri Kurun ve İçe Aktarın

Öncelikle OCR kütüphanesinin kurulu olduğundan emin olun. Örnek, genel bir `pyocr` paketi kullanıyor; tercih ettiğiniz gerçek kütüphane ile değiştirin (örn. `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Şimdi ihtiyacımız olan her şeyi içe aktaralım.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** `pathlib`'ten `Path` kullanmak, betiğinizi OS‑bağımsız ve okunması daha kolay hâle getirir.

---

## Adım 2: OCR Motorunu Oluşturun ve Dili Ayarlayın

Motoru oluşturmak oldukça basittir. Bu demo için Latin diline kilitleyeceğiz.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

`setLanguage` çağrısı bazı motorlar için isteğe bağlıdır, ancak iyi bir alışkanlıktır. OCR modeline, ilgilendiğiniz karakter setine odaklanmasını söyler; bu da hem hızı hem de doğruluğu artırır.

---

## Adım 3: İşlenecek Görüntü Dosyalarını Listeleyin (Extract Text from PNG)

Dönüştürmek istediğiniz tüm PNG dosyalarını toplayın. `Path.glob` kullanmak, betiği düzenlemeden bir klasörü tamamen içine atabilmenizi sağlar.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Neden önemli:** Listeyi sıralayarak deterministik bir sıra garantileyebiliriz; bu da daha sonra her sonucu doğru sayfa numarasıyla eşleştirir.

---

## Adım 4: Toplu OCR İşlemini Başlatın (Convert Image to Text)

Şimdi listeyi motora veriyoruz. Metod, daha sonra sorgulayacağımız bir Future‑benzeri konteyner döndürür.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Motorun altında kendi iş parçacıklarını ya da bir GPU hattını başlatıyor olabilir. Tek ihtiyacımız, bireysel sonuçları nasıl alacağını bilen bir tutamaç (`batch_future`) elde etmek.

---

## Adım 5: Tüm Sonuçları Eşzamanlı Olarak Alın (OCR Multiple Images)

İşte işi gerçekten *toplu* hâle getirdiğimiz yer. `getAll`'a bir `ThreadPoolExecutor` vererek, her sayfanın metni kendi iş parçacığında çekilir.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

`max_workers` değerini CPU çekirdek sayınıza ya da OCR kütüphanesinin önerilerine göre ayarlayabilirsiniz. Daha fazla işçi ≠ her zaman daha hızlı – CPU kullanımınızı izleyin.

---

## Adım 6: Tanınan Metni Çıktılayın (Python OCR Tutorial Finale)

Son olarak, her sayfanın metnini yazdıralım. `Result` nesnesi `getText()` metodunu sunar – kütüphaneniz farklı bir metod adı kullanıyorsa ona göre ayarlayın.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Beklenen çıktı (örnek)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Bir görüntü başarısız olursa, çoğu motor boş bir string döndürür ya da bir istisna fırlatır – döngüyü bir `try/except` bloğuna sararak kenar durumlarını nazikçe ele alabilirsiniz.

---

## Tam Script – Çalıştırmaya Hazır

Aşağıda eksiksiz, bağımsız bir script yer alıyor. `batch_ocr.py` adlı bir dosyaya kopyalayıp yapıştırın, `YOUR_DIRECTORY`'yi ayarlayın ve `python batch_ocr.py` komutunu çalıştırın.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Kaydedin, çalıştırın ve konsolun çıkarılan metinle dolduğunu izleyin. Basit, hızlı ve tamamen asenkron.

---

## Yaygın Tuzaklar & Nasıl Önlenir

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **No output** – empty strings | OCR motoru hiçbir metin bulamadı (görüntü çok gürültülü) | Görüntüleri ön‑işleyin: ikilileştirme, eğriltme düzeltme veya DPI artırma |
| **FileNotFoundError** | Yanlış klasör yolu ya da eksik PNG dosyaları | `YOUR_DIRECTORY`'yi iki kez kontrol edin ve dosyaların `.png` ile bittiğinden emin olun |
| **High CPU usage** | `max_workers` makineniz için çok yüksek ayarlandı | `max_workers` değerini azaltın veya destekleniyorsa GPU hızlandırmasını etkinleştirin |
| **Unicode garble** | Motor varsayılan olarak farklı bir dil kullandı | Batch OCR'dan önce `engine.setLanguage(Language.Latin)` (veya uygun dili) çağırın |

Bu sorunları erken ele almak saatlerce hata ayıklamaktan sizi kurtarır.

---

## Öğreticiyi Genişletmek – Sonraki Adımlar

- **OCR multiple images** diğer formatlarda (JPEG, TIFF) – sadece glob desenini değiştirin.  
- **Extract text from PNG** ve bunu bir arama indeksi (örn. Elasticsearch) içine besleyin.  
- **Convert image to text** PDF oluşturmak için `reportlab` ya da `PyPDF2` kullanın.  
- **Parallelize across machines** `multiprocessing` ya da Celery gibi bir görev kuyruğu ile büyük veri setleri için ölçeklendirin.  

Bu konuların her biri, az önce tamamladığınız **python ocr tutorial** üzerine doğal bir şekilde inşa edilir.

---

## Sonuç

**Toplu OCR**'un bir PNG koleksiyonunda nasıl yapılacağını adım adım gösterdik, toplu‑yönelimli bir API'nin gücünü sergiledik ve bir thread‑havuzlu yaklaşımla **PNG'den metin çıkarmayı** gösterdik. Yukarıdaki tam script üretim‑hazırdır ve artık OCR‑ağır Python projeleriniz için sağlam bir temele sahipsiniz.

Biraz oynayın, dil ayarlarını değiştirin ve belki `pyocr` yerine `pytesseract` kullanın – desen aynı kalır. Sorularınız mı var ya da ilginç bir kullanım senaryosu paylaşmak mı istiyorsunuz? Yorum bırakın, sohbeti sürdürelim.

*İyi kodlamalar!*

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakın ilişkili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}