---
category: general
date: 2026-06-22
description: احصل على إحداثيات الصندوق المحيط من الصور باستخدام بايثون. تعلم كيفية
  استخراج النص من صورة بايثون باستخدام Aspose OCR وتحليل JSON في دقائق.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: ar
og_description: احصل على إحداثيات الصندوق المحيط من الصور باستخدام بايثون. يوضح هذا
  الدليل كيفية استخراج النص من صورة بايثون باستخدام Aspose OCR وتحليل بيانات التخطيط.
og_title: احصل على إحداثيات الصندوق المحيط من OCR في بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: احصل على إحداثيات الصندوق المحيط من OCR في بايثون – دليل كامل
url: /ar/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# احصل على إحداثيات الصندوق المحيط من OCR في بايثون – دليل كامل

هل احتجت يوماً إلى **الحصول على إحداثيات الصندوق المحيط** لكل كلمة في فاتورة ممسوحة ضوئياً، لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من مشاريع الأتمتة، تحتاج إلى تحديد موقع النص على صورة لتسليط الضوء عليه، أو إخفائه، أو إرساله إلى تحليلات لاحقة. الخبر السار؟ ببضع أسطر من بايثون و Aspose.OCR يمكنك استخراج النص **وكذلك** موقعه الدقيق في خطوة واحدة.

في هذا الدرس سنستعرض مثالًا عمليًا يوضح لك كيفية **استخراج النص من صورة بايثون**‑ستايل، ثم الغوص في بيانات تخطيط JSON لاستخراج تلك الصناديق المحيطة. لا إطالة، مجرد سكريبت يعمل، وتوضيحات لأهمية كل خطوة، ونصائح لتجنب الأخطاء الشائعة.

---

## ما ستبنيه

بنهاية هذا الدليل ستحصل على سكريبت بايثون جاهز للتنفيذ يقوم بـ:

1. تحميل صورة (مثلاً، صورة فاتورة بصيغة PNG) إلى Aspose OCR.  
2. ضبط المحرك لإصدار معلومات تخطيط بصيغة JSON.  
3. تحويل JSON إلى قاموس بايثون.  
4. المرور على كل كلمة مُعترف بها، وطباعة نصها **وإحداثيات** الصندوق المحيط بها.

سترى أيضًا كيف تُكيّف الكود لملفات PDF متعددة الصفحات، صيغ صور مختلفة، وأنظمة إحداثيات مخصصة.

### المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- رخصة نشطة لـ Aspose.OCR for Python أو نسخة تجريبية مجانية (المكتبة تعمل بدون رخصة لكنها تضيف علامة مائية).  
- `pip install aspose-ocr` (اسم الحزمة على PyPI).  
- صورة نموذجية باسم `invoice.png` موجودة في مجلد يمكنك الإشارة إليه.

هذا كل شيء—بدون أطر عمل ثقيلة، بدون خدمات خارجية. هيا نبدأ.

---

## الخطوة 1: تثبيت واستيراد المكتبات المطلوبة

أولاً، تأكد من أن حزمة Aspose OCR ووحدة `json` المدمجة متوفرة. وحدة `json` تأتي مع بايثون، لذا نحتاج فقط لتثبيت Aspose.

```bash
pip install aspose-ocr
```

الآن استوردها في سكريبتك:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **لماذا هذا مهم:** استيراد `aspose.ocr` يمنحك الوصول إلى محرك OCR عالي الأداء، بينما `json` يتيح لك تحويل سلسلة التخطيط الخام إلى قاموس بايثون أصلي لتسهيل التجوال.

---

## الخطوة 2: إنشاء محرك OCR وتحميل الصورة

المحرك هو قلب العملية. تقوم بإنشائه، ثم تشير إليه إلى الصورة التي تريد مسحها.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **نصيحة احترافية:** استبدل `"YOUR_DIRECTORY/invoice.png"` بمسار مطلق أو نسبي يشير إلى ملفك الفعلي. إذا لم يتم العثور على الملف، سيُطلق Aspose استثناء `FileNotFoundError`، لذا تحقق من صحة الاسم.

---

## الخطوة 3: ضبط المحرك لإصدار بيانات تخطيط بصيغة JSON

يمكن لـ Aspose OCR إرجاع نص عادي، أو JSON خاص بـ OCR فقط، أو JSON تخطيط كامل يتضمن إحداثيات الكلمات، الأسطر، وحتى الأحرف الفردية. للحصول على **إحداثيات الصندوق المحيط**، نحتاج إلى JSON التخطيط.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **لماذا JSON؟** JSON مستقل عن اللغة، قابل للقراءة البشرية، ويتطابق بسهولة مع قواميس بايثون. يحتوي JSON التخطيط على مصفوفة `"words"` حيث يحمل كل عنصر النص ومصفوفة `boundingBox` المكوّنة من ثمانية أرقام (نقاط الزوايا الأربعة).

---

## الخطوة 4: تشغيل التعرف واستخراج سلسلة JSON الخام

الآن نقوم فعليًا بتشغيل OCR. تُعيد طريقة `recognize()` كائن `OcrResult`، يمكننا من خلاله استخراج سلسلة JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

إذا طبعّت `layout_json` ستظهر لك شيئًا مثل:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **حالة حافة:** قد تُنتج بعض الصور مصفوفة `"words"` فارغة إذا لم يتمكن محرك OCR من اكتشاف أي نص. في هذه الحالة، تحقق من جودة الصورة (التباين، الدقة) قبل المتابعة.

---

## الخطوة 5: تحويل JSON إلى قاموس بايثون

العمل مع هياكل بايثون الأصلية أسهل بكثير من التلاعب بالسلاسل. استخدم الدالة `json.loads()` لتحويل السلسلة.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

الآن `layout_data["words"]` هي قائمة من القواميس، كل واحد يمثل كلمة وصندوقها المحيط.

---

## الخطوة 6: المرور على الكلمات و**الحصول على إحداثيات الصندوق المحيط**

هذا هو جوهر الدرس: التكرار عبر كل كلمة، استخراج النص، وطباعة الإحداثيات. هنا بالضبط نحصل على **إحداثيات الصندوق المحيط**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**نموذج إخراج** (ستختلف أرقامك بناءً على الصورة):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **لماذا صيغة النقاط الثمانية؟** الزوايا الأربعة (أعلى‑يسار، أعلى‑يمين، أسفل‑يمين، أسفل‑يسار) تتيح لك رسم مضلع حول الكلمة حتى لو كان النص مائلًا. إذا كنت تحتاج إلى مستطيل بسيط فقط، يمكنك حساب `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, و `height = max(y…) - y_min`.

---

## تحسينات اختيارية

### 1. تحويل الصناديق المحيطة إلى مستطيلات بسيطة

إذا كانت أداتك اللاحقة تتوقع `(x, y, width, height)` بدلاً من ثمانية نقاط، أضف المساعد التالي:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. معالجة ملفات PDF متعددة الصفحات

يمكن لـ Aspose OCR قبول تدفقات PDF. استبدل سطر تحميل الصورة بـ:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

ثم كرّر `set_page_number` لكل صفحة، واجمع الإحداثيات لكل صفحة.

### 3. تصور الصناديق المحيطة

إذا أردت رؤية الصناديق مرسومة على الصورة الأصلية، استخدم Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

ستظهر الآن حدود حمراء حول كل كلمة مُعترف بها—مثالي للتصحيح أو لتراكب واجهة المستخدم.

---

## أسئلة شائعة ومشكلات محتملة

- **ماذا لو كان JSON كبيرًا؟** للمستندات الضخمة، فكر في تدفق JSON أو معالجة كل صفحة على حدة لتقليل استهلاك الذاكرة.  
- **لماذا بعض الكلمات مفقودة؟** التباين المنخفض أو النص المكتوب يدويًا غالبًا ما يعيق محركات OCR. قم بتهيئة الصورة مسبقًا (زيادة التباين، تحويل إلى ثنائي) قبل تمريرها إلى Aspose.  
- **هل يمكن الحصول على إحداثيات على مستوى الأحرف؟** نعم—اضبط `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` لتلقي مصفوفة `"characters"` مع `boundingBox` الخاص بها.  
- **هل نظام الإحداثيات يبدأ من الصفر؟** بالتأكيد. (0, 0) هو الزاوية العلوية اليسرى للصورة.

---

## السكريبت الكامل – جاهز للنسخ والتنفيذ

فيما يلي المثال الكامل القابل للتنفيذ الذي يجمع كل خطوة. احفظه باسم `extract_bboxes.py` وشغّله بالأمر `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}