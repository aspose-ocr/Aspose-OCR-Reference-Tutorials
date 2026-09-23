---
category: general
date: 2026-01-12
description: Aspose OCR kullanarak Python ile görüntüden metin çıkarın. Tarama görüntüsünü
  metne dönüştürmeyi, asenkron kodla sadece birkaç dakikada öğrenin.
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: tr
og_description: Aspose OCR ile Python’da görüntüden metin çıkarma. Bu öğreticide,
  taranmış görüntüyü asenkron fonksiyonlar kullanarak metne nasıl dönüştüreceğiniz
  gösterilmektedir.
og_title: Görüntüden Metin Çıkarma Python – Asenkron OCR Kılavuzu
tags:
- python
- ocr
- async
title: Python ile Görüntüden Metin Çıkarma – Asenkron OCR Rehberi
url: /tr/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Python – Async OCR Rehberi

Hiç **extract text from image Python** betikleriyle çalışırken OCR kısmında takıldıysanız? Tek başınıza değilsiniz. Birçok geliştirici, taranmış bir belgeyi alınca ve bunu saçlarını çekmeden aranabilir metne dönüştürmek istediğinde bir duvara çarpar.

Bu öğreticide, Aspose OCR’ın asenkron API’sini kullanarak **scanned image to text** nasıl dönüştüreceğinizi gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz tek bir fonksiyonunuz olacak ve OCR birkaç saniye sürse bile uygulamanızın yanıt verebilir kalmasını sağlayan async işleme nedenlerini anlayacaksınız.

## Gereksinimler

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8+ (async özellikleri en az 3.7 gerektirir)
- `asposeocr` paketi (`pip install asposeocr`) – kullanacağımız kütüphane
- Bir taranmış görüntü dosyası (TIFF, PNG, JPEG – Aspose OCR’ın desteklediği herhangi bir format)
- `asyncio` ile temel aşinalık (eğer yoksa endişelenmeyin – her adımı açıklayacağız)

Ek sistem bağımlılıkları gerekmez; Aspose OCR ihtiyacınız olan her şeyi içinde barındırır.

![Diagram showing async OCR flow – extract text from image python](https://example.com/async-ocr-diagram.png "async OCR flow – extract text from image python")

## Adım 1 – Asenkron Yardımcı Fonksiyonu Oluşturma  

Çözümün kalbi, bir görüntüyü yükleyen, OCR’u başlatan ve ardından sonucu bekleyen bir `async` fonksiyonudur. Fonksiyonun asenkron kalması, OCR motoru arka planda çalışırken diğer coroutine’leri (ör. daha fazla dosya indirme) çalıştırabilmenizi sağlar.

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**Neden önemli:** Bir `Future` döndürerek Aspose OCR, ağır işi ayrı bir iş parçacığı havuzunda yapar. `await` olay döngüsünü serbest bırakır, böylece uygulamanız hızlı kalır. Birden çok görüntüyü aynı anda işlemek isterseniz, sadece birkaç `async_ocr` çağrısını `asyncio.gather` ile zamanlayabilirsiniz.

## Adım 2 – Coroutine’ı Olay Döngüsünde Çalıştırma  

Yardımcı fonksiyon elimizde olduğuna göre, onu çalıştırmamız gerekiyor. `asyncio.run` yeni bir olay döngüsü oluşturur, coroutine’ı çalıştırır ve her şeyi temiz bir şekilde kapatır.

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**İpucu:** Bunu daha büyük bir async uygulamaya (ör. FastAPI) entegre ediyorsanız, `asyncio.run` yerine doğrudan `await async_ocr(...)` çağırırsınız.

## Adım 3 – Çıktıyı Doğrulama  

Betik çalıştırıldığında aşağıdakine benzer bir şey görmelisiniz:

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

Çıktı bozuk görünüyorsa, şu noktaları kontrol edin:

1. Görüntü net ve aşırı sıkıştırılmış değil.  
2. Doğru dili seçtiniz (`ocr.Language.ENGLISH` çoğu Latin temelli metin için çalışır).  
3. Dosya yolu doğru ve dosya okunabilir.

## Adım 4 – Kenar Durumlarını Ele Alma  

### Birden Çok Dil  

İngilizce dışındaki bir dilde **convert scanned image to text** yapmak istiyorsanız, sadece dil özelliğini değiştirin:

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### Büyük Dosyalar  

Çok büyük TIFF dosyaları için, OCR’a vermeden önce yeniden boyutlandırmayı veya daha düşük çözünürlüklü PNG’ye dönüştürmeyi düşünün. Bu, bellek baskısını azaltır ve işleme süresini hızlandırır.

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### Hata Yönetimi  

Ağ‑ile ilgili veya lisans hatalarını yakalamak için OCR çağrısını bir `try/except` bloğuna sarın.

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## Adım 5 – Ölçeklendirme: Birçok Görüntüyü Aynı Anda İşleme  

Fonksiyon async olduğu için aynı anda onlarca OCR işi başlatabilirsiniz:

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

Bu desen, OCR motoru paralel çalışırken CPU’yu meşgul tutar ve toplam işleme süresini büyük ölçüde azaltır.

## Sonuç  

Artık Aspose OCR’ın asenkron API’sini kullanan sağlam bir **extract text from image Python** çözümünüz var. Tam örnek şu adımları gösteriyor:

1. OCR motorunu başlatma ve dili seçme.  
2. `process_async` ile OCR’u asenkron başlatma.  
3. Olay döngüsünü engellemeden sonucu bekleme.  
4. Büyük dosyalar ve çok‑dilli destek gibi yaygın sorunları ele alma.  

Kodu kendi veri akışlarınıza uyarlamaktan çekinmeyin— ister bir belge yönetim sistemi, bir arama indeksleyici ya da basit bir komut satırı aracı geliştirin. Bir sonraki adımlar şunlar olabilir:

- Çıkarılan metni tam‑metin arama için bir veritabanına kaydetme.  
- `PyPDF2` gibi bir kütüphane kullanarak aranabilir PDF’ler oluşturma.  
- FastAPI gibi bir web çerçevesiyle RESTful OCR servisi entegrasyonu.

İyi kodlamalar, taranmış görüntülerinizi aranabilir, düzenlenebilir metne dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}