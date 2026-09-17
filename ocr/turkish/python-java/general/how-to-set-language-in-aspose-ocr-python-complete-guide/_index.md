---
category: general
date: 2026-01-12
description: Aspose OCR Python'da dili nasıl ayarlarsınız ve özel bir sözlük kullanarak
  görüntüden metin çıkarırsınız. Geliştiriciler için adım adım öğretici.
draft: false
keywords:
- how to set language
- extract text from image
- how to extract text
- how to add dictionary
- how to process image
language: tr
og_description: Aspose OCR Python'da dili nasıl ayarlayacağınızı ve özel bir sözlükle
  görüntüden metin nasıl çıkaracağınızı öğrenin. Tam iş akışını dakikalar içinde öğrenin.
og_title: Aspose OCR Python'da dili nasıl ayarlarsınız – Tam Kılavuz
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Aspose OCR Python'da Dili Nasıl Ayarlarsınız – Tam Kılavuz
url: /tr/python-java/general/how-to-set-language-in-aspose-ocr-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Python’da dili nasıl ayarlarsınız – Tam Kılavuz

Aspose OCR’u Python’da kullanırken **dili nasıl ayarlarsınız** merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, varsayılan İngilizce modelinin ürün kodlarını, seri numaralarını veya çok dilli metinleri tanımadığı durumlarla karşılaşıyor. İyi haber şu ki çözüm hem basit hem de güçlü. Bu öğreticide dili yapılandırmayı, özel bir sözlük eklemeyi, bir görüntüden metin çıkarmayı ve en iyi OCR sonuçları için görüntüyü işlemeyi adım adım göstereceğiz.

Kütüphaneyi kurmaktan, çıkarılan metni ekrana yazdıran tam bir örnek çalıştırmaya kadar bilmeniz gereken her şeyi ele alacağız. Sonunda, içerik alışılmadık kodlar ya da karışık diller içerdiğinde bile **görüntüden metin çıkar** dosyalarından güvenle metin alabileceksiniz.

## Önkoşullar

* Python 3.8+ yüklü (kod f‑string kullanıyor, bu yüzden daha eski sürümler çalışmaz).
* Aktif bir Aspose OCR for Python lisansı veya ücretsiz deneme anahtarı.
* `asposeocr` paketini `pip install asposeocr` komutuyla kurun.
* Okumak istediğiniz metni içeren bir örnek görüntü (`product_label.png`).

Bu öğelere zaten sahipseniz harika—devam edelim. Yoksa Aspose’un web sitesinden ücretsiz deneme sürümünü alın ve kurulum komutunu çalıştırın; sadece bir dakikanızı alır.

## Adım 1: Aspose OCR modülünü içe aktarın

Kodunuzda OCR sınıflarını kullanmak için ilk yapmanız gereken bunları içe aktarmaktır. Bu, **dili nasıl ayarlarsınız** için temel oluşturur.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr
```

> **Pro ipucu:** İçe aktarmaları dosyanın en üstünde tutun. Böylece scripti daha kolay tarayabilirsiniz, özellikle daha sonra geri döndüğünüzde.

## Adım 2: Dili nasıl ayarlarsınız

Varsayılan olarak Aspose OCR İngilizceyi varsayar. Görüntünüzde Fransızca, Almanca veya başka bir dil varsa, motorun hangi dili kullanacağını belirtmeniz gerekir. İşte bu noktada anahtar kelime devreye girer.

```python
# Step 2: Create an OCR engine and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # change to ocr.Language.FRENCH, etc.
```

Bu neden önemli? OCR motorları dil‑özel karakter modellerine dayanır. Doğru dili sağlamak, doğruluğu büyük ölçüde artırır—özellikle aksanlı karakterler veya dile özgü ligatürler için.

> **Not:** Aynı anda birden fazla dili desteklemeniz gerekiyorsa, `ocr.Language.ENGLISH | ocr.Language.SPANISH` gibi bir liste geçirebilirsiniz.

## Adım 3: Sözlük nasıl eklenir (kullanıcı tanımlı kelimeler)

Bazen OCR motoru “AB‑1234” gibi ürün kodlarını yanlış okur. Özel bir sözlük ekleyerek güveni artırabilirsiniz. Bu, Aspose OCR’da **sözlük nasıl eklenir** sorusuna doğrudan yanıt verir.

```python
# Step 3: Supply product codes that must be recognized with higher confidence
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])
```

Motor bu kelimeleri “bilinen” olarak kabul eder ve benzer görünümlü karakterlerden daha çok tercih eder. SKU numaraları, seri kodları veya doğal bir dilin parçası olmayan marka adları için özellikle kullanışlıdır.

## Adım 4: Görüntüyü nasıl işlersiniz

Motor yapılandırıldıktan sonra analiz etmek istediğiniz görüntüyü yüklemeniz gerekir. Bu, **görüntüyü nasıl işlersiniz** sorusuna temiz ve tekrarlanabilir bir yanıt sunar.

```python
# Step 4: Load the image containing the product label
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")
```

PDF’lerle çalışıyorsanız, önce her sayfayı bir görüntüye dönüştürebilirsiniz—Aspose OCR bunu kutudan çıkar çıkmaz destekler.

## Adım 5: Görüntüden metin nasıl çıkarılır

Her şey ayarlandığında, son adım OCR’u çalıştırıp metni almaktır. Bu, bir görüntüden **metin nasıl çıkarılır** sorusunun özüdür.

```python
# Step 5: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)

# Step 6: Print the extracted text
print(ocr_result.text)
```

Scripti çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Çıktı bozuk görünüyorsa, doğru dili ayarladığınızdan ve özel sözlüğünüzün beklediğiniz tam dizeleri içerdiğinden emin olun.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, `extract_label.py` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam script aşağıdadır. `YOUR_DIRECTORY` kısmını görüntünüzün gerçek yolu ile değiştirin.

```python
import asposeocr as ocr

# Create OCR engine and set language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # Change if needed

# Add custom dictionary entries
ocr_engine.set_user_defined_words(["AB-1234", "ZX-9876", "SKU-001"])

# Load the target image
image = ocr.Image.load("YOUR_DIRECTORY/product_label.png")

# Perform OCR
ocr_result = ocr_engine.process(image)

# Output the result
print("=== OCR Extraction Result ===")
print(ocr_result.text)
```

### Beklenen Çıktı

```
=== OCR Extraction Result ===
Product: AB-1234
Batch: ZX-9876
SKU: SKU-001
```

Sözlüğe eklediğiniz tam kodları görüyorsanız, Aspose OCR kullanarak **dili nasıl ayarlarsınız**, **sözlük nasıl eklenir** ve **görüntüden metin nasıl çıkarılır** konularında başarıyla uzmanlaştınız demektir.

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Ne Yapmalı |
|-----------|------------|
| **Image is blurry** | `ocr.Image.apply_filter()` ile ön‑işlem yaparak `process()` çağırmadan önce netleştirin. |
| **Multiple languages in one image** | `ocr_engine.language = ocr.Language.ENGLISH | ocr.Language.SPANISH` ayarlayın. |
| **Large PDFs** | Her sayfayı döngü içinde `ocr.Image`‑a dönüştürün ve sayfa başına `process()` çağırın. |
| **Unexpected characters** | Bunları kullanıcı tanımlı kelimeler listesine ekleyin; Aspose OCR bunları yüksek güvenilirlikli token olarak değerlendirir. |

Bu ipuçları, giriş verileri mükemmel olmasa bile OCR hattınızı sağlam tutar.

## Görsel Referans

![how to set language in Aspose OCR example](image.png "Screenshot showing how to set language in Aspose OCR Python example")

*Alt metin:* **dili nasıl ayarlarsınız** ekran görüntüsü, Python IDE'sinde dil özelliği atamasını gösterir.

## Sonuç

Artık Aspose OCR Python’da **dili nasıl ayarlarsınız**, **sözlük nasıl eklenir** ve **görüntüden metin nasıl çıkarılır** ile **görüntüyü nasıl işlersiniz** konularını biliyorsunuz. Yukarıdaki tam örnek, herhangi bir projeye eklenebilir, farklı diller için uyarlanabilir ve toplu işleme ya da PDF girişleriyle genişletilebilir.

Bir sonraki meydan okumaya hazır mısınız? `ocr.Language.ENGLISH` yerine `ocr.Language.FRENCH` kullanarak Fransızca etiketlerde doğruluk artışını gözlemleyin. Ya da `set_user_defined_words` metodunu deneyerek bütün bir ürün kataloğunu ekleyin—OCR motorunuz her girişi yüksek güvenilirlikli bir eşleşme olarak ele alacaktır.

İyi kodlamalar, ve OCR sonuçlarınız her zaman kristal gibi net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}