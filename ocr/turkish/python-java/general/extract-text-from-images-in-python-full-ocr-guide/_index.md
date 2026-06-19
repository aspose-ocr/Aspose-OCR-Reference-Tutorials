---
category: general
date: 2026-06-19
description: Python OCR kullanarak görüntülerden metin çıkarın. Otomatik dil algılama,
  paralel işleme ve toplu tanıma konularını kısa bir öğreticide öğrenin.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: tr
og_description: Python OCR ile görüntülerden metin çıkarın. Bu rehber, otomatik dil
  algılamayı, paralel işleme ve toplu tanıma işlemlerini tek bir öğreticide gösterir.
og_title: Python'da Görüntülerden Metin Çıkarma – Tam OCR Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python'da Görüntülerden Metin Çıkarma – Tam OCR Rehberi
url: /tr/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da Görüntülerden Metin Çıkarma – Tam OCR Rehberi

Hiç **görüntülerden metin çıkarmayı** manuel olarak her kelimeyi yazarak yapmayı düşündünüz mü? Tek başınıza değilsiniz. İster eski makbuzları dijitalleştiriyor olun, ister aranabilir bir belge arşivi oluşturuyor olun, ya da sadece havalı AI numaralarıyla oynuyor olun, resimlerden metin çekebilmek günümüz Python geliştiricileri için vazgeçilmez bir yetenek.

Bu öğreticide, popüler bir OCR motoru kullanarak **görüntülerden metin çıkaran** tam çalışır bir örnek üzerinden adım adım ilerleyeceğiz. Otomatik dil algılamayı, hız için paralel işleme ve toplu görüntü tanımını ele alacağız; böylece onlarca dosyayı saniyeler içinde işleyebileceksiniz. Aradığınız şey bu mu? Hadi başlayalım.

## Öğrenecekleriniz

- `ocr.OcrEngine` ile OCR motorunu nasıl başlatacağınızı.
- Motorun kendi kendine doğru dili seçmesi için **otomatik dil algılamayı** nasıl etkinleştireceğinizi.
- Özel bir iş parçacığı havuzu ile **paralel işleme OCR** yapılandırmasını.
- Dosya listesi üzerinde **toplu görüntü tanımını** nasıl çalıştıracağınızı.
- Her görüntü için tanınan metni yazdırarak kaydetmeye veya indekslemeye hazır hale getirmeyi.

Harici bir dokümantasyona ihtiyaç yok—gereken her şey burada ve kod `ocr` paketiyle (kurulum: `pip install ocr`) kutudan çıkar çıkmaz çalışıyor.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

1. Python 3.8 veya daha yeni bir sürüm.
2. `ocr` paketi (`pip install ocr`).
3. İşlemek istediğiniz PNG (veya JPG) görüntülerin bulunduğu bir klasör.
4. Python fonksiyonları ve döngülerine temel aşinalık.

Hepsi bu—ağır bağımlılıklar, GPU sihri yok, sadece saf Python.

![extract text from images example](https://example.com/ocr-demo.png "Screenshot showing extract text from images output")

*Alt metin: görüntülerden metin çıkarma demosu ekran görüntüsü*

## Adım 1 – OCR Motorunu Kurun (Anahtar Kelime Eylemde)

İlk iş: bir OCR motoru örneği oluşturun. `ocr.OcrEngine()` düşünün; bu, işlemin beynidir; karakterleri, satırları ve paragrafları nasıl okuyacağını bilir.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Neden açık bir motor örneğine ihtiyaç duyuyoruz? Çünkü **ocr.OcrEngine kullanımı** dil ayarları, iş parçacığı yönetimi ve daha fazlası üzerinde ince ayar yapmanıza olanak tanır. Tek satırlık yardımcı fonksiyonlara göre **görüntülerden metin çıkarma** konusunda en esnek yoldur.

## Adım 2 – Motorun Dilleri Otomatik Olarak Algılamasını Sağlayın

Çoğu OCR kütüphanesi hangi dili arayacağını sizden ister. Tek dilli bir proje için bu sorun olmaz, ancak karışık dilli bir toplu işlemde zahmetlidir. Neyse ki, `ocr` paketi **otomatik dil algılamayı** destekler.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

`engine.language` değerini `ocr.Language.Auto` olarak ayarlamak, motorun her görüntüyü koklayıp uygun dil modelini seçmesini sağlar. Bu küçük satır, uluslararası belgelerle uğraşırken saatler süren manuel yapılandırmayı ortadan kaldırır.

## Adım 3 – Paralel İşleme OCR ile Hızı Artırın

Dört ya da daha fazla CPU çekirdeğiniz varsa, neden kullanmayasınız? Motor bir iş parçacığı havuzu oluşturabilir ve birden fazla görüntüyü aynı anda işleyebilir. İşte **paralel işleme OCR** burada devreye girer.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Makinenize göre `4` sayısını istediğiniz gibi ayarlayın. Daha fazla iş parçacığı → daha hızlı toplu çalıştırma, ancak her iş parçacığı bellek tüketir; ortamınıza uygun bir denge bulun.

## Adım 4 – İşlemek İstediğiniz Görüntüleri Toplayın

Şimdi dosya yolu listesine ihtiyacımız var. Bu listeyi elle oluşturabilir, bir CSV’den okuyabilir ya da `glob` kullanabilirsiniz. Açıklık olması açısından kısa bir sabit liste tanımlayacağız:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

`YOUR_DIRECTORY` kısmını sisteminizdeki gerçek yol ile değiştirin. Eğer onlarca dosyanız varsa, `glob.glob("*.png")` gibi bir komut işinizi görecektir.

## Adım 5 – Toplu Görüntü Tanımını Çalıştırın

İşte öğreticinin kalbi: `files` içindeki her görüntüyü işleyen ve sonuç nesneleri listesi döndüren tek bir çağrı. Bu, büyük ölçekli OCR’u pratik hâle getiren **toplu görüntü tanımı** özelliğidir.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

Arka planda motor, daha önce yapılandırdığımız dört işçi iş parçacığına dosyaları dağıtırken aynı zamanda her resim için dili otomatik algılar. Metod, tanınan metin ve meta verileri içeren bir liste döndürür.

## Adım 6 – Çıkarılan Metni Yazdırın (Ya da Saklayın)

Son olarak, sonuçlar üzerinde döngü kurup metni ekrana bastırıyoruz. Gerçek bir projede muhtemelen bunu bir veritabanına ya da CSV dosyasına yazarsınız, ancak örnek basit kalması için sadece yazdırıyoruz.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Beklenen çıktı** (kısaltılmış):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Her blok, dosya adını ve OCR‑türetilmiş dizeyi gösterir. Bir görüntü birden fazla dil içeriyorsa, önceki **otomatik dil algılama** adımı sayesinde uygun karakterler görünecektir.

## İpuçları & Yaygın Tuzaklar

- **Görüntü kalitesi önemli** – bulanık ya da düşük kontrastlı fotoğraflar çöp sonuç verir. Gerekirse OpenCV (`cv2.threshold`, `cv2.resize`) ile ön işleme yapın.
- **İş parçacığı sayısı vs. I/O** – Görüntüler yavaş bir ağ sürücüsünde bulunuyorsa, daha fazla iş parçacığı fayda sağlamaz. CPU kullanımını `top` ya da **Task Manager** ile izleyin.
- **Unicode yönetimi** – `result.text` bir Unicode dizesidir. Dosyalara yazarken `encoding="utf‑8"` ile açın, aksi takdirde `UnicodeEncodeError` alabilirsiniz.
- **Bellek tüketimi** – Büyük PDF’ler çok RAM tüketebilir. `MemoryError` alırsanız iş parçacığı havuzunu küçültün ya da görüntüleri daha küçük partiler halinde işleyin.

## Tam Çalışan Betik

Aşağıda, tartıştığımız tüm adımları içeren, kopyala‑yapıştır‑hazır tam betik yer alıyor. `batch_ocr.py` olarak kaydedin ve `python batch_ocr.py` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Şöyle çalıştırın:

```bash
python batch_ocr.py ./my_images 4
```

Her görüntü için güzel biçimlendirilmiş bir metin bloğu göreceksiniz; bu da **görüntülerden metin çıkarma** işini ölçekli bir şekilde yapabildiğinizi kanıtlar.

## Sırada Ne Var?

Python ile **görüntülerden metin çıkarma** temellerini öğrendinize göre, aşağıdaki konuları keşfetmeyi düşünün:

- **Post‑işleme**: OCR çıktısını regex ya da doğal dil işleme kütüphaneleriyle temizleyin.
- **PDF dönüşümü**: Çıkarılan metinleri aranabilir PDF’ler oluşturmak için bir PDF jeneratörüne besleyin.
- **Bulut OCR hizmetleri**: Yerel `ocr` sonuçlarını Google Vision veya Azure OCR ile karşılaştırarak kenar‑durum doğruluğunu ölçün.
- **GUI ön yüz**: Kullanıcıların görüntü yükleyip anında çıkarılan metni görebileceği küçük bir Flask ya da FastAPI uygulaması geliştirin.

Bu konular, yeni kurduğunuz **Python OCR kütüphanesi** temeline dayanır ve hepsi burada kullandığımız **paralel işleme OCR** taktiklerinden faydalanır.

---

*Kodlamanın tadını çıkarın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—OCR inceliklerini birlikte çözebiliriz.*

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Resimden Metin Çıkarma – Aspose OCR ile Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Klasörlerde OCR İşlemi Kullanarak Görüntülerden Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Resimden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}