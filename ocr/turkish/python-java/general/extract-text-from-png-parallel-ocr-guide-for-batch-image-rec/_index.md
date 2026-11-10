---
category: general
date: 2026-03-18
description: Python ve Aspose OCR kullanarak PNG'den metin çıkarın. OCR için görüntüyü
  nasıl yükleyeceğinizi, birden fazla dosyada OCR çalıştırmayı ve paralel görüntü
  tanıma ile toplu OCR görüntülerine ulaşmayı öğrenin.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: tr
og_description: Python'da Aspose OCR ile PNG'den metin çıkarın. Bu öğreticide OCR
  için görüntünün nasıl yükleneceği, birden fazla dosyanın OCR işlemi ve paralel görüntü
  tanıma kullanarak toplu OCR görüntülerinin nasıl çalıştırılacağı gösterilmektedir.
og_title: PNG'den Metin Çıkar – Paralel OCR Rehberi
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: PNG'den Metin Çıkarma – Toplu Görüntü Tanıma için Paralel OCR Rehberi
url: /tr/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkarma – Toplu Görüntü Tanıma için Paralel OCR Rehberi

PNG dosyalarından **metin çıkarmak** gerektiğinde, tek bir görüntünün işlenmesinin sonsuza kadar sürmesiyle takılıp kaldınız mı? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—fatura tarayıcıları, fiş dijitalleştiricileri veya arşivleme araçları gibi—hız önemlidir ve her PNG'yi tek tek işlemek yeterli olmaz.  

Bu rehberde, **OCR için görüntü yükler**, **ocr multiple files**'ı **batch OCR images** biçiminde çalıştırır ve Python'un `threading` modülüyle **paralel görüntü tanıma**yı kullanır bir tam, çalıştırmaya hazır çözümü adım adım inceleyeceğiz. Sonunda, PNG'lerden metni saniyeler içinde, dakikalar yerine çeken bir betiğe sahip olacaksınız.

## Gereksinimler

- Python 3.8 ve üzeri (gösterilen sözdizimi 3.10+’da da çalışır).  
- Java/​Python için Aspose OCR paketi (`aspose-ocr`). `pip` ile kurabilirsiniz.  
- İşlemek istediğiniz birkaç PNG dosyasının bulunduğu bir klasör.  
- Makul miktarda RAM—her iş parçacığı küçük bir OCR motoru örneği tutar, bu yüzden bir dizüstü bilgisayar bile onlarca çalışan başlatabilir.

Harici hizmetler, bulut anahtarları veya gizemli yapılandırma dosyaları yok. Sadece kopyalayıp‑yapıştırıp çalıştırabileceğiniz saf Python kodu.

## Neden PNG'den metni paralel olarak çıkaralım?

Bir PNG işlemek CPU‑ağırlıklıdır: OCR motoru, piksel verilerini işleyen bir dizi görüntü‑analiz algoritması çalıştırır. On, yirmi ya da yüz görüntünüz olduğunda, toplam çalışma süresi temelde her bir çalışmanın toplamına eşittir.  

Her dosya için bir iş parçacığı oluşturduğumuzda, işletim sisteminin bu CPU‑yoğun görevleri eşzamanlı olarak planlamasına izin veririz. Çok çekirdekli bir makinede bu, duvar‑saat süresini genellikle yarıya—hatta çeyreğe—indirir. Dezavantajı biraz daha yüksek bellek kullanımıdır, ancak çoğu toplu iş için hız kazancı buna değerdir.

> **Pro ipucu:** Yüzlerce megabayt görüntüyle çalışıyorsanız, `threading` yerine `concurrent.futures.ProcessPoolExecutor` kullanmayı düşünün. İşlemler, GIL‑bağlı CPython yorumlayıcısında gerçek paralellik sağlar, ancak biraz daha fazla ek yük maliyeti vardır.

## Adım 1: Aspose OCR for Python'ı Kurun

İlk iş olarak—OCR kütüphanesini sisteminize alalım.

```bash
pip install aspose-ocr
```

Bu tek satır, en son Aspose OCR ikili dosyalarını ve Python bağlamalarını çeker. İzin hatası alırsanız, `--user` eklemeyi veya bir sanal ortam kullanmayı deneyin.

## Adım 2: OCR için Görüntüyü Yükle – İşçi Fonksiyonu

Şimdi her iş parçacığında çalıştırılacak temel rutini tanımlıyoruz. Bu, **OCR için görüntüyü yükler**, tanıma işlemini yürütür ve çıkarılan metnin bir önizlemesini yazdırır.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Birkaç dikkat edilmesi gereken nokta:

- **Neden her iş parçacığı için yeni bir `OcrEngine`?** Motor, iç tamponlar tutar; tek bir örnek paylaşmak yarış koşullarına ve bozuk çıktıya neden olur.  
- **Neden satır sonlarını temizliyoruz?** Konsola kaydederken satırı düzenli tutar.  
- **Hata yönetimi?** Üretimde gövdeyi bir `try/except` bloğuna alır ve belki bir dosyaya kaydedersiniz—daha sonra ele alacağımız bir konu.

## Adım 3: İşlemek istediğiniz PNG dosyalarını listeleyin

Listeyi sabit kodlayabilirsiniz, ancak daha esnek bir yaklaşım bir dizini taramaktır. Aşağıda açıklık için üç dosyayı manuel olarak listeliyoruz; yolları kendi klasörünüzle değiştirin.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Otomatik keşfi tercih ederseniz:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Bu küçük ayar, **PNG dosyalarından metin çıkarmanıza** her seferinde kaynak kodunu dokunmadan toplu olarak izin verir.

## Adım 4: batch OCR images ile ocr multiple files'i ayarlayın

Şimdi her görüntü için bir iş parçacığı oluşturuyoruz. Bu, **batch OCR images** deseninin kalbidir.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

Liste kavraması kodu özlü tutar ve her `Thread` nesnesi hedef fonksiyonu ve argümanını (`image_path`) saklar.  

> **Not:** Python'un `threading` modülü yerel OS iş parçacıklarını kullanır, bu yüzden 4‑çekirdekli bir dizüstü bilgisayarda genellikle aynı anda dört iş parçacığının gerçekten çalıştığını görürsünüz; geri kalanlar çekirdekler boşaldıkça planlanır.

## Adım 5: Paralel görüntü tanımını çalıştırın

İşçileri başlatmak basittir: listeyi yineleyin ve `start()` çağırın. Ardından `join()` kullanarak her iş parçacığının bitmesini bekleriz.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Betik tamamlandığında, aşağıdaki gibi bir dizi satır görürsünüz:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Bu çıktı, her PNG'nin işlendiğini ve çıkarılan metnin daha sonraki işlemler için (örneğin bir veritabanına kaydetme veya bir NLP hattına besleme) kullanılabilir olduğunu onaylar.

## Adım 6: Sonuçları doğrulayın ve kenar durumlarını yönetin

### Boş sonuçları kontrol etme

Bazen bir görüntü çok gürültülüdür veya OCR motoru hiçbir karakter algılayamaz. Hızlı bir mantık kontrolü, sonraki hatalardan sizi koruyabilir.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Eşzamanlı iş parçacığı sayısını sınırlama

Bunu mütevazı bir VM'de çalıştırıyorsanız, yüzlerce iş parçacığı oluşturmak zamanlayıcıyı zorlayabilir. Bir semafor ile eşzamanlılığı sınırlayabilirsiniz:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Sonuçları bir dosyaya kaydetme

Yazdırmak yerine, dosya adı ve çıkarılan metni içeren bir CSV isteyebilirsiniz:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

CSV'yi **tek sefer** iş parçacığı fonksiyonunun dışında açtığınızdan emin olun, böylece yarış koşullarından kaçınırsınız; `csv` modülünün yazıcısı basit yazmalar için iş parçacığı‑güvenlidir.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `batch_ocr.py` adlı bir dosyaya koyup çalıştırabileceğiniz tek bir betik:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}