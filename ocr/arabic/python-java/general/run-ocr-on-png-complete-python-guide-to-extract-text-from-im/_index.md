---
category: general
date: 2026-01-12
description: قم بتشغيل OCR على ملفات PNG بسرعة باستخدام بايثون. تعلم كيفية استخراج
  النص من الصورة والفاتورة، وتحميل الصورة للـ OCR باستخدام Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: ar
og_description: قم بتشغيل OCR على ملفات PNG فورًا. يوضح هذا الدليل كيفية استخراج النص
  من الصورة والفاتورة، تحميل الصورة للـ OCR، وحفظ النتائج بصيغة JSON وCSV.
og_title: تشغيل OCR على PNG – دليل بايثون كامل
tags:
- OCR
- Python
- Image Processing
title: تشغيل OCR على PNG – دليل بايثون الكامل لاستخراج النص من الصور
url: /ar/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على PNG – دليل Python الكامل لاستخراج النص من الصور

هل احتجت يومًا إلى **تشغيل OCR على ملفات PNG** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج نظيفة ومهيكلة؟ لست وحدك. في العديد من المشاريع الواقعية—مثل أتمتة الفواتير أو مسح الإيصالات—الخطوة الأولى هي **استخراج النص من ملفات الصورة**، وPNG هو تنسيق شائع لأنه يحافظ على الجودة بدون فقدان.

في هذا الدرس سنستعرض مثالًا عمليًا باستخدام حزمة Aspose.OCR للغة Python. بنهاية الدليل ستعرف كيف **تحمّل الصورة للـ OCR**، تستخرج كل سطر نص، تحول البيانات إلى كائن JSON مرتب، وحتى تصدره إلى CSV للمعالجة اللاحقة. لا إطالة، مجرد حل عملي جاهز للتنفيذ.

## ما ستتعلمه

- كيفية تثبيت واستيراد مكتبة Aspose.OCR.  
- الخطوات الدقيقة **لتشغيل OCR على PNG** ومعالجة كائن النتيجة.  
- طرق **استخراج النص من الفاتورة** وتنسيق المخرجات كـ JSON أو CSV.  
- نصائح للتعامل مع الصور منخفضة التباين، المستندات متعددة اللغات، ودرجات الثقة.  
- عينة كود كاملة يمكن نسخها ولصقها وتشغيلها اليوم.

> **المتطلبات المسبقة:** Python 3.8+ ومعرفة أساسية بـ pip. إذا لم تستخدم Aspose من قبل، لا تقلق—هذا الدليل يغطي كل ما تحتاجه للبدء.

---

## الخطوة 1 – تثبيت Aspose.OCR وإعداد بيئتك

قبل أن نتمكن من **تشغيل OCR على PNG**، يجب أن تكون المكتبة موجودة على نظامك.

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** استخدم بيئة افتراضية (`python -m venv venv`) لعزل الاعتمادات. هذا يمنع تعارض الإصدارات إذا كنت تدير عدة مشاريع.

بعد التثبيت، استورد الوحدات التي سنحتاجها:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

هنا نستورد `asposeocr` للمعالجة الأساسية ومكتبة `json` المدمجة للتسلسل اللاحق.

---

## الخطوة 2 – إنشاء محرك OCR وتحديد اللغة

محرك OCR هو المكوّن الأساسي الذي يقرأ البكسلات فعليًا. لمعظم الفواتير الإنجليزية، ستحتاج حزمة اللغة الإنجليزية:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **لماذا هذا مهم:** تحديد اللغة يحد من مجموعة الأحرف، مما يزيد الدقة ويسرّع المعالجة. إذا احتجت للتعامل مع فواتير متعددة اللغات، استبدل `ocr.Language.ENGLISH` بالعدد المناسب.

---

## الخطوة 3 – تحميل الصورة للـ OCR

الآن سنقوم **بتحميل الصورة للـ OCR**. طريقة `Image.load` تقبل مسار الملف، وتدعم PNG، JPEG، BMP، وأكثر.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **حالة خاصة:** إذا كان ملف PNG كبيرًا جدًا (أكثر من 5 ميغابايت)، فكر في تصغير حجمه أولًا لتقليل استهلاك الذاكرة. يمكن لـ Pillow القيام بذلك بسطر واحد:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## الخطوة 4 – تشغيل OCR على PNG والتقاط النتيجة

مع جاهزية المحرك وتحميل الصورة، حان الوقت **لتشغيل OCR على PNG** واسترجاع النتيجة المهيكلة.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

كائن `ocr_result` يحتوي على مجموعة من عناصر `OcrRegion`، كل منها يحمل النص المُعترف به ودرجة الثقة (0‑100). هنا تحصل على البيانات الدقيقة اللازمة **لاستخراج النص من الفاتورة** سطرًا بسطر.

---

## الخطوة 5 – تحويل النتيجة إلى JSON وعرضها بشكل جميل

معظم الأنظمة اللاحقة تفضّل JSON، لذا سنحوّل مخرجات OCR إلى سلسلة منسقة بشكل جميل.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### مثال على المخرجات

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

لاحظ أن كل سطر يتضمن مقياس الثقة—مثالي لتصفية الإدخالات منخفضة الثقة إذا كنت تخطط **لاستخراج النص من الفاتورة** تلقائيًا.

---

## الخطوة 6 – حفظ بيانات OCR كملف CSV (سطر واحد لكل نص + ثقة)

CSV مثالي للجداول أو استيراد البيانات السريع. Aspose توفر سطرًا واحدًا لتصدير كل شيء إلى ملف CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

الملف CSV الناتج سيبدو هكذا:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

يمكنك الآن فتحه في Excel أو Google Sheets أو إدخاله إلى قاعدة بيانات.

---

## إضافي – التعامل مع النص منخفض الثقة ومستندات PDF متعددة الصفحات

### التصفية حسب الثقة

إذا أردت فقط السطور ذات الثقة العالية، صَفِّي JSON قبل الكتابة:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### المستندات متعددة الصفحات

Aspose.OCR ينشئ تلقائيًا إدخالًا جديدًا `page` لكل صفحة في PNG أو PDF متعدد الصفحات. يمكنك التجول عبر `ocr_data["pages"]` لمعالجة جميعها—بدون كود إضافي.

---

## مثال كامل يعمل

فيما يلي **السكريبت الكامل** الذي يمكنك نسخه، لصقه، وتشغيله فورًا. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على ملف PNG الخاص بك.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

شغّل السكريبت باستخدام `python run_ocr.py` وسترى تفريغ JSON في الطرفية، ملف CSV على القرص، وقائمة مُصفّاة من الإدخالات ذات الثقة العالية.

---

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا لاستخراج النص من إيصال ممسوح ضوئيًا بدلًا من فاتورة؟**  
ج: بالتأكيد. نفس سير العمل ينطبق—فقط وجه `image_path` إلى ملف إيصال PNG الخاص بك. إذا كان الإيصال بلغة مختلفة، غيّر `engine.language` وفقًا لذلك.

**س: ماذا لو كان الـ PNG يحتوي على نص مائل؟**  
ج: Aspose.OCR يكتشف الاتجاه تلقائيًا، لكن في الحالات الصعبة يمكنك تدوير الصورة يدويًا باستخدام Pillow قبل تمريرها إلى المحرك.

**س: هل أحتاج إلى رخصة مدفوعة لـ Aspose.OCR؟**  
ج: المكتبة توفر وضع تقييم مجاني مع علامة مائية على المخرجات. للاستخدام الإنتاجي ستحتاج إلى رخصة يمكن الحصول عليها من موقع Aspose.

---

## الخلاصة

غطّينا كل ما تحتاجه **لتشغيل OCR على PNG** باستخدام Python: تثبيت الـ SDK، تحميل الصورة، استخراج نص مهيكل، وحفظ النتيجة كـ JSON أو CSV. سواء كنت تريد **استخراج النص من صورة** لسكربت بسيط أو **استخراج النص من الفاتورة** لخط أنابيب محاسبة آلي، الخطوات أعلاه تمنحك أساسًا قويًا جاهزًا للإنتاج.

الخطوات التالية قد تشمل:

- ربط مخرجات CSV بقاعدة بيانات لتخزين الفواتير بالجملة.  
- إضافة معالجة لاحقة باستخدام تعبيرات نمطية لاستخراج التواريخ، المبالغ، أو أرقام الضرائب.  
- استخدام ميزة `ocr_engine.recognize_barcode` إذا كانت فواتيرك تحتوي على رموز QR.

جرّبها، عدّل عتبات الثقة، وشاهد سير عمل معالجة المستندات يتحول إلى نسمة. هل لديك أسئلة إضافية أو حالة استخدام مميزة تريد مشاركتها؟ اترك تعليقًا أدناه—نتمنى لك OCR موفق!  

![مثال تشغيل OCR على PNG](run-ocr-on-png.png "تشغيل OCR على PNG – مثال بصري لنتيجة OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}