---
category: general
date: 2026-03-26
description: Python'da görüntüyü nasıl döndüreceğinizi ve OCR nasıl yapacağınızı öğrenin.
  Bu kılavuz ayrıca OCR için görüntüyü nasıl ön işleme tabi tutacağınızı ve görüntüden
  metni verimli bir şekilde nasıl çıkaracağınızı gösterir.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: tr
og_description: Aspose OCR kullanarak görüntüyü doğru bir şekilde döndürüp ardından
  görüntüden metni tanıma. OCR için görüntüyü ön işleme ve görüntüden metin çıkarma
  konusunda bu adım adım öğreticiyi izleyin.
og_title: Resmi Döndürme ve OCR Yapma – Tam Python Rehberi
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Python'da Aspose ile Görüntüyü Döndürme ve OCR Gerçekleştirme
url: /tr/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Döndürme ve Aspose ile Python'da OCR Yapma

Bir OCR motorunun metni gerçekten okuyabilmesi için **görüntüyü nasıl döndüreceğinizi** hiç merak ettiniz mi? Belki bir formu yan yatırarak taradınız ya da bir kamera çekimi saat yönünde 90° döndü. Bu durumda metin insan gözüyle düzgün görünür, ancak OCR motoru bir karmaşa görür. İyi haber? Yönlendirmeyi düzeltmek, ilgilendiğiniz bölgeyi kırpmak ve ardından metni çıkarmak birkaç satır Python ve Aspose kütüphanesi ile çocuk oyuncağı.

Bu öğreticide, döndürülmüş bir TIFF dosyasını yüklemekten, yönünü düzeltmeye, **OCR için görüntüyü ön işleme** ve son olarak **görüntüden metni tanıma** aşamasına kadar tüm iş akışını adım adım inceleyeceğiz. Sonuna geldiğinizde **OCR nasıl yapılır** konusunda tam hakim olacak ve **görüntüden metin çıkarma** işlemini güvenle gerçekleştirebileceksiniz.

## Gereksinimler

- Python 3.8+ (kod, herhangi bir güncel sürümde çalışır)
- `asposeocrjava` ve `asposeimaging` paketleri, `pip` ile kurulmuş
- Döndürülmesi gereken bir örnek görüntü (ör. `rotated_form.tif`)
- Görüntü işleme konusunda biraz merak

Ağır çerçevelere ihtiyaç yok—sadece iki Aspose paketi ve biraz Python mantığı yeterli.

---

## Adım 1: Aspose Paketlerini Kurun (OCR Nasıl Yapılır)

**görüntüyü döndürme** veya **görüntüden metni tanıma** işlemine başlamadan önce, işi gerçekten yapan kütüphanelere ihtiyacımız var.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Kurumsal bir proxy arkasındaysanız komuta `--proxy http://proxy:port` ekleyin. Paketler, Aspose .NET/Java çekirdeği etrafında oluşturulmuş saf Python sarmalayıcılarıdır; bu yüzden kurulum genellikle anında gerçekleşir.

---

## Adım 2: Kaynak Dosyayı Yükleyin ve Döndürün – “Görüntüyü Nasıl Döndürürüm” Adımı

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Neden döndürülür?** Çoğu OCR motoru, metnin soldan sağa ve üstten alta doğru akacağını varsayar. Bitmap yan yatırılmışsa, motor ya anlamsız karakterler döndürür ya da hiç sonuç vermez. Döndürmek, piksel ızgarasını beklenen okuma düzeniyle hizalar ve doğruluğu büyük ölçüde artırır.

> **Köşe durumu:** Görüntünün 90°, 180° veya 270° döndürülmesi gerektiğinden emin değilseniz `source_image.width` ile `source_image.height` karşılaştırabilir ya da `exif` yönlendirme etiketlerini kullanabilirsiniz. Aspose’un `rotate_flip` metodu ayrıca `ROTATE_180` ve `ROTATE_270_CLOCKWISE` seçeneklerini destekler.

> **Görüntü önizlemesi (isteğe bağlı):**  
> ![görüntüyü nasıl döndürürüm örneği](/assets/rotate-demo.png "Görüntüyü nasıl döndürürüm – döndürmeden önce ve sonra")

---

## Adım 3: İlgi Alanını Kırpın – OCR İçin Görüntüyü Ön İşleme

Genellikle sayfanın sadece küçük bir kısmına ihtiyacınız olur—örneğin bir imza alanı ya da bir sayı bloğu. Kırpma, gürültüyü ortadan kaldırır ve **OCR nasıl yapılır** sürecini hızlandırır.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Neden kırpılır?** Görüntü boyutunun küçültülmesi, OCR motorunun arama alanını sınırlar; bu da yanlış pozitifleri azaltır ve işlem süresini kısaltır. Ayrıca kaynak dosyada motoru yanıltabilecek filigranlar ya da diğer grafikler varsa kırpma yardımcı olur.

> **İpucu:** Birden fazla alanla çalışıyorsanız, farklı dikdörtgenlerle kırpma adımını tekrarlayın ve OCR’u her parça için ayrı ayrı çalıştırın.

---

## Adım 4: OCR Motorunu Başlatın – “OCR Nasıl Yapılır” Çekirdeği

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Arka planda:** Aspose OCR, Tesseract ve özel görüntü analizinin bir kombinasyonunu kullanır. Motoru bir kez örnekleyip birden çok görüntüde yeniden kullanmak, her seferinde yeni bir nesne oluşturmaktan daha verimlidir.

---

## Adım 5: Kırpılmış Görüntüyü Besleyin ve Metni Tanıyın – Görüntüden Metin Çıkarma

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Beklenen Çıktı

ROI “Invoice #12345 – Paid” ifadesini içeriyorsa, aşağıdakine benzer bir sonuç görürsünüz:

```
Invoice #12345 – Paid
```

OCR zorlanırsa ekstra boşluklar ya da hatalı karakterler (ör. “Invo1ce #I2345 – Pa1d”) alabilirsiniz. İşte **OCR için görüntüyü ön işleme** hileleri—kontrast ayarı ya da ikilileştirme—devreye girer. Aspose, adım 5’ten önce zincirleyebileceğiniz ek filtreler sunar, ancak temel akış çoğu temiz tarama için yeterlidir.

---

## Adım 6: İsteğe Bağlı – OCR Ayarlarını İnce Ayar Yapın (Gelişmiş “OCR Nasıl Yapılır”)

Belirli bir dil için daha yüksek doğruluk istiyorsanız ya da bazı karakterleri yok saymak istiyorsanız, motoru şu şekilde özelleştirebilirsiniz:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Ne zaman kullanılır:** Belgenizde ilgilenmediğiniz çok sayıda süsleme sembolü varsa bu seçeneği tercih edin. Kara listeleme, yanlış algılamaları azaltır.

---

## Tam Uçtan Uca Betik

Her şeyi bir araya getirerek, **görüntüyü nasıl döndürürüm**, **OCR için görüntüyü ön işleme** ve sonunda **görüntüden metni tanıma** işlemlerini yapan hazır bir betik aşağıdadır:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Bu betiği çalıştırdığınızda tanınan metin konsola yazdırılır ve işlenmiş ROI’nin görseli `processed_roi.png` olarak kaydedilir. PNG dosyasını açarak döndürme ve kırpmanın beklendiği gibi gerçekleştiğini doğrulayabilirsiniz.

---

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|------|-------|
| **Görüntü zaten dik mi?** | Döndürme adımı idempotenttir—doğru yönlendirilmiş bir görüntüyü 90° döndürmek kesinlikle bozar, bu yüzden `source_image.width` ile `height` karşılaştırmalı ya da EXIF yönlendirme verisini kontrol etmelisiniz. |
| **OCR çıktımda ekstra satır sonları var.** | `result.get_text().replace("\n", " ").strip()` ile temizleyebilir ya da `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)` özelliğini etkinleştirebilirsiniz. |
| **PDF dosyalarını doğrudan işleyebilir miyim?** | Evet—Aspose Imaging, PDF sayfalarını görüntü olarak yükleyebilir (`Image.load("file.pdf")`), ardından aynı döndürme ve OCR adımlarını izlersiniz. |
| **Birden çok dosyayı toplu işlemek mümkün mü?** | `ocr_rotated_image` fonksiyonunu bir dizindeki dosyalar üzerinde döngüye alabilir ya da Python’un `concurrent.futures` modülünü kullanarak paralel işleyebilirsiniz. |
| **İngilizce dışındaki dillerle nasıl çalışırım?** | Tanıma dilini `ocr_engine.get_recognition_settings().set_recognition_language("fr")` gibi bir çağrıyla Fransızca, vb. olarak ayarlayabilirsiniz. |

---

## Sonuç

**görüntüyü nasıl döndürürüm**, **OCR için görüntüyü ön işleme** (kırpma) ve sonunda **görüntüden metni tanıma** ve **görüntüden metin çıkarma** işlemlerini Aspose’un Python kütüphaneleriyle nasıl gerçekleştireceğinizi ele aldık. Tam betik, herhangi bir otomasyon hattına kolayca entegre edilebilecek üretim‑hazır bir iş akışı sunar.

Daha ileri gitmek isterseniz şunları deneyin:

- **Görüntü iyileştirme** (kontrast, ikilileştirme) OCR’dan önce
- **Birden çok ROI çıkarma** formlarda birden fazla alan için
- **Klasör bazlı toplu işleme** taranmış belgeler için
- **Entegrasyon** (ör. çıkarılan veriyi bir veritabanına aktarma)

Kodu kendi senaryonuza göre uyarlamaktan çekinmeyin ve kodlamanın tadını çıkarın! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}