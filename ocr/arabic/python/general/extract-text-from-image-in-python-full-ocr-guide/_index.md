---
category: general
date: 2026-06-25
description: استخراج النص من الصورة باستخدام OCR في بايثون. تعلّم كيفية تحميل الصورة
  للـ OCR، إجراء الـ OCR في بايثون، وتحويل الفاتورة إلى JSON في بضع خطوات بسيطة.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: ar
og_description: استخراج النص من الصورة باستخدام OCR في بايثون. يشرح هذا الدليل كيفية
  تحميل صورة لإجراء OCR، تنفيذ OCR في بايثون، وتحويل إيصال إلى JSON.
og_title: استخراج النص من الصورة في بايثون – دليل OCR الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: استخراج النص من الصورة في بايثون – دليل OCR كامل
url: /ar/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام بايثون – دليل OCR كامل

هل احتجت يوماً إلى **استخراج النص من صورة** لكن لم تعرف من أين تبدأ؟ في هذا الدرس سنرشدك خطوة بخطوة إلى كيفية **تحميل الصورة للـ OCR**، **إجراء OCR في بايثون**، و**تحويل الفاتورة إلى JSON**—كل ذلك ببضع أسطر من الشيفرة فقط.

إذا سبق لك أن أنشأت تطبيق مسح فواتير، أو متعقب نفقات، أو ترغب فقط في أتمتة إدخال البيانات، فستدرك لماذا إتقان هذا التدفق يُغيّر قواعد اللعبة. بنهاية الدرس ستحصل على سكريبت يعمل يقرأ صورة فاتورة ويُخرج حمولة JSON نظيفة جاهزة للخدمات اللاحقة.

## ما ستتعلمه

سنغطي كل خطوة من تثبيت مكتبة `aocr` إلى معالجة النتيجة الخام. بالتحديد ستتعلم كيفية:

1. **إنشاء كائن محرك OCR** – نقطة الدخول لجميع عمليات التعرف.  
2. **تحميل صورة للـ OCR** – إخبار المحرك بأي ملف يقرأ.  
3. **اختيار صيغة التصدير** – JSON أو XML، سنختار JSON لأنه أسهل في الاستهلاك.  
4. **تشغيل عملية التعرف** – تنفيذ OCR فعلياً في بايثون.  
5. **طباعة أو تخزين النتيجة** – تحويل الفاتورة إلى JSON ورؤية المخرجات.

لا تحتاج إلى أي خبرة سابقة في OCR؛ فقط إعداد بسيط لبايثون وملف صورة (فاتورة، منشور، أو أي شيء تحتاجه).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="استخراج النص من الصورة باستخدام OCR في بايثون"}

## استخراج النص من الصورة – دليل OCR خطوة‑بخطوة في بايثون

فيما يلي السكريبت الكامل الجاهز للتنفيذ. يمكنك نسخه ولصقه في ملف اسمه `receipt_ocr.py` ثم تشغيله بالأمر `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### لماذا يعمل هذا

- **كائن المحرك** – `aocr.OcrEngine()` يضم كل الأعمال الثقيلة (تحميل النموذج، التحضير المسبق، إلخ).  
- **تحميل الصورة** – `engine.load_image()` يخبر المكتبة بالضبط أي صورة bitmap يجب تحليلها؛ يمكنك تمرير JPEG، PNG، أو حتى ملفات PDF متعددة الصفحات.  
- **صيغة التصدير** – ضبط `engine.export_format` إلى `aocr.ExportFormat.JSON` يجعل النتيجة سلسلة مُهيكلة، مثالية للـ APIs التي تتوقع JSON.  
- **استدعاء التعرف** – `engine.recognize()` يُجري استدلال الشبكة العصبية خلف الكواليس؛ تُعيد سلسلة JSON تحتوي على كتل النص المكتشفة، درجات الثقة، ومعلومات التخطيط.  

---

## تحميل الصورة للـ OCR باستخدام aocr

إذا كنت تتساءل ما إذا كانت الصورة تحتاج إلى أي معالجة مسبقة خاصة، الجواب المختصر هو **لا**—`aocr` يتعامل مع معظم الحالات الشائعة (ضبط التباين، تصحيح الميل) تلقائياً. ومع ذلك، يمكنك تحسين الدقة عبر:

- التأكد من أن الصورة بدقة لا تقل عن 300 dpi.  
- قص الحدود غير الضرورية.  
- التحويل إلى تدرج الرمادي قبل الإرسال (اختياري، `engine.load_image()` سيفعل ذلك لك).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*نصيحة محترف:* إذا كانت الفاتورة تحتوي على الكثير من الضوضاء، فإن الخطوة الإضافية أعلاه يمكن أن تعزز **دقة إجراء OCR في بايثون** بشكل ملحوظ.

---

## اختيار صيغة التصدير وتحويل الفاتورة إلى JSON

قد تتساءل، “لماذا لا أحصل على نص عادي فقط؟” لأن JSON يحافظ على الهيكل الهرمي (السطور، الكلمات، الصناديق المحيطة). هذا يجعل من السهل جداً ربط الحقول مثل *المبلغ الإجمالي* أو *التاريخ* لاحقاً.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

عند تشغيل السكريبت، سيظهر `json_result` شيئاً كهذا (مقتطع للوضوح):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

الآن لديك حمولة **تحويل الفاتورة إلى JSON** يمكنك إرسالها مباشرة إلى قاعدة بيانات، أو نقطة نهاية REST، أو نموذج تعلم آلي.

---

## تشغيل عملية التعرف واسترجاع النتائج

الخطوة الأخيرة—إجراء OCR فعلياً—بساطة استدعاء `recognize()`. خلف الكواليس تقوم المكتبة بـ:

1. إرسال الصورة عبر شبكة عصبية تلافيفية مدربة مسبقاً.  
2. فك تشفير مخرجات الشبكة إلى أحرف قابلة للقراءة.  
3. تجميع كل شيء في الصيغة المختارة (JSON في حالتنا).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

إذا أردت تخزين المخرجات بدلاً من طباعتها، فقط اكتبها إلى ملف:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*حالة خاصة:* بعض الفواتير تحتوي على أحرف غير ASCII (مثلاً “€”). تأكد من فتح الملف بترميز UTF‑8 كما هو موضح أعلاه لتجنب النص المشوّه.

---

## مثال كامل يعمل (جميع الخطوات في سكريبت واحد)

بجمع كل ما سبق، إليك السكريبت النهائي الذي يمكنك تشغيله من البداية إلى النهاية:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

شغّله بالأمر:

```bash
python receipt_ocr.py
```

ستظهر لك سطر تأكيد، وفي نفس المجلد ملف `receipt_output.json` يحتوي على البيانات المُهيكلة.

---

## الخلاصة

أصبحت الآن تعرف **كيفية استخراج النص من صورة** باستخدام بايثون، وكيفية **تحميل الصورة للـ OCR**، وكيفية **إجراء OCR في بايثون**، وكيفية **تحويل الفاتورة إلى JSON** للاستخدام اللاحق. هذا التدفق المتكامل خفيف الوزن، يتطلب فقط حزمة `aocr`، ويمكن دمجه في أي خط أنابيب أتمتة.

ما الخطوة التالية؟ جرّب تغيير صيغة التصدير إلى XML، أو استكشف تقنيات معالجة صور مختلفة، أو أنشئ API صغير باستخدام Flask يقبل فاتورة مرفوعة ويعيد حمولة JSON فوراً. السماء هي الحد عندما تكون الأساسيات تحت يدك.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقاً أدناه، ونتمنى لك برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}