---
category: general
date: 2026-04-26
description: OCR sonuçlarını nasıl son işleme tabi tutar ve koordinatlarla metin çıkarırsınız.
  Yapılandırılmış çıktı ve AI düzeltmesi kullanarak adım adım bir çözüm öğrenin.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: tr
og_description: OCR sonuçlarını nasıl son işleme tabi tutar ve koordinatlarıyla metni
  nasıl çıkarırsınız? Güvenilir bir iş akışı için bu kapsamlı öğreticiyi izleyin.
og_title: OCR'yi Nasıl Son İşleme Alırsınız – Tam Kılavuz
tags:
- OCR
- Python
- AI
- Text Extraction
title: OCR'yi Nasıl Son İşlemeye Alırsınız – Python'da Koordinatlarla Metin Çıkarma
url: /tr/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Sonrası Nasıl İşlenir – Python'da Koordinatlarla Metin Çıkarma

Ever needed to **OCR sonrası nasıl işlenir** results because the raw output was noisy or mis‑aligned? You’re not the only one. In many real‑world projects—invoice scanning, receipt digitization, or even augmenting AR experiences—the OCR engine gives you raw words, but you still have to clean them up and keep track of where each word lives on the page. That’s where a structured output mode combined with an AI‑driven post‑processor shines.

In this tutorial we’ll walk through a complete, runnable Python pipeline that **extracts text with coordinates** from an image, runs an AI‑based correction step, and prints each word together with its (x, y) position. No missing imports, no vague “see the docs” shortcuts—just a self‑contained solution you can drop into your project today.

> **Pro tip:** If you’re using a different OCR library, look for a “structured” or “layout” mode; the concepts stay the same.

---

## Önkoşullar

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | Modern sözdizimi ve tip ipuçları |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | Sınır kutusu verileri için gerekli |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | OCR sonrası doğruluğu artırır |
| An image file (`input.png`) in your working directory | Okuyacağımız kaynak |

If any of these sound unfamiliar, just install the placeholder packages with `pip install myocr ai‑postproc`. The code below also includes fallback stubs so you can test the flow without the real libraries.

---

## Adım 1: OCR Motoru için Yapılandırılmış Çıktı Modunu Etkinleştirin  

The first thing we do is tell the OCR engine to give us more than just plain text. Structured output returns each word together with its bounding box and confidence score, which is essential for **extract text with coordinates** later on.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Why this matters:* Without structured mode you’d only get a long string, and you’d lose the spatial information you need for overlaying text on images or feeding downstream layout analysis.

---

## Adım 2: Görüntüyü Tanıyın ve Kelimeleri, Kutuları ve Güven Skorlarını Yakalayın  

Now we feed the image into the engine. The result is an object that contains a list of word objects, each exposing `text`, `x`, `y`, `width`, `height`, and `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Edge case:* If the image is empty or unreadable, `structured_result.words` will be an empty list. It’s good practice to check for that and handle it gracefully.

---

## Adım 3: Pozisyonları Koruyarak AI‑Tabanlı Post‑İşleme Çalıştırın  

Even the best OCR engines make mistakes—think of “O” vs. “0” or missing diacritics. An AI model trained on domain‑specific text can correct those errors. Crucially, we keep the original coordinates so the spatial layout stays intact.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Why we preserve coordinates:* Many downstream tasks (e.g., PDF generation, AR labeling) rely on exact placement. The AI only touches the `text` field, leaving `x`, `y`, `width`, `height` untouched.

---

## Adım 4: Düzeltlenmiş Kelimeler Üzerinde Döngü Oluşturun ve Metinlerini Koordinatlarıyla Görüntüleyin  

Finally, we loop through the corrected words and print each word together with its top‑left corner `(x, y)`. This satisfies the **extract text with coordinates** goal.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Beklenen çıktı (örnek):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Each line shows the corrected word and its exact location on the original image.

---

## Tam Çalışan Örnek  

Below is a single script that ties everything together. You can copy‑paste it, adjust the import statements to match your actual libraries, and run it directly.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Betik Çalıştırma**

```bash
python ocr_postprocess_demo.py
```

If you have the real libraries installed, the script will process your `input.png`. Otherwise, the stub implementation lets you see the expected flow and output without any external dependencies.

---

## Sık Sorulan Sorular (SSS)

| Question | Answer |
|----------|--------|
| *Bu Tesseract ile çalışır mı?* | Tesseract kendi başına kutu dışı bir yapılandırılmış mod sunmaz, ancak `pytesseract.image_to_data` gibi sarmalayıcılar, aynı AI post‑processor'a besleyebileceğiniz sınır kutularını döndürür. |
| *Üst‑sol yerine alt‑sağ köşeye ihtiyacım olursa ne yapmalıyım?* | Her kelime nesnesi ayrıca `width` ve `height` sağlar. Karşı köşeyi elde etmek için `x2 = x + width` ve `y2 = y + height` hesaplayın. |
| *Birden fazla görüntüyü toplu işleyebilir miyim?* | Kesinlikle. Adımları `for image_path in Path("folder").glob("*.png"):` döngüsü içinde sarın ve dosya başına sonuçları toplayın. |
| *Düzeltme için bir AI modeli nasıl seçilir?* | Genel metin için, OCR hataları üzerinde ince ayar yapılmış küçük bir GPT‑2 işe yarar. Alan‑spesifik veriler (ör. tıbbi reçeteler) için, gürültülü‑temiz eşleşmiş veri üzerinde bir sıralı‑sıralı model eğitin. |
| *AI düzeltmesinden sonra güven skoru faydalı mı?* | Hala hata ayıklama için orijinal güven skorunu tutabilirsiniz, ancak model destekliyorsa AI kendi güven skorunu da üretebilir. |

## Kenar Durumları ve En İyi Uygulamalar  

1. **Boş veya bozuk görüntüler** – ilerlemeden önce her zaman `structured_result.words`'ün boş olmadığını doğrulayın.  
2. **Latin dışı yazı sistemleri** – OCR motorunuzun hedef dil için yapılandırıldığından emin olun; AI post‑processor aynı yazı sisteminde eğitilmiş olmalıdır.  
3. **Performans** – AI düzeltmesi maliyetli olabilir. Aynı görüntüyü yeniden kullanacaksanız sonuçları önbelleğe alın veya AI adımını eşzamansız çalıştırın.  
4. **Koordinat sistemi** – OCR kütüphaneleri farklı kökenler (üst‑sol vs. alt‑sol) kullanabilir. PDF'lerde veya kanvaslarda yerleştirirken buna göre ayarlayın.  

## Sonuç  

You now have a solid, end‑to‑end recipe for **how to post‑process OCR** and reliably **extract text with coordinates**. By enabling structured output, feeding the result through an AI correction layer, and preserving the original bounding boxes, you can turn noisy OCR scans into clean, spatially‑aware text ready for downstream tasks like PDF generation, data entry automation, or augmented‑reality overlays.

Ready for the next step? Try swapping the stub AI with an OpenAI `gpt‑4o‑mini` call, or integrate the pipeline into a FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}