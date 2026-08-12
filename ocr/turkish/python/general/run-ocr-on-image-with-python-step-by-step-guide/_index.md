---
category: general
date: 2026-08-12
description: Python ve Aspose AI kullanarak görüntüde OCR çalıştırın, görüntüden metin
  çıkarın ve bir yazım denetimi sonrası işlemcisiyle OCR doğruluğunu artırın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: tr
lastmod: 2026-08-12
og_description: Python’da görüntü üzerinde OCR çalıştırın ve Aspose AI sonrası işleme
  ile OCR doğruluğunu artırarak görüntüden metni anında çıkarın.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Python ile Görüntüde OCR Çalıştırma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Python ile Görüntüde OCR Çalıştırma – Adım Adım Kılavuz
url: /tr/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Görüntü Üzerinde OCR Çalıştırma – adım adım rehber

Python'da **run OCR on image** dosyalarına ihtiyacınız varsa, bu rehber size tüm iş akışını adım adım gösterir. **extract text from image** nasıl yapılacağını, **OCR text correction** uygulamayı ve sadece birkaç satır kodla **improve OCR accuracy** öğreneceksiniz.

Taranmış belgeler, makbuzlar veya ekran görüntüleri işlemek genellikle gürültülü metinler üretir. Bir yazım‑denetimi sonrası işlemci ekleyerek ham OCR çıktısını ayrı bir araca geçmeden temiz, aranabilir içeriğe dönüştürebilirsiniz. Bu öğreticide ihtiyacınız olan her şey ele alınır—görüntünün yüklenmesinden düzeltilmiş sonucun gösterilmesine kadar.

## Önkoşullar

* Python 3.9 veya daha yeni bir sürüm yüklü.
* Aspose.OCR ve Aspose.AI Python paketlerine (veya eşdeğer açık kaynak sarmalayıcılara) erişim.
* Bilinen bir dizine yerleştirilmiş örnek bir görüntü (ör. `sample.png`).
* Python fonksiyonları ve nesne‑yönelimli kod hakkında temel bilgi.

Gerekli kütüphaneleri pip ile kurabilirsiniz:

```bash
pip install aspose-ocr aspose-ai
```

> **Pro tip:** Bağımlılıkları izole tutmak için bir sanal ortam kullanın (`python -m venv .venv`).

## Adım 1: Görüntü Üzerinde OCR Çalıştırma – motor örneğini oluşturma

İlk adım bir `OcrEngine` nesnesi oluşturmaktır. Bu nesne OCR motoru yapılandırmasını kapsar ve görüntü işleme ve tanıma için yöntemler sağlar.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Motoru bir kez oluşturup birden çok görüntüde yeniden kullanmak, başlangıç yükünü azaltır ve oturum boyunca tutarlı ayarların sağlanmasını garantiler.

## Adım 2: OCR için Görüntüyü Yükleme

Tanıma gerçekleşmeden önce, motorun hangi resmi analiz edeceğini bilmesi gerekir. `load_image` yöntemi bir dosya yolu ya da ikili akış kabul eder.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Neden önemli:** Görüntüyü doğru yüklemek, doğru OCR için temeldir. Yüksek çözünürlüklü bir görüntü (300 dpi veya daha yüksek) sağlamak genellikle **improve OCR accuracy** çünkü motor karakterleri daha net ayırt edebilir.

## Adım 3: Görüntüden Metin Çıkarma – temel tanıma gerçekleştirme

Görüntü yüklendikten sonra, bir sonuç nesnesi elde etmek için `recognize()` çağırabilirsiniz. Sonuç, ham metni, güven skorlarını ve isteğe bağlı olarak her kelime için sınırlayıcı kutuları içerir.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Bu noktada **run OCR on image** işlemini başarıyla gerçekleştirdiniz ve ham karakterleri çıkardınız. Ancak, özellikle düşük kaliteli taramalarda metin hatalı yazımlar içerebilir.

## Adım 4: OCR metin düzeltmesi – bir sonrası‑işlem yazım‑denetleyicisi ekleme

Aspose AI esnek bir sonrası‑işlem hattı sunar. Özel bir yazım‑denetleyici ekleyerek tipik OCR hatalarını (ör. “l” vs. “1”, “O” vs. “0”) düzeltebilirsiniz.

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Yazım‑denetleyicinin nasıl çalıştığı:** `MySpellChecker` bir `process(text: str) -> str` metodunu uygulamalıdır. İçinde, `pyspellchecker` veya `symspellpy` gibi kütüphaneleri kullanarak olası olmayan kelime dizilerini sözlük‑doğrulamalı alternatiflerle değiştirebilirsiniz.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Adım 5: Orijinal ve düzeltilmiş OCR metnini gösterme

Son olarak, ham ve düzeltilmiş çıktıları karşılaştırın. Bu, **OCR text correction**'ın gerçekten **improve OCR accuracy** sağladığını kullanım senaryonuzda doğrulamanıza yardımcı olur.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Beklenen çıktı

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Düzeltilen satır, yazım‑denetleyicinin yaygın OCR hatalarını (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`) değiştirdiğini gösterir.

## Adım 6: OCR doğruluğunu artırma – en iyi uygulama kontrol listesi

Sonrası‑işlemle bile, OCR motorunun temel kalitesini artırabilirsiniz:

| Checklist item | Why it helps |
|----------------|--------------|
| **Yüksek çözünürlüklü görüntüler kullanın (≥300 dpi)** | Daha fazla piksel verisi karakter belirsizliğini azaltır. |
| **Renkli görüntüleri gri tonlamaya dönüştürün** | Motoru yanıltabilecek renk gürültüsünü ortadan kaldırır. |
| **Görüntü eğrilik düzeltmesi uygulayın** | Eğik metni düzleştirir, satır sonu hatalarını önler. |
| **Dil/bölgeyi açıkça ayarlayın** | Tanıyıcıyı doğru karakter setine yönlendirir. |
| **Dil modelini etkinleştirin** (kütüphane destekliyorsa) | Bağlam‑bilgili tahminler sağlar, **improve OCR accuracy**'ı daha da artırır. |

Bu ön‑işleme adımlarını, görüntüyü `ocr_engine`'e vermeden önce Pillow veya OpenCV ile uygulayabilirsiniz.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Tam çalıştırılabilir betik

Her şeyi bir araya getirerek, aşağıdaki betik `run_ocr.py` adlı bir dosyaya kopyalayıp yapıştırmaya ve çalıştırmaya hazır.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Betik çalıştırıldığında, orijinal ve düzeltilmiş metinler yazdırılır; bu da **run OCR on image**, **extract text from image** ve **OCR text correction** aracılığıyla **improve OCR accuracy**'ı başarıyla gerçekleştirdiğinizi doğrular.

## Sonuç

Artık Python'da **run OCR on image** dosyalarını nasıl çalıştıracağınızı, ham metni nasıl çıkaracağınızı ve daha temiz sonuçlar elde etmek için bir sonrası‑işlem yazım‑denetleyicisi uygulayacağınızı biliyorsunuz. **improve OCR accuracy** için kontrol listesini izleyerek bu iş akışını makbuzlar, faturalar, kimlik kartları veya herhangi bir taranmış belgeye uyarlayabilirsiniz.

### Sıradaki adımlar?

* **language‑specific dictionaries**'i çok dilli OCR için keşfedin.
* Çıkarılan metni aranabilir kılmak için boru hattını bir veritabanı veya arama indeksi (ör. Elasticsearch) ile bütünleştirin.
* Daha yüksek doğruluk için basit yazım‑denetleyiciyi sinirsel bir dil modeli (ör. GPT‑tabanlı düzeltme) ile değiştirin.

## Sonra Ne Öğrenmelisin?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Görüntüyü Metne Dönüştür: Aspose OCR (Python) Kullanarak Görüntüden Metin Çıkarma](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Rehber](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}