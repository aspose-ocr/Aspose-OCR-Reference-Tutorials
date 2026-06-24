---
category: general
date: 2026-06-19
description: Aspose OCR kullanarak Python'da OCR doğruluğunu artırın. OCR dilini nasıl
  ayarlayacağınızı, OCR için görüntüyü nasıl yükleyeceğinizi ve özel bir sözlükle
  görüntüden metin nasıl çıkarılacağını öğrenin.
draft: false
keywords:
- improve OCR accuracy
- extract text from image
- perform OCR on image
- load image for OCR
- set OCR language
language: tr
og_description: Python'da OCR doğruluğunu artırmak için OCR dilini ayarlayın, OCR
  için bir görüntü yükleyin ve özel bir sözlükle görüntüden metin çıkarın.
og_title: Python'da OCR Doğruluğunu Artırın – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  headline: Improve OCR Accuracy in Python – Complete Guide
  type: TechArticle
- description: Improve OCR accuracy in Python using Aspose OCR. Learn how to set OCR
    language, load image for OCR, and extract text from image with a custom dictionary.
  name: Improve OCR Accuracy in Python – Complete Guide
  steps:
  - name: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
    text: '**Pre‑processing** – Apply contrast enhancement or binarization with Pillow
      before feeding the image to Aspose OCR.'
  - name: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
    text: '**Multiple Languages** – Set `engine.language = ocr.Language.English |
      ocr.Language.French` to enable bilingual recognition.'
  - name: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
    text: '**Region‑Based OCR** – If you only need a specific area (e.g., a table),
      crop the image first to reduce noise.'
  - name: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
    text: '**Confidence Filtering** – `result.confidence` gives a per‑character score;
      you can discard low‑confidence results programmatically.'
  - name: '**Setting the OCR language** to match your document.'
    text: '**Setting the OCR language** to match your document.'
  - name: '**Loading the image correctly** so the engine sees the right pixels.'
    text: '**Loading the image correctly** so the engine sees the right pixels.'
  - name: '**Performing OCR on the image** with a single method call.'
    text: '**Performing OCR on the image** with a single method call.'
  - name: '**Extracting text from the image** and confirming the result.'
    text: '**Extracting text from the image** and confirming the result.'
  - name: '**Adding a custom dictionary** to lock in domain‑specific terms.'
    text: '**Adding a custom dictionary** to lock in domain‑specific terms.'
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Python'da OCR Doğruluğunu Artırma – Tam Kılavuz
url: /tr/python-java/general/improve-ocr-accuracy-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Doğruluğunu Artırma – Tam Kılavuz

Metin taradığınızda garip semboller, ürün kodları ya da marka adları içeriyorsa **OCR doğruluğunu artırmanın** yollarını hiç merak ettiniz mi? Yalnız değilsiniz. Birçok projede varsayılan motor sadece anlamsız karakterler üretir ve bu gerçek bir verimlilik kaybıdır.

Bu öğreticide, **OCR dilini ayarlama**, **görüntüyü OCR için yükleme**, **görüntü üzerinde OCR gerçekleştirme** ve son olarak **görüntüden metin çıkarma** adımlarını gösteren pratik, uçtan‑uza bir örnek üzerinden ilerleyeceğiz. Ayrıca tanıma oranlarını artıran özel bir sözlük de ekleyeceğiz. Sonunda, herhangi bir Python kod tabanına ekleyebileceğiniz çalıştırmaya hazır bir betiğe sahip olacaksınız.

## Öğrenecekleriniz

- PNG dosyasını okuyan Aspose OCR kullanan tam işlevsel bir Python betiği.
- Dil ve özel kelime listesi yapılandırarak **OCR doğruluğunu artırma** yeteneği.
- Her ayarın neden önemli olduğuna dair net açıklamalar ve Latin dışı karakterler gibi kenar durumlarını ele almanın ipuçları.
- Yaygın OCR tuzaklarını gidermek için hızlı bir kontrol listesi.

### Ön Koşullar

- Makinenizde yüklü Python 3.8 veya daha yeni bir sürüm.  
- `aspose-ocr` paketi (`pip install aspose-ocr` ile kurulur).  
- Okumak istediğiniz metni içeren örnek bir görüntü (`technical_doc.png`).  
- Python’a temel aşinalık—fantezi bir şey gerekmez.

> **Pro tip:** Sanal bir ortamda çalışıyorsanız, paketi kurmadan önce ortamı etkinleştirin. Bağımlılıklarınızı düzenli tutar ve sürüm çakışmalarını önler.

---

## Adım 1: Aspose OCR’yi Kurun ve İçe Aktarın

İlk iş olarak, kütüphaneyi ortamımıza ekleyip ihtiyacımız olan parçaları içe aktaralım.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

import aspose.ocr as ocr
```

`aspose.ocr` ad alanı, OCR sürecinin kalbi olan `OcrEngine` sınıfına erişim sağlar. Burada içe aktarmak, betiğin geri kalanını temiz ve okunabilir tutar.

---

## Adım 2: Bir OCR Motoru Oluşturun ve **OCR Dilini Ayarlayın**

Dil neden önemlidir? OCR motorları, karakter şekillerini ve kelime kalıplarını tanımak için dile özgü modeller kullanır. Motorunuza İngilizce metin taradığınızı söylerseniz, Kiril alfabindeki karakterleri görmezden gelir ve Latin alfabine odaklanır; bu da **OCR doğruluğunu büyük ölçüde artırır**.

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Set the recognition language to English (you can pick other languages too)
engine.language = ocr.Language.English
```

> **Not:** Aspose OCR 50’den fazla dili destekler. Belgeniz İngilizce değilse `ocr.Language.English` yerine `ocr.Language.Spanish`, `ocr.Language.French` vb. kullanın.

---

## Adım 3: **Doğruluğu Artırmak İçin Özel Sözlük** Tanımlayın

Faturalarınızda “AsposeOCR” gibi bir kelime ya da “SKU12345” gibi ürün kodları olduğunu hayal edin. Motor bu terimleri bilmediği için yanlış tahminlerde bulunur. Özel bir kelime listesi sağlamak, motora *“Bu dizgiler geçerli—düzeltme yapma.”* demek gibidir. Bu, **OCR doğruluğunu artırma** için hızlı bir kazanımdır.

```python
# Step 3: Create a list of domain‑specific words
custom_word_list = [
    "AsposeOCR",   # brand name
    "InvoiceID",   # field label
    "SKU12345",    # product code
    "β‑cell"       # Greek character example
]

# Attach the custom dictionary to the engine
engine.text_processing.custom_dictionary = custom_word_list
```

Bu listeyi bir dosyadan ya da veritabanından da yükleyebilirsiniz; basitlik açısından bir Python listesinde tutmak yeterlidir.

---

## Adım 4: **OCR İçin Görüntüyü Yükleyin**

Şimdi bir görüntüye ihtiyacımız var. `Image.load` metodu, desteklenen herhangi bir raster formatının (PNG, JPEG, BMP vb.) yolunu kabul eder. Dosya bulunamazsa motor bir istisna fırlatır; bu yüzden buna karşı önlem alacağız.

```python
import os

image_path = "YOUR_DIRECTORY/technical_doc.png"

if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found: {image_path}")

# Step 4: Load the image into memory
image = ocr.Image.load(image_path)
```

> **Bu adımın önemi:** Görüntüyü doğru şekilde yüklemek, motorun analiz etmek istediğiniz tam piksel verileriyle çalışmasını sağlar. Bozuk dosyalar ya da yanlış yollar sıkça hayal kırıklığı yaratır.

---

## Adım 5: **Görüntü Üzerinde OCR Gerçekleştirin** ve Sonuçları Çıkarın

Motor yapılandırıldı ve görüntü hazır olduğunda, gerçek tanıma tek bir metod çağrısıdır. Sonuç nesnesi ham metni, güven skorlarını ve hatta isterseniz daha sonra kullanabileceğiniz yerleşim bilgilerini içerir.

```python
# Step 5: Run OCR
result = engine.recognize(image)

# The recognized text is stored in result.text
recognized_text = result.text
```

Metni satır satır **görüntüden metin çıkarma** ihtiyacınız varsa, yeni satır karakterlerine göre bölünebilir:

```python
lines = recognized_text.splitlines()
for idx, line in enumerate(lines, start=1):
    print(f"{idx:02d}: {line}")
```

---

## Adım 6: Çıktıyı Doğrulayın – Gerçekten **OCR Doğruluğunu Artırdı** mı?

Sonucu yazdıralım ve özel sözlüğümüzün bir fark yaratıp yaratmadığını görelim.

```python
print("\n--- OCR Output ---")
print(recognized_text)
```

Örnek görüntü için tipik çıktı şöyle görünebilir:

```
--- OCR Output ---
InvoiceID: 2023‑07‑15
Customer: AsposeOCR Ltd.
Product: β‑cell Therapy Kit
SKU: SKU12345
```

Marka adı, Yunan karakteri ve ürün kodunun tam olarak tanımladığımız gibi göründüğüne dikkat edin. Özel sözlük olmadan motor bunları “Aspose OCR” ya da “SKU 1234” gibi düzeltmeye çalışırdı.

---

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **Çöp karakterler** | Yanlış dil ayarı veya düşük çözünürlüklü görüntü | `engine.language` kaynağın diline eşleştiğinden ve yüksek DPI tarama (300 dpi veya üzeri) kullandığınızdan emin olun. |
| **Özel kelimeler yok sayılıyor** | Sözlük eklenmemiş veya özellik adında yazım hatası | `engine.text_processing.custom_dictionary = …` satırını iki kez kontrol edin. |
| **Dosya bulunamadı** | Yanlış yol veya eksik dosya izinleri | `os.path.abspath()` ile mutlak yolu doğrulayın; betiği uygun izinlerle çalıştırın. |
| **Yavaş işleme** | Büyük görüntüler veya çok sayıda sayfa | Görüntüyü ön‑işleyin (kırp, yeniden boyutlandır) veya `engine.recognize(image, max_threads=4)` ile paralel çalıştırın. |

---

## Daha İleri: **OCR Doğruluğunu Artırmak** İçin Gelişmiş Ayarlar

1. **Ön‑işleme** – Görüntüyü Aspose OCR’ye göndermeden önce Pillow ile kontrast artırma ya da ikilileştirme uygulayın.  
2. **Birden Çok Dil** – `engine.language = ocr.Language.English | ocr.Language.French` ile çift‑dilli tanıma etkinleştirin.  
3. **Bölge‑Bazlı OCR** – Sadece belirli bir alan (ör. tablo) gerekiyorsa, gürültüyü azaltmak için önce görüntüyü kırpın.  
4. **Güven Skoru Filtreleme** – `result.confidence` her karakter için bir puan verir; düşük güvenilir sonuçları programatik olarak elerken kullanabilirsiniz.

---

## Tam Çalışan Betik

Aşağıda, tartıştığımız tüm adımları içeren, kopyala‑yapıştır‑hazır betik yer alıyor. `improve_ocr_accuracy.py` adıyla kaydedin ve komut satırından çalıştırın.

```python
# improve_ocr_accuracy.py
# Complete example that shows how to improve OCR accuracy with Aspose OCR in Python.

import os
import aspose.ocr as ocr

def main():
    # ---------- Step 1: Initialize engine and set language ----------
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English          # set OCR language

    # ---------- Step 2: Attach custom dictionary ----------
    custom_word_list = [
        "AsposeOCR",
        "InvoiceID",
        "SKU12345",
        "β‑cell"
    ]
    engine.text_processing.custom_dictionary = custom_word_list

    # ---------- Step 3: Load the image ----------
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    image = ocr.Image.load(image_path)               # load image for OCR

    # ---------- Step 4: Perform OCR ----------
    result = engine.recognize(image)                 # perform OCR on image
    recognized_text = result.text

    # ---------- Step 5: Output the recognized text ----------
    print("\n--- OCR Output ---")
    print(recognized_text)

    # Optional: print line numbers for easier debugging
    print("\n--- Line‑by‑Line View ---")
    for idx, line in enumerate(recognized_text.splitlines(), start=1):
        print(f"{idx:02d}: {line}")

if __name__ == "__main__":
    main()
```

Çalıştırın:

```bash
python improve_ocr_accuracy.py
```

Daha önce gösterdiğimiz güzel biçimlendirilmiş çıktıyı göreceksiniz.

---

## Sonuç

Python’da **OCR doğruluğunu artırmanın** basit bir yolunu şu adımlarla ele aldık:

1. **OCR dilini** belgenize uygun şekilde ayarlama.  
2. **Görüntüyü doğru şekilde** yükleyerek motorun doğru pikselleri görmesini sağlama.  
3. **Görüntü üzerinde OCR** tek bir metod çağrısıyla gerçekleştirme.  
4. **Görüntüden metin çıkarma** ve sonucu doğrulama.  
5. **Özel sözlük** ekleyerek alan‑spesifik terimleri sabitleme.

Bu, ham fotoğraftan temiz, aranabilir metne kadar tüm süreci, düzenli ve yeniden kullanılabilir bir betikle birleştirir.  

Bir sonraki adım için, görüntü ön‑işleme (kontrast, eğikliği düzeltme) deneyebilir ya da `ocr.Language.English | ocr.Language.German` gibi çok‑dilli bir yapılandırmaya geçebilirsiniz. Aynı prensipler geçerlidir ve **OCR doğruluğunu artırmaya** devam edersiniz.

Sorularınız veya tuhaf bir kenar durumunuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

![improve OCR accuracy


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [Görüntüden Metin Çıkarma – Aspose.OCR for .NET ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)
- [Aspose OCR ile Çoklu Dillerde Metin Tanıma](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [OCR Görüntü Tanımasında Eşik Değeri Nasıl Ayarlanır](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}