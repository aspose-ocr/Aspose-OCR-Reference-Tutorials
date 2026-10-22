---
category: general
date: 2026-06-19
description: Görsellerden metin çıkarın Python’da basit bir OCR motoru ile. Tarama
  görüntülerini metne dönüştürmeyi, resimlerden metin tanımayı ve Python’da görüntü
  dosyalarını verimli bir şekilde listelemeyi öğrenin.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: tr
og_description: Python'da hafif bir OCR motoru kullanarak görüntülerden metin çıkarın.
  Bu rehber, taranmış görüntüleri metne dönüştürmeyi, fotoğraflardan metin tanımayı
  ve birkaç adımda Python ile görüntü dosyalarını listelemeyi gösterir.
og_title: Python ile Görüntülerden Metin Çıkarma – Tam Batch OCR Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Python ile Görsellerden Metin Çıkarma – Tam Batch OCR Kılavuzu
url: /tr/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Görüntülerden Metin Çıkarma – Tam Batch OCR Kılavuzu

Görüntülerden **metin çıkarmak** istediğiniz ama nereden başlayacağınızı bilemediğiniz oldu mu? Yalnız değilsiniz—geliştiriciler sürekli taranmış PDF'leri, fotoğraflanmış fişleri veya ekran görüntülerini aranabilir metne dönüştürme zorluğuyla karşılaşıyor. Bu öğreticide, **taran görüntüleri metne dönüştürmeyi**, resimlerden metin tanımayı ve hatta **list image files python**‑stilinde görüntü dosyalarını listelemeyi gösteren eksiksiz, çalıştırmaya hazır bir örnek üzerinden ilerleyeceğiz. Sonunda, bir klasörü tek seferde işleyen yeniden kullanılabilir bir betiğe sahip olacaksınız.

İhtiyacınız olan her şeyi ele alacağız: gerekli kütüphaneler, her adımın neden önemli olduğu, kenar‑durum yönetimi ve biraz hata ayıklama. Harici belgelere koşmanıza gerek yok; aşağıdaki kod kendi içinde yeterli ve açıklamalar “nasıl” *ve* “neden” sorularını yanıtlıyor. Sevdiğiniz IDE'yi açın ve hemen işe koyulalım.

---

## Ne Oluşturacaksınız

- Bir OCR motoru başlatın (`ocr` paketini örnek olarak kullanacağız).
- Bir dizini tarayın ve **list image files python**‑stilinde PNG, JPG ve TIFF dosyalarını filtreleyin.
- Bulunan tüm resimler üzerinde bir **batch OCR** işlemi yürütün.
- Her dosya için çıkarılan metni, net bir etiketle yazdırın.

> **Pro ipucu:** `ocr` kütüphaneniz yüklü değilse, birkaç küçük değişiklikle `pytesseract` ile değiştirebilirsiniz—temel mantık aynı kalır.

---

## Önkoşullar

- Python 3.8+ (betik f‑string ve tip ipuçları kullanıyor).
- `OcrEngine` ve `recognize_batch` sağlayan bir OCR kütüphanesi. Bu rehberde hayali bir `ocr` paketi varsayıyoruz, ancak desen gerçek kütüphanelerle de çalışır.
- İşlemek istediğiniz görüntü dosyalarını içeren bir klasör (`.png`, `.jpg`, `.tif`).

---

## Adım 1 – Gerekli Modülleri Kurun ve İçe Aktarın

Öncelikle OCR paketinin mevcut olduğundan emin olun. Gerçek bir kütüphane (ör. `pytesseract`) kullanıyorsanız, içe aktarmayı buna göre değiştirin.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Neden önemli:** `os`'yi içe aktarmak platformlar arası yol yönetimi sağlar, `typing.List` ise IDE otomatik tamamlamasını ve geleceğe dönük uyumluluğu destekler.

---

## Adım 2 – **Extract Text from Images**: OCR Motorunu Başlatın

Motoru oluşturmak, herhangi bir OCR çalışmasının ilk adımıdır. Ayrıca dili otomatik algılayacak şekilde ayarlıyoruz, böylece motor karışık dildeki belgeleri de işleyebilir.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Açıklama:** Motor oluşturmayı bir fonksiyon içinde kapsüllendirerek kodu modüler tutuyoruz. Daha sonra DPI veya OCR modunu ayarlamanız gerekirse, sadece bu noktayı değiştirmeniz yeterli olur.

---

## Adım 3 – **List Image Files Python**: Dizinden Dosyaları Toplayın

Şimdi işlemek istediğimiz her resmi bulmamız gerekiyor. Aşağıdaki liste kavraması, yaygın bir “list image files python” kalıbını yansıtıyor.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Kenar durumu yönetimi:** Fonksiyon alt‑klasörleri yok sayar (daha sonra yineleme ekleyebilirsiniz) ve gizli dosyaları otomatik olarak filtreler; çünkü genellikle desteklenen uzantılarla bitmezler.

---

## Adım 4 – **Convert Scanned Images to Text**: Batch OCR Çalıştırın

Çoğu OCR kütüphanesi, tek tek resim işlemeye göre çok daha hızlı olan bir batch yöntemi sunar. İşte nasıl çağıracağımız:

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Neden batch?** Tüm resimleri bir kerede göndermek, (ör. OCR modelini tekrar tekrar yüklemek) gibi ek yükleri azaltır ve genellikle CPU/GPU kullanımını iyileştirir.

---

## Adım 5 – **Recognize Text from Pictures**: Sonuçları Görüntüleyin

Son olarak, eşleşen dosya adları ve OCR sonuçları üzerinde döngü kurarak her resim için temiz bir başlık yazdırıyoruz.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **İpucu:** `strip()` OCR'nun sıkça eklediği baştaki/sondaki boşlukları temizler.

---

## Tam Betik – Hepsini Bir Araya Getirin

Aşağıda eksiksiz, çalıştırılabilir program yer alıyor. `batch_ocr.py` olarak kaydedin ve `python batch_ocr.py <your_folder>` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Beklenen Çıktı

Klasörün `invoice1.png` ve `receipt.jpg` içerdiğini varsayarsak, şu şekilde bir çıktı görebilirsiniz:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Her blok net bir şekilde etiketlendiği için, sonraki işlem (ör. veritabanına kaydetme) oldukça basittir.

---

## Yaygın Sorunlarla Baş Etme

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **No text appears** | OCR language not detected or image is too low‑contrast. | Force a language (`engine.language = ocr.Language.English`) or preprocess images (increase contrast). |
| **Memory error on large batches** | The engine tries to load all images at once. | Split `image_files` into chunks (`batch_size = 20`) and call `recognize_batch` repeatedly. |
| **Unsupported file format** | You added a `.gif` or `.bmp`. | Extend `supported_exts` tuple or convert images to PNG/JPG beforehand. |
| **Unicode garbling** | OCR returns bytes instead of strings. | Ensure the OCR library outputs Unicode (`result.text.decode('utf‑8')` if needed). |

---

## İş Akışını Genişletme

Artık **extract text from images** yapabildiğinize göre, aşağıdaki adımları değerlendirin:

- **Export to CSV** – Her dosya adını ve çıkarılan metni analiz için bir tabloya yazın.
- **Parallel processing** – `concurrent.futures.ThreadPoolExecutor` kullanarak birden çok batch'i aynı anda işleyin.
- **Integrate with cloud OCR** – Yerel motoru, daha karmaşık düzenlerde yüksek doğruluk sağlayan Google Vision veya Azure OCR ile değiştirin.
- **Add image preprocessing** – Pillow veya OpenCV gibi kütüphaneler, OCR'dan önce görüntüleri eğme, gürültü azaltma veya eşikleme yaparak sonuçları artırabilir.

Bu fikirlerin tümü, oluşturduğumuz aynı temel fonksiyonları kullanır; bu yüzden sıfırdan başlamanıza gerek kalmaz.

---

## Sonuç

Python'da **extract text from images** için eksiksiz bir çözüm üzerinden geçtik; **list image files python**'dan **recognize text from pictures**'a ve sonunda **convert scanned images to text**'a kadar her adımı bir batch içinde ele aldık. Betik kasıtlı olarak basit, ancak daha büyük projeler için (fiş dijitalleştirme, aranabilir arşiv oluşturma veya veri çıkarma hattı) sağlam bir temel sunacak kadar esnek.

Deneyin, ön işleme adımlarını ayarlayın ve OCR doğruluğunuzun yükseldiğini izleyin. Bir sorunla karşılaşırsanız, “Handling Common Pitfalls” tablosuna göz atın; çoğu sorun küçük bir yapılandırma değişikliğiyle çözülür.

Bir sonraki meydan okumaya hazır mısınız? `pdf2image` kullanarak PDF‑to‑image dönüşüm adımı ekleyin, ardından bu görüntüleri aynı boru hattına besleyin. OCR ile Python ekosisteminin zengin araçlarını birleştirdiğinizde sınır yoktur.

İyi kodlamalar, ve metniniz her zaman okunabilir olsun!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}