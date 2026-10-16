---
category: general
date: 2026-06-28
description: Python OCR kullanarak metin görüntülerini tanımayı, metin PNG dosyalarını
  çıkarmayı ve tanınan metni sağlam hata yönetimiyle yazdırmayı öğrenin.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: tr
og_description: Python'da metin görüntüsünü tanıma, metin PNG'sini çıkarma ve tanınan
  metni güvenli bir şekilde yazdırma adım adım öğreticisi.
og_title: Python OCR ile metin görüntüsünü tanıma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python OCR ile metin görüntüsünü tanıma – Tam Kılavuz
url: /tr/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR ile Metin Görüntüsü Tanıma – Tam Kılavuz

Ağır bir çerçeve (framework) kullanmadan bir Python betiğinde **metin görüntüsü tanıma** nasıl yapılır hiç merak ettiniz mi? Yalnız değilsiniz. Birçok geliştirici, bir ekran görüntüsü, taranmış bir fiş ya da basit bir PNG'yi *load image OCR* edip metni geri almak için hızlı bir yol arıyor.  

Bu öğreticide minimal bir OCR motoru kuracağız, özel bir logger ekleyeceğiz, **load image OCR**, **process image OCR** çalıştıracağız ve sonunda **print recognized text** yapacağız. Sonunda, isteğe bağlı olarak **extract text png** dosyalarını da çıkarabilen bağımsız bir betiğiniz olacak.

## Öğrenecekleriniz

- Tam işlevsel bir Python kod parçacığı, bir OCR motoru oluşturur, her adımı kaydeder ve hataları zarif bir şekilde ele alır.  
- Her satırın *neden* önemli olduğuna dair net açıklamalar—böylece kodu Tesseract, EasyOCR veya başka bir backend'e uyarlayabilirsiniz.  
- Yaygın tuzaklar (eksik fontlar, bozuk PNG'ler) için ipuçları ve bunları nasıl hata ayıklayacağınız.  

### Önkoşullar

- Python 3.8+ yüklü  
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi (örnek, kurgusal ama tipik bir API kullanıyor; `pytesseract`, `easyocr` vb. ile değiştirin).  
- Analiz etmek istediğiniz bir PNG görüntüsü, `input.png` olarak kontrol ettiğiniz bir klasörde kaydedilmiş.  

> **Pro tip:** `pytesseract` kullanıyorsanız, önce sistem Tesseract ikili dosyasını kurun (`sudo apt install tesseract-ocr` Linux'ta) ve ardından `pip install pytesseract pillow`.

---

## ## Metin Görüntüsü Tanıma: Logger'ı Kurma

İyi bir logger, herhangi bir OCR hattının gözden kaçan kahramanıdır. Motorun ne zaman başladığını, hangi dosyayı açtığını ve neden başarısız olabileceğini size *when*, *what* ve *why* olarak bildirir.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Neden önemli:*  
Logger, tanı çıktısını OCR çekirdeğinden ayırır, böylece logları bir dosyaya, izleme hizmetine ya da ileride bir UI'ye yönlendirmek kolaylaşır.  

---

## ## Görüntüyü OCR ile Yükleme: Motoru PNG ile Besleme

Motor **process image OCR** yapabilmeden önce uygun bir görüntü nesnesine ihtiyaç duyar. Çoğu kütüphane bir Pillow `Image` örneğini kabul eder.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Anahtar noktalar:*  

- **load image ocr** – `Image.from_file` PNG çözümleme detaylarını soyutlar.  
- Yolu yapılandırılabilir tutun; sabit kodlama betiği kırılgan hâle getirir.  
- Logger çağrısı, görüntünün başarıyla okunduğunu onaylar; bu, dosya eksik ya da bozuk olduğunda faydalıdır.  

---

## ## Görüntü OCR İşleme: Metni Tanıma

Şimdi zor iş başlar. Motor bitmap'i tarar, sinir ağlarını ya da sezgisel kurallarını uygular ve bir Unicode dizesi üretir.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Neden `try/except` ile sarıyoruz:*  
OCR, düşük çözünürlüklü PNG'lerde, desteklenmeyen renk uzaylarında veya eksik dil verilerinde patlayabilir. `OcrException` yakalamak, **print recognized text** yalnızca gerçekten mevcut olduğunda yapmanıza olanak tanır ve son kullanıcılar için gizemli yığın izlerini önler.  

---

## ## Tanınan Metni Yazdırma & Metin PNG Çıkarma

Tanıma başarılı olursa, sonucu gösterir ve isteğe bağlı olarak orijinal PNG adını yansıtan bir `.txt` dosyasına yazarız.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Ne elde edersiniz:*  

- **print recognized text** – terminalde anlık görsel geri bildirim.  
- Yan yana bir `.txt` dosyası, etkili bir şekilde **extract text png** yapar ve sonraki işlemler (arama indeksleme, veri girişi vb.) için kullanılabilir.  

---

## ## Yaygın Kenar Durumları ve Nasıl Çözülür

| Situation | Symptom | Fix |
|-----------|---------|-----|
| PNG yalnızca gri tonlamalı | OCR boş string döndürür | Motoru beslemeden önce RGB'ye dönüştür (`Image.convert("RGB")`). |
| Dil desteklenmiyor | `OcrException` kodu `LANG_NOT_FOUND` ile | Dil paketini kurun (ör. Fransızca için `tesseract‑lang‑fra`) ve `ocr_engine.language = "fra"` olarak ayarlayın. |
| Çok büyük görüntü ( > 5 MB ) | Yavaş tanıma veya bellek hatası | `set_image`'den önce `image.thumbnail((2000, 2000))` ile küçültün. |
| Beklenmeyen karakterler | Bozuk çıktı | Görüntünün gerçekten PNG olduğundan emin olun; bazı dosyalar PNG gibi görünür ancak aslında JPEG'dir. Doğrulamak için `Image.verify()` kullanın. |

---

## ## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Beklenen konsol çıktısı (başarılı yol):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

Bir şeyler ters giderse, özel logger sayesinde nedeni belirten net bir `[ERROR]` satırı göreceksiniz.

---

## ## Sonraki Adımlar ve İlgili Konular

- **extract text png** toplu olarak: betiği bir dizin ağacını dolaşan `for` döngüsüyle sarın.  
- **process image ocr** ön işleme (eğikliği düzeltme, kontrast artırma) ile OpenCV kullanarak motoru beslemeden önce.  
- `OcrEngine` uygulamasını değiştirerek bir bulut OCR hizmetine (Google Vision, Azure Read) geçin—çevresel kodunuz aynı kalır.  
- `reportlab` kullanarak otomatik rapor üretimi için **print recognized text**'i PDF'lere nasıl yazdıracağınızı öğrenin.  

---

## Sonuç

Python'da **recognize text image** için kompakt, üretime hazır bir yol gösterdik; PNG'yi yüklemekten **print recognized text** yapmaya ve sonucu kaydetmeye kadar. Küçük bir logger ekleyerek, istisnaları ele alarak ve çıktıyı isteğe bağlı olarak kalıcı hâle getirerek, betik hem hızlı denemeler hem de daha büyük hatlara entegrasyon için hazır.

Kendi ekran görüntülerinizle deneyin, görüntü ön işleme ile oynayın ve yakında ona attığınız herhangi bir PNG'den metin çıkarabileceksiniz. Sorularınız mı var? Bir yorum bırakın—mutlu OCRlamalar!  

![recognize text image example](placeholder.png)


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose OCR Kullanarak Akıştan Görüntü Metni Çıkarma Nasıl Yapılır](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Görüntüyü Metne Dönüştür – URL'den Görüntü Üzerinde OCR Yap](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}