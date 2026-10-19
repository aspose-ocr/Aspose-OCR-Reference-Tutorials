---
category: general
date: 2026-08-12
description: Yapay zeka hattınıza imla denetleyicisi ekleyin ve post işleyiciyi nasıl
  ayarlayacağınızı, post işleme eklemeyi ve Python’da imla denetimini nasıl uygulayacağınızı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add spell checker
- add post processing
- use post processor
- apply spell checking
- how to set post processor
language: tr
lastmod: 2026-08-12
og_description: AI pipeline'ınıza yazım denetleyicisi ekleyin. Bu kılavuz, post işlemciyi
  nasıl ayarlayacağınızı, post işlemeyi nasıl ekleyeceğinizi ve birkaç dakika içinde
  yazım denetimini nasıl uygulayacağınızı gösterir.
og_image_alt: Diagram illustrating how to add spell checker as a post processor in
  an AI pipeline
og_title: AI boru hattına yazım denetleyicisi ekleyin – eksiksiz Python öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  headline: Add spell checker to an AI pipeline – step‑by‑step guide
  type: TechArticle
- description: Add spell checker to your AI pipeline and learn how to set post processor,
    add post processing, and apply spell checking in Python.
  name: Add spell checker to an AI pipeline – step‑by‑step guide
  steps:
  - name: Why this works
    text: '* **`SpellChecker`** encapsulates the logic for detecting and correcting
      misspelled tokens. * **`set_post_processor`** tells the pipeline to invoke the
      supplied object after the primary model finishes inference. * The configuration
      dictionary lets you customize behavior (language, custom dictionarie'
  - name: What the wrapper does
    text: 1. **Runs the original inference** and captures the raw output. 2. **Detects
      the appropriate entry point** (`process` method or callable) on the supplied
      processor. 3. **Calls the processor** with the result and any options you provided.
  - name: Handling edge cases
    text: '| Situation | Recommended approach | |----------------------------------------|--------------------------------------------------------------------|
      | Input contains domain‑specific terms | Provide a custom dictionary via the
      `options` parameter. | | Processor raises an exception | Wrap the call in '
  type: HowTo
tags:
- AI pipeline
- Python
- post‑processing
title: AI boru hattına yazım denetleyicisi ekleyin – adım adım rehber
url: /tr/python/general/add-spell-checker-to-an-ai-pipeline-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# AI pipeline'ına yazım denetleyicisi ekleme – adım adım rehber

Bir AI pipeline'ına **yazım denetleyicisi eklemeniz** gerekiyorsa, bu öğretici tam olarak nasıl yapılacağını gösterir. Bir post işlemci ayarlamayı, post işlem eklemeyi ve minimum kodla yazım denetimini uygulamayı göreceksiniz.

Bu kılavuz, özel yazım denetleme kütüphanesinin kurulumundan mevcut bir pipeline'a entegrasyonuna kadar her şeyi kapsar. Makalenin sonunda, oluşturulan metindeki yazım hatalarını düzelten tam bir uçtan uca örnek çalıştırabilirsiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.9 veya daha yeni bir sürüm yüklü.  
* Post‑processing destekleyen bir AI pipeline nesnesi (örneğin, `transformers` kütüphanesinden bir `TransformerPipeline`).  
* `my_spellchecker` paketine veya uyumlu herhangi bir yazım denetleme modülüne erişim.

Pipeline iç yapıları hakkında derin bilgi sahibi olmanıza gerek yok; aşağıdaki adımlar tüm entegrasyon detaylarını halleder.

## Yazım denetleyicisini post işlemci olarak ekleme

Temel fikir, yazım denetleme sınıfının bir örneğini oluşturup `set_post_processor` yöntemiyle pipeline'a kaydetmektir. Bu yöntem, işlemci nesnesini ve isteğe bağlı bir konfigürasyon sözlüğünü kabul eder.

```python
# Step 1: Import the custom spell checker class
from my_spellchecker import SpellChecker

# Step 2: Create an instance of the spell checker
spell_checker = SpellChecker()

# Step 3: Attach the spell checker as a post‑processor to the AI pipeline,
#         providing any necessary options (e.g., language)
ai.set_post_processor(spell_checker, {"lang": "en"})
```

### Neden bu çalışıyor

* **`SpellChecker`** yanlış yazılmış tokenları tespit etme ve düzeltme mantığını kapsüller.  
* **`set_post_processor`** temel model çıkarımını tamamladıktan sonra sağlanan nesneyi çalıştırmasını pipeline'a söyler.  
* Konfigürasyon sözlüğü, işlemci kodunu değiştirmeden davranışı (dil, özel sözlükler vb.) özelleştirmenizi sağlar.

## AI pipeline'ınıza post işlem ekleme

Pipeline'ınız henüz bir `set_post_processor` yöntemi sunmuyorsa, sınıf altına miras alarak veya bir sarmalayıcı fonksiyon kullanarak genişletebilirsiniz. Aşağıda, herhangi bir çağrılabilir pipeline ile çalışan genel bir sarmalayıcı örneği bulunmaktadır.

```python
def add_post_processor(pipeline, processor, options=None):
    """
    Registers a post‑processor on a generic pipeline.
    """
    def wrapped(*args, **kwargs):
        # Run the original pipeline
        result = pipeline(*args, **kwargs)
        # Apply the post‑processor if it implements `process`
        if hasattr(processor, "process"):
            return processor.process(result, **(options or {}))
        # Fallback: assume processor is a callable
        return processor(result, **(options or {}))

    return wrapped

# Example usage with a Hugging Face pipeline
from transformers import pipeline as hf_pipeline

# Create the base pipeline (e.g., text generation)
base = hf_pipeline("text-generation", model="gpt2")

# Wrap it with the spell‑checking post processor
ai = add_post_processor(base, spell_checker, {"lang": "en"})
```

### Sarmalayıcının yaptığı şey

1. **Orijinal çıkarımı çalıştırır** ve ham çıktıyı yakalar.  
2. **Sağlanan işlemci üzerindeki uygun giriş noktasını** (`process` metodu veya callable) tespit eder.  
3. **İşlemciyi** sonuç ve sağladığınız seçeneklerle çağırır.  

Bu desen, başlangıçta pipeline için tasarlanmamış **post işlemci** nesnelerini kullanmanıza olanak tanır; böylece yazım denetimi ya da başka özel mantıkları eklemek için tam esneklik elde edersiniz.

## Yazım denetimi için bir post işlemci kullanma

İşlemci bağlandıktan sonra pipeline'ı her zamanki gibi çağırabilirsiniz. Model metin ürettikten hemen sonra yazım denetimi adımı otomatik olarak çalışır.

```python
# Generate text that may contain spelling errors
raw_output = ai("Write a short paragraph about climate change.")

print("Raw output:", raw_output)
print("Corrected output:", ai.last_result)  # Assuming the wrapper stores the final result
```

**Beklenen çıktı (örnek):**

```
Raw output: ['Climte change is a global issue that affects all nations.']
Corrected output: ['Climate change is a global issue that affects all nations.']
```

Yanlış yazılmış *“Climte”* kelimesinin, yazım denetleyicisi çalıştıktan sonra *“Climate”* olarak düzeldiğine dikkat edin. Bu, **apply spell checking** adımının şeffaf bir şekilde çalıştığını gösterir.

### Kenar durumlarını ele alma

| Durum                                   | Önerilen yaklaşım                                                |
|----------------------------------------|--------------------------------------------------------------------|
| Girdi, alan‑spesifik terimler içeriyor | `options` parametresi aracılığıyla özel bir sözlük sağlayın.      |
| İşlemci bir istisna fırlatıyor          | Çağrıyı bir `try/except` bloğuna sarın ve ham sonuca geri dönün.   |
| Birden fazla post işlemci gerekiyor    | `add_post_processor` çağrılarını iç içe geçirerek zincirleyin veya birleşik bir işlemci oluşturun. |

## Post işlemci seçeneklerini dinamik olarak ayarlama

Çalışma zamanında dil veya sözlük ayarlarını değiştirmeniz gerekebilir. `set_post_processor` yöntemi yeni bir konfigürasyonla tekrar çağrılarak önceki ayarları üzerine yazabilir.

```python
# Switch to French spell checking
ai.set_post_processor(spell_checker, {"lang": "fr"})
```

Metodu ikinci kez çağırmak **post işlemciyi nasıl ayarlayacağınızı** eski konfigürasyonu değiştirir ve sonraki üretimlerin yeni dil modelini kullanmasını sağlar.

## Pro ipucu: yazım denetimi entegrasyonunuzu test etme

Otomatik testler, kod değişikliklerinden sonra yazım denetleyicisinin işlevsel kalmasını garanti eder.

```python
import unittest

class TestSpellCheckerIntegration(unittest.TestCase):
    def test_correction(self):
        result = ai("The qick brown fox.")
        self.assertIn("quick", result[0].lower())

if __name__ == "__main__":
    unittest.main()
```

Bu testi çalıştırmak, **add spell checker** adımının çıktıyı doğru şekilde değiştirdiğini doğrular.

## Özet

Bu kılavuz, bir AI pipeline'ına **yazım denetleyicisi ekleme**, **post işlem ekleme** ve **apply spell checking** için **post işlemci** nesnelerini **kullanma** yollarını gösterdi. **post işlemciyi nasıl ayarlayacağınızı** öğrenerek kenar durumlarını ele almayı ve birim testleriyle entegrasyonu doğrulamayı öğrendiniz.

Bundan sonra şunları yapabilirsiniz:

* Bu deseni, küfür filtresi veya duygu analizi gibi diğer post‑processing görevlerine genişletin.  
* `my_spellchecker` kütüphanesinin bağlam‑duyarlı öneriler gibi gelişmiş özelliklerini keşfedin.  
* Daha zengin çıktı pipeline'ları için birden fazla post işlemciyi birleştirin.

Farklı konfigürasyonlarla deney yapın ve bulgularınızı toplulukla paylaşın. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Improve OCR Accuracy with Spell Checking in Images](/ocr/english/net/ocr-optimization/result-correction-with-spell-checking/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}