---
category: general
date: 2026-01-02
description: Görüntüyü eğriltmeyi düzeltmeyi ve kontrastını artırarak düz metni hızlıca
  elde etmeyi öğrenin. Adım adım Python kodu ve metin çıkarma ipuçları içerir.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: tr
og_description: Görüntüyü eğrilikten düzeltme ve kontrastı artırarak düz metin elde
  etme. Tablo çıkarma ve GPU hızlandırmasıyla tam Python örneği.
og_title: Görüntüyü Düzeltme – Tam GPU OCR Eğitimi
tags:
- OCR
- Python
- Image Processing
title: Görüntüyü Düzeltme – GPU Hızlandırmalı OCR Rehberi
url: /tr/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Düzeltme – GPU Hızlandırmalı OCR Kılavuzu

Makbuzlarınız eğik bir açıyla geldiğinde **görüntüyü nasıl düzeltirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz; eğik bir fotoğraf, tamamen okunabilir bir makbuzu karışık bir hale getirebilir. İyi haber şu ki, birkaç satır Python kodu ile otomatik olarak düzeltme, kontrastı artırma ve temiz düz metin çıkarma işlemlerini yapabilirsiniz—manuel Photoshop müdahalesine gerek yok.  

Bu öğreticide, sadece **görüntüyü nasıl düzeltirsiniz** göstermekle kalmayıp, **kontrastı nasıl artırırsınız**, **düz metni nasıl alırsınız** ve OCR motorunun keşfettiği tablolardan **metni nasıl çıkarırsınız** konularını da kapsayan tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz bağımsız bir betiğiniz olacak.

## Gerekenler

- Python 3.9+ kurulmuş (kod tip ipuçları kullandığı için yeni bir yorumlayıcı faydalı)
- `ocr` kütüphanesi; `OcrEngine`, `EngineMode`, `ImageProcessingOptions` ve `OcrResult` sağlar (kurulum: `pip install ocr‑sdk` – kullandığınız gerçek paket adıyla değiştirin)
- Hız artışı istiyorsanız uyumlu sürücülere sahip bir GPU (isteğe bağlı ama tavsiye edilir)
- Hafifçe döndürülmüş veya düşük kontrastlı bir görüntü dosyası, ör. `receipt_skewed.jpg`

> **Pro ipucu:** GPU’nuz yoksa, sadece `EngineMode.GPU` yerine `EngineMode.CPU` yazın; betik hâlâ çalışır—sadece biraz daha yavaş.

## Adım Adım Uygulama

Aşağıda çözümü mantıksal parçalara ayırıyoruz. Her parçanın başlığında birincil anahtar kelime *görüntüyü nasıl düzeltirsiniz* ya da ikincil anahtar kelimeler bulunur. Kod eksiksiz, yorumlu ve çalıştırılmaya hazır.

### GPU Hızlandırmalı OCR ile Görüntüyü Nasıl Düzeltirsiniz

İlk olarak OCR motorunu GPU’da çalıştırmasını söylüyor ve otomatik düzeltme özelliğini etkinleştiriyoruz. Otomatik düzeltme, görüntünün geometrisini analiz eder ve dik konuma getirir.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Neden önemli:** GPU hızlandırması işleme süresini saniyelerden milisaniyelere indirebilir; bu, dakikada onlarca makbuz işliyorsanız kritik bir fark yaratır.

### Daha İyi Tanıma İçin Görüntü Kontrastını Artırın

Düşük kontrastlı bir makbuz, herhangi bir OCR sistemi için kabus gibidir. Kontrastı artırarak motorun daha net kenarlar üzerinde çalışmasını sağlarız.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Kontrastı nasıl artırırsınız:** `set_contrast_boost` metodu yüzde değeri alır; %30 çoğu taranmış makbuz için güvenli bir varsayılandır. Görüntüleriniz çok karanlıksa %50’ye çıkarabilir ya da deneme yapabilirsiniz.

### İşlenmiş Görüntüden Düz Metni Alın

Görüntü artık düz ve parlak olduğuna göre, motoru çalıştırıp düz metin sonucunu istiyoruz.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Beklenen çıktı** (kısaltılmış):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Düz metni nasıl alırsınız:** `get_text()` metodu tüm düzen bilgilerini atar ve temiz bir string döndürür; bu stringi veritabanına kaydedebilir, bir API’ye gönderebilir ya da sonraki analizlere besleyebilirsiniz.

### Algılanan Tablo İçinden Metni Nasıl Çıkarırsınız

Makbuzlarda sıkça tablo verileri (ürünler, miktarlar, fiyatlar) bulunur. OCR SDK’sı tabloları algılayabilir ve satır‑hücre döngüsüyle erişim sağlar.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Örnek tablo çıktısı**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Tabloları neden çıkarırsınız:** Yapılandırılmış veri, toplamları hesaplamayı, rapor üretmeyi ya da muhasebe yazılımına beslemeyi çok basitleştirir.

### Tam Çalışan Betik

Her şeyi bir araya getirerek, `deskew_and_ocr.py` dosyasına kopyalayıp yapıştırabileceğiniz betiği aşağıda bulabilirsiniz:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Şöyle çalıştırın:

```bash
python deskew_and_ocr.py
```

Temizlenmiş metni ve algılanan tabloları konsolda göreceksiniz.

## Yaygın Kenar Durumları ve Çözüm Önerileri

| Durum | Ne Yapmalı |
|-----------|------------|
| **Görüntü baş aşağı** | SDK bunu destekliyorsa `set_rotation_correction(True)` ile `set_auto_deskew(True)` güvenini artırın. |
| **Kontrast artırma görüntüyü çok parlak yapıyor** | `set_contrast_boost` değerini azaltın (ör. %15). |
| **GPU bulunmuyor** | `EngineMode.GPU` yerine `EngineMode.CPU` kullanın; pipeline’ın geri kalanı aynı kalır. |
| **Tablolar kaçırılıyor** | Daha yüksek çözünürlüklü tarama deneyin veya kütüphane `set_table_detection(True)` sağlıyorsa etkinleştirin. |

## Sonraki Adımlar: Düz Metinden Yapılandırılmış Veriye

Artık **görüntüyü nasıl düzeltirsiniz**, **kontrastı nasıl artırırsınız** ve **düz metni nasıl alırsınız** bildiğinize göre şunları yapabilirsiniz:

- Düz metni düzenli ifadelerle işleyerek anahtar‑değer çiftlerini çıkarın (ör. `total`, `date`).
- Sonuçları daha sonra raporlamak için SQLite veya PostgreSQL veritabanına kaydedin.
- Betiği bir sunucusuz fonksiyona (AWS Lambda, Azure Functions) bağlayarak yüklemeleri otomatik işleyin.

Tüm bu genişletmeler, burada ele aldığımız temelin üzerine inşa edilir.

## Sonuç

GPU hızlandırmalı bir OCR motoru kullanarak **görüntüyü nasıl düzeltirsiniz**, **kontrastı nasıl artırırsınız**, **düz metni nasıl alırsınız** ve hatta **tablolardan metni nasıl çıkarırsınız** konularını adım adım gösterdik. Tam, çalıştırılabilir betik her şeyi birleştiriyor, böylece herhangi bir Python projesine ekleyip eğik, düşük kontrastlı fotoğraflardan temiz veri çekmeye hemen başlayabilirsiniz.

Kendi makbuzlarınızla deneyin, kontrast seviyesini ayarlayın ve OCR’un ağır işini yapmasına izin verin. Bir sorunla karşılaşırsanız, yukarıdaki kenar‑durum tablosuna geri dönün—çoğu sorun sadece bir ayar değişikliğiyle çözülür.

Kodlamanın tadını çıkarın, ve görüntüleriniz her zaman düz ve parlak olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}