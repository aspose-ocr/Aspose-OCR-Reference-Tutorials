---
category: general
date: 2026-03-26
description: Görüntüden metni hızlıca tanıyın; OCR için görüntüyü nasıl yükleyeceğinizi
  öğrenerek ve belirli bir bölgeden veri çıkararak. Bu uygulamalı rehberi izleyin.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: tr
og_description: Python’da OCR için bir görüntü yükleyerek, ilgi bölgesi tanımlayıp
  temiz metin çıkararak görüntüden metni tanıyın. Tam iş akışını öğrenin.
og_title: Görüntüden Metin Tanıma – Tam Python OCR Rehberi
tags:
- OCR
- Python
- Image Processing
title: Görüntüden metin tanıma – Adım Adım Python OCR Öğreticisi
url: /tr/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin tanıma – Tam Python OCR Rehberi

Hiç **görüntüden metin tanıma** ihtiyacı duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Belki taranmış bir form, bir fiş ya da bir ekran görüntüsü var ve sadece belirli bir kutunun içindeki kelimeleri istiyorsunuz. İyi haber şu ki, birkaç satır Python kodu ile resmi OCR için yükleyebilir, tek bir bölgeye odaklanabilir ve ihtiyacınız olan tam metni alabilirsiniz—manuel kopyalama gerekmez.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: resmi yükleme, ilgi bölgesi (ROI) tanımlama, OCR motorunu çalıştırma ve sonucu yazdırma. Sonunda bu kod parçacığını, bir görüntünün belirli bir kısmından metin çıkarması gereken herhangi bir projeye ekleyebileceksiniz. Ağır‑ağır görüntü işleme hatları yerine, bugün çalışan temiz ve okunabilir bir kod.

## Önkoşullar

- Python 3.8+ yüklü  
- `ocr` paketi (veya uyumlu herhangi bir OCR kütüphanesi) – `pip install ocr-lib` ile kurun (kullandığınız gerçek paket adıyla değiştirin)  
- Okunacak formu içeren bir PNG/JPEG resmi  
- Python fonksiyonları ve sınıflarıyla temel aşinalık  

Eğer bunlarla zaten rahat iseniz, harika—ilerleyebilirsiniz. Aksi takdirde, bir kahve alın ve yukarıdaki öğelerin hazır olduğundan emin olun; sonraki adımlar bunların mevcut olduğunu varsayar.

## Adım 1: Bir OCR Motoru Örneği Oluşturma – “görüntüden metin tanıma” Çekirdeği

İlk olarak OCR motoru ile iletişim kurabilecek bir nesneye ihtiyacımız var. Bunu, **görüntüden metin tanıma** verisini daha sonra tanıyacak beyin olarak düşünebilirsiniz.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Neden önemli:** Motoru bir kez başlatmak, ayarları (dil paketleri gibi) birden fazla görüntüde yeniden kullanmanıza olanak tanır, bu da performansı artırır ve kodu düzenli tutar.

## Adım 2: OCR İçin Resmi Yükleme – Resmi Belleğe Getirme

Şimdi gerçekten **OCR için resmi yükle**yoruz. Kütüphane, dosyayı okuyup motorun anlayabileceği bir nesne döndüren kullanışlı bir statik yöntem sunar.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **İpucu:** Resminiz büyükse, yüklemeden önce yeniden boyutlandırmayı düşünün. Daha küçük görüntüler, çoğu basılı metin için doğruluktan ödün vermeden OCR’u hızlandırır.

## Adım 3: OCR İlgi Bölgesi (ROI) Tanımlama

Genellikle tüm sayfaya ihtiyacınız yoktur—kullanıcının veri girdiği belirli bir kutuya sadece ihtiyacınız vardır. Bir **OCR ilgi bölgesi** tanımlamak, motorun diğer her şeyi görmezden gelmesini sağlar; bu da gürültüyü azaltır ve işleme süresini kısaltır.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **ROI’ye odaklanmanın nedeni:**  
> - **Hız:** Motor daha az piksel tarar.  
> - **Doğruluk:** ROI dışındaki arka plan grafikleri karakter tanımını karıştırabilir.  
> - **Basitlik:** İlgilendiğiniz alana tam olarak karşılık gelen temiz bir dize elde edersiniz.

## Adım 4: OCR İşlemini Çalıştırma – Gerçek An

Her şey ayarlandığında, tanımlı ROI içinde **görüntüden metin tanıma** işlemini nihayet gerçekleştiriyoruz.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Motor birden fazla bölgeyi destekliyorsa, `ocr_result` bir liste içerir; tek‑ROI durumumuzda ise `get_text()` metoduna sahip basit bir nesnedir.

## Adım 5: Metni Çıkarma ve Yazdırma – Son Çıktıyı Alma

Şimdi sonuç nesnesinden düz dizeyi alıp ekrana bastırıyoruz. Bu noktada çıktıyı bir veritabanına, bir CSV dosyasına ya da herhangi bir sonraki mantığa bağlayabilirsiniz.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Beklenen çıktı** (doldurulmuş bir isim alanı örneği):

```
Text inside ROI:
 John Doe
```

OCR motoru ekstra boşluk ya da satır sonu döndürürse, `.strip()` ya da bir düzenli ifade ile temizleyebilirsiniz.

## Yaygın Kenar Durumlarını Ele Alma

| Durum                                   | Yapılması Gereken                                                    |
|-----------------------------------------|----------------------------------------------------------------------|
| **Düşük çözünürlüklü görüntü**          | Yüklemeden önce `Pillow` (`Image.resize`) ile büyütün.               |
| **Eğik veya döndürülmüş metin**         | Döndürme düzeltmesi uygulayın (`ocr.Imaging.Image.rotate`).        |
| **Birden fazla dil**                    | Motorun dil paketini ayarlayın: `ocr_engine.set_language('eng+spa')`. |
| **ROI tanımlanmamış**                    | `add_region_of_interest` atlayın; motor tüm görüntüyü işleyecek.    |
| **Beklenmeyen karakterler (örn. virgül)** | Dizeyi sonradan işleyin: `extracted_text.replace(',', '')`.        |

Bu ipuçları, **OCR için resmi yükleme** hattınızı kaynak materyal mükemmel olmasa bile dayanıklı tutar.

## Tam Çalışan Örnek – Kopyala, Yapıştır, Çalıştır

Aşağıda `.py` dosyasına koyup çalıştırabileceğiniz tam betik yer alıyor. Tüm importları, hata yönetimini ve resmin varlığını kontrol eden küçük bir yardımcı fonksiyonu içerir.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Bu betiği çalıştırdığınızda ROI’dan temizlenmiş dizeyi yazdırır ve kullanıma hazır bir veri parçası elde edersiniz.

## Sonuç

Artık **görüntüden metin tanıma** için **OCR için resmi yükleme**, kesin bir **OCR ilgi bölgesi** tanımlama ve sonunda temiz metni çıkarma adımlarını içeren net, uçtan uca bir yönteme sahipsiniz. Yaklaşım, yukarıdaki örnek desenine uyan herhangi bir Python OCR kütüphanesiyle çalışır ve kolayca birden fazla ROI, farklı diller veya ön‑işleme adımları ekleyecek şekilde genişletilebilir.

Sonraki adımlarınız şunlar olabilir:

- **OCR için görüntü ön‑işleme** (eşikleme, gürültü giderme) ile gürültülü taramalarda doğruluğu artırma.  
- **ROI’dan metin çıkarma** sonucunu bir pandas DataFrame’e aktararak toplu veri analizi yapma.  
- Daha yüksek güvenilirlik ve ölçeklenebilirlik gerektiğinde bir bulut‑tabanlı OCR hizmetine (Google Vision, Azure Computer Vision) geçiş.

Deneyin, dikdörtgen koordinatlarını kendi formlarınıza göre ayarlayın ve otomasyonun devreye girdiğini izleyin. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}