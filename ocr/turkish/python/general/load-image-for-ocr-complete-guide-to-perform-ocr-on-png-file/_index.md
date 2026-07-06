---
category: general
date: 2026-06-25
description: OCR için resmi yükleyin ve aocr kullanarak adım adım bir Python öğreticisiyle
  PNG üzerinde OCR gerçekleştirin. Hata ayıklamayı, kaydı ve en iyi uygulamaları öğrenin.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: tr
og_description: OCR için görüntüyü yükleyin ve aocr kullanarak PNG üzerinde OCR gerçekleştirin.
  Bu kılavuz, günlük kaydı, görüntü yükleme ve tanıma işlemlerini tam kodla adım adım
  gösterir.
og_title: OCR için Görüntü Yükleme – Adım Adım Python Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: OCR için Görüntü Yükleme – PNG Dosyalarında OCR Yapma Tam Rehberi
url: /tr/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntü Yükleme – PNG Dosyalarında OCR Gerçekleştirme İçin Tam Kılavuz

Hiç **load image for OCR** yapmanız gerekti ama doğru hata ayıklamayı nasıl kuracağınızdan emin olmadınız mı? Yalnız değilsiniz. Birçok projede ilk engel, PNG'yi motorun içine almak ve aynı zamanda motorun içinde neler olduğunu görebilmektir.  

Bu öğreticide, `aocr` kütüphanesini kullanarak **perform OCR on PNG** dosyaları için ihtiyacınız olan her şeyi adım adım göstereceğiz – ayrıntılı çıktı için bir logger kurmaktan metni gerçekten tanımaya kadar. Sonunda, herhangi bir Python projesine ekleyebileceğiniz yeniden kullanılabilir bir betiğe sahip olacak ve her parçanın neden önemli olduğunu anlayacaksınız.

## Neler Öğreneceksiniz

- Her adımı izleyebilmeniz için `aocr` logger'ı nasıl başlatacağınızı.
- `aocr.OcrEngine` ile **load image for OCR** için tam kodu.
- Ayrıntılı hata ayıklama bilgisi alabilmek için günlükleme seviyesini nasıl yapılandıracağınızı.
- Motoru **perform OCR on PNG** çalıştırmayı ve sonuçları almayı.
- Eksik dosyalar veya desteklenmeyen formatlar gibi yaygın tuzakları ele almak için ipuçları.

`aocr` ile ilgili önceden deneyim gerekmez; sadece çalışan bir Python 3 kurulumu ve okumak istediğiniz bir görüntü yeterlidir. Hadi başlayalım.

![OCR için görüntü yükleme örneği](assets/load-image-ocr.png "Python'da OCR için bir görüntünün yüklenmesinin illüstrasyonu")

## Ön Koşullar

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | `aocr` modern yorumlayıcıları hedefler ve tip ipuçları kullanır. |
| `aocr` library installed (`pip install aocr`) | Paket olmadan kullandığımız sınıflar mevcut olmaz. |
| A PNG image you want to read | Bu öğretici **perform OCR on PNG** üzerine odaklanır, bu yüzden bir PNG gereklidir. |
| Write permission to a log directory | Logger `ocr_debug.log` dosyasını oluşturmalıdır. |

Eğer bunlardan herhangi birine sahip değilseniz, şimdi kurun – sadece bir dakikanızı alır.

```bash
pip install aocr
```

## Adım 1: OCR için Görüntü Yükleme – Günlüklemeyi Başlatma

Görüntüye dokunmadan önce bir logger kurun. OCR hata ayıklama, motorun ne yaptığını göremiyorsanız bir kabus olabilir. `aocr.Logging` sınıfı her şeyi bir dosyaya yazar ve seviyeyi `DEBUG` olarak ayarladığınızda her iç çağrıyı göreceksiniz.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**Neden önemli:**  
OCR motoru dosyayı bulamazsa veya görüntü formatı desteklenmiyorsa, logger istisna yığın izini yakalar. Bu, daha sonra sonsuz tahmin çalışmasından sizi kurtarır.

## Adım 2: PNG Üzerinde OCR Gerçekleştirme – Motoru Yapılandırma

Logger hazır olduğuna göre, onu OCR motoruna ekleyin. Bu adım ikisini birleştirir ve motorun her eylemi kaydedilir.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**Pro ipucu:**  
Aynı `ocr_engine` örneğini birden fazla görüntü için yeniden kullanabilirsiniz. Bir toplu işlem yapıyorsanız önceki durumu temizlemeyi unutmayın.

## Adım 3: OCR için Görüntü Yükleme – PNG Dosyasını Besleme

İşte öğreticinin özü: gerçekten **load image for OCR**. `load_image` yöntemi bir dosya yolu alır; PNG'yi motorun anlayabileceği bir bitmap'e dahili olarak çözer.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### Dikkat Edilmesi Gereken Kenar Durumları

1. **File Not Found** – Yol yanlışsa, `aocr` bir `FileNotFoundError` yükseltir. Logger bunu not eder, ancak siz de yakalayabilirsiniz:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **Unsupported Format** – PNG yaygın olarak desteklense de, bozuk bir dosya `UnsupportedFormatError` tetikleyebilir. Bu durumda, yüklemeden önce görüntüyü Pillow ile temiz bir PNG'ye dönüştürmeyi düşünün.

## Adım 4: PNG Üzerinde OCR Gerçekleştirme – Tanıma Çalıştırma

Görüntü bellekte olduğuna göre, sonunda **perform OCR on PNG** yapabilirsiniz. `recognize` yöntemi motorun boru hatlarını (ön‑işleme, segmentasyon, sınıflandırma) başlatır ve sonuç nesnesini doldurur.

```python
# Execute the OCR process
ocr_engine.recognize()
```

Bu çağrıdan sonra, motor tanınan metni tutar. `result` niteliği üzerinden erişebilirsiniz:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**Neden sonucu kontrol etmelisiniz:**  
Bazı OCR motorları düşük kontrastlı görüntüler için boş string döndürür. Sonucu hemen görmek, yeniden çalıştırmadan önce ön‑işleme (ör. kontrast artırma) yapmanız gerekip gerekmediğine karar vermenizi sağlar.

## Adım 5: Hepsini Birleştirme – Yeniden Kullanılabilir Bir Fonksiyon

Parçaları tek bir fonksiyonda birleştirmek, diğer betiklerden veya bir web servisinden çağırmayı kolaylaştırır. Bu aynı zamanda **load image for OCR** ve **perform OCR on PNG** nasıl yapılır gösterir, tek bir paket içinde.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

Betik çalıştırıldığında `logs` klasöründe ayrıntılı bir `ocr_debug.log` oluşturur, ardından tanınan metni konsola yazdırır. Artık başka bir yerde içe aktarabileceğiniz bir **perform OCR on PNG** yardımcı programına sahipsiniz.

## Sık Sorulan Sorular & Karşılaşılan Sorunlar

- **PNG'yi başka bir formata dönüştürmem gerekiyor mu?**  
  Genellikle gerekmez. `aocr` PNG'yi yerel olarak işler, ancak görüntü çok büyükse (>10 MP) işleme hızını artırmak için önce ölçek küçültmek isteyebilirsiniz.

- **Logger dosyası çok büyürse ne olur?**  
  Her çalıştırmadan sonra logu döndürün veya pipeline'ın çalıştığından emin olduğunuzda seviyeyi `INFO` ile sınırlayın.

- **Bir döngüde birden fazla görüntüyü işleyebilir miyim?**  
  Kesinlikle. Her dosya için `ocr_png` çağırın; fonksiyon her seferinde yeni bir logger oluşturur ve logları izole tutar.

- **Düz metin yerine sınırlama kutuları almanın bir yolu var mı?**  
  Evet – `engine.result` ayrıca `boxes` ve `confidences` içerir. Düzen bilgisine ihtiyacınız varsa `result.boxes` için `aocr` belgelerini inceleyin.

## Sonuç

Artık `aocr` kütüphanesini kullanarak **load image for OCR** ve **perform OCR on PNG** nasıl yapılacağını biliyorsunuz, hata ayıklamayı zahmetsiz hâle getiren sağlam bir günlükleme kurulumu ile birlikte. Örnek fonksiyon tüm iş akışını kapsar, böylece herhangi bir projeye ekleyebilir ve hemen metin çıkarmaya başlayabilirsiniz.

Sonraki adımlar? Motoru farklı görüntü tipleri (JPEG, TIFF) ile besleyerek doğruluğun nasıl değiştiğini görün, ya da gürültülü taramalarda sonuçları artırmak için eşikleme gibi ön‑işleme teknikleriyle deney yapın. Ayrıca yapılandırılmış veri (tablolar, formlar) çıkarmakla ilgileniyorsanız, `aocr` bölümlerindeki düzen analizi konularına göz atın – bunlar yeni oluşturduğunuz şeyle güzel bir uyum sağlar.

Kodlamaktan keyif alın, ve OCR boru hatlarınızın her zaman hatasız olmasını dileriz!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüyü OCR Yapma – OCR Görüntü Tanıma'da Görüntü Üzerinde OCR Gerçekleştirme](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Görüntüden Metin Çıkarma – .NET için Aspose.OCR ile OCR Optimizasyonu](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}