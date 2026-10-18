---
category: general
date: 2026-06-22
description: Python kullanarak birkaç satırda görüntüde OCR yapın. OCR için görüntüyü
  nasıl yükleyeceğinizi, PNG'den metni nasıl tanıyacağınızı ve OCR motorunu verimli
  bir şekilde nasıl kullanacağınızı öğrenin.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: tr
og_description: Python ile görüntüde OCR'yi hızlıca gerçekleştirin. Bu öğreticide
  OCR için görüntünün nasıl yükleneceği, PNG'den metnin nasıl tanınacağı ve güvenilir
  bir OCR motorunun nasıl kullanılacağı gösterilmektedir.
og_title: Python’da Görüntü Üzerinde OCR Yapma – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Python’da Görüntü Üzerinde OCR Yapma – Tam Kılavuz
url: /tr/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Yapma – Python ile Tam Kılavuz

Hiç **görüntüde OCR gerçekleştirme** ihtiyacı duydunuz mu ama ilk satırda takıldınız mı? Yalnız değilsiniz. Bu rehberde **OCR için görüntü yükleme**, hafif bir **OCR engine** kurma ve sadece birkaç komutla **PNG'den metin tanıma** işlemini nasıl yapacağınızı adım adım göstereceğiz.

Kütüphaneyi kurmaktan beyaz listeyi sadece rakamlar ve büyük harfler olacak şekilde ayarlamaya kadar her şeyi ele alacağız. Sonunda, herhangi bir projeye ekleyebileceğiniz, gizemli bir şey içermeyen, fazladan süssüz bir betiğiniz olacak.

## Öğrenecekleriniz

- Python’da **OCR engine**’i programatik olarak nasıl **kullanacağınızı**.  
- Yerel bir klasörden **OCR için görüntü yükleme** adımlarını.  
- Tanıma işlemini özel bir karakter kümesiyle sınırlamanın neden ve nasıl yapılacağını.  
- **PNG'den metin tanıma** ve sonucu güvenli bir şekilde ele almayı.  

**Önkoşullar:** Python 3.7+ yüklü, rahat kullandığınız bir terminal ve okumak istediğiniz bir görüntü (ör. `serial-number.png`). Önceden OCR deneyimi gerekmez.

---

## Görüntüde OCR Yapma – OCR Engine’i Başlatma

İlk yapmanız gereken OCR engine’in bir örneğini oluşturmaktır. Engine’i, pikselleri analiz edip karakterlere dönüştürecek beyin olarak düşünün.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Neden önemli:* Engine olmadan görüntüyü işlemek mümkün değildir. `OcrEngine` sınıfı, ön‑işleme, segmentasyon ve karakter sınıflandırmasını tek bir nesnede toplar ve tekrar kullanılabilir.

---

## OCR için Görüntü Yükleme – PNG Dosyasını Sağlama

Engine artık mevcut olduğuna göre, okumak istediğiniz resmi ona vermeniz gerekir. Kütüphane bir `ImageStream` nesnesi bekler; bunu doğrudan dosya yolundan oluşturabilirsiniz.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*İpucu:* Görüntüyü yüksek kontrastlı bir formatta (beyaz arka plan üzerinde siyah metin) tutun ve sıkıştırma artefaktlarından kaçının; bunlar OCR algoritmasını yanıltabilir.

---

## Karakterleri Sınırlama – Rakamlar ve Büyük Harfler Beyaz Listesi

Çoğu zaman sadece bir karakter alt kümesiyle ilgilenirsiniz—örneğin sadece A‑Z ve 0‑9 içeren bir seri numarası. Beyaz liste ayarlayarak engine’e diğer her şeyi yok saymasını söylersiniz, bu da doğruluğu büyük ölçüde artırır.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Arka planda ne oluyor?* Engine, son sınıflandırma aşamasına gelmeden beyaz listede bulunmayan tüm glifleri eleyen bir filtre oluşturur. Görüntü gürültülü ya da dekoratif metin içerdiğinde bu özellikle çok işe yarar.

---

## PNG'den Metin Tanıma – OCR Sürecini Çalıştırma

Engine hazır ve görüntü yüklendiğine göre, nihayet **görüntüde OCR gerçekleştirme** yapabilirsiniz. `recognize()` çağrısı tam pipeline’ı çalıştırır ve bir sonuç nesnesi döndürür.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Performans merak ediyorsanız, bu metod modern bir dizüstü bilgisayarda 300 × 200 px bir PNG için genellikle birkaç yüz milisaniye içinde tamamlanır.

---

## Çıktıyı Alıp Doğrulama – Tanınan Metni Elde Etme

Son adım, sonuç nesnesinden düz metni çıkarmaktır. Beyaz listeye uymayan her şey otomatik olarak atılır, böylece sonraki işlemler için temiz bir dize elde edersiniz.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Tipik çıktı:* `AB12C3D4E5` (görüntü tam olarak bu seri numarasını içeriyorsa).  

Çıktı boş ya da bozuk ise, görüntü kalitesini ve beyaz listeyi tekrar kontrol edin; sık karşılaşılan bir tuzak, ihtiyaç duyulan karakterlerin yanlışlıkla dışarıda bırakılmasıdır.

---

## Kenar Durumları ve Yaygın Hatalar

| Durum | Kontrol Edilecek | Önerilen Çözüm |
|-----------|---------------|---------------|
| **Dosya bulunamadı** | Yol hatası veya eksik dosya | `set_image` çağırmadan önce tam yolu doğrulamak için `os.path.abspath` kullanın. |
| **Düşük kontrastlı görüntü** | Metin arka planla karışıyor | Engine’e vermeden önce basit bir eşikleme (`Pillow` veya `OpenCV`) uygulayın. |
| **Beklenmeyen karakterler** | Beyaz liste çok kısıtlı | Eksik karakterleri beyaz liste dizesine ekleyin. |
| **Büyük görüntüler** | Tanıma yavaşlıyor | Genişliği maksimum 1024 px olacak şekilde yeniden boyutlandırın; OCR kalitesi genellikle yüksek kalır. |

---

## Tam Betik – Çalıştırmaya Hazır

Aşağıda, tüm parçaları bir araya getiren eksiksiz, bağımsız betik yer alıyor. `ocr_demo.py` olarak kaydedin, `YOUR_DIRECTORY` kısmını gerçek klasörle değiştirin ve `python ocr_demo.py` komutunu çalıştırın.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Beklenen konsol çıktısı* (PNG `SN12345` içeriyorsa):

```
Recognized text: SN12345
```

---

## Sonuç

Artık **görüntüde OCR gerçekleştirme** dosyalarını Python’da nasıl yapacağınızı, **OCR için görüntü yükleme** adımından **PNG'den metin tanıma** ve özelleştirilebilir bir **OCR engine** ile temiz sonuç çıkarma sürecine kadar tam olarak biliyorsunuz. Yaklaşım basit, genişletilebilir ve çoğu seri numarası tarzı tarama için kutudan çıkar çıkmaz çalışır.

Sırada ne var? Beyaz listeyi küçük harflere değiştirin, farklı görüntü formatları (JPEG, BMP) ile deney yapın veya betiği toplu işleme hattına entegre edin. Aynı desen—engine → görüntü → ayarlar → tanı → çıktı—karşılaşacağınız hemen hemen her OCR görevinde geçerlidir.

Sorularınız veya işbirliği etmeyen tuhaf bir görüntünüz varsa, aşağıya yorum bırakın, kodlamanın tadını çıkarın! 

![Python kullanarak görüntüde OCR gerçekleştirme adımlarını gösteren diyagram](https://example.com/ocr-flow.png "Python OCR motoru ile görüntüde OCR nasıl yapılır gösteren diyagram")

## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Görüntüyü Metne Dönüştür – URL'den Görüntüde OCR Yapma](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Görüntüde OCR için Dikdörtgenler Hazırlayarak Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}