---
category: general
date: 2026-03-26
description: Python kullanarak toplu OCR'ı verimli bir şekilde nasıl yapabilirsiniz—görüntülerden
  ve PDF'lerden metin çıkarma, paralel işleme ile OCR dönüşümünü öğrenin.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: tr
og_description: OCR'ı toplu olarak verimli bir şekilde nasıl yapabilirsiniz—görsellerden
  metin çıkarma, PDF OCR dönüşümü ve Python kullanarak toplu OCR işleme için adım
  adım rehber.
og_title: 'Toplu OCR Nasıl Yapılır: Hızlı Paralel Metin Çıkarma'
tags:
- OCR
- Python
- Parallel Computing
title: 'OCR''yi toplu işleme: hızlı paralel metin çıkarımı'
url: /tr/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# toplu ocr nasıl yapılır: hızlı paralel metin çıkarma

Hiç **toplu ocr nasıl yapılır** diye merak ettiniz mi, etrafta onlarca taranmış sayfa, ekran görüntüsü ve PDF'ler varken? Tek tek her dosyayı işlemek, çoğu geliştiricinin aynı duvara çarpması gibi, acı verici bir darboğaz haline geliyor.  

İyi haber şu ki, birkaç işçi iş parçacığı başlatabilir, onlara tüm dosyalarınızı verebilir ve OCR motorunun toplu işi paralel olarak işlediğini izleyebilirsiniz. Bu öğreticide, **görüntülerden metin çıkarma**, **pdf ocr dönüşümü** ve **paralel ocr işleme** hızını gösteren eksiksiz, çalıştırmaya hazır bir örnek üzerinden adım adım ilerleyeceğiz.

> **Neler Öğreneceksiniz**  
> * Tek seferde PNG, TIFF, PDF ve JPG dosyalarının karışık bir listesini işleyen tam işlevsel bir Python betiği.  
> * Bir iş parçacığı havuzunun I/O‑bağlantılı OCR görevlerini neden hızlandırdığını anlama.  
> * Hataları, büyük PDF'leri ve özel iş parçacığı sayısını yönetme ipuçları.  

## Önkoşullar

Başlamadan önce, şunların olduğundan emin olun:

| Gereksinim | Sebep |
|-------------|--------|
| Python 3.8+ | Modern sözdizimi & `concurrent.futures` |
| `ocr` kütüphanesi (veya uyumlu herhangi bir OCR sarmalayıcı) | `OcrBatchProcessor` ve sonuç nesnelerini sağlar |
| Bir avuç örnek dosya (PNG, TIFF, PDF, JPG) | **görüntülerden metin çıkarma** işlemini görmek için |
| İş parçacıklarıyla temel aşinalık (isteğe bağlı) | Yararlı ancak zorunlu değil |

Henüz `ocr` paketini kurmadıysanız, şu komutu çalıştırın:

```bash
pip install ocr-lib   # replace with the actual package name
```

Ortam hazır olduğuna göre, problemi adım adım inceleyelim.

## Adım 1: Yardımcıları içe aktar ve toplu işlemciyi oluştur

İlk olarak, tüm OCR görevlerini toplamak için bir yere ihtiyacımız var. `OcrBatchProcessor` sınıfı tam da bunu yapar—çalışma öğelerini kuyruğa ekler ve size bir `Future` nesnesi listesi döndürür.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Neden önemli*: `as_completed`'i içe aktarmak, en yavaş dosyayı beklemek yerine her tamamlanan işe anında yanıt vermemizi sağlar. Bu, **toplu ocr işleme**'nin özüdür.

## Adım 2: Paralel yürütme için işçi havuzunu ayarla

Varsayılan olarak işlemci tek bir iş parçacığı kullanabilir, bu da toplu işlemenin amacını bozar. Biz açıkça dört işçi istiyoruz—bu sayıyı sahip olduğunuz CPU çekirdek sayısına kadar artırabilirsiniz.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*İpucu*: OCR gibi I/O‑bağlantılı görevlerde, `CPU cores * 2` değerinden sonra getiriler azalır. Birkaç değeri test edin ve en uygun olanı seçin.

## Adım 3: OCR yapmak istediğiniz her dosyayı kuyruğa ekleyin

Burada karışık bir görüntü ve PDF dosyası seti ekliyoruz. `add` metodu sadece yolu kaydeder; gerçek iş, toplu işlemi gönderene kadar başlamaz.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Tüm bir klasörü işlemek istiyorsanız, hızlı bir `glob` döngüsü işe yarar:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Adım 4: İşleri başlat ve future'ları topla

`submit_all` çağrısı işlemciye yeşil ışığı verir. Bu, `Future` nesnelerinden oluşan bir liste döndürür—bunları daha sonra ortaya çıkacak sonuçların yer tutucuları olarak düşünün.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

Bu noktada OCR motoru arka planda meşgul, her iş parçacığı bir dosya üzerinde çalışıyor.

## Adım 5: Sonuçları bitirildiği anda alın

`as_completed` kullanarak future'ları bitiş sırasına göre, gönderim sırasına göre değil, yineleyebiliriz. Bu, betiğimizin yanıt vermesini sağlar, özellikle bazı PDF'ler basit PNG'lerden daha uzun sürdüğünde.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Beklenen çıktı** (kısaltılmıştır):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Her blok, orijinal dosyanın düz‑metin temsilini içerir. **pdf ocr dönüşümü** yapıyorsanız, metin OCR motorunun her sayfadan çözebildiği her şeyi içerecektir.

## Kenar Durumları ve Yaygın Tuzakların Ele Alınması

| Durum | Dikkat edilmesi gereken | Hızlı çözüm |
|-----------|-------------------|-----------|
| Bozuk bir görüntü | `future.result()` `OSError` hatası verir | `try/except` ile sarın (yukarıdaki koda bakın) |
| Çok büyük PDF'ler ( > 100 MB ) | Bellek baskısı, daha yavaş iş parçacıkları | `thread_count` değerini makul şekilde artırın veya PDF'yi önce bölümlere ayırın |
| Karışık dil belgeleri | Varsayılan OCR modeli yanlış algılayabilir | Kütüphane destekliyorsa `OcrBatchProcessor`'a dil ipuçları gönderin |
| Düzeni koruma ihtiyacı | Düz `get_text()` sütunları kaybeder | `ocr_result.get_hocr()` veya benzeri düzen‑duyarlı yöntemi kullanın |

### İpucu: Dosya tipine göre özel iş parçacığı sayısı

Çoğu iş yükünüzün PDF olduğunu biliyorsanız, bunlar için daha fazla iş parçacığı, küçük PNG'ler için daha az iş parçacığı ayırabilirsiniz. Bazı kütüphaneler her iş için `priority` parametresi almanıza izin verir; aksi takdirde iki ayrı toplu işlem oluşturabilirsiniz—biri görüntüler, diğeri PDF'ler için—ve bunları aynı anda çalıştırabilirsiniz.

## Görsel Genel Bakış (isteğe bağlı)

![toplu ocr iş akışı diyagramı](https://example.com/ocr-workflow.png "toplu ocr iş akışı")

*Diyagram, dosya keşfinden → toplu oluşturma → paralel yürütme → sonuç birleştirme akışını gösterir.*

## Kopyala‑Yapıştırabileceğiniz Tam Betik

Aşağıda, bir `.py` dosyasına eklemeye hazır tam program yer alıyor. Yukarıdaki tüm kod parçacıklarını ve bir dizindeki desteklenen dosyaları otomatik olarak keşfeden küçük bir yardımcıyı içerir.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

`batch_ocr.py` olarak kaydedin, taramalarınızı içeren bir klasöre yönlendirin ve konsolun çıkarılan metinle dolduğunu izleyin.  

### Neden Bu Çalışıyor

* **Thread pool** – OCR çoğunlukla disk I/O ve dış motor çağrılarını beklediği için, birden fazla iş parçacığı CPU'yu meşgul tutar.  
* **`as_completed`** – Sonuçları hazır olur olmaz alırsınız, bu UI geri bildirimi veya akış hatları için idealdir.  
* **Error isolation** – Tek bir hatalı dosya tüm toplu işlemi düşürmez; `try/except` bloğu hataları izole eder.

## Sonuç

Özetle, artık Python’un `concurrent.futures`'ını ve toplu işleme destekleyen bir OCR kütüphanesini kullanarak **toplu ocr nasıl yapılır** biliyorsunuz. Makul bir iş parçacığı havuzu yapılandırarak, desteklenen her dosyayı kuyruğa ekleyip sonuçları bitirildikçe alarak, güvenilirliği kaybetmeden hızlı **paralel ocr işleme** elde edersiniz.  

Bundan sonra şunları yapabilirsiniz:

* Çıktıyı hızlı belge getirme için bir arama indeksine bağlayın.  
* Betik'i, her sonucu orijinalin yanına bir `.txt` dosyası olarak yazacak şekilde genişletin.  
* OCR kütüphaneniz async API'ler sunuyorsa, yerleşik iş parçacığı havuzunu `asyncio` ile değiştirin.  

Denemeye devam edin—Tesseract, Azure Cognitive Services veya Google Vision'ı değiştirin, aynı desenin uygulandığını göreceksiniz. İyi OCR'lamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}