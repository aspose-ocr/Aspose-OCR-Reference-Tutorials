---
category: general
date: 2026-03-18
description: Görselde OCR yapın ve bir fotoğraftan el yazısı metni çıkarın. El yazısı
  görüntüsünü nasıl dönüştüreceğinizi, jpg’den metin çıkarmayı ve fotoğraftan metni
  tanımayı öğrenin.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: tr
og_description: Bir fotoğraftan el yazısı metni çıkarmak için görüntüde OCR uygulayın.
  Bu öğreticide, el yazısı görüntüsünü dönüştürme ve jpg dosyalarından metni tanıma
  yöntemleri gösterilmektedir.
og_title: Görselde OCR Yap – Tam El Yazısı Metin Rehberi
tags:
- OCR
- Python
- Handwriting Recognition
title: Görüntüde OCR Yap – El Yazısı Görüntüyü Metne Dönüştür
url: /tr/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Yap – Tam‑Yığın El Yazısı Metin Çıkarma

Hiç **perform OCR on image** dosyalarıyla çalışmanız gerekti, ancak motorun dağınık el yazısını okuyup okuyamayacağından emin olamadınız mı? Yalnız değilsiniz. Gerçek‑dünya uygulamalarında—örneğin harcama‑fişi tarayıcıları veya not‑alma araçları—el yazısı fotoğraflarıyla karşılaşıp bunları düz metne dönüştürmeniz gerekir.  

Bu rehberde, **convert handwritten image** dosyalarını nasıl **extract text from jpg** ve hatta **recognize text from photo** akışlarından çıkaracağınızı, `ocr` adlı küçük bir Python‑stili kütüphane kullanarak göstereceğiz. Sonunda, kalem ne kadar titrek olursa olsun el yazısı nottan her kelimeyi çıkaran çalıştırılabilir bir betiğiniz olacak.

## Gereksinimler

- Python 3.8+ (kod herhangi bir yeni yorumlayıcıda çalışır)
- Hayali `ocr` paketi – `pip install ocr-lib` ile kurun (kullandığınız gerçek paket adıyla değiştirin)
- `note.jpg` (veya başka bir görüntü formatı) olarak kaydedilmiş net bir el yazısı fotoğrafı
- Biraz merak—ileri düzey ML bilgisi gerekmez

Hepsi bu. Harici hizmetler, API anahtarları yok, sadece **perform OCR on image** verisini işleyebilen yerel bir motor.

![perform OCR on image ekran görüntüsü](example.png)

*Alt metin: perform OCR on image ekran görüntüsü, OCR betiğiyle kod editörünü gösteriyor.*

## Adım‑Adım Uygulama

Aşağıda süreci küçük parçalara ayırıyoruz. Her başlık bir anahtar kelime içerir, böylece hızlıca göz atabilirsiniz ve her blok **neden** yaptığımızı açıklar—sadece **ne**yi değil.

### Adım 1: OCR Kütüphanesini Kur ve Doğrula

**perform OCR on image** dosyalarıyla çalışabilmek için kütüphane ortamınızda bulunmalı. Bir terminal açın ve çalıştırın:

```bash
pip install ocr-lib
```

> **İpucu:** Sanal bir ortamda (şiddetle tavsiye edilir) çalışıyorsanız önce onu etkinleştirin. Bu, bağımlılıkları düzenli tutar ve sürüm çakışmalarını önler.

Kurulumdan sonra, Python’un paketi içe aktarabildiğinden emin olalım:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Başarı mesajını görürseniz, **convert handwritten image** verisini işlemeye hazırsınız.

### Adım 2: Bir Motor Örneği Oluştur ve El Yazısı Modunu Seç

Çoğu OCR motoru varsayılan olarak basılı‑metin tanıması yapar. **extract handwritten text** istediğimiz için modu açıkça değiştirmeliyiz. Bu adım kritiktir çünkü el yazısı genellikle farklı ön‑işleme (örneğin darbeleri yumuşatma) gerektirir.

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Neden önemli:* El yazısı karakterleri boyut ve eğim bakımından büyük değişiklikler gösterir. `RecognitionMode.HANDWRITTEN` ayarlanarak motor, el yazısı örnekleriyle eğitilmiş bir model kullanır ve doğruluk dramatik şekilde artar.

### Adım 3: Analiz Etmek İstediğiniz Fotoğrafı Yükleyin

Şimdi gerçekten **perform OCR on image** içeriğini işliyoruz. `load_image` metodu bir yol ya da dosya‑gibi nesne kabul eder. Örnekte bir JPEG yüklüyoruz, aynı çağrı PNG, BMP veya hatta PDF sayfaları için de çalışır.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Görseliniz bir bulut kovasında ise önce indirin ya da bir `BytesIO` akışı geçirin—`ocr` her iki durumu da idare edecek esnekliğe sahiptir.

### Adım 4: Tanıma İşlemini Çalıştırın

Motor hazır ve görüntü bellekteyken, nihayet **perform OCR on image** yapıp ham metni alıyoruz.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

`recognize()` çağrısı düz bir Unicode dizesi döndürür. Çoğu senaryoda bunu doğrudan bir `.txt` dosyasına yazabilir, doğal‑dil işlem hattına besleyebilir veya bir GUI’da gösterebilirsiniz.

### Adım 5: İsteğe Bağlı – Çıktıyı Temizle veya Son‑İşleme Yap

El yazısı OCR’u mükemmel değildir; sık sık gereksiz satır sonları veya hatalı karakterler görürsünüz. Hızlı bir temizlik adımı, sonraki sonuçları iyileştirebilir.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Alanınıza göre imla denetleyicileri, dil modelleri veya özel regex’ler ekleyebilirsiniz.

### Tam Betik – Kopyala & Yapıştır Hazır

Her şeyi bir araya getirdiğimizde, **extract handwritten text** yapan, JPEG’den temiz bir sonuç üreten tam, çalıştırılabilir program aşağıdadır.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Beklenen çıktı** (elbette gerçek metniniz farklı olacaktır):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Eğer anlamsız karakterler görürseniz, görüntü kalitesini (iyi aydınlatma, az bulanıklık) ve `HANDWRITTEN` modunda olduğunuzu tekrar kontrol edin. Bu iki faktör tanıma hatalarının büyük kısmını oluşturur.

## Sıkça Sorulan Sorular (SSS)

| Soru | Cevap |
|------|-------|
| **Bu yöntemi PNG’den metin çıkarmak için kullanabilir miyim?** | Kesinlikle. `engine.load_image("scan.png")` aynı şekilde çalışır. |
| **Görsel bir PDF sayfasıysa ne yapmalıyım?** | Önce sayfayı bir görüntüye dönüştürün (ör. `pdf2image` ile) ardından motorun içine besleyin. |
| **Kütüphane çok‑iş parçacıklı (thread‑safe) mı?** | Evet, her iş parçacığı için ayrı `OcrEngine` nesneleri oluşturabilirsiniz. |
| **Bu, `pytesseract`’tan nasıl farklı?** | `ocr`, Tesseract ikili dosyasını soyutlar ve yerleşik bir el‑yazısı modeli içerir, böylece dış yürütülebilir dosyalar kurmanıza gerek kalmaz. |
| ****extract text from JPG** dosyalarını toplu olarak işlemek istiyorum, ne yapmalıyım?** | Betiği bir döngüye sokun, ya da her dosya için `engine.load_image` çağırıp sonuçları bir liste ya da CSV’ye toplayın. |

## Kenar Durumları & En İyi Uygulamalar

1. **Düşük‑kontrast fotoğraflar** – Yüklemeden önce programatik olarak kontrastı artırın veya `engine.apply_preprocessing('contrast', level=2)` kullanın.
2. **Karışık basılı & el yazısı** – İki geçiş yapın: önce `HANDWRITTEN`, sonra `PRINTED` ve çıktıları birleştirin.
3. **Büyük görüntüler** – Genişliği ~1500 px’e küçültün; OCR motorları genellikle daha küçük tamponlarla daha hızlı çalışır ve doğruluktan ödün vermez.
4. **Unicode karakterler** – Kütüphane UTF‑8 dizeleri döndürür, bu sayede emoji, aksanlı harfler veya matematiksel semboller doğrudan kullanılabilir.

## Özet

**perform OCR on image** dosyalarıyla, özellikle el yazısı notlarla nasıl çalışılacağını somut bir örnekle gösterdik. `ocr` paketini kurup motoru `HANDWRITTEN` moduna ayarlayarak, bir fotoğraf yükleyip `recognize()` çağırarak **convert handwritten image** verisini temiz, aranabilir metne dönüştürebilirsiniz.  

Bundan sonra **extract text from jpg** dosyalarını toplu işleyebilir, çıktıyı bir not‑alma uygulamasına besleyebilir veya erişilebilirlik için ses senteziyle birleştirebilirsiniz. Yukarıdaki kod, denemeleriniz için sağlam bir temel sunar.

Farklı bir dosya formatı ya da ilginç bir ön‑işleme tekniği gibi bir yenilik paylaşmak ister misiniz? Yorum bırakın, sohbeti sürdürelim. Mutlu kodlamalar, ve o karalamaları dijital altına dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}