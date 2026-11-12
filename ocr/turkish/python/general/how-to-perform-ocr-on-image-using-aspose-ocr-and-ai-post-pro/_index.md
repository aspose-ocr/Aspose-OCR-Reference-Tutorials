---
category: general
date: 2026-09-25
description: Aspose OCR ile bir görüntüde OCR nasıl yapılır, OCR için görüntü nasıl
  yüklenir ve bir makbuzdaki metin nasıl tanınır, tam bir Python örneğinde öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: tr
lastmod: 2026-09-25
og_description: Python'da Aspose OCR kullanarak görüntüde OCR yapın. Bu kılavuz, OCR
  için görüntünün nasıl yükleneceğini ve AI iyileştirmesiyle makbuzdaki metni nasıl
  tanıyacağınızı gösterir.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Aspose OCR ve AI post‑işlemcisi ile görüntüde OCR gerçekleştirme – Python
  rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Python'da Aspose OCR ve AI post‑işlemci ile görüntüde OCR nasıl yapılır
url: /tr/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da Aspose OCR ve AI post‑işlemci kullanarak görüntü üzerinde OCR nasıl yapılır

Python'da **görüntü dosyaları üzerinde OCR gerçekleştirmek** istiyorsanız, bu öğretici size tamamen çalıştırılabilir bir çözüm sunar. **Görüntüyü OCR için yükleme**, Aspose OCR motorunu çalıştırma ve **fiş belgelerinden metin tanıma** işlemlerini isteğe bağlı AI destekli post‑işlemle nasıl yapacağınızı öğreneceksiniz.

SDK kurulumundan kaynakların serbest bırakılmasına kadar her adımı adım adım göstereceğiz, böylece kendi uygulamalarınıza güvenilir metin çıkarımını eksiksiz bir şekilde entegre edebilirsiniz.

## Ön Koşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- Python 3.8+  
- Pip aracılığıyla Aspose OCR for Python (`pip install aspose-ocr`)  
- İsteğe bağlı AI model indirmesi için internet erişimi  
- Bilinen bir dizine yerleştirilmiş örnek fiş görüntüsü (`receipt.png`)  

Ek dış hizmetlere ihtiyaç yoktur; kod yerel olarak çalışır ve GPU katmanları mevcut olduğunda ücretsiz Qwen2‑3B‑Instruct modelini kullanır.

## Adım 1: Gerekli paketleri kurun

```bash
pip install aspose-ocr
```

`aspose-ocr` paketi, **görüntü üzerinde OCR gerçekleştirmek** için kullanacağımız `OcrEngine` sınıfını ve `AsposeAI` post‑işlemcisini içerir.

## Adım 2: OCR motorunu oluşturun ve yapılandırın – görüntüyü OCR için yükleyin

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

`load_image` çağrısı, motorun analiz edeceği dosyayı belirtir. **Görüntü üzerinde OCR gerçekleştirmek** istediğiniz herhangi bir PNG, JPG veya TIFF dosyasının yolunu buraya koyabilirsiniz.

## Adım 3: İsteğe bağlı AsposeAI post‑işlemcisini ayarlayın

AI post‑işlemci, imla hatalarını düzeltebilir, biçimlendirmeyi iyileştirebilir veya ham OCR sonucu döndürüldükten sonra özel mantık uygulayabilir.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

Yapılandırma, işlemciye varsayılan Qwen2 modelini indirmesini söyler; bu sayede **görüntü üzerinde OCR gerçekleştirmek** daha yüksek seviyeli dil anlayışıyla yapılır.

## Adım 4: Basit bir post‑işlem fonksiyonu ekleyin

Ham metni alıp düzeltilmiş bir versiyon döndüren herhangi bir callable nesnesi bağlayabilirsiniz. İşte yaygın bir yazım hatasını düzelten minimal bir örnek:

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Fonksiyon kaydedildiği için, `run_postprocessor` her çağrıldığında OCR çıktısı bu adım üzerinden geçer.

## Adım 5: OCR'ı çalıştırın ve sonucu iyileştirin – fişten metin tanıma

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

`recognize` çağrısı, `text` özelliği içinde fiş görüntüsünden çıkarılan ham karakterleri barındıran bir nesne döndürür. Ardından `run_postprocessor` çağrısı, imla kontrolümüzün (ve model tabanlı iyileştirmelerin) uygulandığı yeni bir sonuç verir.

### Beklenen çıktı

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

AI‑geliştirilmiş metnin yazım hatasını düzelttiğine ve okunabilirlik için satır sonları eklediğine dikkat edin—tam da **fişten metin tanıma** dosyalarında istediğiniz şey.

## Adım 6: Kaynakları temizleyin

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Birçok görüntüyü uzun süreli bir hizmette işlerken kaynakları serbest bırakmak özellikle önemlidir.

## Tam çalıştırılabilir betik

Tüm parçaları bir araya getirdiğinizde, kopyalayıp yapıştırıp çalıştırabileceğiniz tek bir betik elde edersiniz:

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Betik şu şekilde çalıştırılır:

```bash
python ocr_receipt.py
```

Orijinal ve AI‑geliştirilmiş çıktılar konsolda görüntülenecektir.

## İpuçları ve yaygın tuzaklar

- **Görüntü kalitesi önemlidir** – fiş görüntüsünün iyi aydınlatılmış ve aşırı sıkıştırılmamış olduğundan emin olun; aksi takdirde OCR motoru karakterleri kaçırabilir ve post‑işlemenin faydası azalır.  
- **GPU bulunabilirliği** – makinenizde uyumlu bir GPU yoksa, `gpu_layers=0` ayarlayarak CPU çıkarımını zorlayın; model hâlâ çalışır, ancak daha yavaş olur.  
- **Özel post‑işlemciler** – birden fazla fonksiyonu zincirleyebilir veya tarih, tutar, satıcı adı gibi öğeleri yeniden biçimlendirmek için daha gelişmiş bir dil modeli kullanabilirsiniz.  
- **Toplu işleme** – tek bir `AsposeAI` nesnesi oluşturup bunu birçok `OcrEngine` örneği arasında yeniden kullanarak model indirmelerinin tekrarlanmasını önleyin.  

## Sonuç

Artık **görüntü dosyaları üzerinde OCR gerçekleştirmek**, **görüntüyü OCR için yükleme** ve **fişten metin tanıma** işlemlerini AI‑destekli iyileştirmelerle nasıl yapacağınızı biliyorsunuz. Yukarıdaki adımları izleyerek, herhangi bir Python uygulamasına doğru, yüksek verimli fiş işleme entegrasyonu sağlayabilirsiniz.

**Sonraki adımlar**: para birimi normalizasyonu gibi ek post‑işlem tekniklerini keşfedin, sonucu bir veritabanına entegre edin veya çok dilli fişler için daha büyük bir modele geçin. Daha derin özelleştirme için Aspose OCR belgelerinde özel dil paketleri ve gelişmiş görüntü ön‑işleme konularına bakın.

İyi kodlamalar!


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Görüntüyü Metne Dönüştür: Aspose OCR (Python) Kullanarak Görüntüden Metin Çıkarma](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Aspose.OCR ile Dil Seçimi Yaparak Görüntü Metnini OCR'lamak](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [C#'ta OCR Nasıl Yapılır – Aspose OCR Kullanarak Görüntüden Metin Çıkarma](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}