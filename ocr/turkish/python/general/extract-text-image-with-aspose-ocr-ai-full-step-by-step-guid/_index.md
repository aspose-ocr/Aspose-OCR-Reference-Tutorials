---
category: general
date: 2026-06-25
description: Aspose OCR ve AI kullanarak metin görüntüsü çıkarın. Görüntü OCR'sini
  yüklemeyi, OCR doğruluğunu artırmayı, OCR hatalarını düzeltmeyi ve AI kaynaklarını
  verimli bir şekilde serbest bırakmayı öğrenin.
draft: false
keywords:
- extract text image
- free ai resources
- improve ocr accuracy
- load image ocr
- correct OCR errors
language: tr
og_description: Aspose OCR ve AI kullanarak metin görüntüsünü çıkarın. Bu öğreticide,
  görüntü OCR'si nasıl yüklenir, OCR doğruluğu nasıl artırılır, OCR hataları nasıl
  düzeltilir ve AI kaynakları nasıl ücretsiz hale getirilir gösterilmektedir.
og_title: Aspose OCR ve AI ile Görüntüden Metin Çıkarma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  headline: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  type: TechArticle
- description: Extract text image using Aspose OCR and AI. Learn to load image OCR,
    improve OCR accuracy, correct OCR errors, and free AI resources efficiently.
  name: Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide
  steps:
  - name: Import Aspose OCR and AI Modules
    text: 'We start by pulling in the two namespaces we’ll need: the core OCR engine
      and the AI helper that hosts the LLM.'
  - name: Create and Configure the OCR Engine (Enable GPU)
    text: Turning on GPU accelerates the pixel‑analysis phase, which can shave seconds
      off large batches.
  - name: Load the Image That Contains the Text to Be Recognized
    text: This is where we **load image OCR**. The path can be absolute or relative;
      just make sure the file exists.
  - name: Perform OCR and Obtain the Raw Extracted Text
    text: Now we actually **extract text image** content. The `recognize()` call returns
      a raw string, often riddled with line breaks and mis‑read characters.
  - name: Set Up the AI Post‑Processor (Auto‑Download Qwen2.5‑3B Model)
    text: We instantiate `AsposeAI`, configure it to pull the Qwen model from Hugging
      Face, and allocate GPU layers for inference.
  - name: Define a Simple Correction Function
    text: The function receives the raw OCR string, builds a prompt, and asks the
      model to proof‑read it. Temperature `0.0` forces deterministic output, which
      is ideal for correction tasks.
  - name: Attach the Correction Function and Clean the Raw OCR Result
    text: We bind `fix` as a post‑processor, then let the AI run over the `raw_text`.
      The result lands in `cleaned_text`.
  - name: Display the Corrected Text
    text: A quick `print` lets you verify that the pipeline succeeded.
  - name: Release AI Resources When Done
    text: Finally, we **free AI resources**. This call unloads the model from GPU
      memory, preventing leaks in long‑running services.
  type: HowTo
tags:
- OCR
- AI
- Aspose
title: Aspose OCR ve AI ile Metin Görüntüsü Çıkarma – Tam Adım Adım Kılavuz
url: /tr/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR & AI ile Metin Görüntüsü Çıkarma – Tam Adım‑Adım Kılavuz

Hiç **metin görüntüsü** içeriğini bulut hizmetlerine çok para harcamadan çıkarmayı düşündünüz mü? Tek başınıza değilsiniz. Birçok geliştirici, ham OCR çıktısının özellikle gürültülü taramalarda karışık bir karmaşa gibi göründüğünde bir duvara çarpar.  

Bu kılavuzda, **görüntü OCR** yükleme, **OCR doğruluğunu artırma**, otomatik **OCR hatalarını düzeltme** ve sonunda **AI kaynaklarını serbest bırakma** adımlarını gösteren, çalıştırmaya hazır tam bir örnek üzerinden ilerleyeceğiz.

Sonunda, veritabanına, arama indeksine ya da herhangi bir sonraki NLP boru hattına doğrudan besleyebileceğiniz temiz bir dize elde edeceksiniz. Dış dökümanlara gizli bağlantılar yok — ihtiyacınız olan her şey burada.

## Ne İnşa Edeceksiniz

- Bir görüntü dosyasını yükleyip Aspose OCR ile ham metin elde edin.  
- OCR boru hattına bir cihaz‑içi LLM (Qwen2.5‑3B modeli) ekleyin.  
- Küçük bir istemle OCR çıktısını kanıt‑okuma ve düzeltme yapın.  
- Tek bir çağrı ile modeli ve GPU belleğini serbest bırakın.  

Sonunda, faturalar, makbuzlar, taranmış sözleşmeler veya okunabilir karakter içeren herhangi bir bitmap için yeniden kullanabileceğiniz sağlam bir deseniniz olacak.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.9+ | Modern sözdizimi ve tip ipuçları. |
| `aspose-ocr` paketi | `OcrEngine` sınıfını sağlar. |
| CUDA destekli GPU (isteğe bağlı) | `ocr_engine.use_gpu = True` ile daha hızlı tanıma. |
| İnternet bağlantısı (ilk çalıştırmada) | Qwen modelinin otomatik indirilmesini sağlar. |
| Fonksiyonlarla temel aşinalık | Düzeltme geri‑çağrısını eklemek için gerekli. |

Kütüphaneleri şu şekilde kurun:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

> **Pro ipucu:** Sadece CPU‑only bir makinede çalışıyorsanız `use_gpu` satırını atlayın; kod sorunsuz bir şekilde geri dönerek çalışır.

---

## Aspose OCR ve AI ile Metin Görüntüsü Çıkarma

Aşağıda, dokuz mantıksal adıma bölünmüş tam betik yer alıyor. Her adım kısa bir açıklama ile başlar, ardından kopyalayıp‑yapıştırabileceğiniz tam kod bulunur.

### Adım 1: Aspose OCR ve AI Modüllerini İçe Aktarın

İhtiyacımız olan iki ad alanını çekerek başlıyoruz: temel OCR motoru ve LLM'yi barındıran AI yardımcı sınıfı.

```python
# Step 1: Import Aspose OCR and AI modules
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai
```

> **Neden?** İçe aktarmaları bir arada tutmak, betiği denetlemeyi kolaylaştırır ve ileride gizli bağımlılıkların ortaya çıkmasını önler.

### Adım 2: OCR Motorunu Oluşturun ve Yapılandırın (GPU’yu Etkinleştirin)

GPU'yu açmak, piksel‑analiz aşamasını hızlandırır ve büyük partilerde saniyeler kazandırabilir.

```python
# Step 2: Create and configure the OCR engine (enable GPU for faster processing)
ocr_engine = aocr.OcrEngine()
ocr_engine.use_gpu = True   # Set to False if you lack a compatible GPU
```

> **Not:** `use_gpu` bayrağı güvenle değiştirilebilir; motor otomatik olarak CUDA kullanılabilirliğini algılar.

### Adım 3: Tanınacak Metni İçeren Görüntüyü Yükleyin

Burada **görüntü OCR** yüklemesini yapıyoruz. Yol mutlak ya da göreli olabilir; dosyanın var olduğundan emin olun.

```python
# Step 3: Load the image that contains the text to be recognized
ocr_engine.load_image("YOUR_DIRECTORY/input.png")
```

> **Yaygın tuzak:** Yanlış bir yol `FileNotFoundError` hatası verir. Özellikle büyük/küçük harf duyarlı dosya sistemlerinde yazımını iki kez kontrol edin.

### Adım 4: OCR’i Gerçekleştirip Ham Çıkarılan Metni Alın

Şimdi gerçekten **metin görüntüsü** içeriğini **çıkarıyoruz**. `recognize()` çağrısı, genellikle satır sonları ve hatalı karakterlerle dolu ham bir dize döndürür.

```python
# Step 4: Perform OCR and obtain the raw extracted text
raw_text = ocr_engine.recognize()
```

Bu noktada `raw_text`’i yazdırırsanız şöyle bir şey görebilirsiniz:

```
Th1s is a s4mple test.
```

“i” yerine “1” ve “e” yerine “4” gördünüz mü? İşte AI post‑processörünün devreye girdiği yer.

### Adım 5: AI Post‑Processörünü Kurun (Qwen2.5‑3B Modelini Otomatik İndir)

`AsposeAI` sınıfını örnekleyip, modeli Hugging Face üzerinden çekmesini ve çıkarım için GPU katmanlarını ayırmasını sağlıyoruz.

```python
# Step 5: Set up the AI post‑processor (auto‑download Qwen2.5‑3B model)
ai_processor = aocr_ai.AsposeAI()
model_cfg = aocr_ai.AsposeAIModelConfig()
model_cfg.allow_auto_download = "true"
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_cfg.gpu_layers = 20               # Adjust based on your GPU VRAM
ai_processor.initialize(model_cfg)
```

> **Neden bu model?** Qwen2.5‑3B‑Instruct, orta‑seviye bir GPU’da çalışabilecek kadar küçük, ancak **OCR doğruluğunu artırma** için yeterince güçlü bir modeldir; böylece bellek tüketimi şişmez.

### Adım 6: Basit Bir Düzeltme Fonksiyonu Tanımlayın

Fonksiyon ham OCR dizesini alır, bir istem oluşturur ve modeli kanıt‑okuma yapması için sorar. Sıcaklık `0.0` deterministik çıktı üretir; bu da düzeltme görevleri için idealdir.

```python
# Step 6: Define a simple correction function that asks the model to proof‑read the OCR output
def fix(text, _):
    prompt = f"Proof‑read and correct the OCR text:\n\n{text}"
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=512)
```

> **Nasıl çalışır:** LLM tam metni görür ve temizlenmiş bir versiyon döndürür; temelde satır‑sonu anormalliklerini ve yazım hatalarını düzelten akıllı bir yazım denetleyicisi gibi davranır.

### Adım 7: Düzeltme Fonksiyonunu Bağlayın ve Ham OCR Sonucunu Temizleyin

`fix` fonksiyonunu bir post‑processör olarak bağlarız, ardından AI’yı `raw_text` üzerinde çalıştırırız. Sonuç `cleaned_text` değişkenine yerleşir.

```python
# Step 7: Attach the correction function as a post‑processor and clean the raw OCR result
ai_processor.set_post_processor(fix, None)
cleaned_text = ai_processor.run_postprocessor(raw_text)
```

Bu aşamada `cleaned_text` şöyle görünmelidir:

```
This is a simple test.
```

### Adım 8: Düzeltlenmiş Metni Görüntüleyin

Hızlı bir `print` ile boru hattının başarılı olup olmadığını doğrulayabilirsiniz.

```python
# Step 8: Display the corrected text
print("Cleaned text:\n", cleaned_text)
```

Konsol çıktısı şöyle olacaktır:

```
Cleaned text:
 This is a simple test.
```

### Adım 9: İş Bittiğinde AI Kaynaklarını Serbest Bırakın

Son olarak **AI kaynaklarını serbest bırakıyoruz**. Bu çağrı modeli GPU belleğinden kaldırır ve uzun‑çalışan servislerde sızıntı oluşmasını önler.

```python
# Step 9: Release AI resources when done
ai_processor.free_resources()
```

> **Neden önemli?** Kaynakları serbest bırakmayı unutmak, özellikle her çağrının kendini temizlemesi gereken serverless ortamlarında bellek taşmalarına yol açabilir.

---

## Görüntü OCR’yi Verimli Yüklemek

Yüzlerce dosyayı işlemek zorundaysanız, yükleme ve tanıma adımlarını bir döngü içinde sarın:

```python
def ocr_one(path):
    ocr_engine.load_image(path)
    return ocr_engine.recognize()
```

Aynı `ocr_engine` örneğini yeniden kullanmayı unutmayın; her görüntü için yeni bir tane oluşturmak gereksiz yük oluşturur ve **görüntü OCR** optimizasyonunun amacını bozar.

---

## OCR Doğruluğunu Artırma Teknikleri

1. **Görüntüyü ön‑işleyin** – Gri tonlamaya çevirin, kontrastı artırın ve eğikliği düzeltin, ardından motora verin.  
2. **GPU’yu etkinleştirin** – Adım 2’de gösterildiği gibi, GPU yolu genellikle daha yüksek güven skorları üretir.  
3. **AI ile post‑process** – **OCR hatalarını düzelt** adımı en güçlü kaldıraçtır; kural‑tabanlı yazım denetleyicilerinin kaçırdığı dil‑spesifik tuhaflıkları halledebilir.  

Bu üç taktiği birleştirdiğinizde gerçek dünya taramalarında kelime‑hata‑orani %30‑40 azalır.

---

## AI Post‑Processor ile OCR Hatalarını Düzeltme

Daha önce tanımladığımız `fix` fonksiyonu kasıtlı olarak minimal tutulmuştur. İsterseniz ek talimatlarla zenginleştirebilirsiniz, örneğin:

```python
def fix_with_formatting(text, _):
    prompt = (
        "You are a proofreading assistant. Return ONLY the corrected text, "
        "preserving line breaks and punctuation. Do not add explanations.\n\n"
        f"{text}"
    )
    return ai_processor.run_inference(prompt, temperature=0.0, max_new_tokens=1024)
```

`ai_processor.set_post_processor(fix_with_formatting, None)` kullanmak, formatı koruyan daha temiz sonuçlar verir — **iyileştirme** için bir başka yol.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan yakın konuları kapsar. Her kaynak, adım‑adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Görüntüden Metin Çıkarma – Aspose.OCR ile OCR Optimizasyonu (.NET)](/ocr/english/net/ocr-optimization/)
- [C# ile Görüntü Metni Çıkarma – Dil Seçimiyle Aspose.OCR Kullanımı](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Görüntüyü Metne Dönüştür – URL’den Görüntü Üzerinde OCR Yapma](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}