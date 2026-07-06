---
category: general
date: 2026-06-25
description: Python'da OCR nasıl yapılır öğrenin ve OCR için görüntüyü yüklemenin
  en iyi yolunu keşfedin, ardından Aspose AI sonrası işleme ile doğruluğu artırın.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: tr
og_description: Python'da OCR nasıl yapılır? OCR için görüntüyü yüklemek, temel tanıma
  çalıştırmak ve sonuçları Aspose AI sonrası işleme ile iyileştirmek için bu rehberi
  izleyin.
og_title: Python'da OCR Nasıl Yapılır – Tam Aspose OCR ve AI Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Python'da OCR Nasıl Yapılır – Tam Aspose OCR ve AI Rehberi
url: /tr/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Yapılır – Tam Aspose OCR & AI Kılavuzu

Python'da **OCR nasıl yapılır** diye hiç merak ettiniz mi, düşük seviyeli görüntü hileleriyle uğraşmadan? Yalnız değilsiniz. Bu öğreticide OCR için bir görüntüyü yüklemeyi, düz metin çıkarımını çalıştırmayı ve ardından çıktıyı Aspose'un AI post‑işlemcisiyle parlatmayı adım adım göstereceğiz. Sonunda, gürültülü taramaları temiz, aranabilir metne dönüştüren, ek hizmetlere ihtiyaç duymayan hazır bir betiğe sahip olacaksınız.

SDK'yı kurmaktan uzun süren uygulamalarda kaynakları serbest bırakmaya kadar her şeyi ele alacağız. **OCR için görüntü yükleme** işlemini denediniz ve karışık bir karışıma ulaştıysanız, bu kılavuz tam bir panzehir. Geleneksel OCR'yi bir dil modeliyle birleştirmenin, insan tarafından yazılmış gibi görünen sonuçlar verdiğini göreceksiniz.

## Önkoşullar

- Python 3.9 ve üzeri (kod, daha eski yorumlayıcıların sevmediği tip ipuçları kullanıyor)
- Aktif bir Aspose OCR lisansı veya ücretsiz deneme (community sürümü değerlendirme için çalışır)
- AI modelini hızlandırmak istiyorsanız en az 4 GB VRAM'li bir GPU (isteğe bağlı ama faydalı)
- Örnek bir görüntü, örn. `sample_invoice.png`, erişebileceğiniz bir konuma yerleştirilmiş

Eğer bunlardan biri size yabancı geliyorsa, panik yapmayın—SDK'yı kurmak tek satır bir komut, ve GPU ayarları daha sonra kapatılabilir.

## Adım 1: Aspose OCR ve Bağımlılıkları Kurun

Bir terminal açın ve şu komutu çalıştırın:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

İlk paket `aspose.ocr` sağlar, ikincisi AI post‑işlemci yardımcı programlarını ekler. İkisi de saf Python tekerlekleri olduğundan, kendiniz bir şey derlemenize gerek yok.

## Adım 2: OCR için Görüntüyü Yükleyin ve Motoru Başlatın

Şimdi Aspose'un `OcrEngine`'i kullanarak **OCR için görüntü yükleyeceğiz**. Bunu, her karakteri okuyan çok özenli bir memura bir kağıt vermek gibi düşünün.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Neden önemli:** `load_image` çağrısı, dosya sisteminiz ile OCR motoru arasındaki köprüdür. Yol yanlışsa, herhangi bir tanıma başlamadan önce `FileNotFoundError` alırsınız. Özellikle Windows ile macOS/Linux arasında dizin ayırıcılarını daima iki kez kontrol edin.

## Adım 3: Aspose AI Post‑İşlemcisini Ayarlayın

Aspose AI, Hugging Face'ten bir dil modeli indirebilir, yerel olarak önbelleğe alabilir ve GPU (veya CPU) üzerinde çıkarım yapabilir. Aşağıda, çoğu modern dizüstü bilgisayara sığan hafif bir 3 milyar parametreli modeli yapılandırıyoruz.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **İpucu:** Sadece CPU'lu bir makinede iseniz, `gpu_layers = 0` olarak ayarlayın. Model hâlâ çalışacak, sadece biraz daha yavaş. `int8` kuantizasyonu, modelin doğruluğunun çoğunu korurken bellek ayak izini çok küçük tutar.

## Adım 4: Özel Bir Post‑İşlemci Kaydedin

AI modelinin ne yapacağını söyleyen bir isteme ihtiyacı vardır. Burada ona bir OCR düzelticisi gibi davranmasını, yazım hatalarını düzeltmesini, kırık kelimeleri birleştirmesini ve artefaktları kaldırmasını istiyoruz.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Neden özel bir işlemci?** Varsayılan post‑işlemci, ihtiyacınız olmayan ekstra açıklamalar veya biçimlendirme ekleyebilir. Kendi fonksiyonumuzu sağlayarak çıktıyı sadece temizlenmiş metin olarak tutarız; bu, sonraki indeksleme veya veri tabanı depolaması için mükemmeldir.

## Adım 5: AI‑Destekli OCR İş Akışını Çalıştırın

Şimdi ham OCR çıktısını AI katmanına besliyoruz. Motor, `correction_processor`'ımızı çağıracak ve bu da dil modeliyle iletişim kuracak.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Dikkate değer bir iyileşme göreceksiniz: eksik karakterler geri getirilecek, “0” ile “O” gibi yaygın OCR hataları düzeltilecek ve satır sonları daha mantıklı hale gelecek.

## Adım 6: Temizleme – Kaynakları Serbest Bırakma

Bunu bir web hizmeti veya uzun süren bir daemon içinde çalıştırmayı planlıyorsanız, GPU belleğini serbest bırakmak çok önemlidir. `free_resources` çağrısını unutmak, birkaç yüz istekten sonra “bellek yetersizliği” çöküşlerine yol açabilir.

```python
ocr_ai.free_resources()
```

Hepsi bu—tam OCR iş akışınız artık üretime hazır.

## Tam Betik Özeti

Aşağıda tam, çalıştırılabilir örnek yer alıyor. `ocr_with_ai.py` adlı bir dosyaya kopyalayıp yapıştırın, görüntü yolunu ayarlayın ve `python ocr_with_ai.py` komutunu çalıştırın.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Beklenen Çıktı

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

“Inv0ice” kelimesinin “Invoice” haline geldiğine ve tutardan sonra çıkan yalnız “O” harfinin kaybolduğuna dikkat edin. Bu, AI'nın sihrini yapmasıdır.

## Yaygın Sorular & Kenar Durumlar

### GPU'm yoksa ne olur?

`model_config.gpu_layers = 0` olarak ayarlayın ve isteğe bağlı olarak `model_config.context_size` değerini 2048'e yükselterek CPU performansını artırın. Model daha yavaş çalışacak, ancak yine aynı kalite düzeltmeyi alacaksınız.

### Görüntüm döndürülmüş—`load_image` bunu halleder mi?

Aspose OCR otomatik olarak yönelim tespit eder, ancak aşırı eğik taramalar için Pillow kullanarak önceden döndürmek isteyebilirsiniz:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Bir klasördeki birden fazla dosyayı nasıl işlerim?

Tüm iş akışını bir `for` döngüsü içinde sarın ve her `enhanced_text`'i bir listeye kaydedin ya da doğrudan bir CSV'ye yazın. Döngüden sonra `ocr_ai.free_resources()` **bir kez** çağırmayı unutmayın; her dosyadan sonra çağırmak, modeli tekrar tekrar başlatmak gereksiz tüketim olur.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Dil modelini değiştirebilir miyim?

Kesinlikle. `model_config.hugging_face_repo_id` değerini Hugging Face üzerindeki herhangi bir GGUF‑uyumlu modelle değiştirin (örnek: `Meta/Llama-3.2-1B-Instruct-GGUF`). Kuantizasyon ayarını donanımınızla tutarlı tutun.

## Profesyonel İpuçları & Tuzaklar

- **Pro ipucu:** Belirleyici düzeltmeler için `temperature=0.0` ayarlayın. Daha yüksek sıcaklıklar yaratıcı ama hatalı değişiklikler getirebilir.
- **Dikkat edin:** Aşırı uzun belgeler (> 5000 karakter). Örnekte modelin bağlam penceresi 1024 token ile sınırlıdır; AI'ye göndermeden önce metni paragraflara bölün.
- **Güvenlik notu:** Bunu düzenlenmiş bir ortamda çalıştırıyorsanız, model indirme URL'sinin beyaz listede olduğundan emin olun. `allow_auto_download` bayrağı ...

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose OCR ile Görüntüden Metin Çıkarma – Adım Adım Kılavuz](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [AspOCR Nasıl Kullanılır: .NET için Görüntü OCR Filtrelerini Ön İşleme](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Aspose.OCR Kullanarak Dil Seçimiyle Görüntü Metni Çıkarma C#](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}