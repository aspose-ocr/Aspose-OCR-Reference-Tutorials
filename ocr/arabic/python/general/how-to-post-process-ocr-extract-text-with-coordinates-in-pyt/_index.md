---
category: general
date: 2026-04-26
description: كيفية ما بعد معالجة نتائج التعرف الضوئي على الأحرف واستخراج النص مع الإحداثيات.
  تعلّم حلاً خطوة بخطوة باستخدام الإخراج المُنظم وتصحيح الذكاء الاصطناعي.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: ar
og_description: كيفية ما بعد معالجة نتائج OCR واستخراج النص مع الإحداثيات. اتبع هذا
  الدليل الشامل للحصول على سير عمل موثوق.
og_title: كيفية ما بعد معالجة OCR – دليل كامل
tags:
- OCR
- Python
- AI
- Text Extraction
title: كيفية ما بعد معالجة OCR – استخراج النص مع الإحداثيات في بايثون
url: /ar/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية ما بعد معالجة OCR – استخراج النص مع الإحداثيات في بايثون

هل احتجت يومًا إلى **how to post‑process OCR** لأن المخرجات الأولية كانت صاخبة أو غير محاذاة؟ لست وحدك. في العديد من المشاريع الواقعية—مسح الفواتير، رقمنة الإيصالات، أو حتى تعزيز تجارب الواقع المعزز—يُعطيك محرك OCR كلمات خام، لكن لا يزال عليك تنظيفها وتتبع مكان كل كلمة على الصفحة. هنا يبرز دور وضع الإخراج المُنظم مع معالج ما بعد المعالجة المدفوع بالذكاء الاصطناعي.

> **نصيحة احترافية:** إذا كنت تستخدم مكتبة OCR مختلفة، ابحث عن وضع “structured” أو “layout”؛ المفاهيم تبقى نفسها.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

| المتطلب | لماذا يهم |
|-------------|----------------|
| Python 3.9+ | الصياغة الحديثة وتلميحات الأنواع |
| `ocr` library that supports `OutputMode.STRUCTURED` (e.g., a fictional `myocr`) | ضرورية لبيانات الصناديق المحيطة |
| An AI post‑processing module (could be OpenAI, HuggingFace, or a custom model) | تحسن الدقة بعد OCR |
| An image file (`input.png`) in your working directory | المصدر الذي سنقرأه |

إذا كان أي من هذه غير مألوف، ما عليك سوى تثبيت الحزم الوهمية باستخدام `pip install myocr ai‑postproc`. يحتوي الكود أدناه أيضًا على نماذج احتياطية لتتمكن من اختبار التدفق دون المكتبات الحقيقية.

---

## الخطوة 1: تمكين وضع الإخراج المُنظم لمحرك OCR  

الأول الذي نفعله هو إخبار محرك OCR بأن يعطينا أكثر من مجرد نص عادي. الإخراج المُنظم يُعيد كل كلمة مع صندوقها المحيط ودرجة الثقة، وهو أمر أساسي لـ **extract text with coordinates** لاحقًا.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*لماذا يهم هذا:* بدون وضع مُنظم ستحصل فقط على سلسلة طويلة، وستفقد المعلومات المكانية التي تحتاجها لتراكب النص على الصور أو لتغذية تحليل التخطيط اللاحق.

---

## الخطوة 2: التعرف على الصورة واستخلاص الكلمات والصناديق ومستوى الثقة  

الآن نُدخل الصورة إلى المحرك. النتيجة هي كائن يحتوي على قائمة من كائنات الكلمات، كل منها يُظهر `text`، `x`، `y`، `width`، `height`، و `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*حالة حافة:* إذا كانت الصورة فارغة أو غير قابلة للقراءة، سيكون `structured_result.words` قائمة فارغة. من الممارسات الجيدة التحقق من ذلك ومعالجته بلطف.

---

## الخطوة 3: تشغيل ما بعد معالجة AI مع الحفاظ على المواقع  

حتى أفضل محركات OCR ترتكب أخطاء—مثل الخلط بين “O” و “0” أو فقدان الحركات. يمكن لنموذج AI مدرب على نصوص محددة المجال تصحيح هذه الأخطاء. الأهم أننا نحافظ على الإحداثيات الأصلية بحيث يبقى التخطيط المكاني سليمًا.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*لماذا نحافظ على الإحداثيات:* العديد من المهام اللاحقة (مثل توليد PDF، وضع علامات AR) تعتمد على التحديد الدقيق للموقع. يتعامل AI فقط مع حقل `text`، ويترك `x`، `y`، `width`، `height` دون تغيير.

---

## الخطوة 4: التكرار على الكلمات المصححة وعرض نصها مع الإحداثيات  

أخيرًا، نمر على الكلمات المصححة ونطبع كل كلمة مع زاويةها العلوية اليسرى `(x, y)`. هذا يحقق هدف **extract text with coordinates**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**الناتج المتوقع (مثال):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

كل سطر يُظهر الكلمة المصححة وموقعها الدقيق على الصورة الأصلية.

---

## مثال كامل يعمل  

فيما يلي سكريبت واحد يجمع كل شيء معًا. يمكنك نسخه، تعديل عبارات الاستيراد لتتناسب مع مكتباتك الفعلية، وتشغيله مباشرة.

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

**تشغيل السكريبت**

```bash
python ocr_postprocess_demo.py
```

إذا كانت المكتبات الحقيقية مثبتة، سيعالج السكريبت ملف `input.png` الخاص بك. وإلا، سيسمح لك تنفيذ النموذج الاحتياطي برؤية التدفق المتوقع والناتج دون أي تبعيات خارجية.

---

## الأسئلة المتكررة (FAQ)

| السؤال | الجواب |
|----------|--------|
| *هل يعمل هذا مع Tesseract؟* | لا يوفّر Tesseract وضعًا منظمًا بشكل افتراضي، لكن الأغلفة مثل `pytesseract.image_to_data` تُعيد الصناديق المحيطة التي يمكنك تمريرها إلى نفس معالج AI. |
| *ماذا لو احتجت الزاوية السفلية اليمنى بدلاً من العليا اليسرى؟* | كل كائن كلمة يوفر أيضًا `width` و `height`. احسب `x2 = x + width` و `y2 = y + height` للحصول على الزاوية المقابلة. |
| *هل يمكنني معالجة عدة صور دفعة واحدة؟* | بالتأكيد. ضع الخطوات داخل حلقة `for image_path in Path("folder").glob("*.png"):` وجمع النتائج لكل ملف. |
| *كيف أختار نموذج AI للتصحيح؟* | للنص العام، نموذج GPT‑2 صغير مُدرب على أخطاء OCR يعمل. للبيانات المتخصصة (مثل الوصفات الطبية)، درّب نموذج تسلسل‑إلى‑تسلسل على بيانات مزدوجة (ضجيج‑نظيفة). |
| *هل درجة الثقة مفيدة بعد تصحيح AI؟* | يمكنك الاحتفاظ بالثقة الأصلية للتصحيح، لكن قد يُخرج AI درجة ثقته الخاصة إذا كان النموذج يدعم ذلك. |

---

## الحالات الحدية وأفضل الممارسات  

1. **صور فارغة أو تالفة** – تحقق دائمًا من أن `structured_result.words` غير فارغ قبل المتابعة.  
2. **نصوص غير لاتينية** – تأكد من تكوين محرك OCR للغة المستهدفة؛ يجب أن يكون معالج AI مدربًا على نفس النص.  
3. **الأداء** – تصحيح AI قد يكون مكلفًا. خزن النتائج مؤقتًا إذا كنت ستعيد استخدام نفس الصورة، أو نفّذ خطوة AI بشكل غير متزامن.  
4. **نظام الإحداثيات** – قد تستخدم مكتبات OCR أصولًا مختلفة (أعلى‑يسار مقابل أسفل‑يسار). عدّل وفقًا لذلك عند وضع النص على ملفات PDF أو القماش.  

---

## الخلاصة  

أصبح لديك الآن وصفة شاملة من البداية إلى النهاية لـ **how to post‑process OCR** واستخراج النص مع الإحداثيات بشكل موثوق. من خلال تمكين الإخراج المُنظم، تمرير النتيجة عبر طبقة تصحيح AI، والحفاظ على الصناديق المحيطة الأصلية، يمكنك تحويل مسحات OCR الصاخبة إلى نص نظيف ومُدرك مكانيًا جاهز للمهام اللاحقة مثل توليد PDF، أتمتة إدخال البيانات، أو تراكب الواقع المعزز.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال نموذج AI الاحتياطي بـ استدعاء OpenAI `gpt‑4o‑mini`، أو دمج خط الأنابيب في FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}