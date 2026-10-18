---
category: general
date: 2026-03-26
description: Python OCR kullanarak görüntüden tabloları çıkarın ve görüntüyü elektronik
  tabloya dönüştürün. OCR için görüntüyü nasıl yükleyeceğinizi, tabloları nasıl okuyacağınızı
  ve tablo verilerini nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: tr
og_description: Python OCR ile görüntüden tablo çıkarma. Bu kılavuz, OCR için görüntünün
  nasıl yükleneceğini, tabloların nasıl okunacağını ve bir elektronik tabloya nasıl
  dönüştürüleceğini gösterir.
og_title: Görüntüden Tablo Çıkarma – Tam OCR Öğreticisi
tags:
- OCR
- Python
- Data Extraction
title: Görüntüden Tablo Çıkarma – Adım Adım OCR Rehberi
url: /tr/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Tablo Çıkarma – Tam OCR Eğitimi

Hiç **görüntüden tablo çıkarmak** gerekti ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz. Bir PDF ya da ekran görüntüsü içinde tablo verileri olduğunda, bu verileri düzenlenebilir satır ve sütunlara dönüştürmek çoğu geliştiriciyi zorlar. İyi haber? Birkaç satır Python kodu ve sağlam bir OCR motoru, o resmi saniyeler içinde kullanılabilir bir elektronik tabloya dönüştürebilir.

Bu öğreticide bir resmi OCR için nasıl yükleyeceğimizi, tanıma motorunu çalıştıracağımızı ve her tabloyu satır satır nasıl çıkaracağımızı adım adım göstereceğiz. Sonunda **görüntüyü elektronik tabloya dönüştürme** yapabilecek ve **ocr read tables** ve **ocr extract table data** işlemlerinin nasıl yapılacağını göreceksiniz. Gizli bir sihir yok, sadece projenize bugün ekleyebileceğiniz net, çalıştırılabilir kodlar.

---

## Gereksinimler

İlerlemeye başlamadan önce aşağıdakilerin elinizde olduğundan emin olun:

- **Python 3.9+** – en yeni stabil sürüm en iyisidir.
- **`ocr`** kütüphanesi (veya `OcrEngine`, `Image` ve tablo‑ile ilgili metodları sunan uyumlu bir OCR SDK). `pip install ocr‑sdk` ile kurun (paket adını gerçek adıyla değiştirin).
- Açıkça basılmış bir tablo içeren bir görüntü dosyası (`.png`, `.jpg` vb.).  
- İsteğe bağlı: **pandas** – çıkarılan verileri doğrudan CSV ya da Excel dosyasına yazmak isterseniz (`pip install pandas`).

Her şey hazır mı? Harika—başlayalım.

---

## Adım 1: OCR SDK’yı İçe Aktarın ve Ortamınızı Hazırlayın

İlk olarak OCR sınıflarını betiğimize getirmemiz ve ham tablo verilerini bir DataFrame’e dönüştürecek küçük bir yardımcı fonksiyon hazırlamamız gerekiyor.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Neden önemli:** `ocr`’ı içe aktarmak, `OcrEngine`, `Imaging.Image` ve üzerinde döneceğimiz tablo nesnelerine erişim sağlar. `pandas` çıkarma için zorunlu değildir, ancak **görüntüyü elektronik tabloya dönüştürme** kısmını çok basitleştirir.

---

## Adım 2: İşlemek İstediğiniz Görüntüyü Yükleyin

Şimdi **görüntüyü OCR için yükleyelim**. SDK bir `Image` nesnesi beklediği için dosya yolumuzu yardımcı metod `Image.load()` ile sarmalayacağız.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**İpucu:** Görüntü dosyalarınızı ayrı bir klasörde (`assets/` veya `data/`) tutun ve göreli yollar kullanın. Böylece betik farklı makinelerde de çalışabilir.

---

## Adım 3: Tanıma İşlemini Çalıştırın

Görüntü eklendikten sonra motoru **ocr read tables** komutuyla çalıştırabiliriz. `recognize()` çağrısı, motorun bulduğu tüm şeyleri—metin blokları, satırlar ve bizim için en önemli tablo nesnelerini—içeren bir sonuç nesnesi döndürür.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Neden kontrol ediyoruz:** Bazı görüntüler gürültülü olabilir ya da tablo kenarları soluk, bu da motorun tabloyu kaçırmasına yol açar. Bir uyarı kaydetmek, betiği kırmadan erken geri bildirim almanızı sağlar.

---

## Adım 4: Her Tablonun Satır ve Hücrelerini Çıkarın

İşte gerçek sihir burada gerçekleşiyor. Tespit edilen her tabloyu dolaşacağız, her satırı çekecek, ardından her hücrenin metnini alacağız. İç içe liste kavraması kodu kısa tutar, ama akışı hâlâ açıklayacağız.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Ne oluyor?**  

- `enumerate(..., start=1)` loglama için dostça bir tablo numarası verir.  
- `row_obj.get_cells()` her hücre nesnesini döndürür; `cell.get_text()` OCR‑çözülmüş dizeyi alır.  
- Satırları `rows_data` içinde saklarız, ardından `pandas.DataFrame`’e veririz; bu sınıf otomatik olarak sütunları hizalar.  
- `print` bloğu, orijinal kod parçacığındaki **temel çıktıyı** yansıtır, böylece sonuçları anında doğrulayabilirsiniz.

**Köşe durumları:** Bir satır diğerlerinden farklı sayıda hücreye sahipse, `pandas` eksik alanları `NaN` ile doldurur. İsterseniz daha sonra `df.fillna('')` ile boş stringe çevirebilirsiniz.

---

## Adım 5: Çıkarılan Tabloları Elektronik Tabloya Kaydedin

Şimdi elimizde bir DataFrame listesi var; bunları bir Excel çalışma kitabına (veya CSV dosyalarına) dönüştürmek çok kolay. Bu, “görüntüyü elektronik tabloya dönüştür” hedefini karşılar.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Neden Excel?** Çoğu iş kullanıcısı `.xlsx` formatını sever. CSV tercih ederseniz döngüyü `df.to_csv(f"table_{idx}.csv", index=False)` ile değiştirin.

---

## Tam, Çalıştırılabilir Betik

Her şeyi bir araya getirdiğimizde, kopyalayıp çalıştırabileceğiniz tam program aşağıdadır.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Beklenen konsol çıktısı** (basit bir 2×3 tablo varsayarsak):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Ve betiğin bulunduğu klasörde `extracted_tables.xlsx` dosyasını bulacaksınız; her tablo ayrı bir sayfada yer alacak.

---

## Sık Sorulan Sorular & İpuçları

| Soru | Cevap |
|----------|--------|
| **Farklı bir OCR kütüphanesi kullanabilir miyim?** | Tabii ki. Akış aynı kalır: görüntüyü yükle → tanı → `get_tables()` üzerinde döngü. Sadece import ve nesne adlarını değiştirin. |
| **Görüntüm gürültülüyse ne yapmalıyım?** | OCR motoruna vermeden önce OpenCV ile ön‑işleme (eşikleme, eğikliği düzeltme) yapın. Gürültü azaltma, **ocr extract table data** doğruluğunu artırır. |
| **`openpyxl` kurmam gerekiyor mu?** | Evet, `pandas` Excel çıktısı için arka planda bunu kullanır. `pip install openpyxl` ile kurun. |
| **Birleştirilmiş hücreleri nasıl yönetirim?** | Bazı SDK’lar `cell.is_merged()` sunar; değeri birleştirilmiş aralığa manuel olarak yayabilirsiniz. |
| **Sadece belirli tabloları çıkarmak mümkün mü?** | `table_obj.get_confidence()` ile filtreleyebilir ya da başlık anahtar kelimelerini kontrol ederek işlem yapabilirsiniz. |

---

## Sonuç

Artık **görüntüden tablo çıkarmak**, sonucu düzenli bir elektronik tabloya dönüştürmek ve tek bir resimde birden fazla tabloyu işlemek için eksiksiz, uçtan uca bir çözümünüz var. Betik, **load image for OCR**, **ocr read tables** ve **ocr extract table data** işlemlerini gösterirken gerçek dünya varyasyonlarına da esnek kalıyor.

Sırada ne var? OCR motoruna PDF sayfasını görüntü olarak verin ya da farklı diller ve yazı tipleriyle deneyler yapın. DataFrame’leri doğrudan bir veritabanına ya da raporlama aracına da aktarabilirsiniz—hayal gücünüz sınırlama.

Bu rehberi faydalı bulduysanız, paylaşın, SDK’yı barındıran depoyu yıldızlayın ya da kendi püf noktalarınızı yorum olarak bırakın. İyi kodlamalar, ve tablolarınız her zaman kusursuz ayrışsın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}