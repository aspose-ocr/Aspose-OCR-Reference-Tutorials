---
category: general
date: 2026-07-05
description: Python'da OCR için görüntüyü nasıl yükleyeceğinizi ve görüntüden metni
  nasıl çıkaracağınızı öğrenin. Bu adım adım öğretici, OCR kütüphanesini verimli bir
  şekilde nasıl kullanacağınızı gösterir.
draft: false
keywords:
- load image for OCR
- extract text from image python
- how to use OCR library
- Python OCR tutorial
- OCR performance metrics
language: tr
og_description: Python'da OCR için görüntüyü yükleyin ve görüntüden Python tarzında
  metin çıkarın. Performans ölçütleriyle OCR kütüphanesini nasıl kullanacağınızı öğrenmek
  için bu rehberi izleyin.
og_title: Python'da OCR için Görüntü Yükleme – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to load image for OCR in Python and extract text from image
    python style. This step‑by‑step tutorial shows how to use OCR library efficiently.
  headline: Load Image for OCR in Python – Complete Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Python'da OCR için Görüntü Yükleme – Tam Rehber
url: /tr/python-java/general/load-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR için Görüntü Yükleme – Tam Kılavuz

Hiç **load image for OCR** yapmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz; birçok geliştirici ilk kez resimlerden metin çıkarma üzerine çalıştığında bu engelle karşılaşıyor. Bu öğreticide, **how to use OCR library** gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz; paketi kurmaktan tüm karakterleri çekmeye ve performansı ölçmeye kadar.

Bir fiş‑tarama uygulaması ya da otomatik form‑işleyici geliştirdiğinizi hayal edin. **load image for OCR** işlemini güvenilir bir şekilde yapıp metni çıkardığınız anda, geri kalan işlem hattı sorunsuz çalışır. Hadi dalalım ve bugün bunu çalışır hâle getirelim.

## Ne Öğreneceksiniz

- **loads image for OCR** yapan temiz bir Python betiği, tanıma çalıştırır ve hem çıkarılan metni hem de performans istatistiklerini yazdırır.  
- Her adımın neden önemli olduğunu, sadece “ne”yi değil “neden”i de anlayacaksınız.  
- Yaygın tuzakları (yanlış dil, büyük dosyalar, bellek dalgalanmaları) ele alma ipuçları.  
- Örneği genişletmek için hızlı bir yol haritası—ön‑işleme ekleyin, toplu işleme yapın veya farklı bir OCR motoruna geçin.

### Ön Koşullar

- Python 3.8+ yüklü (kod f‑string kullanıyor).  
- pip ve sanal ortamlar hakkında temel bilgi.  
- İşlemek istediğiniz bir görüntü dosyası (PNG, JPEG, TIFF hepsi çalışır).  

OCR kütüphanesi dışındaki ağır bağımlılıklar yok, bu yüzden birkaç dakika içinde çalışır hâle geleceksiniz.

---

## Adım 1: OCR Kütüphanesini Kurun ve İçe Aktarın

İlk olarak bir Python OCR paketine ihtiyacımız var. Paylaştığınız snippet genel bir `ocr` modülü kullanıyor, bu yüzden `pip install ocr` ile gelen popüler **ocr** sarmalayıcısını kullandığınızı varsayalım. `pytesseract` tercih ederseniz kavramlar aynı kalır; sadece import satırlarını değiştirin.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # on Windows use `venv\Scripts\activate`

# Install the OCR library
pip install ocr
```

Şimdi ihtiyacınız olan parçaları içe aktarın:

```python
import ocr               # The main OCR package
import os                # For path handling and optional file checks
```

> **Pro tip:** `requirements.txt` dosyanızı düzenli tutun—sadece `ocr==<latest>` ekleyin, böylece gelecekteki derlemeler tekrarlanabilir olur.

---

## Adım 2: OCR Motorunu Başlatın ve Dili Ayarlayın

Neden açık bir motor nesnesi oluşturmalıyız? Çoğu OCR arka‑uç (Tesseract, EasyOCR, vb.) motorun hangi dil modelini yükleyeceğini belirttiğiniz bir yapılandırma aşaması gerektirir. Bu adımı atlamak bozuk çıktı ya da çok daha yavaş işleme ile sonuçlanabilir.

```python
# Step 2: Initialize the OCR engine and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # Switch to 'ocr.Language.SPANISH' for Spanish text
```

Çok dilli belgeler işlemeniz gerektiğinde sadece `language` özniteliğini değiştirin ya da bir liste geçin—çoğu kütüphane virgülle ayrılmış bir dize kabul eder.

---

## Adım 3: OCR için Görüntüyü Yükleyin

İşte öğretinin kalbi: **load image for OCR**. `ocr.Image.load` yöntemi dosyayı motorun anlayacağı iç formatta okur. Ayrıca küçük bir doğrulama yapar (ör. dosyanın varlığını kontrol eder).

```python
# Step 3: Load the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")

# Guard against missing files – a small but often‑overlooked edge case
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Cannot find image at {image_path}")

image = ocr.Image.load(image_path)
```

> **Neden önemli:** Görüntüyü erken yüklemek, boyutlarını, DPI’sını veya renk modunu incelemenizi sağlar—daha sonra ön‑işleme (ör. gri tonlamaya dönüştürme) için ihtiyaç duyabileceğiniz bilgiler.

---

## Adım 4: OCR Tanımasını Gerçekleştirin

Şimdi nihayet **extract text from image python** tarzında metni çıkarıyoruz. `engine.recognize` çağrısı ağır işi yapar: sinir ağını ya da klasik desen eşleştiriciyi çalıştırır, ardından ham metin, güven puanları ve zaman ölçümleri içeren bir sonuç nesnesi döndürür.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

`result` nesnesi tipik olarak şu özniteliklere sahiptir:

- `text` – tanınan karakterlerin düz metin dizisi.  
- `confidence` – 0 ile 1 arasında, genel kesinliği gösteren bir ondalık sayı.  
- `processing_time` – motorun bu görüntü üzerinde harcadığı milisaniye.  
- `memory_used` – işlem sırasında ayrılan kilobayt miktarı.

---

## Adım 5: Çıkarılan Metni ve Performans Metriklerini Görüntüleyin

Her şeyi düzenli bir formatta yazdıralım. Bu sadece “how to use OCR library” merakını gidermekle kalmaz, aynı zamanda profil oluşturma için hızlı geri bildirim sağlar.

```python
# Step 5: Output the recognized text and performance metrics
print("=== OCR RESULT ===")
print(result.text)                         # The extracted text
print(f"Confidence: {result.confidence:.2%}")  # Convert to percentage
print(f"Time taken: {result.processing_time} ms")
print(f"Memory used: {result.memory_used} KB")
```

**Beklenen çıktı** (gerçek metniniz görüntüye bağlı olarak farklı olacaktır):

```
=== OCR RESULT ===
Performance Test
Confidence: 98.73%
Time taken: 124 ms
Memory used: 58 KB
```

Güven puanı düşükse, ikilileştirme veya eğrilik giderme gibi ön‑işleme adımlarını düşünün—bunlar “sonraki adımlar” bölümünde ele alınmıştır.

---

## Adım 6: Kenar Durumları ve Yaygın Tuzakları Ele Alma

Mükemmel bir betik bile gerçek dünya verileriyle karşılaştığında sorun yaşayabilir. Aşağıda karşılaşabileceğiniz birkaç senaryo ve bunlara karşı alabileceğiniz önlemler yer alıyor.

| Durum | Kontrol Edilecek | Hızlı Çözüm |
|-----------|---------------|-----------|
| **Wrong language** | `engine.language` metinle eşleşmiyor | `engine.language = ocr.Language.FRENCH` ayarlayın veya `engine.languages = ["ENGLISH", "SPANISH"]` kullanın. |
| **Huge image ( > 5 MB )** | Bellek dalgalanmaları, daha uzun `processing_time` | Yüklemeden önce `PIL.Image.thumbnail` ile küçültün. |
| **No text found** | `result.text` boş, confidence 0 | Görüntü kontrastını kontrol edin; adaptif eşikleme deneyin. |
| **Library not found** | `ocr` üzerinde ImportError | Doğru paketi kurduğunuzdan emin olun (`pip install ocr`) ve sanal ortamınızı aktif edin. |

```python
# Example: simple preprocessing with Pillow
from PIL import Image as PilImage

def preprocess(path):
    img = PilImage.open(path)
    # Convert to grayscale and resize to a max of 1024px width
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    # Save to a temporary file that OCR can read
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

# Use the helper
image = preprocess(image_path)
result = engine.recognize(image)
```

---

## Adım 7: Hepsini Bir Araya Getirin – Tam Betik

Aşağıda **loads image for OCR** yapan, metni çıkaran ve performans sayılarını yazdıran, tamamen çalıştırılabilir program yer alıyor. `ocr_demo.py` dosyasına kopyalayıp `python ocr_demo.py` ile çalıştırın.

```python
#!/usr/bin/env python3
"""
Load Image for OCR in Python – Full Example
Demonstrates how to use OCR library, extract text from image python, and measure performance.
"""

import os
import ocr
from PIL import Image as PilImage   # Optional, for preprocessing

def preprocess(image_path: str) -> ocr.Image:
    """Resize and grayscale the image to improve OCR accuracy."""
    img = PilImage.open(image_path)
    img = img.convert("L")
    img.thumbnail((1024, 1024))
    tmp_path = "temp_preprocessed.png"
    img.save(tmp_path)
    return ocr.Image.load(tmp_path)

def main():
    # 1️⃣ Initialize engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Locate image
    image_path = os.path.join("YOUR_DIRECTORY", "performance_test.png")
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # 3️⃣ Load image for OCR (with optional preprocessing)
    image = preprocess(image_path)          # Swap with ocr.Image.load(image_path) if you skip preprocessing

    # 4️⃣ Recognize text
    result = engine.recognize(image)

    # 5️⃣ Show results
    print("=== OCR RESULT ===")
    print(result.text)
    print(f"Confidence: {result.confidence:.2%}")
    print(f"Time taken: {result.processing_time} ms")
    print(f"Memory used: {result.memory_used} KB")

if __name__ == "__main__":
    main()
```

**Çalıştırın**:

```bash
python ocr_demo.py
```

`performance_test.png` dosyasından metni, işlem süresini ve bellek kullanımını görmelisiniz. Sayılar garip görünüyorsa, ön‑işleme fonksiyonunu gözden geçirin veya dil ayarını tekrar kontrol edin.

---

## Sonuç

Python’da **load image for OCR**, **extract text from image python** tarzında metin çıkarma ve işlemin hızını ölçme konularını ele aldık—gerçek bir projede *how to use OCR library* sorusunu soran herkes için temel beceriler. Betik, bir bakışta anlaşılacak kadar küçük, toplu işler, bulut fonksiyonları veya mobil back‑end’lere genişletilebilecek kadar esnek.

Sırada ne var? `ocr` yerine `pytesseract` deneyin ve API’nin nasıl değiştiğini görün, farklı dil paketleriyle oynayın ya da çıktıyı aranabilir PDF’ler için bir veritabanına entegre edin. Temel artık sağlam, yeniden tekerlek icat etmeden üzerine inşa edebilirsiniz.

Belirli bir görüntü türü hakkında sorularınız mı var, ya da PDF’leri doğrudan nasıl işleyeceğinizi öğrenmek mi istiyorsunuz? Bırakın bir

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Görüntüden Metin Çıkarma – Aspose OCR ile Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Görüntü OCR – OCR Görüntü Tanıma’da Görüntü Üzerinde OCR Yapma](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}