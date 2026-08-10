---
category: general
date: 2026-06-22
description: Python'da Aspose OCR kullanarak png dosyalarından metin tanıyın. Toplu
  OCR görüntülerini öğrenin ve hızlı işleme için GPU katmanlarını ayarlayın.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: tr
og_description: Python'da Aspose OCR ile png dosyalarından metin tanıyın. Bu kılavuz,
  görüntüleri toplu OCR yapmayı ve hız için GPU katmanlarını ayarlamayı gösterir.
og_title: png'den metin tanıma – Adım Adım Aspose OCR Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: png'den metin tanıma – Aspose OCR ve AI ile Tam Kılavuz
url: /tr/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png dosyalarından metin tanıma – Tam Özellikli Aspose OCR & AI Öğreticisi

png dosyalarından **metin tanıma** ihtiyacınız oldu mu ve kurulum detayları içinde kaybolduğunuzu hissettiniz mi? Tek başınıza değilsiniz. Makbuzları dijitalleştiriyor, formları tarıyor ya da ekran görüntülerini aranabilir metne dönüştürüyor olun, Python’da toplu OCR görüntüleri yönetmek saatler kazandırabilir.  

Bu rehberde, **png dosyalarından metin tanıma** yapmanın yanı sıra **GPU katmanlarını ayarlama** ile belirgin bir hız artışı elde etmenizi sağlayan hazır bir örneği adım adım inceleyeceğiz. Sonunda, bağımsız bir betiğiniz, her adımın net açıklaması ve kendi projelerinizde kopyalayıp yapıştırabileceğiniz birkaç pratik ipucu olacak.

## Bu Öğreticide Neler Ele Alınıyor

- Aspose OCR ve Aspose AI Python paketlerinin kurulumu  
- Hugging Face üzerinden otomatik indirme ile bir AI modelinin yapılandırılması  
- En yaygın OCR hatalarını düzelten küçük bir post‑processor oluşturma  
- Bir klasördeki tüm PNG dosyaları için **batch OCR images** döngüsü çalıştırma  
- **set GPU layers** seçeneğiyle grafik kartınızı kullanma  
- İşlem sonrası kaynakları güvenli bir şekilde temizleme  

Harici hizmetler yok, gizli sihir yok—sadece `.py` dosyasına yapıştırıp çalıştırabileceğiniz saf Python kodu.

![Diagram of recognize text from png workflow](workflow.png){alt="png'den metin tanıma iş akışı diyagramı"}

## Ön Koşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.8+ | Aspose AI’nin tekerlekleri yeni yorumlayıcıları hedefler |
| CUDA‑uyumlu bir GPU (isteğe bağlı) | **set GPU layers** ile hızlandırma istiyorsanız gerekir |
| İlk çalıştırmada internet erişimi | Model Hugging Face’den otomatik indirilecek |
| `pip` kurulu | Aspose paketlerini indirmek için |

Bu gereksinimlere zaten sahipseniz, harika—başlamaya hazırsınız. Yoksa, aşağıdaki kurulum adımları eksik parçaları size gösterecek.

---

## Adım 1: Aspose OCR ve Aspose AI Paketlerini Kurun

İlk olarak kütüphaneleri PyPI’dan alın. Aşağıdaki komut OCR motorunu ve AI yardımcı paketini tek seferde çeker.

```bash
pip install aspose-ocr aspose-ai
```

*İpucu:* Paketlerin global Python kurulumunuzdan izole kalması için sanal ortam (`python -m venv .venv`) kullanın.

---

## Adım 2: Aspose AI Örneğini Oluşturun ve Yapılandırın

AI bileşeni OCR motorunun “akıllı” modunu besler. `Qwen/Qwen2.5-3B-Instruct-GGUF` modeline işaret edeceğiz, eksikse otomatik indirme yapacak ve **set GPU layers** değerini 30 olarak ayarlayacağız (daha sonra ayarlayabilirsiniz).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Neden Önemli:**  
- `allow_auto_download` yaklaşık 2 GB’lık modeli manuel indirme adımını ortadan kaldırır.  
- `gpu_layers=30` temel dönüştürücünün ilk 30 katmanını GPU’da çalıştırarak, uyumlu bir GPU mevcutsa çıkarım süresini büyük ölçüde kısaltır.  
- `int8` kuantizasyonu, hafıza kullanımını düşük tutarken doğruluktan çok fazla ödün vermez.

---

## Adım 3: OCR Hatalarını Temizleyen Basit Bir Post‑Processor Tanımlayın

OCR mükemmel değildir—özellikle düşük çözünürlüklü PNG’lerde. Sıkça yanlış okunan karakterleri değiştirmek hızlı bir çözümdür. Aşağıdaki fonksiyon “0”ı “o” ve “1”i “l” ile değiştirir; bu kalıp taranan faturalarda sık görülür.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Bu fonksiyonu bir sonraki adımda AI örneğine ekleyeceğiz, böylece her tanıma sonucu otomatik olarak bu işlemden geçer.

---

## Adım 4: Post‑Processor ve OCR Motorunu Bağlayın

Şimdi her şeyi birleştiriyoruz: OCR motoru, AI modeli ve post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Arka planda ne oluyor?**  
`OcrEngine`, ağır işi yapılandırdığınız AI modeline devreder. Model ham metni döndürdükten sonra Aspose, `fix_common_errors` fonksiyonunu çağırarak çıktıyı temizler ve size sunar.

---

## Adım 5: Batch OCR Images – Bir Klasördeki Her PNG’yi İşleyin

İşte öğreticinin kalbi: bir dizini dolaşan, her `.png` dosyasını yükleyen, OCR çalıştıran ve temizlenmiş sonucu yazdıran döngü. Bu desen, **batch OCR images** işlemini verimli bir şekilde yapmanın kanonik yoludur.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Beklenen çıktı** (bir makbuz örneği):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Yüzlerce dosyanız varsa, bu döngü aynı AI örneğini yeniden kullanarak dosyaları sıralı bir biçimde işler, modelin tekrar tekrar yüklenmesinden kaynaklanan ek yükten kaçınır.

---

## Adım 6: Temizleme – Kaynakları Serbest Bırakın ve Motoru Yok Edin

İşiniz bittiğinde GPU belleği ve diğer yerel kaynakları serbest bırakmak iyi bir uygulamadır. Aspose bunun için açık metodlar sunar.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Bu adımı atlamak, bir sonraki çalıştırmada bellek yetersizliği hatalarına yol açabilecek GPU belleğinin serbest bırakılmamasına neden olur.

---

## Bonus: Farklı Donanımlar İçin GPU Katmanlarını Ayarlama

Önceden belirlediğiniz `gpu_layers` değeri birçok modern GPU için uygun bir denge sunar, ancak ayarlamanız gerekebilir:

| GPU Belleği (GB) | Önerilen `gpu_layers` |
|-----------------|--------------------------|
| 4 GB veya daha az | 10‑15 |
| 6‑8 GB | 20‑30 |
| 12 GB+ | 35‑45 (veya daha yüksek) |

GPU belleğinizi aşarsanız, motor kalan katmanlar için otomatik olarak CPU’ya geçer; bu yüzden çökmez—sadece daha yavaş çalışır. `nvidia‑smi` ile kullanımınızı izleyerek deney yapın.

---

## Yaygın Tuzaklar ve Kaçınma Yöntemleri

1. **Model indirme başarısız** – Ortamınızın `https://huggingface.co` adresine ulaşabildiğinden emin olun. Kurumsal bir proxy gerekiyorsa (`https_proxy` ortam değişkeni) yapılandırın.  
2. **GPU algılanmadı** – Bağımlılık olarak kurulan `torch` kütüphanesinin GPU’yu gördüğünü doğrulayın: `import torch; print(torch.cuda.is_available())`. `False` dönerse, CUDA‑uyumlu PyTorch tekerleğini kurun.  
3. **Yanlış resim yolu** – `Path.glob("*.png")` Linux’ta büyük/küçük harfe duyarlıdır. Güvenli olmak için `*.PNG` ya da `*.png` kullanın, ya da `pathlib.Path(...).rglob("*.[pP][nN][gG]")` ekleyin.  
4. **Post‑processor aşırı düzeltme yapıyor** – Basit değiştirme, gerçek “0” karakterlerini “o”ya çevirebilir. Temsilci bir örnek üzerinde test edin ve gerekirse mantığı ayarlayın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Şu şekilde çalıştırın:

```bash
python recognize_text_from_png_batch.py
```

Her PNG dosya adı ardından çıkarılan metin, daha önce gösterildiği gibi görüntülenecek.

---

## Sonuç

Bu rehberde **png dosyalarından metin tanıma** işlemini Aspose OCR ve Aspose AI ile Python’da nasıl yapacağınızı adım adım gösterdik. Adımları temiz bir betikte birleştirerek **batch OCR images** işlemini zahmetsizce gerçekleştirebilir ve `set gpu layers` sayesinde hız kazanabilirsiniz.


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan kaynaklardır. Her biri, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}