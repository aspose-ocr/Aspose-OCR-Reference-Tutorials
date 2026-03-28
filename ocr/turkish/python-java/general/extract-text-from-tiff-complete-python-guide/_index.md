---
category: general
date: 2026-03-28
description: Aspose OCR'yi Python'da kullanarak TIFF dosyalarından metin çıkarın.
  TIFF'i hızlı ve güvenilir bir şekilde metne dönüştürmeyi öğrenin.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: tr
og_description: Aspose OCR kullanarak Python'da TIFF dosyalarından metin çıkarın.
  Bu rehber, TIFF'i metne adım adım nasıl dönüştüreceğinizi gösterir.
og_title: TIFF'ten Metin Çıkarma – Tam Python Rehberi
tags:
- OCR
- Python
- Aspose
title: TIFF'ten Metin Çıkarma – Tam Python Rehberi
url: /tr/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'ten Metin Çıkarma – Tam Python Rehberi

Python projenizde **TIFF'ten metin çıkarmak** mı istiyorsunuz? Bu rehber, Aspose OCR kütüphanesini kullanarak **TIFF'i metne dönüştürmenin** nasıl yapılacağını gösterir ve bunu bir başlangıç seviyesindekinin bile takip edebileceği bir şekilde sunar.  

Eğer bir çok sayfalı TIFF'e bakıp, kelimeleri manuel olarak yazmadan nasıl çıkarabileceğinizi merak ettiyseniz, doğru yerdesiniz. Paketi kurmaktan şifreli dosyalar gibi uç durumları ele almaya kadar tüm süreci adım adım göstereceğiz; böylece önemli özellikleri geliştirmeye odaklanabilirsiniz.

## Neler Öğreneceksiniz

* Aspose OCR'ı Python için nasıl kuracağınızı.
* Çok sayfalı bir TIFF'in her sayfasını okumak için gereken tam kod.
* Eksik fontlar veya bozuk sayfalar gibi yaygın sorunları ele almanın yolları.
* Büyük ölçekli **TIFF'ten metin çıkarma** işlemlerinde doğruluk ve performansı artırmak için ipuçları.

### Ön Koşullar

* Python 3.8 ve üzeri (kütüphane 3.7+ destekler).
* Geçerli bir Aspose OCR lisansı—ya da ücretsiz deneme sürümüyle başlayabilirsiniz (kod değerlendirme modunda çalışır, sadece çıktıya bir filigran eklenir).
* Python sanal ortamlarıyla temel aşinalık (isteğe bağlı ancak önerilir).

---

## Adım 1 – Aspose OCR Paketi'ni Kurun

İlk olarak, `aspose-ocr` paketine ihtiyacınız var. Paket PyPI'de barındırılıyor, bu yüzden basit bir `pip` kurulumu işinizi görür.

```bash
pip install aspose-ocr
```

> **Pro ipucu:** Bağımlılıkları izole tutmak için bir sanal ortam (`python -m venv venv`) kullanın. Bu, aynı anda yürüttüğünüz diğer projelerle sürüm çakışmalarını önler.

> **Neden önemli:** Paketi kurmak, asıl işi yapan yerel OCR motoru ikili dosyalarını da getirir. Bunlar olmadan `recognize_from_tiff` metodu mevcut olmaz ve bir `ImportError` alırsınız.

---

## Adım 2 – Kütüphaneyi İçe Aktarın ve bir OCR Motoru Oluşturun

Kütüphane artık makinenizde olduğuna göre, onu içe aktarın ve bir `OcrEngine` başlatın. Bu nesne, görüntü verisini işleyecek ana motor olacaktır.

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*`OcrEngine` sınıfı, dil, çözünürlük ve ön işleme seçenekleri gibi tüm OCR ayarlarını kapsar. Doğruluğu artırmak için daha sonra bu ayarlardan birkaçını inceleyeceğiz.*

---

## Adım 3 – Çok Sayfalı TIFF Dosyanıza Yol Gösterin

Okumak istediğiniz TIFF'in yoluna ihtiyacınız var. Kütüphane mutlak veya göreli yollarla çalışır, ancak mutlak yollar, betik farklı bir çalışma dizininden çalıştırıldığında sürprizleri önler.

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **Yaygın hata:** Windows'ta ters eğik çizgileri kaçırmak (`C:\\Images\\file.tif`). Raw string'ler (`r"C:\Images\file.tif"`) veya ileri eğik çizgiler kullanmak bu sorunu önler.

---

## Adım 4 – Tüm Sayfalardan Metni Tanıyın

İşte öğreticinin özü: `recognize_from_tiff` metodunu çağırmak. Bu metod, her sayfa için bir `OcrResult` nesnesi içeren bir liste döndürür; böylece her birini ayrı ayrı döngüye alabilirsiniz.

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**Neden işe yarar:** Aspose OCR, TIFF'i içindeki çerçevelere ayırır, her birine OCR motorunu uygular ve sonuçları birleştirir. Bu, sayfaları Pillow veya ImageMagick ile manuel olarak ayırmaya çalışmaktan çok daha güvenilirdir.

---

## Adım 5 – Sonuçlar Üzerinde Döngü Oluşturun ve Metni Çıktılayın

Son olarak, `OcrResult` listesini döngüye alıp çıkarılan metni yazdırın (veya kaydedin). İş akışınıza uygunsa, her sayfayı ayrı bir `.txt` dosyasına da yazabilirsiniz.

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**Beklenen çıktı** (kısaltılmıştır):

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **Uç durum yönetimi:** Bir sayfada tanınabilir metin yoksa, `page_result.text` boş bir string olacaktır. Bu sayfaları daha sonraki manuel inceleme için kaydetmek isteyebilirsiniz.

---

## Bonus – Daha İyi Doğruluk İçin OCR Ayarlarını Düzenleme

Bazen varsayılan yapılandırma yeterli olmayabilir, özellikle düşük çözünürlüklü taramalar veya alışılmadık fontlarla. Aşağıda ayarlayabileceğiniz birkaç seçenek bulunuyor:

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*Bu seçenekler isteğe bağlıdır, ancak genellikle karışık bir çıktıyı temiz ve aranabilir bir transkripte dönüştürmede fark yaratır.*

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| Tüm sayfalar için boş çıktı | Yanlış dosya yolu veya desteklenmeyen TIFF sıkıştırması | Yolu doğrulayın, TIFF'in desteklenen bir sıkıştırma (ör. LZW, PackBits) kullandığından emin olun. |
| Bozuk karakterler (ör. �) | Yanlış dil ayarı veya eksik font dosyaları | `ocr_engine.language` değerini doğru yerel ayara ayarlayın; gerekli fontları işletim sistemine kurun. |
| Büyük TIFF'lerde yavaş işleme | Varsayılan tek‑iş parçacıklı mod | Kütüphane sürümü destekliyorsa `ocr_engine.recognize_from_tiff(..., parallel=True)` kullanın. |
| Lisans uyarısı | Lisans dosyası olmadan deneme sürümünü kullanmak | `aocr.License().set_license("Aspose.OCR.lic")` ile bir lisans anahtarı sağlayın. |

---

## Tam Script – Çalıştırmaya Hazır

Aşağıda, yukarıda tartışılan tüm adımları ve isteğe bağlı ayarlamaları içeren tam, bağımsız bir script bulunuyor. `extract_tiff_text.py` adlı bir dosyaya yapıştırın ve `python extract_tiff_text.py` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**Script'i Çalıştırma**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

Her sayfanın bir konsol önizlemesini ve `output` adlı bir klasörde `page_1.txt`, `page_2.txt` vb. dosyaları göreceksiniz.

---

## Sonuç

Python ve Aspose OCR kullanarak **TIFF'ten metin çıkarma** için ihtiyacınız olan her şeyi yeni kapsadık. Paketi kurmaktan çok sayfalı belgeleri işlemeye, doğruluk için ayarları ince ayarlamaya ve sonuçları kaydetmeye kadar tüm iş akışı artık parmaklarınızın ucunda.  

Üretim hattında **TIFF'i metne dönüştürmek** istiyorsanız, dosyaları toplu işleyin, OCR çağrılarını paralelleştirin ve çıktıyı Elasticsearch gibi aranabilir bir indekste saklamayı düşünün. Maceraperestler için, diğer dillerle (`aocr.Language.Spanish`) denemeler yapabilir veya ham OCR sonuçlarını bir yazım denetimi kütüphanesine besleyerek OCR gürültüsünü temizleyebilirsiniz.  

Ölçekleme, lisanslama veya bulut depolama entegrasyonu hakkında sorularınız mı var? Aşağıya bir yorum bırakın, iyi kodlamalar! 

![TIFF dosyasından çıkarılan metne kadar OCR akışını gösteren diyagram](https://example.com/placeholder-image.png "Python kullanarak TIFF'ten metin çıkarma")

*Görsel alt metni: Python kullanarak TIFF'ten metin çıkarma*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}