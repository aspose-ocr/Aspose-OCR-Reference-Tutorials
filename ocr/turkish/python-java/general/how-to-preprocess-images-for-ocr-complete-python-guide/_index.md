---
category: general
date: 2026-06-06
description: Python kullanarak OCR için görüntüleri nasıl ön işleme alacağınızı öğrenin.
  Otsu yöntemiyle görüntüyü ikili hale getirmeyi, taranmış belgeleri nasıl düzleştireceğinizi
  ve Almanca metin için OCR doğruluğunu nasıl artıracağınızı keşfedin.
draft: false
keywords:
- how to preprocess images for OCR
- binarize image using otsu
- how to deskew scanned documents
- how to improve OCR accuracy
- extract text from german image
language: tr
og_description: Python’da OCR için görüntüleri nasıl ön işleme alacağınızı öğrenin.
  Bu öğreticide Otsu yöntemiyle görüntüyü ikiliye çevirme, taranmış belgeleri eğriltme
  ve Almanca görüntülerde OCR doğruluğunu artırma konuları gösterilmektedir.
og_title: OCR için Görüntüleri Nasıl Ön İşlemeye Alırsınız – Tam Python Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  headline: How to Preprocess Images for OCR – Complete Python Guide
  type: TechArticle
- description: How to preprocess images for OCR using Python. Learn to binarize image
    using Otsu, how to deskew scanned documents, and improve OCR accuracy for German
    text.
  name: How to Preprocess Images for OCR – Complete Python Guide
  steps:
  - name: How to Deskew Scanned Documents
    text: The `deskew` call above is the concrete answer to **how to deskew scanned
      documents**. Internally it estimates the dominant text line angle via Hough
      transform and rotates the image back. If your documents are rotated more than
      5°, bump `max_angle` up, but beware of over‑rotation artifacts.
  - name: Binarize Image Using Otsu
    text: The `binarize(method="otsu")` line directly answers the query **binarize
      image using otsu**. Otsu’s algorithm computes a threshold that minimizes intra‑class
      variance, which is perfect for documents with bimodal histograms (dark text
      vs. light background).
  - name: Expected Output
    text: 'Assuming the sample scan contains the sentence “Die schnelle braune Füchsin
      springt über den faulen Hund.” you should see something like:'
  type: HowTo
tags:
- OCR
- image preprocessing
- Python
- German language
title: OCR için Görüntüleri Nasıl Ön İşlemeye Alırsınız – Tam Python Rehberi
url: /tr/python-java/general/how-to-preprocess-images-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntüleri Ön İşleme – Tam Python Rehberi

OCR için görüntüleri nasıl ön işleme yapacağınızı hiç merak ettiniz mi, böylece metin kristal netliğinde çıkar? Tek başınıza değilsiniz. Tarama belgeleri—özellikle gürültülü Almanca sayfalar—herhangi bir OCR motoru için bir kabus olabilir. İyi haber? Birkaç akıllı ön işleme adımı, bulanık, lekeli bir taramayı temiz, makine tarafından okunabilir bir görüntüye dönüştürebilir.

Bu öğreticide, Python kullanarak **OCR için görüntüleri nasıl ön işleme yapacağınızı** gösteren pratik bir örnek üzerinden ilerleyeceğiz. **Otsu ile görüntüyü ikiliye dönüştürmeyi**, **tarama belgelerini nasıl düzleştireceğinizi** ve genel olarak **OCR doğruluğunu nasıl artıracağınızı** öğreneceksiniz; özellikle **Almanca görüntü dosyalarından metin çıkarmak** gerektiğinde. Süslü bir giriş yok, bugün kopyalayıp yapıştırabileceğiniz çalışan bir betik.

## What You’ll Need

- **Python 3.9+** (herhangi bir yeni sürüm yeterlidir)
- `OcrEngine` sınıfını sunan bir OCR kütüphanesi – demo için genel bir `ocr` paketi varsayacağız. `pip install ocr-lib` ile kurun.
- Test etmek istediğiniz gürültülü bir Almanca tarama (`noisy_german_scan.tif`).
- Python fonksiyonları hakkında temel bir anlayış (daha önce bir `def` yazdıysanız, hazırsınız).

> **Pro ipucu:** Farklı bir OCR SDK’sı (ör. `pytesseract` ile Tesseract) kullanıyorsanız, kavramlar aynı kalır—sadece metod isimlerini uyarlayın.

## Overview of the Solution

1. **Bir OCR motoru örneği oluşturun.**  
2. **Tanıma dilini Almanca olarak ayarlayın.**  
3. **Özel bir ön işleme hattı oluşturun**; bu hat, düzleştirme, gürültü giderme, ikiliye dönüştürme (Otsu) ve kontrast genişletmeyi içerir.  
4. **Hattı motorla ilişkilendirin**; böylece her görüntü otomatik olarak bu hattı geçer.  
5. **OCR’ı** gürültülü bir Almanca tarama üzerinde çalıştırın.  
6. **Çıkarılan metni** yazdırarak sonucu doğrulayın.

Aşağıda her adımı ayrıntılı olarak açıklıyor, **neden** önemli olduğunu gösteriyor ve ihtiyacınız olan tam kodu sunuyoruz.

![how to preprocess images for OCR example](image.png "how to preprocess images for OCR example")

## Step 1: Create an OCR Engine Instance

İlk iş olarak—bir motor olmadan hiçbir şey olmaz. `OcrEngine` nesnesi, sonraki tüm işlemleri koordine eden giriş noktasıdır.

```python
# Step 1: Initialize the OCR engine
from ocr import OcrEngine, Language

ocr_engine = OcrEngine()
```

*Why this matters:* Motoru başlatmak, iç kaynakları (dil modelleri gibi) kurar ve daha sonra özel bir hat eklemek için temiz bir ortam sağlar.

## Step 2: Set the Recognition Language to German

OCR doğruluğu büyük ölçüde dile bağlıdır. Motora Almanca bekleyeceğini söyleyerek doğru karakter kümesini ve dil modelini etkinleştirirsiniz.

```python
# Step 2: Tell the engine we’re working with German text
ocr_engine.set_recognition_language(Language.GERMAN)
```

Bunu atlamanız durumunda motor, varsayılan olarak İngilizceye geçebilir ve umlautları (ä, ö, ü) ve ß karakterini yanlış tanıyabilir—Almanca taramalarla çalışırken sık karşılaşılan tuzaklardır.

## Step 3: Build a Custom Preprocessing Pipeline

Bu, **OCR için görüntüleri nasıl ön işleme yapacağınız** konusunun kalbidir. Dört dönüşümü zincirleyeceğiz:

| Dönüşüm | Ne yapar | Neden yardımcı olur |
|---------|----------|----------------------|
| **Deskew** | Görüntüyü yataya (maks 5°) döndürür | Taramalar nadiren mükemmel hizalanır; düzleştirme, karakter segmentasyonunu karıştıran eğimi ortadan kaldırır. |
| **Denoise** | Rastgele lekeleri azaltır (güç 0.7) | Gürültü, OCR motorunun karakter olarak yorumlayabileceği sahte kenarlar oluşturur. |
| **Binarize (Otsu)** | Otsu yöntemiyle siyah‑beyaz dönüştürür | Temiz bir ikili görüntü, motorun ön plan (metin) ve arka plan arasında keskin bir kontrast elde etmesini sağlar. |
| **Contrast Stretch** | Dinamik aralığı genişletir | Özellikle eski belgelerde soluk çizgilerin okunabilirliğini artırır. |

```python
# Step 3: Assemble the preprocessing pipeline
preprocessing_pipeline = (
    ocr_engine.preprocessing()
               .deskew(max_angle=5)          # auto‑deskew up to 5°
               .denoise(strength=0.7)       # medium denoise
               .binarize(method="otsu")      # **binarize image using Otsu**
               .contrast(stretch=True)      # auto contrast stretch
)

# Explanation:
# - `deskew` corrects rotation; 5° is a safe ceiling for most scans.
# - `denoise` with 0.7 balances smoothing without erasing thin characters.
# - `binarize` with method "otsu" automatically selects the optimal threshold.
# - `contrast` stretch brightens faint ink while keeping dark ink dark.
```

### How to Deskew Scanned Documents

Yukarıdaki `deskew` çağrısı, **tarama belgelerini nasıl düzleştireceğiniz** sorusunun somut cevabıdır. İçsel olarak, Hough dönüşümüyle baskın metin satırı açısını tahmin eder ve görüntüyü geri döndürür. Belgeleriniz 5°’den fazla döndürülmüşse `max_angle` değerini artırın, ancak aşırı döndürme artefaktlarına dikkat edin.

### Binarize Image Using Otsu

`binarize(method="otsu")` satırı, **otsu kullanarak görüntüyü ikiliye dönüştür** sorusuna doğrudan yanıt verir. Otsu algoritması, sınıf içi varyansı en aza indirecek bir eşik hesaplar; bu, koyu metin ve açık arka planın ikili histogramına sahip belgeler için mükemmeldir.

## Step 4: Attach the Pipeline to the Engine

Şimdi OCR motoruna, her gelen görüntünün az önce oluşturduğumuz hattı çalıştırmasını söylüyoruz.

```python
# Step 4: Register the custom pipeline
ocr_engine.set_preprocessing(preprocessing_pipeline)
```

*Why this matters:* Kayıt yapılmazsa motor, ham taramayı işler ve yapılandırdığımız temizlik adımlarını görmez. Bu adım, **OCR doğruluğunu nasıl artıracağınız** konusunda aynı ön işleme adımlarını tutarlı bir şekilde uygulamayı sağlar.

## Step 5: Recognize Text from a Noisy German Scan

Her şeyi bir araya getirme zamanı. Motoru gürültülü bir Almanca görüntüye besliyoruz ve işi ona bırakıyoruz.

```python
# Step 5: Run OCR on the target file
image_path = "YOUR_DIRECTORY/noisy_german_scan.tif"
recognition_result = ocr_engine.recognize_image(image_path)
```

Performans merak ediyorsanız, çağrıyı zamanlayabilirsiniz:

```python
import time
start = time.time()
result = ocr_engine.recognize_image(image_path)
print(f"OCR took {time.time() - start:.2f}s")
```

## Step 6: Output the Recognized Text

Son olarak, çıkarılan dizeyi yazdırıyoruz. Bu, **Almanca görüntüden metin çıkar** sorusunun doğrudan yanıtıdır.

```python
# Step 6: Display the OCR output
print("=== Recognized German Text ===")
print(recognition_result.text)
```

### Expected Output

Örnek tarama “Die schnelle braune Füchsin springt über den faulen Hund.” cümlesini içeriyorsa, aşağıdakine benzer bir çıktı görmelisiniz:

```
=== Recognized German Text ===
Die schnelle braune Füchsin springt über den faulen Hund.
```

Çıktı hâlâ bozuk karakterler içeriyorsa, `denoise` gücünü ayarlamayı veya düzleştirme için `max_angle` değerini artırmayı düşünün.

## Common Pitfalls & How to Tackle Them

- **Dil modeli eksik:** `set_recognition_language(Language.GERMAN)` çağrısını unutmak, umlautların eksik olmasına yol açar. Bu satırı iki kez kontrol edin.  
- **Aşırı gürültü giderme:** 0.9 üzerindeki bir güç, özellikle eski yazı tiplerinde ince çizgileri silebilir. Çoğu durum için 0.5‑0.7 arasında kalın.  
- **Yanlış dosya formatı:** Bazı OCR motorları çok sayfalı TIFF’lerde takılır. Çok sayfalı bir belgeniz varsa, önce tek sayfalık dosyalara bölün.  
- **Hattın sırası:** Gösterilen sıra (deskew → denoise → binarize → contrast) kasıtlıdır. İkiliye dönüştürme, gürültü giderme öncesinde yapılırsa gürültü kilitlenir; her zaman önce gürültü giderin.

## Extending the Pipeline (What’s Next?)

Şimdi sağlam bir temeliniz olduğuna göre, şunları eklemek isteyebilirsiniz:

- Küçük lekeleri temizlemek için morfolojik bir açma ekleyin (`.morph_open(kernel=3)`).  
- Son‑işleme düzeltmesi için bir dil modeli entegre edin (`ocr_engine.apply_spellcheck()`).  
- Büyük veri kümeleri için `concurrent.futures` kullanarak toplu işleme paralelleştirin.

Tüm bunlar, **OCR için görüntüleri nasıl ön işleme yapacağınız** temel fikrini korurken **OCR doğruluğunu nasıl artıracağınız** konusunda daha da ilerlemenizi sağlar.

## Conclusion

Başlangıçtan sona kadar **OCR için görüntüleri nasıl ön işleme yapacağınızı** kapsadık: bir motor oluşturun, Almanca dilini ayarlayın, **Otsu ile görüntüyü ikiliye dönüştürün**, **tarama belgelerini nasıl düzleştireceğinizi** yapın ve sonunda **Almanca görüntüden metin çıkar** ile daha yüksek güvenle sonuç alın. Yukarıdaki altı adımı izleyerek tanıma kalitesinde belirgin bir artış göreceksiniz—artık sonsuz manuel düzeltme yok.

Kendi taramalarınızla betiği deneyin, parametrelerle oynayın ve sonuçların kendini kanıtlamasına izin verin. Belirli bir ön işleme ayarı hakkında sorularınız mı var? Yorum bırakın, birlikte daha derine inelim.

İyi kodlamalar, OCR’unuz her zaman doğru olsun!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakın konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose.OCR kullanarak dil seçimiyle C# görüntü metni çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [OCR Görüntü Tanıma’da Eşik Değerini Nasıl Ayarlarsınız](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Görüntüyü OCR Yapma – OCR Görüntü Tanıma’da Görüntü Üzerinde OCR Gerçekleştirme](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}