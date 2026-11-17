---
category: general
date: 2026-06-28
description: تحليل الإيصالات باستخدام OCR في بايثون بسهولة – تعلم كيفية استخراج بيانات
  الإيصال، تحميل صورة OCR، وشاهد مثالًا كاملاً لـ OCR في بايثون.
draft: false
keywords:
- receipt parsing OCR
- how to extract receipt
- python ocr example
- load image ocr
- how to ocr receipt
language: ar
og_description: 'تحليل الفواتير باستخدام OCR في بايثون: تعلم كيفية استخراج بيانات
  الفاتورة، تحميل صورة OCR، وتشغيل مثال كامل لـ OCR بايثون في دقائق.'
og_title: تحليل الفواتير باستخدام OCR في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Receipt parsing OCR in Python made easy – learn how to extract receipt
    data, load image OCR, and see a complete python OCR example.
  headline: Receipt Parsing OCR in Python – Full Step‑By‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- receipt parsing
- image processing
title: تحليل الفواتير باستخدام OCR في بايثون – دليل كامل خطوة بخطوة
url: /ar/python/general/receipt-parsing-ocr-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحليل الفواتير باستخدام OCR في بايثون – دليل كامل خطوة بخطوة

هل تساءلت يومًا كيف تحول إيصال سوبرماركت غير واضح إلى JSON نظيف يمكن البحث فيه؟ **تحليل الفواتير باستخدام OCR** هو الجواب، ولا تحتاج إلى شهادة دكتوراه في رؤية الحاسوب لتجعلها تعمل. في هذا الدرس سنستعرض مثالًا عمليًا **python ocr example** يقوم بتحميل صورة، تشغيل التعرف على النص المهيكل، وإخراج سلسلة JSON منسقة بشكل جميل—مثالي لتغذيته إلى برامج المحاسبة أو خطوط التحليل.

سنجيب أيضًا على السؤال الملح: **كيفية استخراج بيانات الفاتورة** بشكل موثوق، حتى عندما لا تكون الصورة مثالية. بنهاية الدرس ستحصل على سكريبت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع بايثون، سواء كنت تبني تطبيقًا للمالية الشخصية أو نظام تتبع نفقات على مستوى المؤسسة.

## ما ستتعلمه

* كيف تُعد محرك OCR خفيف الوزن في بايثون.
* الخطوات الدقيقة لـ **load image OCR** لملف إيصال.
* كيفية استدعاء طريقة التعرف المهيكل وتحويل النتيجة إلى JSON.
* نصائح للتعامل مع الحالات الشائعة—فواتير مائلة، تباين منخفض، وحروف يونيكود.
* عينة كود جاهزة للنسخ واللصق يمكنك تشغيلها اليوم.

### المتطلبات المسبقة

* Python 3.8 أو أحدث مثبت على جهازك.  
* مكتبة OCR توفر فئة `OcrEngine` ومساعد `Image` (العديد من المكتبات تعرض واجهات مشابهة؛ سنفترض وجود غلاف عام لهذا الدليل).  
* صورة إيصال (`receipt.png`) موجودة في مجلد يمكنك الإشارة إليه.  
* اختياري لكن يُنصح به: `pip install pillow` لمعالجة الصور وأي تبعيات إضافية تحتاجها مكتبة OCR الخاصة بك.

إذا كنت تفتقد أيًا من هذه المتطلبات، قم بتثبيتها الآن—بدون عناء، فهي سطر واحد لمعظم الحزم.

---

## تحليل الفواتير باستخدام OCR – الخطوة 1: تثبيت واستيراد الوحدات المطلوبة

أولًا، لنجهز بيئة بايثون. سنستورد `json` للتسلسل وفئات OCR الخاصة.

```python
# Step 1: Import required modules
import json                     # Built‑in JSON handling
from ocr_library import OcrEngine, Image   # Replace with your actual library
```

*لماذا هذا مهم*: الاستيراد في أعلى الملف يبقي السكريبت منظمًا ويضمن توفر محرك OCR طوال الوقت. إذا نسيت استيراد `json`، ستفشل الدالة `json.dumps` لاحقًا مع خطأ `NameError`.

**نصيحة احترافية**: إذا كانت مكتبة OCR الخاصة بك تحت مساحة اسم مختلفة (مثل `easyocr` أو `pytesseract`)، عدل سطر الاستيراد وفقًا لذلك. باقي الدرس يبقى كما هو.

---

## كيفية استخراج بيانات الفاتورة – الخطوة 2: إنشاء نسخة من محرك OCR

الآن نقوم بتشغيل المحرك. فكر في `OcrEngine()` كالعقل الذي سيقرأ الفاتورة.

```python
# Step 2: Create an OCR engine instance
engine = OcrEngine()
```

معظم SDKs الحديثة لـ OCR تسمح لك بتكوين حزم اللغات أو أوضاع الكشف هنا. لفاتورة نموذجية ستحتاج إلى الإنجليزية (أو لغة الفاتورة) ووضع “structured” إذا كان متاحًا.

> **ملاحظة**: إذا كانت مكتبتك تتطلب مفتاح ترخيص، مرره كمعامل: `engine = OcrEngine(api_key="YOUR_KEY")`.

---

## تحميل صورة OCR – الخطوة 3: توجيه المحرك إلى فاتورتك

مع جاهزية المحرك، نحتاج إلى إمداده بملف الصورة. هنا يأتي دور **load image OCR**.

```python
# Step 3: Load the image to be processed
engine.set_image(Image.from_file("YOUR_DIRECTORY/receipt.png"))
```

*ما يحدث*: `Image.from_file` يقرأ ملف PNG (أو JPG، TIFF، إلخ) ويغلفه بصيغة يفهمها محرك OCR. إذا كان الفاتورة PDF، حوّل الصفحة الأولى إلى صورة أولًا—العديد من المكتبات توفر مساعد `pdf2image`.

**حالة حافة**: الفواتير الممسوحة مقلوبة لا تزال قابلة للقراءة إذا قمت بتدويرها:

```python
# Optional: auto‑rotate if needed
image = Image.from_file("YOUR_DIRECTORY/receipt.png")
image = image.rotate(180) if image.is_upside_down() else image
engine.set_image(image)
```

---

## كيفية OCR الفاتورة – الخطوة 4: تشغيل التعرف على النص المهيكل

الآن يحدث السحر. نطلب من المحرك إجراء مسح مهيكل، يحاول تجميع العناصر، الإجماليات، والتواريخ.

```python
# Step 4: Perform structured text recognition
result = engine.recognize_structured()
```

إذا كانت مكتبة OCR الخاصة بك تقدم فقط طريقة `recognize()` العادية، يمكنك لا يزال استخراج الحقول يدويًا، لكن `recognize_structured()` غالبًا ما تُعيد قاموسًا يحتوي على مفاتيح مثل `items`، `total`، و `date`.

---

## مثال بايثون OCR – الخطوة 5: تحويل النتيجة إلى JSON

كائن النتيجة الخام عادةً ما يكون فئة مخصصة. تحويله إلى قاموس بايثون عادي يجعل عملية التسلسل سهلة.

```python
# Step 5: Convert the recognition result to a nicely formatted JSON string
json_str = json.dumps(result.to_dict(), ensure_ascii=False, indent=2)
```

*لماذا `ensure_ascii=False`؟* قد تحتوي الفواتير على رموز عملة (€، £) أو أحرف مُعَلَّمة. هذه العلامة تحافظ عليها بدلاً من تحويلها إلى `\u00e9`.

---

## كيفية استخراج الفاتورة – الخطوة 6: إخراج تمثيل JSON

أخيرًا، نطبع (أو نكتب) الـ JSON حتى تتمكن من توجيهه إلى قاعدة بيانات، جدول بيانات، أو API.

```python
# Step 6: Output the JSON representation of the recognized data
print(json_str)
```

**الناتج المتوقع** (منسق للقراءة):

```json
{
  "merchant": "Coffee House",
  "date": "2024-03-15",
  "items": [
    {"name": "Latte", "quantity": 1, "price": "3.50"},
    {"name": "Bagel", "quantity": 2, "price": "4.00"}
  ],
  "subtotal": "7.50",
  "tax": "0.60",
  "total": "8.10"
}
```

إذا رأيت قاموسًا فارغًا أو حقولًا مفقودة، تحقق من وضوح صورة الفاتورة وأن محرك OCR مضبوط على اللغة الصحيحة.

---

## نصائح احترافية ومشكلات شائعة (قسم إضافي)

| المشكلة | لماذا يحدث | الحل السريع |
|-------|----------------|-----------|
| **صورة غير واضحة أو ذات تباين منخفض** | OCR يواجه صعوبة مع الضوضاء | عالج مسبقًا باستخدام OpenCV: `cv2.threshold` أو `cv2.bilateralFilter` |
| **فاتورة مائلة** | المحرك يفترض نصًا عموديًا | اكتشف الاتجاه باستخدام `engine.detect_orientation()` أو دوّر يدويًا (انظر الخطوة 3) |
| **حروف غير لاتينية** | حزمة اللغة غير صحيحة | ابدأ المحرك بـ `language="spa"` للإسبانية، إلخ. |
| **فواتير كبيرة تسبب خطأ في الذاكرة** | تحميل الصورة بالكامل مرة واحدة | قص إلى منطقة الاهتمام: `engine.set_image(image.crop((x, y, w, h)))` |

---

## ما التالي؟ توسيع سير العمل

لقد أتقنت الآن **تحليل الفواتير باستخدام OCR** في بايثون. إليك بعض الأفكار لاستمرار التطور:

* **المعالجة الدفعية** – كرر عبر مجلد من صور الفواتير وأضف كل JSON إلى ملف رئيسي.  
* **إدخال قاعدة البيانات** – استخدم `sqlite3` أو `SQLAlchemy` لتخزين كل فاتورة كسطر.  
* **إثراء تعلم الآلة** – اغذِ العناصر المستخرجة إلى نموذج تصنيف لتوسيم النفقات.  

جميع هذه الأفكار تبني على الخطوات الأساسية التي غطيناها، وكلها ستتبع نمط **python ocr example** نفسه: تحميل → التعرف → التسلسل → التخزين.

---

## الخلاصة

في هذا الدليل استعرضنا سير عمل كامل لـ **تحليل الفواتير باستخدام OCR** في بايثون، موضحين بالضبط **كيفية استخراج بيانات الفاتورة**، وكيفية **load image OCR**، وقدّمنا مثالًا عمليًا **python ocr example** يمكنك تشغيله اليوم. باتباع الخطوات الستة—التثبيت، الاستيراد، الإنشاء، التحميل، التعرف، والتسلسل—أصبح لديك أساس قوي لأي مشروع معالجة فواتير.

لا تتردد في التجربة: جرّب محركات OCR مختلفة، عدّل المعالجة المسبقة، أو أضف معالجة الأخطاء للحقول المفقودة. السماء هي الحد عندما تجمع بين OCR موثوق وبايثون مرن. لديك أسئلة أو تعديل مميز على هذه الوصفة؟ اترك تعليقًا أدناه ولنستمر في النقاش.

Happy coding!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}