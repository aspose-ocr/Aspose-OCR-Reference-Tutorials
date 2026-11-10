---
category: general
date: 2026-07-05
description: Python OCR ile görüntüyü metne dönüştür – görüntüden metin çıkarmayı
  ve jpg'den metin tanımayı gösteren adım adım bir Python OCR örneği.
draft: false
keywords:
- convert image to text
- extract text from image
- python ocr example
- ocr engine python
- recognize text from jpg
language: tr
og_description: Python OCR kullanarak görüntüyü metne dönüştürün. Görüntüden metin
  çıkarmak ve dakikalar içinde jpg dosyasındaki metni tanımak için bu Python OCR örneğini
  izleyin.
og_title: Python'da Görüntüyü Metne Dönüştür – Tam OCR Motoru Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert image to text with Python OCR – a step‑by‑step python ocr example
    that shows how to extract text from image and recognize text from jpg.
  headline: Convert Image to Text in Python – Complete OCR Engine Python Tutorial
  type: TechArticle
tags:
- ocr
- python
- image-processing
- text-extraction
title: Python’da Görüntüyü Metne Dönüştür – Tam OCR Motoru Python Eğitimi
url: /tr/python-java/general/convert-image-to-text-in-python-complete-ocr-engine-python-t/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Metne Dönüştürme Python’da – Tam OCR Motoru Python Öğreticisi

Hiç **convert image to text** yapmanız gerektiğinde hangi kütüphaneye güveneceğinizi bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici, taranmış bir makbuzdan ya da bir işaret levhasının fotoğrafından karakter çıkarmaya ilk kez çalıştıklarında bu engelle karşılaşıyor. İyi haber? Python'un OCR ekosistemi işi neredeyse ağrısız hale getiriyor.

Bu **python ocr example** içinde gerçek bir senaryoyu adım adım inceleyeceğiz: Cyrillic karakterler içeren bir JPEG'iniz var ve güvenilir bir şekilde **extract text from image** yapmak istiyorsunuz. Sonunda **recognize text from jpg** dosyalarını nasıl tanıyacağınızı, her adımın neden önemli olduğunu ve kodu diğer diller veya görüntü formatları için nasıl uyarlayacağınızı öğreneceksiniz.

## İhtiyacınız Olanlar

* Python 3.8+ yüklü (en son stabil sürüm en iyisidir).
* OCR paketini kurmak için çalışan bir internet bağlantısı.
* Çekmek istediğiniz metni içeren bir görüntü dosyası (ör. `cyrillic_sample.jpg`).
* İsteğe bağlı ama kullanışlı: bağımlılıkları düzenli tutmak için bir sanal ortam.

Ağır OS‑seviyesi bağımlılıkları yok, karmaşık derleme araçları yok—sadece birkaç pip komutu ve bir avuç kod satırı.

## Adım 1: OCR Motoru Python Paketi'ni Kurun

İlk yapmanız gereken, Python ile iyi çalışan bir OCR motoru edinmektir. Bu öğreticide, API'si birçok gerçek dünya kütüphanesini (ör. `pytesseract` veya `easyocr`) yansıttığı için hayali `ocr` paketini kullanacağız. Şöyle kurun:

```bash
pip install ocr
```

> **Bu adımın önemi:** Paketi kurmak, asıl işi yapan yerel ikili dosyaları ve dil veri dosyalarını da getirir. Bunu atlamak, `import ocr` yapmaya çalıştığınız anda bir `ImportError` oluşturur.

## Adım 2: Modülleri İçe Aktarın ve Ortamı Hazırlayın

Kütüphane artık makinenizde olduğuna göre, ihtiyacınız olan parçaları içe aktarın. Ayrıca motorun ne yaptığını görebilmeniz için logging'i yapılandıracağız—bu, daha sonra **extract text from image** dosyaları temiz olmadığında faydalı olur.

```python
import ocr
import logging

# Enable debug output (optional but recommended for first runs)
logging.basicConfig(level=logging.INFO)
```

> **Pro ipucu:** Jupyter notebook içinde çalışıyorsanız, daha fazla ayrıntı görmek için `logging.getLogger().setLevel(logging.DEBUG)` ayarlamak isteyebilirsiniz.

## Adım 3: Bir OCR Motoru Örneği Oluşturun

Motoru oluşturmak, herhangi bir **ocr engine python** iş akışının temel taşıdır. Bunu karanlık bir odada ışıkları açmak gibi düşünün; olmadan, pipeline'ın geri kalanı hiçbir şey göremez.

```python
# Step 3: Instantiate the OCR engine
ocr_engine = ocr.OcrEngine()
```

> **Bu adımın önemi:** `OcrEngine` nesnesi dil paketleri, ön işleme seçenekleri ve donanım hızlandırma bayrakları gibi yapılandırmaları tutar. Bunlardan herhangi birini daha sonra değiştirmek, sonraki tüm tanıma işlemlerini etkiler.

## Adım 4: Doğru Dili Seçin – Cyrillic Desteği

Cyrillic metinle (veya herhangi bir Latin dışı betik) çalışıyorsanız, motorun hangi dil modelini yükleyeceğini belirtmeniz gerekir. Aksi takdirde bozuk bir çıktı ya da daha kötüsü boş bir string alırsınız.

```python
# Step 4: Set language to Cyrillic (enables Cyrillic block support)
ocr_engine.language = ocr.Language.CYRILLIC
```

> **Köşe durum:** Bazı motorlar dil verilerini ayrı olarak indirmenizi gerektirir. `LanguageDataNotFound` gibi bir hata görürseniz, dili atamadan önce `ocr.download_language('CYRILLIC')` komutunu çalıştırın.

## Adım 5: **convert image to text** Yapmak İstediğiniz Görüntüyü Yükleyin

İşte **convert image to text** ifadesinin gerçekten gerçekleşmeye başladığı yer. OCR motoru bir `Image` nesnesi üzerinde çalışır, ham dosya yolu üzerinde değil, bu yüzden JPEG'i önce sarmalamamız gerekir.

```python
# Step 5: Load the image containing the text
cyrillic_image = ocr.Image.load("YOUR_DIRECTORY/cyrillic_sample.jpg")
```

> **Neden önemli:** Görüntüyü yüklemek, motorun boyutlarını, renk derinliğini ve DPI'yi incelemesine olanak tanır. Bu özellikler, motorun **recognize text from jpg** dosyalarını ne kadar iyi tanıyabileceğini etkiler.

## Adım 6: Metni Tanıma – Python OCR Örneğinin Çekirdeği

Şimdi motoru nihayetinde inşa edildiği işi yapması için istiyoruz: pikselleri karakterlere dönüştürmek. `recognize` metodu, çıkarılan stringi, güven skorlarını ve sınırlama kutularını tutan bir sonuç nesnesi döndürür.

```python
# Step 6: Run OCR and capture the result
ocr_result = ocr_engine.recognize(cyrillic_image)
```

> **Aldığınız sonuç:** `ocr_result.text` satır sonları korunmuş düz bir Python stringidir. Kelime‑seviye konumlara ihtiyacınız varsa, `ocr_result.boxes`'ı inceleyin.

## Adım 7: Tanınan Metni Çıktılamak – **convert image to text** Başarınızı Doğrulayın

Başarılı bir şekilde **convert image to text** yapıp yapmadığınızı görmenin en basit yolu sonucu yazdırmaktır. Gerçek bir uygulamada muhtemelen bunu bir veritabanına ya da bir metin dosyasına yazarsınız.

```python
# Step 7: Print the extracted text
print("=== OCR OUTPUT ===")
print(ocr_result.text)
```

### Beklenen Çıktı

`cyrillic_sample.jpg` dosyasının “Привет, мир!” ifadesini içerdiğini varsayarsak, konsol şu çıktıyı verir:

```
=== OCR OUTPUT ===
Привет, мир!
```

Eğer çıktı boş ya da anlamsız görünüyorsa, dil ayarını ve görüntü kalitesini tekrar kontrol edin. Bulanık görüntüler veya düşük kontrast genellikle kötü **extract text from image** sonuçlarına yol açar.

## Yaygın Sorunlarla Baş Etme

| Problem | Neden Olur | Hızlı Çözüm |
|---------|------------|-------------|
| **Empty string** | Dil modeli yüklenmedi veya görüntü çok karanlık | `ocr_engine.language`'ın betikle eşleştiğinden emin olun; görüntü kontrastını `ocr.Image.adjust_contrast()` ile artırın |
| **Garbage characters** | Yanlış dil veya karışık betikler | `ocr_engine.language = ocr.Language.MULTI` olarak ayarlayın veya iki geçiş yapın (Latin ardından Cyrillic) |
| **Slow performance on large batches** | Motor görüntüleri sıralı işliyor | Çoklu iş parçacığını etkinleştirin: `ocr_engine.set_threads(4)` |
| **Memory leaks** | Görüntü kaynakları serbest bırakılmıyor | Tanıma sonrası `cyrillic_image.close()` çağırın |

> **Pro ipucu:** Toplu işleme için, tanıma döngüsünü bir `try/except` bloğuna sararak ara sıra oluşan `ocr.EngineError` istisnalarını yakalayın ve tüm işi durdurmayın.

## Örneği Genişletme – JPEG'den PDF'ye, Cyrillic'ten Çok Dilli'ye

**convert image to text** için izlediğimiz desen, herhangi bir raster formatına uygulanabilir: PNG, BMP, TIFF, hatta taranmış PDF'ler (önce sayfayı bir görüntü olarak çıkarın). Birden fazla dil içeren **extract text from image** dosyalarına ihtiyacınız varsa, bir liste geçirebilirsiniz:

```python
ocr_engine.language = [ocr.Language.CYRILLIC, ocr.Language.ENGLISH]
```

Ve akıllı telefonla çekilmiş yüksek çözünürlüklü fotoğraflarla çalışıyorsanız, bir ön‑işleme adımını düşünün:

```python
# Denoise and binarize for better OCR accuracy
clean_image = cyrillic_image.filter(ocr.Filter.GAUSSIAN_BLUR, radius=1)
clean_image = clean_image.binarize(threshold=127)
ocr_result = ocr_engine.recognize(clean_image)
```

Bu ince ayarlar, genellikle vasat bir **python ocr example**'ı üretim‑düzeyi koda dönüştürür.

## Tam Çalışan Betik

Aşağıda, tüm parçaları bir araya getiren eksiksiz, çalıştırmaya hazır betik bulunmaktadır. `convert_image_to_text.py` olarak kaydedin ve `python convert_image_to_text.py` komutuyla çalıştırın.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Görüntüyü Metne Dönüştür – URL'den Görüntüye OCR Uygula](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [OCR'da Dikdörtgen Hazırlayarak Görüntüden Metin Çıkarma](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}