---
category: general
date: 2026-05-03
description: PNG görüntü dosyalarını nasıl yükleyeceğinizi, görüntüden metin tanımayı
  ve toplu OCR işleme için ücretsiz AI kaynaklarını gösteren Python OCR öğreticisi.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: tr
og_description: Python OCR öğreticisi, PNG görüntülerini yükleme, görüntüden metin
  tanıma ve toplu OCR işleme için ücretsiz AI kaynaklarını yönetme konusunda size
  rehberlik eder.
og_title: Python OCR Öğreticisi – Ücretsiz AI Kaynaklarıyla Hızlı Toplu OCR
tags:
- OCR
- Python
- AI
title: Python OCR Eğitimi – Toplu OCR İşlemi Kolaylaştırıldı
url: /tr/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Eğitimi – Toplu OCR İşleme Kolaylaştırıldı

Hiç **python ocr tutorial** gibi, saçınızı yolmak zorunda kalmadan onlarca PNG dosyasında OCR çalıştırmanıza izin veren bir şey aradınız mı? Yalnız değilsiniz. Birçok gerçek‑dünyada projede **load png image** dosyalarını yüklemeniz, bir motorun içine vermeniz ve işiniz bittiğinde AI kaynaklarını temizlemeniz gerekir.  

Bu rehberde, **recognize text from image** dosyalarından tam olarak nasıl metin tanınacağını, toplu olarak işleneceğini ve temel AI belleğinin nasıl serbest bırakılacağını gösteren eksiksiz, çalıştırmaya hazır bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz, ekstra süslemeler olmadan sadece temel gereksinimleri içeren bağımsız bir betiğe sahip olacaksınız.

## Gereksinimler

- Python 3.10 ve üzeri (burada kullanılan sözdizimi f‑string'ler ve tip ipuçlarına dayanır)  
- Bir OCR kütüphanesi, `engine.recognize` metodunu sunmalı – demo amaçlı hayali bir `aocr` paketini varsayacağız, ancak Tesseract, EasyOCR vb. ile değiştirebilirsiniz.  
- `ai` yardımcı modülü, kod snippet'inde gösterildiği gibi (model başlatma ve kaynak temizleme işlemlerini yönetir).  
- İşlemek istediğiniz PNG dosyalarıyla dolu bir klasör  

`aocr` veya `ai` yüklü değilse, stub'larla taklit edebilirsiniz – sonuna yakın “Optional Stubs” bölümüne bakın.

## Adım 1: AI Motorunu Başlatma (AI Kaynaklarını Serbest Bırakma)

Herhangi bir resmi OCR işlem hattına vermeden önce, temel modelin hazır olması gerekir. Sadece bir kez başlatmak bellek tasarrufu sağlar ve toplu işler için hızı artırır.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Neden önemli:**  
`ai.initialize`'ı her resim için tekrarlamalı olarak çağırmak GPU belleğini defalarca ayırır ve sonunda betiğin çökmesine neden olur. `ai.is_initialized()` kontrolüyle tek bir tahsis garantilenir – bu “AI kaynaklarını serbest bırakma” ilkesidir.

## Adım 2: Toplu OCR İşleme için PNG Resim Dosyalarını Yükleme

Şimdi OCR ile işlemek istediğimiz tüm PNG dosyalarını topluyoruz. `pathlib` kullanmak kodun işletim sistemi bağımsız olmasını sağlar.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Köşe durumu:**  
Klasör PNG olmayan dosyalar (ör. JPEG) içeriyorsa bunlar göz ardı edilir, `engine.recognize`'ın desteklenmeyen bir formatta takılmasını önler.

## Adım 3: Her Resimde OCR Çalıştırma ve Son İşlem Uygulama

Motor hazır ve dosya listesi oluşturulduğunda, resimler üzerinde döngü kurabilir, ham metni çıkarabilir ve yaygın OCR artefaktlarını (ör. gereksiz satır sonları) temizleyen bir post‑processöre verebiliriz.

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Neden yüklemeyi tanımadan ayırıyoruz:**  
`aocr.Image.load` tembel kod çözme yapabilir, bu da büyük toplular için daha hızlıdır. Yükleme adımını açık tutmak, daha sonra JPEG veya TIFF dosyalarını işlemek isterseniz farklı bir görüntü kütüphanesine geçişi de kolaylaştırır.

## Adım 4: Temizleme – Toplu İşlem Sonrası AI Kaynaklarını Serbest Bırakma

Toplu işlem tamamlandığında, özellikle GPU destekli makinelerde bellek sızıntılarını önlemek için modeli serbest bırakmalıyız.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Hepsini Bir Araya Getirme – Tam Script

Aşağıda, dört adımı tutarlı bir iş akışına birleştiren tek bir dosya bulunmaktadır. `batch_ocr.py` olarak kaydedin ve komut satırından çalıştırın.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Beklenen Çıktı

Üç PNG içeren bir klasörde scripti çalıştırmak şu çıktıyı verebilir:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

`ocr_results.txt` dosyası, her resim için net bir ayırıcı ve ardından temizlenmiş OCR metnini içerecek.

## aocr ve ai için Opsiyonel Stub'lar (Gerçek Paketleriniz Yoksa)

Ağır OCR kütüphanelerini dahil etmeden akışı test etmek istiyorsanız, minimal taklit modüller oluşturabilirsiniz:

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Bu klasörleri `batch_ocr.py`'nin yanına yerleştirin, script çalışacak ve taklit sonuçları yazdıracak.

## Profesyonel İpuçları & Yaygın Tuzaklar

- **Bellek dalgalanmaları:** Binlerce yüksek çözünürlüklü PNG işliyorsanız, OCR'den önce yeniden boyutlandırmayı düşünün. `aocr.Image.load` genellikle bir `max_size` argümanını kabul eder.  
- **Unicode yönetimi:** Çıktı dosyasını her zaman `encoding="utf-8"` ile açın; OCR motorları ASCII olmayan karakterler üretebilir.  
- **Paralellik:** CPU‑ağır OCR için `ocr_batch`'i bir `concurrent.futures.ThreadPoolExecutor` içinde sarabilirsiniz. Tek bir `ai` örneği tutmayı unutmayın – her biri `ai.initialize` çağıran çok sayıda iş parçacığı oluşturmak “AI kaynaklarını serbest bırakma” hedefini bozar.  
- **Hata dayanıklılığı:** Tek bir bozuk PNG'nin tüm toplu işlemi durdurmaması için her‑resim döngüsünü bir `try/except` bloğuna sarın.

## Sonuç

Artık **python ocr tutorial**'ı, **load png image** dosyalarını nasıl yükleyeceğinizi, **batch OCR processing**'i nasıl gerçekleştireceğinizi ve **free AI resources**'ı sorumlu bir şekilde nasıl yöneteceğinizi gösteren bir örneğe sahipsiniz. Tam, çalıştırılabilir örnek, **recognize text from image** nesnelerinden metin tanımanın ve sonrasında temizlemenin tam olarak nasıl yapılacağını gösterir, böylece eksik parçaları aramadan kendi projelerinize kopyala‑yapıştır yapabilirsiniz.

Bir sonraki adıma hazır mısınız? Stub'lanmış `aocr` ve `ai` modüllerini gerçek kütüphanelerle, örneğin `pytesseract` ve `torchvision` ile değiştirin. Scripti JSON çıktı vermek, sonuçları bir veritabanına itmek ya da bir bulut depolama kovasına entegre etmek için de genişletebilirsiniz. Gökyüzü sınır—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}