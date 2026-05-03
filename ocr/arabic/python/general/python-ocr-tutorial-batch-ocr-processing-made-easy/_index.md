---
category: general
date: 2026-05-03
description: دورة بايثون لتقنية OCR تُظهر كيفية تحميل ملفات PNG، والتعرف على النص
  من الصورة، وموارد الذكاء الاصطناعي المجانية لمعالجة OCR على دفعات.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: ar
og_description: يُرشدك برنامج تعليمي OCR بلغة بايثون إلى تحميل صور PNG، والتعرف على
  النص من الصورة، والتعامل مع موارد الذكاء الاصطناعي المجانية لمعالجة OCR على دفعات.
og_title: دليل بايثون للتعرف الضوئي على الأحرف – التعرف الضوئي السريع على دفعات باستخدام
  موارد الذكاء الاصطناعي المجانية
tags:
- OCR
- Python
- AI
title: دورة بايثون للتعرف الضوئي على الأحرف – معالجة التعرف الضوئي على الأحرف الدفعيّة
  بسهولة
url: /ar/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR بايثون – معالجة OCR دفعة واحدة بسهولة

هل احتجت يوماً إلى **python ocr tutorial** يتيح لك فعلياً تشغيل OCR على العشرات من ملفات PNG دون أن تشعر بالإحباط؟ لست وحدك. في العديد من المشاريع الواقعية عليك **load png image** ملفات، وتغذيتها إلى محرك، ثم تنظيف موارد AI عندما تنتهي.  

في هذا الدليل سنستعرض مثالاً كاملاً وجاهزاً للتنفيذ يوضح بالضبط كيفية **recognize text from image** الملفات، ومعالجتها دفعة واحدة، وتحرير ذاكرة AI الأساسية. في النهاية ستحصل على سكريبت مستقل يمكنك إدراجه في أي مشروع—بدون إضافات غير ضرورية، فقط الأساسيات.

## ما ستحتاجه

- Python 3.10 أو أحدث (الصياغة المستخدمة هنا تعتمد على f‑strings وتلميحات الأنواع)  
- مكتبة OCR تُظهر طريقة `engine.recognize` – لأغراض العرض سنفترض حزمة خيالية `aocr`، لكن يمكنك استبدالها بـ Tesseract أو EasyOCR، إلخ.  
- وحدة المساعدة `ai` المعروضة في مقتطف الشيفرة (تتعامل مع تهيئة النموذج وتنظيف الموارد)  
- مجلد يحتوي على ملفات PNG تريد معالجتها  

إذا لم يكن لديك `aocr` أو `ai` مثبتين، يمكنك محاكاتهما باستخدام stubs – راجع قسم “Optional Stubs” قرب النهاية.

## الخطوة 1: تهيئة محرك AI (تحرير موارد AI)

قبل أن تغذي أي صورة إلى خط أنابيب OCR، يجب أن يكون النموذج الأساسي جاهزاً. التهيئة مرة واحدة فقط توفر الذاكرة وتسرّع وظائف الدفعات.

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

**لماذا هذا مهم:**  
استدعاء `ai.initialize` بشكل متكرر لكل صورة سيؤدي إلى تخصيص ذاكرة GPU مراراً وتكراراً، مما سيتسبب في تعطل السكريبت في النهاية. من خلال التحقق من `ai.is_initialized()` نضمن تخصيصاً واحداً فقط – وهذا هو مبدأ “تحرير موارد AI”.

## الخطوة 2: تحميل ملفات PNG لمعالجة OCR دفعة واحدة

الآن نجمع جميع ملفات PNG التي نريد تشغيلها عبر OCR. استخدام `pathlib` يحافظ على استقلالية الكود عن نظام التشغيل.

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

**حالة حافة:**  
إذا كان المجلد يحتوي على ملفات غير PNG (مثل JPEG) فسيتم تجاهلها، مما يمنع `engine.recognize` من التعطل بسبب تنسيق غير مدعوم.

## الخطوة 3: تشغيل OCR على كل صورة وتطبيق المعالجة اللاحقة

مع جاهزية المحرك وإعداد قائمة الملفات، يمكننا التكرار على الصور، استخراج النص الخام، وتسليمه إلى معالج لاحق يقوم بتنظيف الأخطاء الشائعة في OCR (مثل فواصل الأسطر العشوائية).

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

**لماذا نفصل التحميل عن التعرف:**  
قد يقوم `aocr.Image.load` بعملية فك ترميز كسولة، مما يكون أسرع للدفعات الكبيرة. إبقاء خطوة التحميل صريحة يجعل من السهل استبدال مكتبة الصور إذا احتجت لاحقاً للتعامل مع ملفات JPEG أو TIFF.

## الخطوة 4: التنظيف – تحرير موارد AI بعد الانتهاء من الدفعة

بعد انتهاء الدفعة، يجب تحرير النموذج لتجنب تسرب الذاكرة، خاصةً على الأجهزة التي تدعم GPU.

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

## تجميع كل شيء معاً – السكريبت الكامل

فيما يلي ملف واحد يجمع الخطوات الأربع في سير عمل متكامل. احفظه باسم `batch_ocr.py` وشغّله من سطر الأوامر.

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

### النتيجة المتوقعة

تشغيل السكريبت على مجلد يحتوي على ثلاث صور PNG قد يطبع:

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

ملف `ocr_results.txt` سيحتوي على فاصل واضح لكل صورة يليه النص المنظف من OCR.

## stubs اختيارية لـ aocr و ai (إذا لم تتوفر لديك حزم حقيقية)

إذا كنت ترغب فقط في اختبار التدفق دون استدعاء مكتبات OCR الضخمة، يمكنك إنشاء وحدات mock بسيطة:

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

ضع هذه المجلدات بجوار `batch_ocr.py` وسيعمل السكريبت، مطبعاً نتائج mock.

## نصائح احترافية ومشكلات شائعة

- **Memory spikes:** إذا كنت تعالج آلاف ملفات PNG عالية الدقة، فكر في تغيير حجمها قبل OCR. غالباً ما يقبل `aocr.Image.load` معامل `max_size`.  
- **Unicode handling:** افتح دائمًا ملف الإخراج باستخدام `encoding="utf-8"`؛ يمكن لمحركات OCR إنتاج أحرف غير ASCII.  
- **Parallelism:** بالنسبة لـ OCR المعتمد على CPU يمكنك تغليف `ocr_batch` في `concurrent.futures.ThreadPoolExecutor`. فقط تذكر الحفاظ على نسخة واحدة من `ai` – إنشاء العديد من الخيوط التي تستدعي كل منها `ai.initialize` يتعارض مع هدف “تحرير موارد AI”.  
- **Error resilience:** غلف حلقة الصور الفردية داخل كتلة `try/except` حتى لا يتسبب PNG تالف واحد في إيقاف الدفعة بأكملها.

## الخلاصة

أصبحت الآن تمتلك **python ocr tutorial** يوضح كيفية **load png image** الملفات، تنفيذ **batch OCR processing**، وإدارة **free AI resources** بمسؤولية. المثال الكامل القابل للتنفيذ يوضح بالضبط كيفية **recognize text from image** الكائنات وتنظيف الموارد بعد ذلك، بحيث يمكنك نسخه ولصقه في مشاريعك دون البحث عن أجزاء مفقودة.  

هل أنت مستعد للخطوة التالية؟ جرّب استبدال وحدات `aocr` و `ai` الوهمية بمكتبات حقيقية مثل `pytesseract` و `torchvision`. يمكنك أيضًا توسيع السكريبت لإنتاج JSON، أو إرسال النتائج إلى قاعدة بيانات، أو دمجه مع دلو تخزين سحابي. السماء هي الحد—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}