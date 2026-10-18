---
category: general
date: 2026-06-22
description: Python toplu OCR öğreticisi, Tesseract ve pathlib kullanarak PNG görüntülerden
  oluşan bir klasörde çok iş parçacıklı OCR nasıl çalıştırılır gösterir. Python’da
  hızlı toplu görüntü OCR’ını öğrenin.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: tr
og_description: Python toplu OCR öğreticisi, çoklu iş parçacıkları kullanarak Tesseract
  ile birçok PNG'yi işleyen eksiksiz, çalıştırılabilir bir betiği adım adım gösterir.
og_title: Python toplu OCR öğreticisi – PNG Görüntüler için Hızlı Çok İşlemcili OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Python toplu OCR öğretici: Birden çok PNG''yi verimli şekilde işleyin'
url: /tr/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# python batch ocr tutorial – PNG Görüntüleri için Hızlı Çoklu İşlemci OCR

Ever wondered how to **python batch ocr tutorial** your way through hundreds of PNG screenshots without watching your CPU melt? You're not the only one. Whether you're digitizing scanned forms, extracting text from receipts, or building a searchable archive, a solid batch OCR pipeline saves you hours.

Bu rehberde, bir klasördeki tüm `*.png` dosyalarını toplayan, bunları çoklu iş parçacıklı bir işlemci aracılığıyla Tesseract'a yönlendiren ve düz metin sonuçlarını düzenli bir çıktı dizinine bırakan küçük ama güçlü bir betik oluşturacağız. Gizemli kütüphaneler yok—sadece `pathlib`, `concurrent.futures` ve her zaman güvenilir `pytesseract`. Sonunda, **python batch ocr tutorial**'ı herhangi bir projeye kopyala‑yapıştır yapabileceğiniz bir hâle getireceksiniz.

## Öğrenecekleriniz

- **pathlib image handling** ile görüntü dosyalarını nasıl toplarsınız  
- **multithreaded OCR in Python** işçi havuzunu nasıl kurarsınız  
- **OCR thread count optimization** ayarlarını CPU çekirdekleriniz için nasıl ayarlarsınız  
- Her sonucu daha sonraki arama için net bir adlandırma şemasıyla kaydetmek  
- Tüm süreci tek, bağımsız bir betik olarak çalıştırmak  

## Önkoşullar (İhtiyacınız Olanlar)

| Gereksinim | Neden Önemli |
|------------|--------------|
| Python 3.9+ | Modern sözdizimi (`pathlib`, f‑strings) |
| Tesseract 5.x kurulu ve `PATH` içinde erişilebilir | `pytesseract`'ın arkasındaki OCR motoru |
| `pytesseract` (`pip install pytesseract`) | Tesseract için Python sarmalayıcısı |
| `Pillow` (`pip install pillow`) | Tesseract için görüntü yükleme |
| İşlemek istediğiniz PNG dosyalarının bulunduğu klasör | Bizim **tesseract OCR batch processing** hedefimiz |

> **Pro ipucu:** Windows kullanıyorsanız, `C:\Program Files\Tesseract-OCR` yolunu sistem `PATH`'inize ekleyin, böylece `pytesseract` yürütülebilir dosyayı otomatik olarak bulabilir.

---

## Adım 1 – Tüm PNG Görüntülerini Topla (pathlib Kullanarak)

First things first: we need a list of every image we plan to run OCR on. `pathlib` makes this a one‑liner and keeps the code OS‑agnostic.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Why `pathlib`?* It abstracts away Windows backslashes vs. Unix slashes, letting the same script run everywhere. This is the cornerstone of **pathlib image handling** in our tutorial.

*Neden `pathlib`?* Windows ters eğik çizgileri ile Unix eğik çizgilerini soyutlayarak aynı betiğin her yerde çalışmasını sağlar. Bu, eğitimimizdeki **pathlib image handling**'in temel taşıdır.

## Adım 2 – Basit Bir Toplu OCR İşlemci Sınıfı Tanımla

Below is a lightweight wrapper that hides the threading boilerplate. It mirrors the pseudo‑code you saw earlier but is fully functional.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Ana seçimlerin açıklaması**

- **ThreadPoolExecutor** dosyaları okuma ve harici Tesseract ikili dosyasını çağırma gibi I/O‑ağır görevler için gerçek çoklu iş parçacığı sağlar.  
- `set_thread_count` yöntemi, **OCR thread count optimization** ile deney yapabileceğiniz yerdir; daha fazla iş parçacığı genellikle CPU çekirdekleriniz doygunlaşana kadar daha hızlı veri akışı anlamına gelir.  
- Her görüntü, orijinal PNG'nin adıyla bir `.txt` dosyası üretir—daha sonraki indeksleme veya arama için mükemmeldir.

## Adım 3 – Her Şeyi Birleştir

Now we instantiate the processor, tweak the thread count, point it at our output folder, and finally hand it the list of images.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

Running the script will produce output similar to:

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Each `.txt` contains the raw OCR output. Open any file and you’ll see the extracted text ready for indexing, sentiment analysis, or whatever comes next.

## Adım 4 – Yaygın Tuzaklar ve Nasıl Kaçınılır

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Boş `.txt` dosyaları | Tesseract dil verilerini bulamıyor veya görüntü çok karanlık | Dil paketlerini (`tesseract-ocr-eng`) kurun ve görüntüleri ön işleyin (kontrastı artırın). |
| `UnicodeDecodeError` sonuçları okurken | Çıktı UTF-8 olmayan karakterler içeriyor | Dosyaları `encoding="utf-8"` ile yazın (kodda zaten) veya hızlı bir geçici çözüm için `errors="ignore"` kullanın. |
| CPU dalgalanmaları, hız artışı yok | İş parçacığı sayısı fiziksel çekirdekleri aşıyor | `set_thread_count` değerini `os.cpu_count()` ya da daha düşük bir değere indirin. |
| Görüntü açarken `FileNotFoundError` | Yol Windows'ta ASCII olmayan karakterler içeriyor | Dizgenin başına `r` ekleyin veya doğrudan `pathlib` nesnelerini kullanın (bizim yaptığımız gibi). |

## Adım 5 – Eğitimi Genişletmek (İleri Adımlar)

- OpenCV (`cv2`) ile **görüntü ön işleme** ekleyerek OCR doğruluğunu artırın (ör. eğikliği düzeltme, eşikleme).  
- `multiprocessing` veya RabbitMQ gibi basit bir görev kuyruğu kullanarak **makinelere yayarak paralelleştirin** büyük iş yükleri için.  
- Çıkarılan metni gerçek zamanlı olarak aranabilir kılmak için **bir arama motoru** (Elasticsearch) ile bütünleştirin.  
- El yazısı metinlerde daha yüksek doğruluk gerekiyorsa **Tesseract'ı bir bulut OCR API'si** (Google Vision, Azure Computer Vision) ile değiştirin.

All of these ideas build on the foundation you now have: a clean, **python batch ocr tutorial** that works out of the box.

## Sonuç

You’ve just built a complete **python batch ocr tutorial** that:

1. **Collects** every PNG with **pathlib image handling**. → **pathlib image handling** ile her PNG'yi toplar.  
2. **Spins up** a **multithreaded OCR in Python** worker pool. → **multithreaded OCR in Python** işçi havuzunu başlatır.  
3. **Optimizes** the number of threads for your hardware (**OCR thread count optimization**). → Donanımınız için iş parçacığı sayısını (**OCR thread count optimization**) optimize eder.  
4. **Writes** each result to a dedicated folder (**tesseract OCR batch processing**). → Her sonucu ayrı bir klasöre (**tesseract OCR batch processing**) yazar.  

The script is ready to drop into any pipeline, whether you’re processing receipts, legal documents, or a mountain of screenshots. Play with the thread count, throw in image pre‑processing, or hook the output into a database—your choice.

Got questions? Feel free to comment below, and happy coding!

![Paralel olarak birden çok PNG dosyasını işleyen python batch ocr tutorial iş akışı diyagramı](/images/python-batch-ocr-workflow.png){.center width=600 alt="python batch ocr tutorial iş akışı"}

---


## Sonraki Öğrenmeniz Gerekenler?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR Eğitimi – Optik Karakter Tanıma](/ocr/english/)
- [.NET için Aspose.OCR'da Liste ile Toplu OCR Görüntüleri Nasıl Yapılır](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Aspose.OCR kullanarak dil seçimiyle C# görüntü metni çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}