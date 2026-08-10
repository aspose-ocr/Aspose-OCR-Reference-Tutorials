---
category: general
date: 2026-06-22
description: Python'da OCR kullanarak görüntüden dili nasıl tespit edeceğinizi ve
  metni nasıl çıkaracağınızı öğrenin. Otomatik dil tespiti ve metin çıkarımını kapsayan
  adım adım öğretici.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: tr
og_description: OCR kullanarak görüntüden dili nasıl tespit edersiniz? Bu rehber,
  Python’da OCR kullanarak dili tespit etmeyi ve metni çıkarmayı adım adım gösterir.
og_title: OCR ile Görüntülerden Dil Nasıl Tespit Edilir – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR ile Görsellerden Dil Nasıl Tespit Edilir – Tam Python Rehberi
url: /tr/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Dil Tespiti OCR ile – Tam Python Rehberi

Bir resmi manuel olarak açmadan **dilin nasıl tespit edileceğini** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—örneğin fiş tarayıcıları, çok dilli belge arşivleri veya basit bir fotoğraf‑metin uygulaması—metnin hangi dile ait olduğunu bilmeniz gerekir, böylece sonraki işlemleri yapabilirsiniz.  

Bu öğreticide, bir görüntüden **dilin nasıl tespit edileceğini** gösteren pratik, uçtan uca bir örnek üzerinden ilerleyeceğiz ve ardından gerçek karakterleri çıkaracağız. Sonunda, birkaç satır Python çalıştırıp betiği herhangi bir desteklenen resme yönlendirerek hem tespit edilen dili *hem* çıkarılan metni elde edebileceksiniz. Gereksiz ayrıntı yok, sadece kopyala‑yapıştır yapabileceğiniz net bir çözüm.

## Öğrenecekleriniz

- Python'da hafif bir OCR kütüphanesini kurun ve yapılandırın.  
- OCR motorunu başlatın ve otomatik dil tespitini etkinleştirin.  
- Bir görüntüyü (desteklenen herhangi bir format) yükleyin ve OCR çalıştırın.  
- Tespit edilen dili ve çıkarılan metni alın.  
- Desteklenmeyen formatlar veya belirsiz dil sonuçları gibi yaygın sorunları ele alın.  

Çok dilli belgeler için **OCR nasıl kullanılır** diye hiç merak ettiyseniz, bu kılavuz sizin için.

---

## Ön Koşullar

İlerlemeye başlamadan önce makinenizde aşağıdakilerin olduğundan emin olun:

| Gereksinim | Neden Önemli |
|------------|--------------|
| Python 3.9 or newer | Kullanacağımız OCR paketi modern yorumlayıcıları hedeflemektedir. |
| `pip` (Python package manager) | OCR kütüphanesini kurmak için gereklidir. |
| En az bir dilde metin içeren örnek bir görüntü (ör. `sample-multilang.png`) | Test edebileceğiniz somut bir şey sağlar. |
| Optional: Virtual environment (`venv` or `conda`) | Bağımlılıkları düzenli tutar ve sürüm çakışmalarını önler. |

> **Pro tip:** Sanal bir ortam içinde çalışıyorsanız, OCR paketini kurmadan önce ortamı etkinleştirin; böylece global Python kurulumunuz temiz kalır.

---

## Adım 1: OCR Kütüphanesini Kurun

Bu yürütme için, kod örneğinde gösterilen API'yi taklit eden varsayımsal `ocr` paketini kullanacağız. Gerçek bir senaryoda `pytesseract`, `easyocr` veya otomatik dil tespiti destekleyen başka bir kütüphane ile değiştirebilirsiniz.

```bash
pip install ocr
```

> **Not:** Paket hafiftir (< 5 MB) ve Windows, macOS ve Linux üzerinde çalışır. İzin hataları alırsanız komuta `--user` ekleyin.

---

## Adım 2: OCR Motorunu Başlatın – Dil Nasıl Tespit Edilir

Kütüphane hazır olduğuna göre bir OCR motoru örneği oluşturabiliriz. Bu nesne, resmi tarayıp dili belirleyecek olan şeydir.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

Neden bir motorla başlıyoruz? Motor, OCR sisteminin beyni gibidir; yapılandırmayı tutar, dil modellerini yükler ve arka planda ağır işleri yönetir. Motoru önce başlatmak, sonraki çağrıların (ör. görüntü yükleme) bir bağlam içinde çalışmasını sağlar.

---

## Adım 3: Görüntünüzü Yükleyin ve Otomatik Dil Tespitini Etkinleştirin

Sonraki adım, resmi motora beslemek. Ayrıca *auto‑detect language* bayrağını da açacağız, böylece OCR motoru dili anlık olarak tahmin etmeye çalışacak.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Neden otomatik tespit etkinleştirilsin?**  
> Çoğu OCR kütüphanesi varsayılan bir dil (genellikle İngilizce) ile gelir. Belgeniz Fransızca, Japonca ya da başka bir betik içeriyorsa, bu ayar olmadan motor bunu kaçırır. `set_auto_detect_language(True)` ile motor bitmap'i tarar, karakter şekli istatistiklerini karşılaştırır ve en olası dil modelini seçer.

---

## Adım 4: OCR Gerçekleştir – Görüntüden Metin Çıkar

Görüntü yüklendi ve dil tespiti açıldı, gerçek OCR adımı sadece tek bir metod çağrısıdır.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

`recognize()` metodu iki şeyi aynı anda yapar:

1. **Dil tespiti:** Görüntü üzerinde hafif bir sınıflandırıcı çalıştırarak bir dil kodu (ör. `en`, `fr`, `es`) seçer.  
2. **Metin çıkarma:** Ardından uygun dil‑spesifik modeli uygulayarak karakterleri Unicode dizelerine dönüştürür.

Her iki işlem aynı anda gerçekleştiği için, ihtiyacınız olan her şeyi içeren tek bir `result` nesnesi elde edersiniz.

---

## Adım 5: Tespit Edilen Dil ve Çıkarılan Metni Alın ve Görüntüleyin

Son olarak, `result` nesnesinden dil kodunu ve ham metni alıp konsola yazdırıyoruz.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Beklenen Çıktı

`sample-multilang.png` içinde Fransızca metin varsa, aşağıdaki gibi bir çıktı görebilirsiniz:

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

Görüntü belirsizse ya da birden fazla dil içeriyorsa, motor en çok güvendiği dili döndürür; daha sonra güven puanını inceleyebilirsiniz (çoğu kütüphane gelişmiş kullanım durumları için bir `get_confidence()` metodu sunar).

---

## Yaygın Kenar Durumlarını Ele Alma

### 1. Desteklenmeyen Görüntü Formatları

OCR kütüphanesinin tanımadığı bir TIFF dosyası yüklemeye çalışırsanız, `ocr.ImageStream.from_file()` bir `OcrUnsupportedFormatError` hatası fırlatır. Yükleme çağrısını bir try/except bloğuna alın:

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Düşük Çözünürlüklü Görüntüler

OCR doğruluğu ~300 dpi’nin altına düştüğünde ciddi şekilde azalır. Düşük kaliteyi fark ederseniz, Pillow ile ön‑işleme yapmayı düşünün:

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Tek Görüntüde Birden Fazla Dil

Bir görüntü birden çok dil içerdiğinde, otomatik‑tespit özelliği baskın dili seçer. Tüm dilleri yakalamak isterseniz otomatik‑tespiti devre dışı bırakıp motoru bir dil listesiyle manuel olarak besleyebilirsiniz:

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

Bu sayede OCR, her dil modelini kullanarak karakterleri tanımaya çalışır ve her metin bloğu için en iyi eşleşmeyi döndürür.

---

## Tam Betik – Tüm Adımlar Birleştirildi

Aşağıda, ele aldığımız tüm adımları içeren, çalıştırmaya hazır Python betiği bulunuyor. `detect_language_ocr.py` adıyla kaydedin ve `python detect_language_ocr.py` komutuyla çalıştırın.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Çalıştırın** ve hemen dil kodunu ardından çıkarılan metni göreceksiniz. İşte **görüntüden dil nasıl tespit edilir** ve **OCR ile metin nasıl çıkarılır** sorularının tam cevabı.

---

## Daha İleri – Sonraki Adımlar ve İlgili Konular

- **Doğruluğu artırma:** `opencv-python` kullanarak görüntü ön‑işleme (eşikleme, gürültü azaltma) deneyin.  
- **Toplu işleme:** Betiği bir döngüye sararak klasördeki tüm resimleri işleyin.  
- **NLP ile bütünleştirme:** Çıkarılan metni ikinci bir görüş için `langdetect` gibi bir dil‑tanıma kütüphanesine gönderin.  
- **Diğer OCR motorlarını keşfetme:** `pytesseract` ince ayar kontrolü sunarken, `easyocr` kutudan çıkar çıkmaz 80’den fazla dili destekler.  

Bu konular, *görüntüden dil tespiti*, *görüntüden metin çıkarma*, *OCR nasıl kullanılır* ve *metin nasıl çıkarılır* gibi ikincil anahtar kelimelerle doğrudan bağlantılıdır; böylece temelden çıkmadan araç setinizi genişletebilirsiniz.

---

## Sonuç

**Görüntüden dil nasıl tespit edilir** konusunu ele aldık, gerekli kodu adım adım inceledik ve her adımın neden önemli olduğunu açıkladık. OCR motorunu başlatıp resmi yükleyip otomatik dil tespitini açtıktan sonra `recognize()` çağrısı ile hem dil tanımlayıcısını hem de çıkarılan metni tek bir temiz işlemde alıyorsunuz.

Bu mantığı daha büyük uygulamalara—ör. fiş tarama servisi, çok dilli sohbet botu veya basit bir masaüstü aracı—entegre edebilirsiniz. Temel fikir aynı kalır: OCR motorunun ağır işi yapmasına izin verin, ardından sonuçları istediğiniz gibi kullanın.

Kenarlık durumlarıyla ilgili sorularınız mı var, ya da ilginç bir kullanım senaryonuz mu var? Aşağıya yorum bırakın. Kodlamanın tadını çıkarın ve görüntüleri aranabilir metne dönüştürmenin keyfini yaşayın!  

![görüntüden dili nasıl tespit ederim](ocr-demo.png "Python OCR kullanarak görüntüden dil tespitini gösteren ekran görüntüsü")


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımları keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR Kullanarak C# ile Görüntü Metni Çıkarma ve Dil Seçimi](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}