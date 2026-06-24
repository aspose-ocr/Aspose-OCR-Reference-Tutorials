---
category: general
date: 2026-06-19
description: Aspose OCR ve AI post‑işlemcisini Python’da kullanarak görüntü üzerinde
  OCR nasıl yapılır öğrenin. Otomatik indirilen model, yazım denetimi ve GPU hızlandırma
  içerir.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: tr
og_description: Aspose OCR ve AI post‑işlemci kullanarak görüntüde OCR yapın. Otomatik
  indirilen model, yazım denetimi ve GPU hızlandırmasıyla adım adım kılavuz.
og_title: Görselde OCR yap – Tam Python Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Aspose AI ile görüntüde OCR gerçekleştir – Tam Python Rehberi
url: /tr/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görselde OCR Gerçekleştirme – Tam Python Öğreticisi

Hiç **görselde OCR gerçekleştirme** dosyalarıyla kütüphane karmaşası yaşamadan nasıl yapılır diye merak ettiniz mi? Deneyimlerime göre sorun genellikle ham bir OCR motoru ile uğraşmak ve ardından gürültülü çıktıyı temizlemeye çalışmaktır. Neyse ki, Aspose OCR for Python ve AI post‑processor’ı bütün süreci çok kolaylaştırıyor.

Bu rehberde, **görselde OCR gerçekleştirme** verisini nasıl işleyebileceğinizi, otomatik indirilmiş bir modelle doğruluğu artırmayı, imla denetimini etkinleştirmeyi ve mümkün olduğunda GPU hızlandırmasından yararlanmayı adım adım gösteren uçtan uca bir örnek üzerinden ilerleyeceğiz. Bu örnek sayesinde, fatura, makbuz tarama veya belge dijitalleştirme projelerinizde kullanabileceğiniz yeniden kullanılabilir bir betiğe sahip olacaksınız.

## Ne Oluşturacaksınız

Küçük bir Python programı oluşturacağız ve bu program:

1. Aspose OCR motorunu başlatır ve örnek bir fatura görseli yükler.  
2. Temel bir OCR çalıştırır ve ham metni ekrana yazdırır.  
3. **Aspose AI**’yi Hugging Face’den **otomatik indirilen bir model** ile yapılandırır.  
4. **AI post‑processor**’ı (içinde **imla denetimi post‑processor** da bulunur) çalıştırarak OCR çıktısını temizler.  
5. Tüm kaynakları sorunsuz bir şekilde serbest bırakır.

Harici hizmetler, API anahtarları yok—sadece birkaç satır Python ve Aspose’un gücü.

> **İpucu:** Eğer yeterli bir GPU’ya sahip bir makinede çalışıyorsanız, `gpu_layers` ayarı post‑processing adımındaki süreyi saniyelerce kısaltabilir.

## Önkoşullar

- Python 3.8 ve üzeri (kod tip ipuçları içeriyor, ancak isteğe bağlı).  
- `aspose-ocr` ve `aspose-ai` paketleri `pip` ile kurulmuş olmalı.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- `sample_invoice.png` gibi bir örnek görsel (PNG, JPG veya TIFF) erişilebilir bir konumda bulunmalı.  
- (İsteğe bağlı) **GPU hızlandırması** istiyorsanız CUDA‑destekli bir GPU ve uygun sürücüler.

Temel hazırlıklar tamam, şimdi koda dalalım.

![görselde OCR gerçekleştirme örneği](image.png)

## Görselde OCR Gerçekleştirme – Adım 1: OCR motorunu başlatma ve görseli yükleme

İlk olarak bir OCR motoru örneğine ihtiyacımız var. Aspose OCR, düşük seviyeli görsel ön‑işlemeyi soyutlayan temiz, nesne‑yönelimli bir API sunar.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Neden önemli:**  
Dili önceden ayarlamak, motorun hangi karakter setini bekleyeceğini belirler ve tanıma hızı ile doğruluğu artırabilir. Çok dilli belgelerle çalışıyorsanız, `"en"` yerine ihtiyacınıza göre `"fr"` veya `"de"` gibi bir kod kullanın.

## Adım 2: Temel OCR çalıştırma ve ham metni görüntüleme

Şimdi tanıma işlemini gerçekleştiriyoruz. Sonuç nesnesi ham metni, güven puanlarını ve gerekirse daha sonra kullanabileceğiniz sınırlama kutularını içerir.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Tipik bir çıktı şöyle görünebilir (zaman zaman hatalı karakterler fark edeceksiniz):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Motorun bir “O” gördüğünü düşündüğü yerlerde sıfır (`0`) görüyorsunuz. İşte **AI post‑processor** burada devreye giriyor.

## Aspose AI’yı Yapılandırma – otomatik indirilen model ve imla denetimi

Ham OCR sonucunu AI katmanına vermeden önce, Aspose AI’ya hangi modeli kullanacağını söylememiz gerekir. Kütüphane, Hugging Face’den otomatik olarak bir model indirebilir, böylece büyük `.bin` dosyalarıyla uğraşmazsınız.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Ayarların Açıklaması**

| Ayar | Ne işe yarar | Ne zaman ayarlanmalı |
|------|--------------|----------------------|
| `allow_auto_download` | Aspose’un modeli ilk çalıştırmada otomatik olarak indirmesini sağlar. | Çevrim dışı kullanım için önceden indirme yapmadığınız sürece `true` bırakın. |
| `hugging_face_repo_id` | Hugging Face üzerindeki modelin tanımlayıcısı. | Alan‑spesifik bir model gerekiyorsa farklı bir repo kimliğiyle değiştirin. |
| `hugging_face_quantization` | Kuantizasyon seviyesini seçer (`int8`, `float16`, vb.). | Düşük bellek ortamları için `int8`, daha yüksek doğruluk için `float16` kullanın. |
| `gpu_layers` | GPU’da çalıştırılacak transformer katman sayısı. | CPU‑only için `0`, modelin toplam katman sayısına kadar (Qwen2.5‑3B için 20) bir değer verin. |

## OCR sonucunda AI post‑processor’ı çalıştırma

Motor hazır olduğunda, ham OCR çıktısını AI hattına besliyoruz. Dahili **imla denetimi post‑processor** bariz yazım hatalarını düzeltirken, dil modeli ek işlemciler etkinleştirildiğinde eksik bilgileri doldurabilir veya yeniden ifade edebilir.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

İmla denetimi adımından sonra beklenen çıktı:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Sıfırların doğru harflere, “Am0unt” hatalı kelimesinin ise “Amount” olarak düzeltildiğine dikkat edin. **AI post‑processor**, ham metni seçilen model üzerinden geçirerek eğitimine dayalı olarak iyileştirilmiş bir versiyon döndürür.

### Kenar Durumları ve İpuçları

- **Düşük çözünürlüklü görseller**: OCR motoru zorlanıyorsa, önce görseli yükseltmeyi (`Pillow` yardımcı olabilir) veya `ocr_engine.ImagePreprocessingOptions` değerlerini artırmayı düşünün.  
- **Latin dışı betikler**: `ocr_engine.Language` değerini uygun ISO kodu ile değiştirin (`"zh"` Çince, `"ar"` Arapça vb.).  
- **GPU algılanmadı**: `gpu_layers` ayarı, uyumlu bir GPU bulunmadığında sessizce CPU’ya geçiş yapar; ekstra hata yönetimi eklemenize gerek yok.  
- **Model boyutu sınırlamaları**: Qwen2.5‑3B modeli sıkıştırılmış hâliyle ~4 GB; otomatik indirme için yeterli disk alanınız olduğundan emin olun.

## Kaynakları Serbest Bırakma – Temiz Kapatma

Aspose nesneleri yerel tutucular içerdiği için işiniz bittiğinde serbest bırakmak iyi bir uygulamadır. Bu, özellikle uzun süren hizmetlerde bellek sızıntılarını önler.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

İsterseniz tüm betiği `try…finally` bloğu içine alarak açık bir temizlik de yapabilirsiniz.

## Tam Betik – kopyala‑yapıştır hazır

Aşağıda, `YOUR_DIRECTORY` kısmını görselinizin yolu ile değiştirmeniz yeterli olacak tam program yer alıyor.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Şu komutla çalıştırın:

```bash
python perform_ocr_on_image.py
```

Ham ve temizlenmiş çıktıları konsolda göreceksiniz.

## Sonuç


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları daha derinlemesine ele alan örnekler sunar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose OCR ile Görselden Metin Çıkarma – Adım‑Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Aspose.OCR ile Dil Seçimi Yaparak C#’ta Görsel Metin Çıkarma](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görseli Metne Dönüştür – URL’den Görselde OCR Gerçekleştirme](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}