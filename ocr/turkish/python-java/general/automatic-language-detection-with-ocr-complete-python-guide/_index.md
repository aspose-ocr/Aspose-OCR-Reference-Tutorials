---
category: general
date: 2026-05-31
description: OCR'da otomatik dil algılaması artık çok kolay. Görüntü OCR'sini nasıl
  yükleyeceğinizi, otomatik dil algılamasını nasıl etkinleştireceğinizi ve metin görüntüsünü
  sadece birkaç adımda nasıl tanıyacağınızı öğrenin.
draft: false
keywords:
- automatic language detection
- recognize text image
- load image ocr
- enable auto language detection
- detect language ocr
language: tr
og_description: OCR'da otomatik dil algılaması artık çok kolay. Otomatik dil algılamasını
  etkinleştirmek, görüntü OCR'sini yüklemek ve metin görüntüsünü tanımak için bu adım
  adım öğreticiyi izleyin.
og_title: OCR ile Otomatik Dil Tespiti – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Automatic language detection in OCR made easy. Learn how to load image
    OCR, enable auto language detection, and recognize text image in just a few steps.
  headline: Automatic Language Detection with OCR – Complete Python Guide
  type: TechArticle
- description: Automatic language detection in OCR made easy. Learn how to load image
    OCR, enable auto language detection, and recognize text image in just a few steps.
  name: Automatic Language Detection with OCR – Complete Python Guide
  steps:
  - name: Python 3.8+ installed (any recent version works).
    text: Python 3.8+ installed (any recent version works).
  - name: 'The OCR library that provides `OcrEngine`, `LanguageAutoDetectMode`, etc.
      – for this guide we’ll assume a hypothetical package called `myocr`. Install
      it with:'
    text: 'The OCR library that provides `OcrEngine`, `LanguageAutoDetectMode`, etc.
      – for this guide we’ll assume a hypothetical package called `myocr`. Install
      it with:'
  - name: An image file (`multilingual_sample.png`) that contains text in at least
      two different languages.
    text: An image file (`multilingual_sample.png`) that contains text in at least
      two different languages.
  - name: A little curiosity—if you’ve never touched OCR before, don’t worry; the
      code is deliberately straightforward.
    text: A little curiosity—if you’ve never touched OCR before, don’t worry; the
      code is deliberately straightforward.
  type: HowTo
tags:
- OCR
- Python
- Multilingual
- Computer Vision
title: OCR ile Otomatik Dil Tespiti – Tam Python Rehberi
url: /tr/python-java/general/automatic-language-detection-with-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Otomatik Dil Algılama ile OCR – Tam Python Rehberi

Hiç bir OCR motorunun taranmış bir belgenin dilini size ne aradığını söylemeden *tahmin* etmesini düşündünüz mü? İşte **otomatik dil algılama** tam da bunu yapar ve çok dilli PDF'lerle, sokak işareti fotoğraflarıyla veya farklı yazı sistemlerini karıştıran herhangi bir görüntüyle çalışırken tamamen oyunu değiştirir.  

Bu öğreticide, **otomatik dil algılamayı etkinleştirme**, **görüntü OCR yükleme** ve **görüntüden metin tanıma** işlemlerini Python‑stilinde bir API kullanarak nasıl yapacağınızı adım adım göstereceğiz. Sonunda, algılanan dil kodunu ve çıkarılan metni ekrana yazdıran, manuel dil ayarı gerektirmeyen bağımsız bir betiğiniz olacak.

## Öğrenecekleriniz

- Bir OCR motoru örneği oluşturmayı ve **otomatik dil algılamayı** etkinleştirmeyi.  
- Diskten **görüntü OCR** yüklemek için tam adımları.  
- Motorun `recognize()` metodunu nasıl çağıracağınızı ve dil kodunu içeren bir sonuç alacağınızı.  
- Düşük çözünürlüklü görüntüler veya desteklenmeyen yazı sistemleri gibi kenar durumlarını ele almak için ipuçları.  

Çok dilli OCR konusunda önceden bir deneyime sahip olmanıza gerek yok; sadece temel bir Python kurulumu ve bir görüntü dosyası yeterli.

---

## Ön Koşullar

1. Python 3.8+ yüklü (herhangi bir güncel sürüm çalışır).  
2. `OcrEngine`, `LanguageAutoDetectMode` vb. sağlayan OCR kütüphanesi – bu rehberde hayali bir paket olan `myocr` varsayacağız. Şu komutla kurun:

   ```bash
   pip install myocr
   ```

3. En az iki farklı dilde metin içeren bir görüntü dosyası (`multilingual_sample.png`).  
4. Biraz merak—eğer OCR ile hiç çalışmadıysanız endişelenmeyin; kod kasıtlı olarak basittir.

---

## Adım 1: Otomatik Dil Algılamayı Etkinleştirme

Motorun kendi kendine dili *bulması* gerektiğini ona söylemeniz gerekir. İşte **otomatik dil algılama** bayrağının devreye girdiği yer.

```python
from myocr import OcrEngine, LanguageAutoDetectMode

# Step 1: Create an OCR engine instance
engine = OcrEngine()

# Step 2: Enable automatic language detection
engine.language_auto_detect_mode = LanguageAutoDetectMode.AUTO_DETECT
```

> **Why this matters:**  
> When `AUTO_DETECT` is set, the engine runs a lightweight language classifier on the image before the heavy‑weight character recognition kicks in. That means you don’t have to guess whether the text is English, Russian, French, or any combination thereof. The engine will automatically pick the best language model for each region of the image.

> **Neden Önemli:**  
> `AUTO_DETECT` ayarlandığında, motor ağır karakter tanıma işlemine geçmeden önce görüntü üzerinde hafif bir dil sınıflandırıcısı çalıştırır. Bu sayede metnin İngilizce, Rusça, Fransızca veya bunların bir kombinasyonu olup olmadığını tahmin etmeniz gerekmez. Motor, görüntünün her bölgesi için en uygun dil modelini otomatik olarak seçecektir.

---

## Adım 2: Görüntü OCR Yükleme

Motor artık dilleri otomatik olarak algılaması gerektiğini bildiğine göre, ona çalışacak bir şey vermemiz gerekiyor. **Görüntü OCR yükleme** adımı bitmap'i okur ve iç tamponları hazırlar.

```python
# Step 3: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual_sample.png"
engine.load_image(image_path)
```

> **Pro tip:**  
> If your image is larger than 300 dpi, consider downscaling it to around 150‑200 dpi. Too much detail can actually *slow* down the language detection stage without improving accuracy.

> **Pro ipucu:**  
> Görüntünüz 300 dpi'den büyükse, yaklaşık 150‑200 dpi'ye küçültmeyi düşünün. Çok fazla detay, doğruluğu artırmadan dil algılama aşamasını *yavaşlatabilir*.

---

## Adım 3: Görüntüden Metin Tanıma

Görüntü bellekte ve dil algılama etkinleştirildiğinde, son adım motoru **görüntüden metin tanıma** yapmaya istemektir. Bu tek çağrı tüm ağır işi yapar.

```python
# Step 4: Perform OCR recognition
result = engine.recognize()
```

| Özellik | Açıklama |
|-----------|-------------|
| `language` | Algılanan dilin ISO‑639‑1 kodu (ör. İngilizce için `"en"`). |
| `text`     | Görüntünün düz metin transkripsiyonu. |

---

## Adım 4: Algılanan Dili ve Çıkarılan Metni Almak

Şimdi motorun keşfettiğini basitçe ekrana yazdırıyoruz. Bu, **detect language OCR** yeteneğinin pratikte nasıl çalıştığını gösterir.

```python
# Step 5: Display the detected language and extracted text
print("Detected language:", result.language)   # e.g. "en", "ru", "fr"
print("Text:", result.text)
```

**Örnek çıktı**

```
Detected language: fr
Text: Bonjour le monde! This is a multilingual sample.
```

> **What if the engine returns `None`?**  
> That usually means the image is too blurry or the text is too small (< 8 pt). Try increasing contrast or using a higher‑resolution source.

> **Motor `None` döndürürse ne olur?**  
> Bu genellikle görüntünün çok bulanık olduğu veya metnin çok küçük (< 8 pt) olduğu anlamına gelir. Kontrastı artırmayı veya daha yüksek çözünürlüklü bir kaynak kullanmayı deneyin.

---

## Tam Çalışan Örnek (Otomatik Dil Algılamayı Uçtan Uca Etkinleştirme)

Her şeyi bir araya getirerek, **otomatik dil algılamayı etkinleştirme**, **görüntü OCR yükleme**, **görüntüden metin tanıma** ve **dil algılama OCR** işlemlerini tek seferde yapan hazır bir betik sunuyoruz.

```python
# automatic_language_detection_ocr.py
from myocr import OcrEngine, LanguageAutoDetectMode

def main():
    # Create engine and turn on auto language detection
    engine = OcrEngine()
    engine.language_auto_detect_mode = LanguageAutoDetectMode.AUTO_DETECT

    # Load the image (adjust the path to your own file)
    image_path = "YOUR_DIRECTORY/multilingual_sample.png"
    engine.load_image(image_path)

    # Run OCR
    result = engine.recognize()

    # Output results
    print("Detected language:", result.language)
    print("Text:", result.text)

if __name__ == "__main__":
    main()
```

Bu betiği `automatic_language_detection_ocr.py` olarak kaydedin, `YOUR_DIRECTORY` kısmını PNG dosyanızın bulunduğu klasörle değiştirin ve çalıştırın:

```bash
python automatic_language_detection_ocr.py
```

Çıktıda, örnek çıktıda gösterildiği gibi, önce dil kodu ardından çıkarılan metni görmelisiniz.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Önerilen Çözüm |
|-----------|----------------|
| **Çok düşük çözünürlüklü görüntü** (100 dpi altında) | Yüklemeden önce bikübik filtre ile ölçeklendirin veya daha yüksek çözünürlüklü bir kaynak isteyin. |
| **Tek bir görüntüde karışık yazı sistemleri** (ör. İngilizce + Kiril) | Motor genellikle sayfayı bölgelere ayırır; hatalı algılamalar fark ederseniz `engine.enable_region_split = True` ayarlayın. |
| **Desteklenmeyen dil** | OCR kütüphanesinin ihtiyacınız olan yazı sistemi için bir dil paketi içerdiğini doğrulayın; ek modeller indirmeniz gerekebilir. |
| **Büyük toplu işleme** | Motoru bir kez başlatın, ardından birden fazla `load_image` / `recognize` döngüsü boyunca yeniden kullanın, böylece modelin tekrar tekrar yüklenmesinin önüne geçilir. |

---

## Görsel Genel Bakış

![otomatik dil algılama örnek çıktısı](https://example.com/auto-lang-detect.png "otomatik dil algılama")

*Alt text:* otomatik dil algılama örnek çıktısı, algılanan dil kodunu ve çıkarılan çok dilli metni gösterir.

---

## Sonuç

**Otomatik dil algılama** sürecini baştan sona ele aldık—motoru oluşturma, otomatik dil algılamayı etkinleştirme, bir görüntüyü OCR için yükleme, metni tanıma ve sonunda algılanan dili elde etme. Bu uçtan uca akış, her seferinde dil modellerini manuel olarak yapılandırmadan çok dilli belgeleri işleyebilmenizi sağlar.

Daha ileri gitmek isterseniz şunları düşünebilirsiniz:

- **Toplu işleme** yüzlerce görüntüyü aynı `OcrEngine` örneğini yeniden kullanan bir döngü ile işlemek.  
- **Son‑işleme** çıkarılan metni bir imla denetleyicisi veya dile özgü bir ayrıştırıcı ile işlemek.  
- **Entegrasyon** scripti, kullanıcı yüklemelerini kabul eden ve `language` ve `text` alanlarıyla JSON döndüren bir web servisine.

Farklı görüntü formatları (`.jpg`, `.tif`) ile deney yapın ve algılama doğruluğunun nasıl değiştiğini görün. Sorularınız veya okunması zor bir görüntünüz varsa aşağıya yorum bırakın—mutlu kodlamalar!

## Sonra Ne Öğrenmelisiniz?

- [Aspose.OCR Kullanarak Dil ile Görüntü Metni OCR Nasıl Yapılır](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR Kullanarak Dil Seçimiyle C# Görüntü Metni Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Aspose OCR ile Çoklu Diller İçin Görüntü Metni Tanıma](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}