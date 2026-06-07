---
category: general
date: 2026-06-06
description: دورة تعليمية في Python للتعرف الضوئي على الأحرف توضح كيفية التعرف على
  نص الصورة، وإجراء OCR عالي الدقة واستخراج النص الإسباني باستخدام OCR المعجل بوحدة
  معالجة الرسومات.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: ar
og_description: دورة تعليمية في OCR باستخدام بايثون تُرشدك إلى التعرف على نصوص الصور،
  OCR عالي الدقة، واستخراج النص الإسباني مع تسريع باستخدام وحدة معالجة الرسومات.
og_title: دورة بايثون للتعرف الضوئي على الحروف – التعرف على النص باستخدام تسريع GPU
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
title: دورة بايثون للتعرف الضوئي على الأحرف – التعرف على نص الصورة باستخدام تسريع
  وحدة المعالجة الرسومية
url: /ar/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR بلغة Python – التعرف على نص الصورة مع تسريع GPU

هل تساءلت يومًا كيف **تتعرف على نص الصورة** في سكريبت Python دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك. في هذا **python ocr tutorial** سنظهر لك طريقة نظيفة وشاملة لاستخراج النص الإسباني من صورة عالية الدقة، وسنضيف تسريع GPU لتصبح العملية سريعة كالبرق.

فكر فيها كعرض سريع أثناء استراحة القهوة يمكنك توسيعه لاحقًا إلى خط أنابيب جاهز للإنتاج. بنهاية هذا الدليل ستحصل على برنامج قابل للتنفيذ يقوم بـ **high resolution OCR**، يستخدم GPU مدعوم بـ CUDA، ويُخرج الأحرف الإسبانية الدقيقة التي تحتاجها.

## ما ستتعلمه

- كيفية تثبيت واستيراد مكتبة OCR حديثة تدعم تسريع GPU.  
- كيفية إنشاء مثيل محرك OCR وتعيينه **لتعرف على نص الصورة** بالإسبانية.  
- كيفية تمكين **gpu accelerated OCR** للحصول على سرعات هائلة على ملفات عالية الدقة.  
- كيفية التعامل مع الحالات الحدية مثل نقص تعريفات CUDA أو الرجوع إلى CPU.  
- نصائح لتحسين الدقة عندما تحتاج إلى **استخراج النص الإسباني** من مسحات ضوضائية.

### المتطلبات المسبقة

- Python 3.9+ (الكود يعمل على 3.10 وما بعده أيضًا).  
- GPU متوافق مع CUDA (اختياري لكن يُنصح به بشدة).  
- معرفة أساسية بـ pip وبيئات افتراضية.  

إذا كنت تفتقد أيًا من هذه المتطلبات، سيظل الدليل يعمل — فقط تخطى خطوة GPU وستعود المكتبة تلقائيًا إلى CPU.

---

## دليل OCR بلغة Python: تثبيت الحزم المطلوبة

أولاً، نحتاج إلى محرك OCR قوي. لهذا الدليل سنستخدم الحزمة المفتوحة المصدر **`easyocr`**، التي تأتي بدعم مدمج لـ GPU عندما يتم اكتشاف جهاز متوافق.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **نصيحة احترافية:** إذا كان لديك PyTorch مثبتًا بالفعل، تأكد من أنه يتطابق مع نسخة CUDA الخاصة بك (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). الإصدارات غير المتطابقة هي مصدر شائع لأخطاء “GPU غير موجود”.

---

## الخطوة 1: إنشاء مثيل محرك OCR

الآن نقوم بتشغيل المحرك. EasyOCR يطلق على الفئة الرئيسية اسم `Reader`. المُنشئ يقبل قائمة بأكواد اللغات؛ سنمرر `"es"` للإسبانية.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*لماذا هذا مهم:* من خلال إعلان اللغة مسبقًا، يقوم المحرك بتحميل الأوزان العصبية الضرورية فقط، مما يوفر الذاكرة ويسرّع الاستدلال — مفيد بشكل خاص عندما تتعامل مع **high resolution OCR** لاحقًا.

---

## الخطوة 2: إعداد صورة عالية الدقة

الصور عالية الدقة تعطي النموذج المزيد من البكسلات للعمل معها، مما يترجم عادةً إلى تحسين في التعرف على الأحرف. لنفترض أن لديك ملفًا اسمه `high_res_spanish.png` موجودًا في مجلد اسمه `samples`.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

إذا لم يكن لديك عينة عالية الدقة جاهزة، يمكنك تنزيل واحدة مجانية من Unsplash أو إنشاء صورة اصطناعية باستخدام Pillow. المفتاح هو الحفاظ على DPI أعلى من 300 للحصول على أفضل النتائج.

---

## الخطوة 3: تمكين تسريع GPU (اختياري لكن موصى به)

EasyOCR بالفعل يحاول استخدام GPU عندما تضبط `gpu=True`. ومع ذلك، من الممارسات الجيدة التحقق من أن الجهاز يُستخدم فعليًا، خاصةً في الأنظمة متعددة الـ GPU.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*لماذا نتحقق من ذلك؟* إذا عاد السكريبت صامتًا إلى CPU، قد تتساءل لماذا عملية تستغرق 5 ثوانٍ فجأة تأخذ 30 ثانية. هذا الفحص الصغير يجعل السلوك شفافًا ويحافظ على توقعية خط أنابيب **gpu accelerated OCR** الخاص بك.

---

## الخطوة 4: تنفيذ OCR عالي الدقة والتعرف على نص الصورة

الآن الجزء الممتع — قراءة النص فعليًا. طريقة `readtext` في EasyOCR تُعيد قائمة من tuples تحتوي على المربع المحيط، السلسلة المعترف بها، ونسبة الثقة.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

إذا كنت تحتاج السلسلة الخام بدون إحداثيات، اضبط `detail=0`. بالنسبة لمعظم حالات **recognize image text**، الإعداد الافتراضي (`detail=1`) يمنحك ما يكفي من السياق للمعالجة اللاحقة.

---

## الخطوة 5: استخراج النص الإسباني وتنظيف المخرجات

نظرًا لأننا طلبنا من EasyOCR اللغة الإسبانية، فإن السلاسل المسترجعة تكون بالفعل بهذه اللغة. مع ذلك، قد ترغب في دمجها، إزالة المسافات الفارغة، أو تصفية الاكتشافات ذات الثقة المنخفضة.

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

**ماذا لو كانت الثقة منخفضة؟** يمكنك إما خفض العتبة (مع خطر الضوضاء) أو معالجة الصورة مسبقًا (زيادة التباين، تحويل إلى ثنائي، أو تصحيح الميل). هذه الحيل شائعة عند التعامل مع **high resolution OCR** على المستندات الممسوحة.

---

## الخطوة 6: معالجة الحالات الحدية وتحسين الأداء

حتى النماذج المدربة بأفضل شكل تواجه بعض السيناريوهات الصعبة. أدناه بعض الإصلاحات السريعة التي يمكنك لصقها في السكريبت.

### 6.1 الرجوع إلى CPU عندما لا يتوفر GPU

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 تقليل حجم الصور الكبيرة جدًا

إذا كانت صورتك أكبر من 4000 × 4000 px، قد تنفد ذاكرة GPU. قلل الحجم بنسبة متناسبة مع الحفاظ على DPI:

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

هذه المقاطع تجعل السكريبت قويًا، سواء كنت تعمل على محطة عمل أو على لابتوب متوسط المواصفات.

---

## مثال كامل يعمل

بجمع كل ما سبق، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه وتشغيله فورًا:

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

**الإخراج المتوقع (مثال):**



## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك الخاصة.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية التعرف على نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [كيفية التعرف على مستطيلات الصفحة لتعرف نص OCR في Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}