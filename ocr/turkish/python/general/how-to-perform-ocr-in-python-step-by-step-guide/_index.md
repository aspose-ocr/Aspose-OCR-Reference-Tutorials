---
category: general
date: 2026-01-12
description: OCR nasıl yapılır ve görüntü hızlıca metne dönüştürülür. Özel karakterleri
  tanımayı, görüntüden metin çıkarmayı ve tam bir Python örneğiyle OCR için görüntüyü
  yüklemeyi öğrenin.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: tr
og_description: Python'da OCR nasıl yapılır, görüntüyü metne dönüştürür ve özel karakterleri
  tanır. Görüntülerden metin çıkarmak için bu uygulamalı rehberi izleyin.
og_title: Python'da OCR Nasıl Yapılır – Tam Kılavuz
tags:
- OCR
- Python
- Image Processing
title: Python'da OCR Nasıl Yapılır – Adım Adım Rehber
url: /tr/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Nasıl Yapılır – Adım‑Adım Kılavuz

Bir ekran görüntüsünde hem Latin hem de Kiril karakterleri içeren **OCR gerçekleştirme** ihtiyacı hiç duydunuz mu? Yalnız değilsiniz. Makbuzları dijitalleştirmek, çok dilli belgeleri indekslemek ya da aranabilir bir arşiv oluşturmak gibi projelerde **Python’da OCR nasıl yapılır** sorusu hızla öncelikli hale gelir.  

Bu öğreticide, **görüntüyü metne dönüştürme**, **özel karakterleri tanıma** ve **görüntüden metin çıkarma** işlemlerini gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, OCR için bir görüntüyü yükleyen, çok dilli içeriği işleyen ve sonucu ekrana yazdıran hazır bir betiğiniz olacak.

## Gerekenler

Başlamadan önce aşağıdaki ön koşullara sahip olduğunuzdan emin olun:

- Makinenizde Python 3.8+ yüklü.  
- `ocr` paketi (veya uyumlu bir OCR kütüphanesi) `pip install ocr` ile kurulmuş.  
- Hem Latin hem de Kiril karakterler içeren bir görüntü dosyası (`multilingual.png`).  
- Basit bir metin editörü veya IDE — VS Code, PyCharm ya da basit bir Notepad yeterli.  

`ocr` paketiniz yoksa, birkaç küçük değişiklikle `pytesseract` ile değiştirebilirsiniz; temel kavramlar aynı kalır.

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak OCR motorunu hazır hale getirelim. Kütüphaneyi içe aktaracağız, bir motor örneği oluşturacağız ve çok dilli desteği için yapılandıracağız.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Neden önemli:**  
Motorun oluşturulması temeldir — olmadan **OCR için görüntü yükleme** yapılamaz. Dil paketlerini etkinleştirmek, motorun “Ŀ”, “Ҕ” ve “Ǣ” gibi karakterleri doğru tanımasını sağlar. Bu adımı atlamanız, Latin dışı betiklerde bozuk çıktı almanıza yol açar.

## Adım 2: Çok Dilli Metin İçeren Görüntüyü Yükleyin

Şimdi motoru işlemek istediğimiz dosyaya yönlendirelim. Yol mutlak ya da göreli olabilir; sadece okunabilir bir görüntüye işaret ettiğinden emin olun.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![OCR örneği nasıl yapılır](/images/ocr-example.png "çok dilli bir görüntüde OCR nasıl yapılır")

**Neden önemli:**  
`load_image` çağrısı piksel verilerini belleğe okur ve OCR algoritması için hazırlar. Görüntü büyükse, motor otomatik olarak ölçeklendirebilir; yüksek çözünürlüklü taramalar için daha sonra `engine.set_max_resolution(3000)` ile ince ayar yapabilirsiniz.

## Adım 3: Tanıma İşlemini Çalıştırın

Motor hazır ve görüntü yüklendi, artık metin içeriğini çıkarabiliriz.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Neden önemli:**  
`recognize()` arka planda ağır bir sinir ağı çalıştırır. Ham metni, güven skorlarını ve isterseniz görsel hata ayıklama için sınırlayıcı kutuları içeren bir nesne döndürür.

## Adım 4: Tanınan Metni Çıktılayın

Motorun ne bulduğunu görelim. Metni konsola yazdıracağız, ancak isterseniz bir dosyaya ya da veritabanına da kaydedebilirsiniz.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Beklenen Çıktı

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Böyle bir şey görürseniz, **görüntüyü metne dönüştürme** ve **özel karakterleri tanıma** işlemlerini başarıyla tamamlamışsınız demektir.

## Yaygın Sorunlarla Baş Etme

Basit bir betik olsa da birkaç aksaklıkla karşılaşabilirsiniz. İşte kendi deneyimlerimden pratik ipuçları.

### 1. Dil Paketleri Eksik

Eğer Kiril harfleri yerine soru işaretleri (`?`) görüyorsanız, dil paketlerinin yüklü olduğundan emin olun. Birçok OCR motoru için ilgili `.traineddata` dosyalarını indirip motorun `tessdata` klasörüne koymanız gerekir.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Düşük Görüntü Kalitesi

Bulanık ya da düşük kontrastlı görüntüler düşük güven skorları üretir. Görüntüyü OpenCV ile ön işleme tabi tutun:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Büyük Dosyalar ve Bellek Kullanımı

10 MB bir fotoğraf işlemek belleği zorlayabilir. Çözünürlüğü sınırlamak için `engine.set_max_image_size(2000)` kullanın ya da görüntüyü parçalara bölüp her parçayı ayrı ayrı OCR’a gönderin.

### 4. Sınırlayıcı Kutuları Yakalama

Her kelimenin nerede göründüğünü vurgulamanız (UI katmanları için faydalı) gerekiyorsa, `result.boxes` özelliğine erişin:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Tam Betik – Tek‑Tıkla Çalıştırma

Her şeyi bir araya getirdik; işte `python ocr_demo.py` olarak çalıştırabileceğiniz tek dosya. Hata yönetimi, isteğe bağlı ön işleme ve açıklayıcı yorumlar içerir.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Şöyle çalıştırın:

```bash
python ocr_demo.py path/to/multilingual.png
```

Daha önce gösterilen aynı çıktıyı görmelisiniz; bu da **görüntüden metin çıkarma** işlemini başarıyla tamamladığınızı doğrular.

## Sonuç

Python’da **OCR nasıl yapılır** konusunu baştan sona ele aldık: kütüphaneyi kurma, görüntüyü yükleme, çok dilli içeriği tanıma ve en yaygın kenar durumlarıyla başa çıkma. Bu kılavuzu izleyerek artık kendi projelerinizde **görüntüyü metne dönüştürme**, **özel karakterleri tanıma** ve **görüntüden metin çıkarma** yapabilirsiniz — manuel transkripsiyona son.

Sırada ne var? Şunları deneyin:

- Daha fazla dil paketi ekleyin (ör. `spa` İspanyolca).  
- Sonuçları JSON’a aktararak sonraki iş akışları için hazırlayın.  
- OCR adımını bir Flask API’sine entegre edip diğer hizmetlerin kullanımına açın.  

Herhangi bir sorunla karşılaşırsanız, çoğu OCR kütüphanesinin aktif bir topluluğu vardır — “ocr library language pack installation” gibi anahtar kelimelerle arama yapın ya da aşağıya yorum bırakın. Kodlamanın tadını çıkarın, ve resimleri aranabilir metne dönüştürmenin keyfini yaşayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}