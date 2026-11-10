---
category: general
date: 2026-03-18
description: Görsellerden metin çıkarmak için OCR nasıl kullanılır – PNG dosyalarından
  metin tanıma ve OCR için görüntü yükleme üzerine hızlı bir rehber.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: tr
og_description: Görüntülerden metin çıkarmak için OCR nasıl kullanılır – PNG'den metni
  tanımayı öğrenin, OCR için görüntüyü yükleyin ve basit bir Python betiğiyle metni
  çıkarın.
og_title: 'OCR Nasıl Kullanılır: Python''da Görüntülerden Metin Çıkarma'
tags:
- OCR
- Python
- Image Processing
title: 'OCR Nasıl Kullanılır: Python''da Görüntülerden Metin Çıkarma'
url: /tr/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python’da OCR Nasıl Kullanılır: Görsellerden Metin Çıkarma

Karmaşık bir ekran görüntüsü ya da taranmış bir fişiniz olduğunda **OCR nasıl kullanılır** diye merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler, özellikle mobil uygulamalardan ya da web yüklemelerinden gelen PNG dosyalarından okunabilir metin çıkarmak zorunda kalıyor. Bu öğreticide, **görselden metin çıkarma**, **PNG’den metin tanıma** ve **OCR için görsel yükleme** işlemlerini sadece birkaç satır Python ile gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Doğru kütüphaneyi kurmaktan çok dilli belgelerle çalışmaya kadar her şeyi ele alacağız; böylece sonunda motorunuzu herhangi bir görsele uyguladığınızda *metin nasıl çıkarılır* sorusunun cevabını net bir şekilde bileceksiniz. Belirsiz referanslar yok, sadece kopyalayıp çalıştırabileceğiniz adım‑adım bir çözüm var.

## Neler Öğreneceksiniz

İlerleyen bölümlerde:

1. Hafif bir OCR motoru kuracağız (ağır bağımlılıklar gerektirmiyor).  
2. Görsel dosyasını—özellikle bir PNG’yi—motora yükleyeceğiz.  
3. Otomatik dil algılamayı etkinleştirerek motorun çok dilli içeriği işlemesini sağlayacağız.  
4. Tanıma sürecini çalıştırıp düz metin sonucunu alacağız.  
5. Eksik dosyalar ya da desteklenmeyen formatlar gibi uç durumlar için iş akışını inceleyeceğiz.

Temel Python bilgisine sahipseniz yeterli. Önceden OCR deneyimi şart değil, kütüphane dokümantasyonuna hızlı bir göz atmak da faydalı olur.

---

![PNG görselinde OCR kullanımı](placeholder.png "PNG görselinde OCR kullanımı – adım adım kılavuz")

## OCR Nasıl Kullanılır – Görsel Yükleme ve Metin Tanıma {#how-to-use-ocr}

### Adım 1: OCR kütüphanesini kurun

İlk olarak, bir `OcrEngine` sınıfı sağlayan bir Python paketi gerekir. Bu öğreticide, kurgusal ama açıklayıcı **SimpleOCR** paketini kullanacağız; pip ile şu şekilde kurabilirsiniz:

```bash
pip install simple-ocr
```

> **İpucu:** Sanal bir ortamda (şiddetle tavsiye edilir) çalışıyorsanız, kurulum komutunu çalıştırmadan önce ortamı etkinleştirin. Böylece proje bağımlılıklarınız düzenli kalır.

### Adım 2: Motoru içe aktarın ve bir örnek oluşturun

Motoru oluşturmak, yapıcı metodunu çağırmak kadar basit. Motor, daha sonra besleyeceğiniz görseli işleyen “beyin” gibidir.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Neden her seferinde yeni bir örnek oluşturuyoruz? İzolasyon. Yeni bir motor, önceki çalışmalardan kalan durumun mevcut tanıma müdahale etmemesini sağlar; bu, toplu dosya işleme sırasında kritik öneme sahiptir.

### Adım 3: İşlemek istediğiniz görseli yükleyin

Şimdi **OCR için görsel yükleme** işlemini yapıyoruz. `setImageFromFile` metodu, herhangi bir raster görsele giden yolu kabul eder; biz `mixed_doc.png` adlı bir PNG’ye işaret edeceğiz.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Dosya bulunamazsa, `SimpleOCR` net bir `FileNotFoundError` fırlatır. Kullanıcı dostu bir hata mesajı vermek için yakalayabilirsiniz:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Adım 4: Otomatik dil algılamayı etkinleştirin

Çoğu modern OCR motoru dil paketleriyle gelir. `"multilingual"` parametresini geçirerek motorun metni koklayıp doğru dil modelini otomatik seçmesini sağlarız. Bu, örneğin PNG’nizde İngilizce ve İspanyolca karışık olduğunda çok kullanışlıdır.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Dili önceden biliyorsanız, `"multilingual"` yerine `"eng"` ya da `"spa"` gibi belirli bir yerel ayarı kullanarak işleme süresini hızlandırabilirsiniz.

### Adım 5: Tanıma sürecini çalıştırın

Yoğun işlem burada gerçekleşir. `recognize()` görseli tarar, segmentasyon uygular, sinir ağını çalıştırır ve dahili bir metin tamponu oluşturur.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Arka planda motor şunları yapar:

- **Ön‑işleme** (eğrilik düzeltme, ikilileştirme)  
- **Düzen analizi** (sütun, tablo tespiti)  
- **Karakter sınıflandırması** (derin öğrenme modeli kullanarak)  

Tüm bunlar soyutlanmıştır; bu yüzden sadece bir satıra ihtiyacınız var.

### Adım 6: Tanınan metni alın ve yazdırın

Son olarak, sonuç nesnesini alıp düz stringi çıkarıyoruz. İşte **görselden metin çıkarma** kısmı burada gerçekleşir.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Beklenen çıktı** (kısaltılmış):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Görsel tanınabilir karakter içermiyorsa, `text` boş bir string olur. Bunun için kontrol ekleyebilirsiniz:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Görselden Metin Çıkarma – Yaygın Uç Durumları Ele Alma

### Tek bir dosyada birden fazla dil

Bir belge birden fazla dil içerdiğinde, `"multilingual"` ayarı genellikle doğru çalışır. Ancak hatalı tanıma görürseniz, manuel olarak bir yedek dil listesi belirtebilirsiniz:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### PNG dışı formatlar

Odak noktamız **PNG’den metin tanıma** olsa da, `SimpleOCR` JPEG, BMP ve TIFF gibi formatları da kabul eder. `setImageFromFile` içinde dosya uzantısını değiştirmeniz yeterlidir. TIFF yığınları için belirli bir sayfa seçmeniz gerekebilir:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Büyük dosyalar ve bellek kullanımı

Gigapiksel taramalar işliyorsanız, OCR’dan önce yeniden boyutlandırmayı düşünün:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Yeniden boyutlandırma, bellek baskısını azaltırken tanıma için yeterli detayı korur.

### Yükleme hatalarını ayıklama

Bazen bir görsel gözle sağlıklı görünür ama içsel olarak bozulmuş olabilir. Motorun ne gördüğünü görmek için ayrıntılı loglamayı etkinleştirin:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Tam, Çalıştırılabilir Script

Aşağıda tüm parçaları bir araya getiren tam program yer alıyor. `ocr_demo.py` adlı bir dosyaya kopyalayın, `YOUR_DIRECTORY` yer tutucusunu ayarlayın ve `python ocr_demo.py` komutunu çalıştırın.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Bu scripti çalıştırdığınızda `mixed_doc.png` içindeki metnin düz metin versiyonu ekrana basılır. Dosyayı başka bir resimle değiştirmeniz **metin nasıl çıkarılır** sürecini aynı şekilde çalıştırır.

---

## Sonuç

Python’da **OCR nasıl kullanılır** sorusunu, **görselden metin çıkarma** dosyaları, özellikle **PNG’den metin tanıma** varlıkları ve **OCR için görsel yükleme** adımlarını ele alarak yanıtladık. Yukarıdaki kod parçacığı, paketi kurma, dosyayı besleme, çok dilli algılamayı etkinleştirme, motoru çalıştırma ve sonucu alma adımlarını tek bir, bağımsız çözümde birleştiriyor.

Bundan sonra şunları yapabilirsiniz:

- Kullanıcı yüklemelerini kabul eden bir web servisine scripti entegre edin.  
- PNG’ye dönüştürülmüş PDF’lerin bulunduğu bir klasörü toplu işleyin.  
- Doğruluğu artırmak için regex temizleme, yazım denetimi gibi son‑işlem adımları ekleyin.

Unutmayın, OCR kalitesi görsel netliğine, doğru dil paketlerine ve bazen ön‑işleme adımlarına bağlıdır—deneyerek en iyi sonucu elde edin.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}