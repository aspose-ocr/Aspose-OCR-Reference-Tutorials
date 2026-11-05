---
category: general
date: 2026-06-16
description: Python OCR motoru kullanarak görüntüden metin tanıyın – fişten metin
  nasıl çıkarılır ve OCR doğruluğu dakikalar içinde nasıl artırılır öğrenin.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- improve ocr accuracy
- python ocr tutorial
- image preprocessing for OCR
language: tr
og_description: Görselden metni hızlıca tanıyın. Bu kılavuz, makbuzdan metin çıkarmayı
  ve Python kullanarak OCR doğruluğunu artırmayı gösterir.
og_title: Python OCR ile görüntüden metin tanıma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  headline: recognize text from image with Python OCR – Complete Guide
  type: TechArticle
- description: recognize text from image using a Python OCR engine – learn how to
    extract text from receipt and improve OCR accuracy in minutes.
  name: recognize text from image with Python OCR – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - Basic familiarity with pip and
      virtual environments. - A sample receipt image (JPEG or PNG) that you want to
      process. - The `ocr` package (the example uses a fictional `ocr` module for
      illustration; replace it with `pytesseract`, `easyocr`, or any library t'
  - name: Expected Output
    text: 'Running the script on a typical grocery receipt yields something like:'
  - name: H3 – Crop to the Receipt Region
    text: 'If your image contains a lot of background (e.g., a photo of a desk), crop
      it first:'
  - name: H3 – Use a Custom Language Pack
    text: 'For receipts that contain foreign characters (e.g., “€” or “¥”), load the
      appropriate language data:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Python OCR ile görüntüden metin tanıma – Tam Kılavuz
url: /tr/python-java/general/recognize-text-from-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Resimden Metin Tanıma Python OCR ile – Tam Kılavuz

Hiç **resimden metin tanıma** yapmanız gerektiğinde sonuçların anlamsız harf yığını gibi göründüğünü düşündünüz mü? Tek başınıza değilsiniz. Birçok küçük işletme senaryosunda—örneğin makbuz tarama, fatura dijitalleştirme veya kimlik kartlarından veri çekme—temiz ve güvenilir bir çıktı elde etmek, sorunsuz bir iş akışı ile baş ağrısı arasında fark yaratır.

Bu öğreticide, hafif bir Python OCR kütüphanesi kullanarak **resimden metin tanıma** işlemini pratik bir şekilde nasıl yapacağınızı adım adım göstereceğiz. Ayrıca **makbuzdan metin çıkarma** dosyalarını nasıl elde edeceğinizi ve pahalı yazılımlar satın almadan **OCR doğruluğunu artırma** ipuçlarını paylaşacağız. Hazır mısınız? Hadi başlayalım.

## Ne Oluşturacaksınız

Bu rehberin sonunda, aşağıdaki özelliklere sahip çalıştırılabilir bir betiğiniz olacak:

1. Bir OCR motoru örneği oluşturur.  
2. Akıllı ön işleme (eğik düzeltme, lekesizleştirme, ikilileştirme) etkinleştirir.  
3. Gürültülü bir makbuz görüntüsü yükler.  
4. Tanıma hattını otomatik olarak çalıştırır.  
5. Temiz, aranabilir metni konsola yazdırır.

Harici hizmetler, gizli API anahtarları yok—sadece istediğiniz projeye uyarlayabileceğiniz saf Python kodu.

### Ön Koşullar

- Makinenizde Python 3.8+ yüklü.  
- pip ve sanal ortamlar hakkında temel bilgi.  
- İşlemek istediğiniz bir örnek makbuz görüntüsü (JPEG veya PNG).  
- `ocr` paketi (örnek, açıklama amaçlı hayali bir `ocr` modülü kullanıyor; `pytesseract`, `easyocr` veya benzer bir API sunan herhangi bir kütüphane ile değiştirin).

> **Pro ipucu:** Eksik bağımlılıklar ile karşılaşırsanız, ilerlemeden önce `pip install ocr` (veya gerçek paket adı) komutunu çalıştırın.

## Adım 1 – Resimden Metin Tanıma: Motoru Kurun

İlk iş olarak, piksel verisini okuyup karakterlere dönüştürebilen bir nesneye ihtiyacımız var. Motor, işlemin beyni gibidir; geri kalan her şey ona bilgi sağlar.

```python
import ocr  # Replace with your actual OCR library import

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Motoru manuel olarak neden oluşturuyoruz? Bazı kütüphaneler tek bir fonksiyon çağrısı ile işinizi halleder, ancak açık bir örnek, ön işleme üzerinde ince ayar yapma imkanı verir—**OCR doğruluğunu artırma** için sonradan ihtiyacımız olan şey bu.

## Adım 2 – Makbuzdan Metin Çıkarma: Ön İşlemeyi Etkinleştirin

Telefon kamerasıyla taranan bir makbuz nadiren mükemmeldir. Hafifçe eğik, toz lekeleriyle dolu ya da dengesiz aydınlatma olabilir. Ön işleme, motor harflere bakmadan önce ağır işi üstlenir.

```python
# Step 2: Enable preprocessing to improve recognition quality
preprocess = engine.preprocessing
preprocess.deskew = True        # Auto‑rotate slightly tilted pages
preprocess.despeckle = True     # Remove isolated noise pixels
preprocess.binarization = True  # Convert image to pure black‑white
```

*Eğik düzeltme* sayfayı düzleştirir, *lekesizleştirme* istenmeyen nokta izlerini siler ve *ikilileştirme* her pikseli ya siyah ya da beyaz yapar. Bu üç bayrak, gürültülü makbuzlarda **OCR doğruluğunu %20‑30** artırabilir.

## Adım 3 – Tanımak İstediğiniz Görüntüyü Yükleyin

Şimdi motoru gerçek dosyaya yönlendiriyoruz. Yol mutlak ya da göreceli olabilir; sadece görüntünün var olduğundan emin olun.

```python
# Step 3: Load the scanned receipt image
engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")
```

Motorun PDF veya çok sayfalı TIFF destekleyip desteklemediğini merak ediyorsanız, çoğu modern kütüphane bunu yapar—sadece dokümantasyona bakın. Tek sayfalı bir JPEG için yukarıdaki satır yeterlidir.

## Adım 4 – OCR Çalıştırın – Motor Geri Kalanı Yapar

Ön işleme ayarlandı ve görüntü yüklendi, sonraki çağrı her şeyi yapar: ön işler, tanıma algoritmasını çalıştırır ve bir sonuç nesnesi döndürür.

```python
# Step 4: Run OCR – the configured preprocessing is applied automatically
ocr_result = engine.recognize()
```

Arka planda motor Tesseract, bir sinir ağı ya da tescilli bir motor kullanıyor olabilir. İç detayları bilmenize gerek yok; sadece temiz bir sonuç alırsınız.

## Adım 5 – Tanınan Metni Çıktılayın

Son olarak, sonuç nesnesinden düz metni alıp ekrana yazdırıyoruz. Gerçek bir uygulamada bunu bir veritabanına, CSV dosyasına ya da bir analiz hattına besleyebilirsiniz.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Beklenen Çıktı

Tipik bir market makbuzu üzerinde betiği çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
WALMART STORE #1234
123 Main St.
Anytown, USA

Date: 06/15/2026   Time: 14:32
Cashier: J. Doe

Item                Qty   Price
---------------------------------
Milk                1     2.99
Bread               2     5.48
Eggs                1     3.20
---------------------------------
Subtotal                    11.67
Tax                         0.93
Total                       12.60
```

Çıktı karışık görünüyorsa, ön işleme bayraklarının açık olduğundan ve görüntünün çok karanlık olmadığından emin olun. İkilileştirme eşiğini (bazı kütüphaneler özelleştirilmiş bir değer ayarlamanıza izin verir) ayarlamak **OCR doğruluğunu** daha da artırabilir.

## İleri Seviye: Makbuzdan Metin Çıkarma Hızını Artırmak İçin İnce Ayar

Beş adımlı akış çoğu durum için işe yarasa da, geceleri yüzlerce makbuzu işlerken hızı artırmak isteyebilirsiniz. İşte iki isteğe bağlı iyileştirme:

### H3 – Makbuz Bölgesine Kırpma

Görüntünüzde çok fazla arka plan (ör. bir masa fotoğrafı) varsa, önce kırpın:

```python
engine.image = engine.image.crop((50, 200, 800, 1200))  # left, top, right, bottom
```

### H3 – Özel Dil Paketi Kullanma

Makbuzlarda yabancı karakterler (ör. “€” veya “¥”) bulunuyorsa, uygun dil verisini yükleyin:

```python
engine.set_language('eng+deu+fra')  # English, German, French
```

Bu iki yöntem, **resimden metin tanıma** işlemini daha güvenilir hâle getirir, özellikle kaynak materyal değişken olduğunda.

## Yaygın Tuzaklar ve Kaçınma Yolları

- **Eksik Yazı Tipleri:** Bazı OCR motorları, özel makbuz yazı tipleri için font dosyalarına ihtiyaç duyar. Gerekli dil paketlerini kurun.  
- **Aşırı Gürültü:** `despeckle=True` olsa bile çok grenli taramalar motoru şaşırtabilir. Pillow’da hızlı bir manuel filtre (`Image.filter(ImageFilter.MedianFilter)`) yardımcı olabilir.  
- **Yanlış DPI:** OCR motorları yaklaşık 300 dpi varsayar. Görüntünüz daha düşükse, önce yeniden boyutlandırın: `engine.image = engine.image.resize((width*2, height*2))`.

Bu sorunları doğrudan ele alarak **OCR doğruluğunu** pahalı üçüncü‑taraf hizmetlerine başvurmadan artırabilirsiniz.

## Tam Script – Çalıştırmaya Hazır

Aşağıda, tartıştığımız tüm unsurları içeren tam, çalıştırılabilir Python programı yer alıyor. `receipt_ocr.py` olarak kaydedin ve `python receipt_ocr.py` komutuyla çalıştırın.

```python
import ocr  # Replace with the actual library you use

def main():
    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Enable preprocessing steps
    preprocess = engine.preprocessing
    preprocess.deskew = True
    preprocess.despeckle = True
    preprocess.binarization = True

    # Load the receipt image (change the path to your file)
    engine.image = ocr.Image.load_from_file("YOUR_DIRECTORY/receipt-noisy.jpg")

    # Optional: crop out unnecessary background
    # engine.image = engine.image.crop((50, 200, 800, 1200))

    # Run the recognition pipeline
    result = engine.recognize()

    # Print the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

Bu betiği çalıştırdığınızda **resimden metin tanıma** yapılır ve güzel biçimlendirilmiş bir makbuz verisi bloğu ekrana yazdırılır. Kırpma koordinatlarını, dil ayarlarını veya ön işleme bayraklarını kendi makbuz düzeninize göre özgürce uyarlayın.

## Sonuç

Python kullanarak **resimden metin tanıma** için basit bir yöntemi, **makbuzdan metin çıkarma** dosyalarını nasıl elde edeceğinizi ve **OCR doğruluğunu artırma** için çeşitli pratik ipuçlarını ele aldık. Temel fikir basit: bir OCR motoru kurun, akıllı ön işleme etkinleştirin, temiz bir görüntü besleyin ve kütüphanenin işi halletmesine izin verin.

Sıradaki adımlar? Makbuzları bir döngü içinde işleyin, her sonucu bir CSV’ye kaydedin veya çıktıyı bir muhasebe sistemine bağlayın. Daha karmaşık yazı tipleri için `easyocr` gibi derin öğrenme tabanlı OCR kütüphanelerini deneyerek doğruluğu daha da artırabilirsiniz.

Belirli bir makbuz formatı hakkında sorularınız mı var ya da çok sayfalı PDF’lerle nasıl başa çıkılacağını görmek ister misiniz? Aşağıya yorum bırakın, kodlamanız keyifli olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Resimden Metin Çıkarma – Aspose OCR ile Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [OCR’da Dikdörtgen Hazırlayarak Resimden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Resimden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}