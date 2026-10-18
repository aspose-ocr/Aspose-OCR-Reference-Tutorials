---
category: general
date: 2026-06-06
description: Python OCR öğreticisi, görüntü metnini tanıma, yüksek çözünürlüklü OCR
  gerçekleştirme ve GPU hızlandırmalı OCR kullanarak İspanyolca metin çıkarma yöntemlerini
  gösterir.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: tr
og_description: Görüntü metnini tanıma, yüksek çözünürlüklü OCR ve GPU hızlandırmalı
  İspanyolca metin çıkarma konularında size rehberlik eden Python OCR öğreticisi.
og_title: Python OCR Eğitimi – GPU Hızlandırmalı Metin Tanıma
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Python OCR Öğreticisi – GPU Hızlandırmasıyla Görüntü Metnini Tanıma
url: /tr/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Recognize Image Text with GPU Acceleration

Hiç **görüntü metnini** bir Python betiğinde saatlerce ayar yapmadan tanımayı düşündünüz mü? Tek başınıza değilsiniz. Bu **python ocr tutorial**da yüksek çözünürlüklü bir resimden İspanyolca metni çıkarmanın temiz, uçtan uca bir yolunu göstereceğiz ve sürece GPU hızlandırmasını ekleyerek işlemi ışık hızında çalıştıracağız.

Bunu, daha sonra üretim‑ağır bir pipeline’a genişletebileceğiniz hızlı bir kahve molası demosu gibi düşünün. Bu rehberin sonunda **yüksek çözünürlüklü OCR** yapan, CUDA‑destekli bir GPU kullanan ve ihtiyacınız olan tam İspanyolca karakterleri veren çalıştırılabilir bir programınız olacak.

## What You’ll Learn

- GPU hızlandırmasını destekleyen modern bir OCR kütüphanesinin nasıl kurulup içe aktarılacağını.  
- OCR motoru örneği oluşturup **görüntü metnini** İspanyolca olarak tanımasını nasıl ayarlayacağınızı.  
- Yüksek çözünürlüklü dosyalarda devasa hız artışı sağlayan **gpu accelerated OCR** nasıl etkinleştirileceğini.  
- Eksik CUDA sürücüleri gibi kenar durumlarını nasıl ele alıp CPU’ya geri dönüleceğini.  
- Gürültülü taramalardan **extract spanish text** alırken doğruluğu artırmak için ipuçları.

### Prerequisites

- Python 3.9+ (kod 3.10 ve üzeri sürümlerde de çalışır).  
- CUDA‑uyumlu bir GPU (isteğe bağlı ama şiddetle tavsiye edilir).  
- pip ve sanal ortamlarla temel aşinalık.  

Eğer bunlardan birine sahip değilseniz, öğretici yine çalışır—GPU adımını atlayın, kütüphane otomatik olarak CPU’ya geçer.

---

## Python OCR Tutorial: Install the Required Packages

İlk iş olarak sağlam bir OCR motoruna ihtiyacımız var. Bu öğreticide, uyumlu bir cihaz tespit edildiğinde yerleşik GPU desteği sunan açık kaynak **`easyocr`** paketini kullanacağız.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** Eğer zaten PyTorch yüklüyse, CUDA sürümünüzle eşleştiğinden emin olun (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). Uyumsuz sürümler “GPU not found” hatalarının yaygın bir kaynağıdır.

---

## Step 1: Create an OCR Engine Instance

Şimdi motoru başlatıyoruz. EasyOCR ana sınıfına `Reader` denir. Yapıcı, dil kodlarının bir listesini kabul eder; İspanyolca için `"es"` geçeceğiz.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Bu neden önemli:* Dili önceden belirterek motor yalnızca gerekli sinir ağı ağırlıklarını yükler, bu da belleği tasarruf ettirir ve çıkarım süresini hızlandırır—özellikle **high resolution OCR** ile çalışırken çok faydalıdır.

---

## Step 2: Prepare a High‑Resolution Image

Yüksek çözünürlüklü görüntüler modele daha fazla piksel sağlar ve genellikle daha iyi karakter tanıma anlamına gelir. `samples` adlı klasörde `high_res_spanish.png` adlı bir dosyanız olduğunu varsayalım.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

Eğer elinizde yüksek çözünürlüklü bir örnek yoksa, Unsplash’tan ücretsiz bir tane indirebilir ya da Pillow ile sentetik bir görüntü oluşturabilirsiniz. En iyi sonuçlar için DPI’nın 300’ün üzerinde olmasına dikkat edin.

---

## Step 3: Enable GPU Acceleration (Optional but Recommended)

EasyOCR, `gpu=True` ayarlandığında GPU’yu kullanmaya çalışır. Ancak çoklu GPU sistemlerinde cihazın gerçekten kullanıldığını doğrulamak iyi bir uygulamadır.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Bunu neden kontrol etmelisiniz?* Eğer betik sessizce CPU’ya geri dönerse, 5 saniyelik bir işlemin aniden 30 saniyeye çıkmasını sorgulayabilirsiniz. Bu küçük kontrol, davranışı şeffaf hâle getirir ve **gpu accelerated OCR** pipeline’ınızın öngörülebilir olmasını sağlar.

---

## Step 4: Perform High‑Resolution OCR and Recognize Image Text

Şimdi eğlenceli kısım—metni gerçekten okumak. EasyOCR’un `readtext` metodu, sınırlayıcı kutu, tanınan dize ve bir güven puanı içeren tuple listesi döndürür.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

Koordinatlar olmadan ham dizeye ihtiyacınız varsa `detail=0` ayarlayın. Çoğu **recognize image text** senaryosu için varsayılan (`detail=1`) daha sonra işleme koymak için yeterli bağlam sağlar.

---

## Step 5: Extract Spanish Text and Clean the Output

EasyOCR’dan İspanyolca istediğimiz için dönen dizeler zaten bu dilde. Yine de birleştirmek, boşlukları temizlemek ya da düşük güvenli tespitleri filtrelemek isteyebilirsiniz.

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**Güven skoru düşük olursa ne yapmalı?** Eşiği düşürebilirsiniz (gürültü riski artar) ya da görüntüyü ön‑işleme tabi tutabilirsiniz (kontrastı artırma, ikilileştirme veya eğikliği düzeltme). Bu püf noktaları, taranmış belgelerde **high resolution OCR** ile uğraşırken yaygındır.

---

## Step 6: Handling Edge Cases and Performance Tweaks

En iyi eğitilmiş modeller bile bazı senaryolarda zorlanır. Aşağıda betiğe yapıştırabileceğiniz birkaç hızlı çözüm var.

### 6.1 Fallback When No GPU Is Present

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Down‑sampling Very Large Images

Görüntünüz 4000 × 4000 px’den büyükse GPU belleği tükenebilir. DPI’yı koruyarak orantılı bir şekilde aşağı örnekleyin:

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

Bu kod parçacıkları, ister bir iş istasyonunda ister mütevazı bir dizüstü bilgisayarda çalışıyor olun, betiğinizi dayanıklı tutar.

---

## Full Working Example

Hepsini bir araya getirdiğimizde, hemen kopyalayıp çalıştırabileceğiniz tam script aşağıdadır:

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**Beklenen çıktı (örnek):**



## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}