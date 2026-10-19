---
category: general
date: 2026-07-05
description: Python OCR kullanarak görüntüden tablo çıkarın. Tabloyu nasıl çıkaracağınızı,
  görüntüyü TSV’ye nasıl dönüştüreceğinizi öğrenin ve OCR tablo görüntüsü Python tekniklerinde
  uzmanlaşın.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: tr
og_description: Python OCR ile görüntüden tablo çıkarın. Bu kılavuz, tabloyu nasıl
  çıkaracağınızı, görüntüyü TSV'ye nasıl dönüştüreceğinizi ve OCR tablo görüntüsü
  Python araçlarını nasıl kullanacağınızı gösterir.
og_title: Görüntüden Tablo Çıkar – Görüntüyü Python'da TSV'ye Dönüştür
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Görüntüden Tablo Çıkar – Görüntüyü Python'da TSV'ye Dönüştür
url: /tr/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Tablo Çıkarma – Görüntüyü Python’da TSV’ye Dönüştürme

Hiç saçınızı yolmak zorunda kalmadan bir görüntüden tabloyu nasıl çıkaracağınızı merak ettiniz mi? Bu öğreticide `aocr` kütüphanesini kullanarak bir resimden **tablo verilerini nasıl çıkaracağınızı** adım adım gösterecek ve ardından bu verileri düzenli bir TSV dosyasına dönüştüreceğiz. Hiç bir sihir yok, sadece birkaç satır Python ve biraz AI destekli sonrası işleme.

Tarayıcıdan taranmış bir faturadan ya da ekran görüntüsünden tabloyu kopyalayıp yapıştırmaya çalışıp karışık bir karmaşa ile karşılaştıysanız, OCR‑tabanlı bir yaklaşımın neden öğrenmeye değer olduğunu takdir edeceksiniz. Sonuna geldiğinizde, herhangi bir tablo görüntüsünü Python’a besleyebilecek ve elektronik tablo ya da veritabanları için temiz, sekme‑ayırmalı değerler elde edebileceksiniz.

---

## İhtiyacınız Olanlar

İlerlemeye başlamadan önce, makinenizde aşağıdakilerin bulunduğundan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.9+ | `aocr` paketi modern Python çalışma ortamlarını hedefler. |
| `aocr` library (`pip install aocr`) | Kullanacağımız OCR motorunu ve AI sonrası işlemcisini sağlar. |
| Tablo içeren bir görüntü dosyası (PNG, JPG, vb.) | Çıkaracağımız kaynak veri. |
| Opsiyonel: sanal ortam | Bağımlılıkları izole tutar—şiddetle tavsiye edilir. |

Bu gereksinimlerin hazır olması, rehberin ortasında kesintiye uğramanızı önler.

---

## Bağımlılıkları Kurun

Öncelikle OCR araçlarını kuracağız. Bir terminal açın ve şu komutu çalıştırın:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** İzin hataları alırsanız, `pip install` komutuna `--user` ekleyin ya da global kurulum için `pipx` kullanın.

---

## Adım 1 – OCR Motorunu Başlatma

Motor, sürecin kalbidir. Her piksele bakıp hangi karakterin nereye ait olduğuna karar veren “beyin” gibi düşünün.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Neden tek bir fonksiyon çağırmak yerine bir motor örneği oluşturuyoruz? Motor nesnesi, daha sonra özel sonrası işlemciler eklememize olanak tanır ve çıktıyı ince ayar yapmamızı sağlar—**ocr table image python** doğruluğuna ihtiyacınız olduğunda kritik bir avantaj.

---

## Adım 2 – AI Son İşlemcisini Ekleme

`aocr`, ham OCR sonuçlarını hücre kenarlarını koruyarak temizleyen hafif bir AI sonrası işlemci ile birlikte gelir. Ek argüman gerektirmez, bu da kodu düzenli tutar.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Bu adımı atlayıp sadece ham metin alırsanız, tablo yapısı gürültülü olur—her hücrenin bir gizem olduğu bir elektronik tablo düşünün. Son işlemci, metni orijinal ızgarasına hizalama işini üstlenir.

---

## Adım 3 – Tablo Görüntünüzü Yükleyin

Herhangi bir yoldan bir görüntü yükleyebilirsiniz, ancak açıklık olması açısından bir yer tutucu dizin kullanacağız. `"YOUR_DIRECTORY/invoice_table.png"` ifadesini dosyanızın gerçek yolu ile değiştirin.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Not:** `aocr.Image` görüntü formatını otomatik algılar ve renk kanallarını normalleştirir, bu yüzden dosyayı ön‑işleme yapmanıza genellikle gerek yoktur, yalnızca çok bozulmuşsa.

---

## Adım 4 – Yapılandırılmış OCR Gerçekleştirme

Şimdi motor görüntüyü tarar ve ham bir tablo nesnesi döndürür. Bu nesne satırları, sütunları ve her hücrenin ham metnini içerir.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Neden genel bir `recognize` çağrısı yerine `recognize_structured` kullanıyoruz? Yapılandırılmış sürüm, satır/sütun sınırlarını tahmin etmeye çalışır ve daha sonra TSV’ye dönüştürmesi çok daha kolay bir matris‑benzeri sonuç verir.

---

## Adım 5 – Veriyi AI Son İşlemcisiyle Temizleme

Son işlemciyi çalıştırmak ham çıktıyı iyileştirir: gereksiz karakterleri kaldırır, bölünmüş parçaları birleştirir ve her hücrenin metninin doğru hizalanmasını sağlar.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

`processed_table.table` öğesine baktığınızda, her biri `Cell` nesnelerinden oluşan bir satır listesi göreceksiniz. Her `Cell` nesnesinin temizlenmiş dizeyi tutan bir `.text` özelliği vardır.

---

## Adım 6 – Tabloyu TSV Olarak Dışa Aktarma

Son adım, işlenmiş veriyi sekme‑ayırmalı değerler (TSV) dosyasına dönüştürmektir—Excel ya da Google Sheets için **convert image to TSV** yapmanız gerektiğinde tam olarak ihtiyacınız olan şey.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Script’i çalıştırmak her satırı konsola (isteğe bağlı) yazdırır ve herhangi bir elektronik tablo programında açabileceğiniz temiz bir TSV dosyası oluşturur.

### Hızlı doğrulama

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Aşağıdaki gibi düzgün hizalanmış sütunlar görmelisiniz:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Çıktı karışık görünüyorsa, görüntü kalitesini (keskinlik, kontrast) iki kez kontrol edin ve OCR motorunun ayarlarını ince ayar yapmayı düşünün—`engine.set_config(...)` dil modellerini ve güven eşiğini ayarlamanıza izin verir.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Önerilen Çözüm |
|-----------|---------------|
| **Eğimli görüntü** | `aocr`’a beslemeden önce `Pillow` (`Image.rotate`) ile ön‑döndürme yapın. |
| **Düşük kontrast** | Okunabilirliği artırmak için histogram eşitlemesi (`cv2.equalizeHist`) uygulayın. |
| **Birleştirilmiş hücreler** | Bilinen ayırıcılar üzerinden TSV’yi son‑işlemden geçirerek hücreleri bölün veya mevcutsa `merge_cells=False` bayrağını kullanın. |
| **Çok sayfalı PDF’ler** | Önce her sayfayı bir görüntüye dönüştürün (`pdf2image`) ve döngü içinde pipeline’ı çalıştırın. |

Bu ayarlamalar, **ocr table image python** iş akışınızı farklı kaynak materyallerde bile sağlam tutar.

---

## Tam Script – Tek Çözüm

Aşağıda, tartışılan tüm adımları bir araya getiren, çalıştırılmaya hazır tam script yer alıyor. `extract_table.py` olarak kaydedin ve `python extract_table.py` komutuyla çalıştırın.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR for .NET ile Görüntüden Tablo Nasıl Çıkarılır](/ocr/english/net/text-recognition/recognize-table/)
- [OCR’da Dikdörtgenler Hazırlayarak Görüntüden Metin Nasıl Çıkarılır](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}