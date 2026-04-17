---
category: general
date: 2026-03-26
description: 'Python OCR öğreticisi: Görüntüden metin çıkarmayı, OCR için görüntüyü
  yüklemeyi ve Aspose OCR kullanarak makbuzdan metni tanımayı birkaç adımda öğrenin.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: tr
og_description: 'Python OCR öğreticisi: görüntüden metin çıkarmayı hızlıca öğrenin,
  OCR için görüntüyü yükleyin ve Aspise OCR ile makbuzdaki metni tanıyın.'
og_title: Python OCR öğreticisi – Görüntüden Metin Çıkarma
tags:
- OCR
- Aspose
- Python
title: Python OCR öğreticisi – Aspose ile Görüntüden Metin Çıkarma
url: /tr/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR öğretici – Aspose ile Görüntüden Metin Çıkarma

Hiç bulanık bir makbuzdan veya taranmış bir formdan metni saatlerce özel regexler yazarak çıkarmayı düşündünüz mü? Yalnız değilsiniz. Bu **python ocr tutorial**'da OCR için bir görüntüyü yüklemeyi, Python'da OCR gerçekleştirmeyi ve son olarak Aspose OCR kütüphanesini kullanarak makbuz dosyalarından metni tanımayı adım adım göstereceğiz.  

Bu rehberin sonunda, desteklenen herhangi bir görüntü formatını okuyabilen, metin içeriğini çıkaran ve konsola yazdıran, çalıştırmaya hazır bir betiğiniz olacak. Harici hizmetler, API anahtarları yok — sadece saf Python ve güçlü bir OCR motoru.  

## Gereksinimler

- Python 3.8 ve üzeri (kod tip ipuçları kullandığı için yeni bir yorumlayıcı tercih edilir)
- `asposeocrjava` paketi `pip install aspose-ocr` ile kurulu
- Örnek bir görüntü – örneğin tipik bir mağaza makbuzu içeren `receipt_noisy.jpg`
- (İsteğe bağlı) Bağımlılıkları düzenli tutmak için bir sanal ortam

Bu maddeleri tamamladıysanız, doğrudan koda geçebiliriz.  

## Adım 1: Aspose OCR Sınıflarını Kurun ve İçe Aktarın

İlk olarak, Aspose OCR paketinin mevcut olduğundan emin olun. Ardından ihtiyacımız olan sınıfları içe aktarın.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Neden önemli:** Yalnızca gerekli sembolleri içe aktarmak isim alanını temiz tutar ve yorumlayıcıya kütüphanenin hangi bölümlerini kullandığımızı gösterir. Ayrıca sonraki kod satırlarını kısaltır, öğreticinin daha kolay takip edilmesini sağlar.

> **Pro ipucu:** Jupyter defteri kullanıyorsanız, kurulum satırının başına `!` ekleyerek hücre içinde çalıştırabilirsiniz.

## Adım 2: OCR Motorunu Oluşturun ve Derin Öğrenme Modunu Etkinleştirin

Aspose çeşitli motor modları sunar. Çoğu gerçek dünya makbuzu için, derin öğrenme modeli özellikle gürültülü taramalarda en yüksek doğruluğu sağlar.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Neden derin öğrenme?** Geleneksel kural‑tabanlı OCR düşük kontrastlı veya bozulmuş karakterlerde zorlanabilir. Milyonlarca glif üzerinde eğitilmiş derin öğrenme modeli, değişkenliklere daha iyi uyum sağlar — telefon kamerasıyla çekilen makbuzlarda *perform OCR in Python* yaparken tam da buna ihtiyacınız var.

## Adım 3: OCR İçin Görüntüyü Yükleyin

Şimdi gerçekten **load image for OCR** yapıyoruz. Aspose.Imaging PNG, JPEG, BMP, TIFF ve daha fazlasını destekler, böylece neredeyse her belge fotoğrafını işaretleyebilirsiniz.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Yaygın tuzak:** Motorun üzerine görüntüyü ayarlamayı unutmak, çalışma zamanında `NullReferenceException` hatasına yol açar. Dosyayı yükledikten sonra her zaman `set_image` çağırın.

## Adım 4: OCR Gerçekleştirin ve Metni Çıkarın

Motor hazır ve görüntü eklendiğinde, nihayet **perform OCR in Python** yapabilir ve metinsel sonucu alabiliriz.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

`recognize()` metodu, yalnızca ham metni değil aynı zamanda güven skorlarını, sınırlama kutularını ve dil bilgilerini içeren bir `OcrResult` nesnesi döndürür. Hızlı bir **extract text from image** senaryosu için sadece `get_text()` yeterlidir.

## Adım 5: Tanınan Metni Görüntüleyin

Motorun makbuzdan gerçekte ne okuduğuna bir bakalım.

```python
print("Recognized text:\n", recognized_text)
```

Tipik çıktı şu şekildedir:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Eğer çıktı bozuk karakterler içeriyorsa, OCR motoruna yüklemeden önce görüntüyü ön işleme (örneğin kontrastı artırma veya eğikliği düzeltme filtresi uygulama) düşünün. Aspose.Imaging, bir araya bağlayabileceğiniz tam bir görüntü iyileştirme araçları seti sunar.

## Kenar Durumlarını Yönetme ve Daha İyi Doğruluk İçin İpuçları

### 1. Aşırı Gürültülü Makbuzlarla Başa Çıkma
Makbuz çok lekeli ise, daha hızlı ama daha az doğru bir geçiş için `OcrEngineMode.HIGH_SPEED` moduna geçmek isteyebilirsiniz, ardından temizlenmiş görüntüde `DEEP_LEARNING` ile ikinci bir geçiş çalıştırın.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Dil Belirleme
Varsayılan olarak Aspose dili otomatik algılamaya çalışır. İngilizce makbuzlar için dili sabitleyebilirsiniz:

```python
ocr_engine.set_language("eng")
```

### 3. Bellek Yönetimi
Bir döngü içinde birçok görüntü işlenirken, kaynakları açıkça serbest bırakın:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. OCR Sonuçlarını Dosyaya Kaydetme
Bazen çıkarılan metnin daha sonraki analiz için kalıcı olarak saklanması gerekir.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Tam Çalışan Örnek

Aşağıda her şeyi bir araya getiren tam betik yer alıyor. `receipt_ocr.py` adlı bir dosyaya kopyalayıp yapıştırın, görüntü yolunu ayarlayın ve `python receipt_ocr.py` komutunu çalıştırın.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Betik çalıştırıldığında, makbuzun içeriği konsolda görüntülenecek ve aynı verileri içeren `receipt_output.txt` dosyası da oluşturulacak.

![Python OCR öğretici – örnek makbuz çıktısı](https://example.com/receipt_output.png "python ocr tutorial örneği")

*Görsel alt metni:* **python ocr tutorial – örnek makbuz çıktısı**

## Özet ve Sonraki Adımlar

Az önce **python ocr tutorial**'ı tamamladık; bu öğreticide **load image for OCR**, **perform OCR in Python** ve son olarak Aspose kullanarak **recognize text from receipt** dosyalarını nasıl yapacağınızı gösterdik. Temel çıkarımlar şunlardır:

- Doğru motor modunu seçin (doğruluk için derin‑öğrenme)
- `recognize()` çağırmadan önce her zaman görüntüyü ekleyin
- Temiz metni almak için `OcrResult` nesnesini kullanın, ardından ihtiyacınıza göre saklayın veya işleyin

Sırada ne var? Düşük kontrastlı taramaları iyileştirmek için Aspose Imaging filtrelerini zincirlemeyi düşünün veya betiği bir Flask API'sine entegre ederek makbuzları bir web formu üzerinden yükleyebilmenizi sağlayın. Ayrıca muhasebe otomasyonu için OCR verilerini CSV'ye aktarmayı keşfedebilirsiniz.

Çok sayfalı PDF'ler veya Latin dışı betikler ile ilgili sorularınız mı var? Yorum bırakın—yardımcı olmaktan memnuniyet duyarız!  

**Belge otomasyonunuzu bir üst seviyeye taşımaya hazır mısınız?** Kodu alın, farklı görüntülerle deney yapın ve OCR motorunun ağır işi halletmesine izin verin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}