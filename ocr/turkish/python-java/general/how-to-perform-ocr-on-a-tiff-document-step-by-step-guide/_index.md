---
category: general
date: 2026-01-12
description: OCR'yi hızlı ve doğru bir şekilde nasıl gerçekleştireceğinizi öğrenin.
  Belge üzerinde OCR çalıştırmayı, TIFF'ten metin çıkarmayı, OCR için görüntü yüklemeyi
  ve Python'da OCR dilini ayarlamayı öğrenin.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: tr
og_description: Python'da OCR nasıl yapılır. Bu öğreticide belge üzerinde OCR çalıştırma,
  tiff dosyasından metin çıkarma, OCR için görüntü yükleme ve OCR dilini ayarlama
  yöntemlerini gösterir.
og_title: TIFF Belgesi Üzerinde OCR Nasıl Yapılır – Tam Rehber
tags:
- OCR
- Python
- Image Processing
title: TIFF Belgesinde OCR Nasıl Yapılır – Adım Adım Rehber
url: /tr/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF Belgesi Üzerinde OCR Nasıl Yapılır – Tam Kılavuz

Doğru kütüphaneyi bulmak için saatler harcamadan taranmış bir TIFF dosyası üzerinde **OCR nasıl yapılır** diye hiç merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, özellikle performans ve dil ayarları önemli olduğunda, tiff görüntülerinden metin çıkarmaya çalışırken bir duvara çarpar.

Bu öğreticide, bilmeniz gereken her şeyi adım adım ele alacağız: OCR paketini kurmaktan, OCR için görüntüyü yüklemeye, OCR dilini ayarlamaya, son olarak **belge üzerinde OCR çalıştırmaya** ve temiz metin elde etmeye kadar. Sonunda, herhangi bir projeye ekleyebileceğiniz hazır‑çalıştır scriptine sahip olacaksınız.

> **Pro ipucu:** Örnek, genel bir `ocr` modülü kullansa da, aynı kavramlar Tesseract, EasyOCR veya Python API'si sunan herhangi bir modern OCR motoru için geçerlidir.

---

## Gereksinimler

- Python 3.8+ (herhangi bir yeni sürüm çalışır)
- Bir `OcrEngine` sınıfı sağlayan OCR kütüphanesi (örnek, hayali bir `ocr` paketi kullanıyor; gerçek olanla değiştirin)
- İşlemek istediğiniz çok sayfalı bir TIFF dosyası (biz buna `big_document.tif` diyeceğiz)
- İş parçacığı sayısını ayarlamayı planlıyorsanız en az 4 CPU çekirdeğine sahip bir makine

Harici hizmetler yok, bulut anahtarları yok—sadece saniyeler içinde çalışan yerel kod.

![ocr örneği nasıl yapılır](/images/ocr-example.png "TIFF Belgesi Üzerinde OCR Nasıl Yapılır")

*Görsel alt metni: TIFF belgesi üzerinde OCR nasıl yapılır – çıkarılan metnin önizlemesi.*

---

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak: kütüphaneyi makinenize alın. Çoğu OCR paketi PyPI'de bulunur, bu yüzden basit bir `pip install` işinizi görür.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Şimdi ihtiyacınız olan sınıfları içe aktarın. Tesseract kullanıyorsanız, import satırı farklı görünebilir, ancak kodun geri kalanı aynı kalır.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Neden önemli:* Doğru sembolleri erken içe aktarmak, daha sonra isim alanı çakışmalarını önler ve scripti okumayı kolaylaştırır.

---

## Adım 2: OCR Motorunu Oluşturun ve Yapılandırın (OCR Dilini Ayarlayın)

Motoru yapılandırmak, doğru tanıma için **OCR dilini ayarladığınız** yerdir. İngilizce varsayılan dildir, ancak tek bir satırla Fransızca, Almanca veya çok dilli moda geçebilirsiniz.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Neden 4 iş parçacığı?** Çoğu modern dizüstü bilgisayar en az dört çekirdeğe sahiptir ve iş parçacığı sayısını sınırlamak, OCR sürecinin tüm makineyi tüketmesini önler—özellikle script paylaşılan bir sunucuda çalıştığında faydalıdır.

Başka bir dile ihtiyacınız varsa, sadece `ocr.Language.ENGLISH` yerine `ocr.Language.FRENCH`, `ocr.Language.SPANISH` vb. kullanın.

---

## Adım 3: OCR İçin Görüntüyü Yükleyin (OCR İçin Görüntüyü Yükleyin)

Şimdi **OCR için görüntüyü yüklüyoruz**. `Image.load` yöntemi, TIFF dosyasını belleğe okur ve çok sayfalı belgeleri otomatik olarak işler.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Köşe durum:* Dosya çok büyükse, RAM tükenebilir. Bu durumda, `Image.load_page(page_number)` ile bir sayfayı bir seferde yüklemeyi düşünebilirsiniz (kütüphane destekliyorsa).

---

## Adım 4: Belge Üzerinde OCR Çalıştırın

Motor hazır ve görüntü yüklendiğine göre, **belge üzerinde OCR çalıştırma** zamanı geldi. `process` yöntemi ağır işi yapar ve bir sonuç nesnesi döndürür.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Arka planda motor, görüntüyü metin bloklarına ayırır, tanıma modelini çalıştırır ve sonuçları birleştirir. Çağrı bloklayıcıdır, yani script tüm TIFF işlenene kadar bekler—toplu işler için mükemmeldir.

---

## Adım 5: TIFF'ten Metni Çıkarın ve Çıktıyı Doğrulayın

Son olarak, sonucu `text` özelliğine erişerek **tiff'ten metni çıkarıyoruz**. Hızlı bir doğrulama için ilk 200 karakteri yazdıralım.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Beklenen çıktı (örnek):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Tam metne ihtiyacınız varsa, sadece `ocr_result.text` kullanın. Sonraki işlemler için `.txt` dosyasına yazmak isteyebilirsiniz:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Tam Çalışan Örnek

Hepsini bir araya getirerek, işte hazır‑çalıştır scripti. Yer tutucu paket adını, aslında kurduğunuz paketle değiştirin.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Scripti şu şekilde çalıştırın:

```bash
python ocr_tiff_example.py
```

Konsolda bir önizleme görmeli ve tam transkripsiyonu içeren `extracted_text.txt` adlı bir dosya oluşturulmuş olmalı.

---

## Yaygın Sorular & Köşe Durumları

- **TIFF birden fazla sayfa içeriyorsa ne olur?**  
  Çoğu OCR motoru, her sayfayı dahili olarak ayrı bir görüntü olarak işler. `ocr_result.text` sayfalar arasında bir yeni satır içerir. Sayfa bazlı işleme ihtiyacınız varsa, `Image.load_page(page_number)` ile yineleyin.

- **TIFF yerine PNG veya JPEG işleyebilir miyim?**  
  Kesinlikle. `Image.load` yöntemi genellikle Pillow veya alt kütüphane tarafından desteklenen herhangi bir formatı kabul eder. Sadece dosya uzantısını değiştirin.

- **Metnim bozuk çıktı—dili değiştirmeli miyim?**  
  Evet. **OCR dilini ayarlama** adımı, İngilizce dışındaki belgeler için kritiktir. Dil paketinin kurulu olduğundan emin olun (ör. Fransızca için `tesseract‑lang‑fra`).

- **Bellek tükeniyor mu?**  
  `set_memory_limit` değerini düşürün veya sayfaları tek tek işleyin. Bazı motorlar, tanımadan önce görüntüyü küçültmenize de izin verir.

---

## Sonuç

İşte bu kadar—Python kullanarak bir TIFF dosyası üzerinde **OCR nasıl yapılır** konusundaki kısa ve tam işlevsel rehber. Kütüphaneyi kurmaktan, motoru yapılandırmaya (**OCR dilini ayarlama** dahil), **OCR için görüntüyü yükleme**, **belge üzerinde OCR çalıştırma** ve son olarak **tiff'ten metni çıkarma** konularını ele aldık.

Denemekten çekinmeyin: iş parçacığı sayısını ayarlayın, dilleri değiştirin veya OCR çıktısını bir doğal dil işleme hattına besleyin. Temelleri kavradıktan sonra sınır yoktur.

Daha fazla sorunuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}