---
category: general
date: 2026-06-22
description: التعرف على النص من ملفات PNG باستخدام Aspose OCR في بايثون. تعلم معالجة
  دفعات من الصور باستخدام OCR وتعيين طبقات GPU للمعالجة السريعة.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: ar
og_description: التعرف على النص من ملفات PNG باستخدام Aspose OCR في بايثون. يوضح هذا
  الدليل كيفية معالجة الصور دفعةً واحدة باستخدام OCR وتعيين طبقات GPU للسرعة.
og_title: التعرف على النص من PNG – دليل Aspose OCR خطوة بخطوة
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
title: التعرف على النص من PNG – دليل شامل باستخدام Aspose OCR والذكاء الاصطناعي
url: /ar/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من PNG – دليل Aspose OCR و AI المتكامل

هل احتجت يومًا إلى **recognize text from png** للملفات لكن شعرت بالتعقيد في تفاصيل الإعداد؟ لست وحدك. سواءً كنت تقوم برقمنة الإيصالات، أو مسح النماذج، أو تحويل لقطات الشاشة إلى نص قابل للبحث، فإن إتقان **batch OCR images** في بايثون يمكن أن يوفر لك ساعات.  

في هذا الدليل سنستعرض مثالًا جاهزًا للتنفيذ لا يقتصر فقط على **recognize text from png** بل يوضح لك أيضًا كيفية **set GPU layers** للحصول على تسريع ملحوظ. في النهاية ستحصل على سكربت مستقل، شرح واضح لكل خطوة، ومجموعة من النصائح العملية التي يمكنك نسخها ولصقها في مشاريعك الخاصة.

## ما يغطيه هذا الدرس

- تثبيت حزم Aspose OCR و Aspose AI للبايثون  
- تكوين نموذج AI مع التحميل التلقائي من Hugging Face  
- إنشاء معالج ما بعد بسيط يُصلح أكثر الأخطاء الشائعة في OCR  
- تشغيل حلقة **batch OCR images** على مجلد كامل من ملفات PNG  
- استخدام خيار **set GPU layers** للاستفادة من بطاقة الرسوميات الخاصة بك  
- تنظيف الموارد بأمان بعد المعالجة  

![Diagram of recognize text from png workflow](workflow.png){alt="مخطط سير عمل التعرف على النص من PNG"}

## المتطلبات المسبقة

| المتطلبات | لماذا يهم |
|-------------|----------------|
| Python 3.8+ | حزم Aspose AI تستهدف المترجمات الحديثة |
| A CUDA‑compatible GPU (optional) | مطلوب إذا كنت ترغب في **set GPU layers** للتسريع |
| Internet access on first run | سيتم تنزيل النموذج تلقائيًا من Hugging Face |
| `pip` installed | لجلب حزم Aspose |

إذا كنت تمتلك هذه المتطلبات بالفعل، فأنت جاهز للبدء. إذا لم تكن كذلك، فإن خطوات التثبيت أدناه ستوجهك لتغطية ما ينقصك.

---

## الخطوة 1: تثبيت حزم Aspose OCR و Aspose AI

أولاً، احصل على المكتبات من PyPI. الأمر أدناه يجلب كلًا من محرك OCR ومساعد AI في خطوة واحدة.

```bash
pip install aspose-ocr aspose-ai
```

*نصيحة احترافية:* استخدم بيئة افتراضية (`python -m venv .venv`) لتبقى الحزم معزولة عن تثبيت بايثون العام لديك.

---

## الخطوة 2: إنشاء وتكوين كائن Aspose AI

المكوّن AI يزود محرك OCR بـ “الوضع الذكي”. سنشير إلى نموذج `Qwen/Qwen2.5-3B-Instruct-GGUF`، ونطلب منه التحميل التلقائي إذا كان مفقودًا، ونحدد **set GPU layers** إلى 30 (يمكنك تعديل ذلك لاحقًا).

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

**لماذا هذا مهم:**  
- `allow_auto_download` يلغي الحاجة إلى تحميل النموذج يدويًا (~2 GB).  
- `gpu_layers=30` يوجه أول 30 طبقة من المحول إلى الـ GPU، مما يقلل زمن الاستدلال بشكل كبير عندما تكون بطاقة رسومية متوافقة متوفرة.  
- استخدام `int8` يقلل استهلاك الذاكرة دون فقدان كبير في الدقة.

---

## الخطوة 3: تعريف معالج ما بعد بسيط لتنظيف أخطاء OCR

OCR ليس مثاليًا—خاصةً على PNG منخفض الدقة. حل سريع هو استبدال الأحرف التي تُقرأ بشكل خاطئ كثيرًا. الدالة التالية تستبدل “0” بـ “o” و “1” بـ “l”، وهو نمط نراه كثيرًا في الفواتير الممسوحة.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

سنربط هذا بالـ AI في الخطوة التالية بحيث يمر كل نتيجة التعرف عبره تلقائيًا.

---

## الخطوة 4: ربط معالج ما بعد الـ OCR بمحرك OCR

الآن نربط كل شيء: محرك OCR، نموذج AI، ومعالج ما بعد.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**ما الذي يحدث خلف الكواليس؟**  
`OcrEngine` يوكّل الجزء الثقيل إلى نموذج AI الذي قمت بتكوينه. بعد أن يُعيد النموذج النص الخام، تقوم Aspose باستدعاء `fix_common_errors` لتنظيف المخرجات قبل أن تراها.

---

## الخطوة 5: معالجة مجموعة من صور PNG – تشغيل OCR على كل ملف في مجلد

هذا هو جوهر الدرس: حلقة تتجول في دليل، تحمل كل ملف `.png`، تشغل OCR، وتطبع النتيجة المنقحة. هذا النمط هو الطريقة القياسية لـ **batch OCR images** بفعالية.

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

**الناتج المتوقع** (مثال لإيصال):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

إذا كان لديك العشرات أو المئات من الملفات، ستتعامل هذه الحلقة معها تسلسليًا، مع إعادة استخدام نفس كائن AI لتجنب عبء تحميل النموذج المتكرر.

---

## الخطوة 6: التنظيف – تحرير الموارد وإغلاق المحرك

عند الانتهاء، من الممارسات الجيدة تحرير ذاكرة الـ GPU والموارد الأصلية الأخرى. توفر Aspose طرقًا صريحة لذلك.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

تخطي هذه الخطوة قد يترك ذاكرة GPU غير مُحررة، مما قد يسبب أخطاء نفاد الذاكرة في المرة التالية التي تشغل فيها السكربت.

---

## إضافي: تعديل قيمة GPU Layers لأجهزة مختلفة

القيمة `gpu_layers` التي حددتها سابقًا تمثل نقطة مثالية للعديد من بطاقات GPU الحديثة، لكن قد تحتاج إلى تعديلها:

| ذاكرة GPU (GB) | القيمة الموصى بها لـ `gpu_layers` |
|-----------------|--------------------------|
| 4 GB أو أقل    | 10‑15                    |
| 6‑8 GB          | 20‑30                    |
| 12 GB+          | 35‑45 (أو أعلى)        |

إذا تجاوزت ذاكرة GPU المتاحة، سيعود المحرك تلقائيًا إلى CPU للطبقات المتبقية، لذا لن يتعطل البرنامج—ستكون العملية أبطأ. لا تتردد في التجربة ومراقبة الاستخدام عبر `nvidia‑smi`.

---

## المشكلات الشائعة وكيفية تجنّبها

1. **فشل تحميل النموذج** – تأكد أن بيئتك تستطيع الوصول إلى `https://huggingface.co`. قد تحتاج إلى ضبط بروكسي الشركة (`https_proxy` env var).  
2. **عدم اكتشاف GPU** – تحقق أن مكتبة `torch` (المثبتة كاعتماد) ترى الـ GPU: `import torch; print(torch.cuda.is_available())`. إذا أرجعت `False`، ثبّت نسخة PyTorch المتوافقة مع CUDA.  
3. **مسار الصورة غير صحيح** – `Path.glob("*.png")` حسّاس لحالة الأحرف على لينكس. استخدم `*.PNG` أو `*.png` حسب الحاجة، أو أضف `pathlib.Path(...).rglob("*.[pP][nN][gG]")` للسلامة.  
4. **معالج ما بعد يصحح أكثر من اللازم** – الاستبدال البسيط قد يحول الأحرف “0” الحقيقية إلى “o”. اختبر على عينة ممثلة واضبط المنطق حسب الحاجة.

---

## مثال كامل جاهز للنسخ واللصق

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

شغّله باستخدام:

```bash
python recognize_text_from_png_batch.py
```

سترى كل اسم ملف PNG متبوعًا بالنص المستخرج، تمامًا كما تم توضيحه سابقًا.

---

## الخلاصة

لقد استعرضنا معًا سير عمل كامل وجاهز للإنتاج لت **recognize text from png** باستخدام Aspose OCR و Aspose AI في بايثون. من خلال تجميع الخطوات في سكربت نظيف، يمكنك بسهولة **batch OCR images**، وبفضل `set gpu layers`


## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يحتوي على أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية معالجة مجموعة من صور OCR باستخدام List في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [كيفية التعرف على نص الصورة باستخدام اللغة عبر Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}