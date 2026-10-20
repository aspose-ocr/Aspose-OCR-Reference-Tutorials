---
category: general
date: 2026-08-12
description: AsposeAI kullanarak Python'da AI'yı hızlı bir şekilde başlatma, otomatik
  indirmeyi etkinleştirme, model yolunu ayarlama ve GPU katmanlarını yapılandırma.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to initialize ai
- enable automatic download
- set model path
- auto download model
- set gpu layers
language: tr
lastmod: 2026-08-12
og_description: AsposeAI ile Python’da AI’yı nasıl başlatılır. Otomatik indirmeyi
  etkinleştirin, model yolunu ayarlayın ve optimal performans için GPU katmanlarını
  yapılandırın.
og_image_alt: Diagram showing how to initialize AI with configuration settings
og_title: Yapay Zekayı nasıl başlatılır – otomatik indirme, model yolu ve GPU katmanları
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to initialize AI quickly, enable automatic download, set model
    path, and configure GPU layers in Python using AsposeAI.
  headline: How to initialize AI with automatic download and GPU layers
  type: TechArticle
- description: How to initialize AI quickly, enable automatic download, set model
    path, and configure GPU layers in Python using AsposeAI.
  name: How to initialize AI with automatic download and GPU layers
  steps:
  - name: Why each key matters
    text: '* **Automatic download** removes the manual step of downloading large `.bin`
      files from Hugging Face, which can be error‑prone. * **Model path** lets you
      keep models on fast local storage, reducing latency when loading. * **GPU layers**
      allow you to balance performance and memory usage; you can expe'
  - name: 'Common edge case: network failures'
    text: 'If the network is unavailable, AsposeAI raises a `ConnectionError`. Wrap
      the initialization in a `try` block to provide a graceful fallback:'
  - name: Expected output
    text: 'When you run `python initialize_ai.py` for the first time, you should see
      something like:'
  type: HowTo
tags:
- AsposeAI
- Python
- AI configuration
- GPU acceleration
title: AI'yi otomatik indirme ve GPU katmanlarıyla nasıl başlatılır
url: /tr/python/general/how-to-initialize-ai-with-automatic-download-and-gpu-layers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# AI'yi otomatik indirme ve GPU katmanlarıyla başlatma

AI'yi başlatmak, büyük dil modellerini kendi donanımınızda çalıştırmak istediğinizde ilk adımdır. Otomatik indirmeyi etkinleştirmek, gerekli model dosyalarının manuel adım olmadan alınmasını sağlar ve geliştirme döngülerini hızlandırır. Bu öğreticide AsposeAI'yi nasıl yapılandıracağınızı, model yolunu nasıl ayarlayacağınızı, otomatik indirmeyi nasıl etkinleştireceğinizi ve daha hızlı çıkarım için GPU katmanlarını nasıl belirleyeceğinizi göstereceğiz.

Şunları öğreneceksiniz:

* Tam bir AI yapılandırma sözlüğü tanımlama.
* Bu yapılandırma ile AsposeAI örneğini başlatma.
* Otomatik model indirme ve GPU hızlandırma ayarlarını düzenleme.
* Eksik dizinler veya desteklenmeyen GPU katman sayısı gibi yaygın tuzakları ele alma.

Standart bir Python 3 ortamı ve AsposeAI paketi dışında dış araçlara ihtiyaç yoktur.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Python 3.8 veya daha yeni bir sürüm.
* Sanal ortamınızda `pip install asposeai` komutunu çalıştırılmış.
* GPU katmanları kullanacaksanız en az 4 GB VRAM'li bir NVIDIA GPU.
* Modelin saklanacağı dizine yazma izni.

Bu gereksinimler, kodun izin hataları veya donanım uyumsuzlukları olmadan çalışmasını garantiler.

## AsposeAI ile AI'yi nasıl başlatılır

İşlemin temelini, AsposeAI'nin tükettiği bir yapılandırma sözlüğü oluşturmak oluşturur. Sözlük, otomatik indirme, model konumu ve GPU katman sayısı için anahtarlar içerir.

```python
# Step 1: Define the AI configuration
ai_config = {
    "allow_auto_download": "true",                # enable automatic download
    "directory_model_path": r"C:\Models\gpt2",    # set model path on disk
    "hugging_face_repo_id": "openai/gpt2",        # identifier of the model repository
    "gpu_layers": 20                              # set GPU layers for acceleration
}
```

* `allow_auto_download` (string `"true"` veya `"false"`) AsposeAI'nin eksik dosyaları otomatik olarak indirip indirmeyeceğini belirler. Bu doğrudan **otomatik indirmeyi etkinleştir** gereksinimini karşılar.
* `directory_model_path` modelin saklanacağı klasöre işaret eder. Ortamınıza uygun yolu ayarlayın; bu **model yolunu ayarla** ihtiyacını karşılar.
* `gpu_layers` kaç transformer katmanının GPU'da çalıştırılacağını belirtir. Daha yüksek değerler daha iyi throughput sağlar ancak daha fazla VRAM tüketir; bu da **GPU katmanlarını ayarla** hedefini yerine getirir.

### Her anahtarın önemi

* **Otomatik indirme**, Hugging Face'ten büyük `.bin` dosyalarını manuel olarak indirme adımını ortadan kaldırır ve hataya açık bir süreci ortadan kaldırır.
* **Model yolu**, modelleri hızlı yerel depolamada tutmanıza olanak tanır, yükleme gecikmesini azaltır.
* **GPU katmanları**, performans ve bellek kullanımını dengelemenizi sağlar; bellek yetersizliği hataları alırsanız daha düşük sayılarla deneme yapabilirsiniz.

## Model için otomatik indirmeyi etkinleştirme

`allow_auto_download` değerini `"true"` olarak ayarlarsanız, AsposeAI modele ilk ihtiyaç duyulduğunda indirmeyi deneyecektir. İndirme arka planda gerçekleşir ve sağladığınız `directory_model_path` konumunu kullanır.

```python
# Step 2: Initialize the AsposeAI instance with the configuration
from asposeai import AsposeAI

ai = AsposeAI(**ai_config)
```

Yapıcı çalıştığında, AsposeAI `directory_model_path` içinde model dosyalarının mevcut olup olmadığını kontrol eder. Dosyalar eksikse, `hugging_face_repo_id` ile belirtilen Hugging Face deposuna bağlanır ve dosyaları dizine akış olarak indirir. Bu davranış, ekstra kod yazmadan **otomatik model indirme** özelliğini gerçekleştirir.

### Yaygın kenar durumu: ağ hataları

Ağ erişilemezse, AsposeAI bir `ConnectionError` fırlatır. Başlatmayı bir `try` bloğuna sararak nazik bir geri dönüş sağlayabilirsiniz:

```python
try:
    ai = AsposeAI(**ai_config)
except ConnectionError as e:
    print("Failed to download the model automatically:", e)
    # Optionally, instruct the user to download manually.
```

## Yapılandırmada model yolunu ayarlama

Model için doğru konumu seçmek, performans ve yeniden üretilebilirlik açısından önemlidir. Yaygın bir desen, modelleri sürümlü bir dizin altında saklamaktır:

```python
import os

model_root = r"C:\Models"
model_name = "gpt2"
model_path = os.path.join(model_root, model_name)

# Ensure the directory exists before passing it to the config
os.makedirs(model_path, exist_ok=True)

ai_config["directory_model_path"] = model_path
```

Yolu programatik olarak oluşturduğunuzda, mutlak dizin string'lerini sabitlemekten kaçınır ve betiği farklı geliştirme makineleri ve CI boru hatları arasında taşınabilir hâle getirirsiniz.

## Daha hızlı çıkarım için GPU katmanlarını yapılandırma

AsposeAI'de GPU hızlandırması, yapılandırılabilir sayıda transformer katmanını GPU'ya devrederek çalışır. `gpu_layers` anahtarı bir tamsayı alır; tipik değerler VRAM'e bağlı olarak 4 ile 24 arasında değişir.

```python
# Example: Use 12 GPU layers on a 8 GB GPU
ai_config["gpu_layers"] = 12
```

#### Doğru sayıyı nasıl seçilir

1. **VRAM'i kontrol edin** – Her katman yaklaşık 200 MB tüketir. Kullanılabilir VRAM'inizi 200 MB'e bölerek güvenli bir üst sınır elde edin.
2. **Hızlı bir benchmark çalıştırın** – Farklı katman sayılarıyla gecikmeyi ölçün ve en uygun noktayı seçin.
3. **CPU'ya geri dönün** – `gpu_layers` mevcut belleği aşarsa, AsposeAI otomatik olarak fazla katmanları CPU'ya taşır, ancak bu performansı düşürebilir.

## Tam çalıştırılabilir örnek

Tüm parçaları bir araya getirdiğinizde, `initialize_ai.py` adlı bir dosyaya kopyalayabileceğiniz bağımsız bir betik elde edersiniz.

```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

"""
Complete example that demonstrates:
* enabling automatic download,
* setting a custom model path,
* configuring GPU layers,
* handling common errors.
"""

import os
from asposeai import AsposeAI

# ----------------------------------------------------------------------
# Step 1: Build the configuration dictionary
# ----------------------------------------------------------------------
model_root = r"C:\Models"
model_name = "gpt2"
model_path = os.path.join(model_root, model_name)

# Ensure the directory exists
os.makedirs(model_path, exist_ok=True)

ai_config = {
    "allow_auto_download": "true",           # enable automatic download
    "directory_model_path": model_path,      # set model path
    "hugging_face_repo_id": "openai/gpt2",   # model repository
    "gpu_layers": 12                         # set GPU layers
}

# ----------------------------------------------------------------------
# Step 2: Initialize AsposeAI with robust error handling
# ----------------------------------------------------------------------
try:
    ai = AsposeAI(**ai_config)
    print("AI instance initialized successfully.")
except ConnectionError as conn_err:
    print("Network error during auto download:", conn_err)
    raise
except RuntimeError as run_err:
    print("Runtime issue (e.g., insufficient VRAM):", run_err)
    raise

# ----------------------------------------------------------------------
# Step 3: Verify that the model is ready
# ----------------------------------------------------------------------
if ai.is_ready():
    print("Model is ready for inference.")
else:
    print("Model initialization failed.")
```

### Beklenen çıktı

`python initialize_ai.py` komutunu ilk kez çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
AI instance initialized successfully.
Downloading model files...
[==========] 124.5 MB / 124.5 MB
Model is ready for inference.
```

Sonraki çalıştırmalarda, dosyalar zaten `C:\Models\gpt2` içinde bulunduğu için indirme atlanır.

## Pro ipuçları ve sorun giderme

* **Pro ipucu:** `ai_config`'i bir JSON dosyasında saklayıp `json.load` ile yükleyin. Bu, kodu yapılandırmadan ayırır ve ayarları betiği düzenlemeden değiştirmenizi kolaylaştırır.
* **Bellek uyarısı:** `OutOfMemoryError` alırsanız, `gpu_layers` değerini azaltın veya modeli daha fazla VRAM'e sahip bir makineye taşıyın.
* **İzin hatası:** Betiği çalıştıran kullanıcının `directory_model_path` üzerinde yazma izni olduğundan emin olun. Linux'ta hedef klasöre `chmod 775` vermeniz gerekebilir.
* **Otomatik indirmeyi devre dışı bırakma:** `"allow_auto_download": "false"` olarak ayarlayın ve model dosyalarını yolu kendiniz yerleştirin. Bu, hava aralıklı (air‑gapped) ortamlarda kullanışlıdır.

## Sonraki adımlar

Artık **AI'yi nasıl başlatacağınızı** bildiğinize göre aşağıdakileri keşfedebilirsiniz:

* `ai.generate(prompt="Hello, world!")` ile çıkarım çalıştırma.
* `EleutherAI/gpt-neo-2.7B` gibi daha büyük bir modele geçiş (daha fazla GPU katmanı gerektirir).
* AI örneğini gerçek zamanlı uygulamalar için bir Flask veya FastAPI servisine entegre etme.

Bu konular, burada ele alınan yapılandırma kavramları üzerine inşa edilir ve **otomatik indirmeyi etkinleştir**, **model yolunu ayarla**, **GPU katmanlarını ayarla** temellerini pekiştirir.

---


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Python ile Makine Öğrenimi Modelleri Listesi – Hızlı Kılavuz](/ocr/indonesian/python/general/list-machine-learning-models-with-python-quick-guide/)
- [Görüntüyü Düzleştirme – GPU Hızlandırmalı OCR Kılavuzu](/ocr/english/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/)
- [.NET'te OCR Doğruluğunu Artırmak İçin İş Parçacığı Sayısını Ayarlama](/ocr/english/net/ocr-settings/set-threads-count/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}