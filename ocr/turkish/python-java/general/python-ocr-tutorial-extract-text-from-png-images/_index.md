---
category: general
date: 2026-06-25
description: Metin PNG dosyalarını çıkarmayı, metin görüntüsünü okumayı ve basit,
  lisans ücreti olmayan bir motor kullanarak görüntü metnini tanımayı gösteren Python
  OCR öğreticisi.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: tr
og_description: Python OCR öğreticisi, OCR için görüntü yüklemeyi, PNG dosyalarından
  metin çıkarmayı ve sadece birkaç satır kodla görüntü metnini tanımayı öğretir.
og_title: Python OCR Öğreticisi – PNG'den Metin Çıkarma
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Python OCR Öğretici: PNG Görsellerinden Metin Çıkarma'
url: /tr/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Eğitimi – PNG Görsellerinden Metin Çıkarma

Hiç **python ocr tutorial** bir fişin ekran görüntüsünü düzenlenebilir metne nasıl dönüştürebileceğini merak ettiniz mi? Yalnız değilsiniz. Gerçek dünyadaki birçok projede *read text image* dosyalarını hızlıca **okumamız** gerekir ve bunu kendiniz yapmak, her seferinde bir GUI'den kopyala‑yapıştır yapmaktan daha iyidir.  

Bu rehberde, **extract text PNG** dosyalarını **load image for OCR** ile nasıl okuyacağınızı gösteren uygulamalı bir örnek üzerinden geçecek ve sonunda *recognize image text* sonucunu ekrana basacağız – hepsi ücretsiz, sadece değerlendirme amaçlı bir OCR motoru ile. Lisans anahtarı yok, ağır bağımlılıklar yok—sadece saf Python ve birkaç küçük paket.

## Öğrenecekleriniz

- Hafif OCR kütüphanesini nasıl kurup içe aktaracağınızı.
- **load image for OCR** adımlarını ve yaygın tuzakları nasıl yöneteceğinizi.
- Farklı kalite seviyelerindeki **read text image** dosyalarını okuma yolları.
- **extract text png** dosyalarını daha doğru hale getirmek için ipuçları.
- Tanınan dizeyi nasıl göstereceğinizi ve isteğe bağlı olarak diske nasıl yazacağınızı.

Bu eğitimin sonunda, **recognize image text** ihtiyacı olan herhangi bir projeye kolayca ekleyebileceğiniz yeniden kullanılabilir bir betiğe sahip olacaksınız. Sihir yok, sadece net kod ve açıklamalar.

### Önkoşullar

- Python 3.8 ve üzeri (kütüphane 3.7+ ile çalışır ancak 3.8+ önerilir).
- pip ve sanal ortamlar hakkında temel bilgi.
- `sample.png` adlı bir görüntü dosyası (veya test etmek istediğiniz herhangi bir PNG) erişebileceğiniz bir klasörde kaydedilmiş.

Eğer bunlardan biri size yabancı geliyorsa, bir dakikalık ara verin ve kurulumları yapın—sonuç buna değer.

---

## Python OCR Eğitimi – Motoru Kurma

İlk iş: bir OCR motoru nesnesine ihtiyacımız var. Kullanacağımız kütüphane, değerlendirme amaçlı kutudan çıkar çıkmaz çalışan yerel bir OCR motorunun küçük bir sarmalayıcısı. Lisans anahtarı gerektirmiyor, bu da *python ocr tutorial*'ı hızlı prototipler için mükemmel kılıyor.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Neden önemli:** Motoru oluşturmak, OCR çalışma zamanını kodunuzun geri kalanından izole eder; böylece ağır kaynakları her seferinde yeniden başlatmadan birden fazla görüntüde yeniden kullanabilirsiniz.

---

## Load Image for OCR – PNG Dosyasını Okuma

Motor mevcut olduğuna göre, *load image for OCR* yapmamız gerekiyor. Kütüphanenin `Image.load` yöntemi bir yol alır ve PNG, JPEG, BMP ve birkaç diğer formatı otomatik olarak çözer.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro ipucu:** PNG'niz bir alfa kanalı içeriyorsa, kütüphane bunu otomatik olarak atar. Ancak *read text image* görevlerinde en iyi sonuçlar için görüntüyü gri tonlamada tutun—bu, gürültüyü azaltır ve tanıma hızını artırır.

---

## Recognize Image Text – OCR Motorunu Çalıştırma

Görüntü nesnesi hazır olduğunda, nihayet **recognize image text** yapabiliriz. Bu, *python ocr tutorial*'ın çekirdeğidir ve sadece tek bir kod satırı gerektirir.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Arka planda ne oluyor?** Motor, bitmap'i milyonlarca karakter üzerinde eğitilmiş bir sinir ağına beslemeden önce bir dizi ön‑işleme filtresi (eğik düzeltme, ikilileştirme) uygular. Bu yüzden düşük çözünürlüklü PNG'lerde bile şaşırtıcı derecede doğru sonuçlar alırsınız.

---

## Çıkarılan Metni Görüntüleme ve Kaydetme

Sonucu elde etmek harika, ama muhtemelen ya görüp kontrol etmek ya da bir yere kaydetmek istersiniz. `result` nesnesi, düz metin çıktısını içeren bir `text` özelliği sunar.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Beklenen çıktı** (`sample.png` içinde “Hello, OCR!” olduğunu varsayarsak):

```
Eval-mode result: Hello, OCR!
```

Eğer okunabilir karakterler yerine çöp alıyorsanız, yaygın çözümler için bir sonraki bölüme bakın.

---

## Extract Text PNG Yaparken Yaygın Sorunları Ele Alma

En iyi OCR motorları bile bazı görüntülerde zorlanır. Aşağıda tipik engeller ve bunları aşma yolları yer alıyor.

### 1. Düşük Kontrast veya Koyu Arka Planlar

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Eğik Metin Satırları

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. İngilizce Olmayan Karakterler

PNG'niz aksanlı harfler veya Latin dışı yazı sistemleri içeriyorsa, motoru uygun dil paketini belirterek başlatın:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Çok Büyük Görüntüler

4000×3000 bir PNG işlemek yavaş olabilir. Okunabilirliği koruyarak ölçek küçültün:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Bu ayarlamalar, mutlu‑yol senaryosunun ötesinde çalışan sağlam bir *python ocr tutorial*'ın parçasıdır.

---

## Tam Betik – Tek‑Dosya Çözümü

Aşağıda, tartışılan tüm adımları ve isteğe bağlı iyileştirmeleri içeren, çalıştırmaya hazır tam betik yer alıyor. `ocr_extract.py` dosyasına kopyalayıp `python ocr_extract.py` komutuyla çalıştırın.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Çalıştırın:**  
```bash
python ocr_extract.py ./sample.png
```

Tanıdığınız dizeyi ekranda görecek ve görüntünün yanına `sample_extracted.txt` adlı bir dosya oluşturulmuş olacak.

---

## Görsel Genel Bakış

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt metin:* *Python OCR tutorial diyagramı, OCR için görüntü yüklemeden metin PNG çıkarımına kadar olan akışı gösteriyor.*

Diagram, **load image for OCR** → **recognize image text** → **extract text PNG** akışını lineer bir şekilde gösterir ve ön‑işleme adımlarını nerede ekleyebileceğinizi vurgular.

---

## Sonuç

Bir **python ocr tutorial** tamamladık; *load image for OCR*, *recognize image text* ve sonunda sadece birkaç Python komutuyla **extract text png** dosyalarını nasıl çıkaracağınızı gösterdik. Betik tam işlevsel, yaygın kenar durumlarını ele alıyor ve toplu işleme ya da çok‑dilli destek için genişletilebilir.

Bir sonraki meydan okumaya hazır mısınız? Motoru PDF'leri görüntülere dönüştürerek besleyin, farklı dil paketleriyle deney yapın veya OCR adımını bir Flask API'sine entegre edin; böylece web uygulamanız yüklenen ekran görüntülerini anında okuyabilir. *read text image* otomasyonu neredeyse sınırsızdır.

Sorularınız veya çözemediğiniz bir görüntünüz varsa, aşağıya yorum bırakın; birlikte sorun giderelim. İyi kodlamalar!

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}