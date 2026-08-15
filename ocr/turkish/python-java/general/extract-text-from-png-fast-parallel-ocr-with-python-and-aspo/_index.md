---
category: general
date: 2026-03-28
description: Aspose OCR'ı Python'da kullanarak PNG'den hızlıca metin çıkarın. Yüksek
  performanslı sonuçlar için paralel görüntü tanıma Python ile taranmış sayfaların
  metnini dönüştürmeyi öğrenin.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: tr
og_description: Python'da Aspose OCR kullanarak PNG'den metni hızlıca çıkarın. Bu
  rehber, taranmış sayfaların metnini paralel görüntü tanıma Python'u ile nasıl dönüştüreceğinizi
  gösterir ve yüksek hızlı sonuçlar sunar.
og_title: PNG'den Metin Çıkar – Python ile Hızlı Paralel OCR
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: PNG'den Metin Çıkar – Python ve Aspose ile Hızlı Paralel OCR
url: /tr/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkarma – Python ile Hızlı Paralel OCR

PNG dosyalarından **PNG'den metin çıkarma** gerektiğinde tek‑iş parçacıklı OCR'un acı verici derecede yavaş olduğunu gördünüz mü? Yalnız değilsiniz. İster taranmış makbuz yığınını dijitalleştiriyor olun, ister ders slaytlarını aranabilir PDF'lere dönüştürüyor olun, darboğaz genellikle OCR adımıdır.  

Bu öğreticide, Aspose OCR'un asenkron toplu modunu Python'un `ThreadPoolExecutor`'ı ile birlikte kullanarak **tarama sayfalarının metnini dönüştürür** paralel olarak, eksiksiz, çalıştırmaya hazır bir çözüm göstereceğiz. Sonuna kadar **görüntü metnini python tarzında tanır**‑stilinde tanıma yapabilecek, onlarca görüntüyü naif bir döngünün alacağı sürenin bir kısmında işleyebileceksiniz.

> **Neler Öğreneceksiniz**  
> * PNG görüntülerinden metni eşzamanlı olarak çıkaran tam işlevsel bir betik.  
> * Asenkron toplu modunun neden daha hızlı olduğunu anlama.  
> * Çözümü daha büyük iş yüklerine ölçeklendirmek için ipuçları.

## Gereksinimler

| Önkoşul | Sebep |
|--------------|--------|
| Python 3.9+ | Modern sözdizimi ve tip ipuçları. |
| `aspose-ocr` and `aspose-storage` packages | OCR motorunu ve görüntü yükleyiciyi sağlar. |
| PNG dosyalarının bulunduğu bir klasör (örn., taranmış sayfalar) | İşlemek istediğiniz kaynak materyal. |
| Python eşzamanlılığı hakkında temel bilgi | Yararlı ancak zorunlu değil; her şeyi açıklayacağız. |

Aspose kütüphanelerini şu şekilde kurabilirsiniz:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro ipucu:** Paketlerinizi güncel tutun (`pip list --outdated`) böylece en son performans iyileştirmelerinden faydalanabilirsiniz.

## Adım 1: Aspose OCR Motorunu Asenkron Toplu Modda Başlatma

İlk olarak bir `OcrEngine` örneği oluşturur ve **asenkron toplu mod**'a geçiririz. Bu mod, tanıma isteklerini dahili olarak kuyruğa alır ve motorun birden fazla görüntüyü Python iş parçacığınızı engellemeden işlemesine olanak tanır.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Why async?*  
Senkron modda `recognize` çağrısı yaptığınızda, çağrı görüntü tamamen işlenene kadar bloklanır. Asenkron modda ise motor, mevcut görüntü hâlâ çözülürken bir sonraki görüntü üzerinde çalışmaya başlayabilir; böylece I/O ve CPU işleri etkili bir şekilde üst üste biner.

## Adım 2: İşlemek İstediğiniz PNG Dosyalarını Listeleyin

Burada görüntü koleksiyonunu tanımlıyoruz. Gerçek bir projede bu listeyi dinamik olarak oluşturabilirsiniz (örn., `glob.glob("*.png")`), ancak açık tutmak örneği takip etmeyi kolaylaştırır.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Not:** `YOUR_DIRECTORY` ifadesini PNG taramalarınızın bulunduğu gerçek yol ile değiştirin. Yüzlerce dosyanız varsa, `os.listdir` kullanıp `.png` için filtrelemeyi düşünün.

## Adım 3: Görüntüyü Yükleyen ve Metnini Döndüren Yardımcı Fonksiyonu Yazın

Yardımcı, **Aspose Storage** aracılığıyla bir dosyayı yükleme ve ardından OCR motoruna besleme iki adımlı sürecini soyutlar. Küçük bir docstring eklemek fonksiyonu kendi kendini belgeleyen hâle getirir—gelecek bakım için faydalıdır.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Why a separate function?*  
Bu, thread‑pool kodunu temiz tutar ve mantığı başka yerlerde (örn., bir Flask uç noktasında) yeniden kullanmamıza izin verir. Ayrıca, I/O'yu izole etmek hata ayıklamayı kolaylaştırır—belirli bir dosya başarısız olursa, istisna izinde dosya adını göreceksiniz.

## Adım 4: Thread Pool ile Paralel Görüntü Tanıma Python'u Çalıştırın

Şimdi `ThreadPoolExecutor`'ı getiriyoruz. Varsayılan olarak dört işçi başlatılır, ancak `max_workers` değerini CPU çekirdeklerinize ve görüntü setinizin boyutuna göre ayarlayabilirsiniz.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Bu, Paralel Görüntü Tanıma Python'u Nasıl Sağlar

* **ThreadPoolExecutor**, her biri `recognize_image` çağıran bir işçi iş parçacığı havuzu oluşturur.  
* OCR motoru asenkron toplu modda olduğu için, her iş parçacığı motora işi devredebilir ve hâlâ yanıt verebilir.  
* `as_completed`, tamamlandıkları sıraya göre future'ları döndürür, böylece sonuçları hazır olduğunda hemen alırsınız—büyük toplu işlemleri akışa almak için mükemmeldir.

> **Yaygın tuzak:** `max_workers=1` kullanmak paralellik amacını boşa çıkarır. 8‑çekirdekli bir makinede, `max_workers=8` genellikle en iyi verimi verir, ancak donanımınız için en uygun değeri bulmak üzere birkaç değer deneyin.

## Adım 5: Çıktıyı Doğrulayın ve Kenar Durumlarını Ele Alın

Betik çalıştırıldığında, her PNG için dosya adıyla ön eklenmiş bir metin bloğu görmelisiniz:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Herhangi bir görüntü başarısız olursa (bozuk dosya, desteklenmeyen format), `except` bloğu tüm toplu işlemi çökertmek yerine yardımcı bir hata mesajı yazdırır.

### Çözümü Genişletmek

| Senaryo | Önerilen ayar |
|----------|-----------------|
| **Binlerce sayfa** | `ProcessPoolExecutor`'a geçerek birden fazla CPU sürecinden yararlanın veya listeyi parçalayarak toplu işlemleri sıralı olarak işleyin. |
| **Farklı görüntü formatları (JPG, TIFF)** | `storage.Image.load` yöntemi formatı otomatik algılar, bu yüzden dosyaları `input_images`'a eklemeniz yeterlidir. |
| **Sonuçları depolama ihtiyacı** | `text`'i bir `.txt` dosyasına yazın veya `else` bloğu içinde bir veritabanına ekleyin. |
| **Performans izleme** | `recognize_image`'ı bir zamanlayıcı (`time.perf_counter`) ile sarın ve dosya başına süreyi kaydedin. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda `parallel_ocr.py` adlı bir dosyaya koymaya hazır tam betik yer alıyor. Hiçbir parça eksik değil—gereken her şey burada.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Dosyayı kaydedin, `YOUR_DIRECTORY` yer tutucusunu ayarlayın ve çalıştırın:

```bash
python parallel_ocr.py
```

Her PNG için çıkarılan metnin konsolda göründüğünü, daha önce gösterildiği gibi, görmelisiniz.

## Sonuç

Aspose OCR'un asenkron toplu modunu Python'un `ThreadPoolExecutor`'ı ile birleştirerek **PNG dosyalarından metin çıkarma**nın verimli bir yolunu gösterdik. Betik, tarama sayfalarının metnini paralel olarak dönüştürür ve **görüntü metnini python tarzında tanıma** için sıfırdan özel bir thread‑pool yazmadan ölçeklenebilir bir yöntem sunar.  

Bunu daha da ileriye taşımaya hazırsanız, şunları deneyin:

* Sonuçları aranabilir bir SQLite veritabanında depolamak.  
* OCR'dan önce OpenCV ile görüntü ön işleme (eğik düzeltme, gürültü giderme) eklemek.  
* Betiği bir Flask veya FastAPI uç noktasının arkasında mikro hizmet olarak dağıtmak.

Unutmayın, yüksek performanslı OCR'ın anahtarı sadece daha hızlı bir motor olmak değil; aynı zamanda motoru, eşzamanlılığı en üst düzeye çıkaracak şekilde beslemektir. Burada gösterilen desenle, kodda minimal değişiklikle onlarca hatta yüzlerce PNG taramasını işleyebilirsiniz.

Kodlamaktan keyif alın, ve PDF'leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}