---
category: general
date: 2026-01-12
description: دورة بايثون لتقنية OCR تُظهر كيفية استخراج نص جدول من صورة. تعلم قراءة
  الجدول من الصورة واستخراج النص المحدد باستخدام Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: ar
og_description: دروس OCR بلغة بايثون تعلمك كيفية استخراج نص الجدول من صورة، قراءة
  الجدول من الصورة واستخراج النص المحدد باستخدام Aspose OCR.
og_title: 'دورة OCR بايثون: استخراج نص الجدول من الصور'
tags:
- OCR
- Python
- AsposeOCR
title: 'دورة OCR بايثون: استخراج نص الجدول من الصور'
url: /ar/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR بلغة بايثون: استخراج نص الجدول من الصور

هل احتجت يومًا إلى **python ocr tutorial** يوضح لك فعليًا كيفية استخراج جدول من نموذج ممسوح ضوئيًا؟ لست وحدك. معظم الدروس تتوقف عند استخراج النص العام، مما يتركك تتساءل كيف تعزل شبكة البيانات التي تهمك.

في هذا الدليل سنستعرض سيناريو واقعي: قراءة جدول من صورة، استخراج النص المحدد الذي تحتاجه فقط، ثم طباعة النتائج. على طول الطريق سنضيف نصائح حول **how to extract table** بشكل موثوق، حتى لا تضطر إلى إعادة اختراع العجلة في كل مرة.

## ما ستتعلمه

- كيفية إعداد Aspose OCR للغة بايثون.
- كيفية تعريف منطقة مستطيلة تحتوي على جدول.
- الخطوات الدقيقة لـ **extract table text** و **read table from image**.
- نصائح للتعامل مع لغات متعددة أو تخطيطات جداول غير منتظمة.
- سكريبت كامل قابل للتنفيذ يمكنك إدراجه في مشروعك اليوم.

**المتطلبات المسبقة**  
- Python 3.8 أو أحدث.  
- إلمام أساسي بمفاهيم OCR (ليس من الضروري أن تكون خبيرًا).  
- صورة PNG أو JPEG تحتوي على جدول واضح (سنسميها `form_with_table.png`).  

إذا كان لديك كل ذلك، لنبدأ—بدون إطالة، فقط كود عملي.

![python ocr tutorial example of table region](table_region_example.png){alt="مثال على دليل OCR بايثون يوضح منطقة الجدول"}

## الخطوة 1: تثبيت واستيراد Aspose OCR

أولًا: تحتاج إلى مكتبة Aspose OCR. الحزمة موجودة على PyPI، لذا أمر `pip` واحد يكفي.

```bash
pip install aspose-ocr
```

الآن استورد الوحدة وأي مساعدات تحتاجها.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*نصيحة محترف:* احفظ تبعياتك في ملف `requirements.txt`. هذا يجعل إعادة إنشاء البيئة أمرًا سهلًا.

## الخطوة 2: تهيئة محرك OCR (نواة دليل OCR بايثون)

إنشاء المحرك هو قلب أي **python ocr tutorial**. هنا نضبط اللغة الافتراضية إلى الإنجليزية—يمكنك تغييرها لاحقًا.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

لماذا نضبط اللغة؟ دقة OCR يمكن أن ترتفع بشكل كبير عندما يعرف المحرك الأحرف المتوقعة. إذا كنت تتعامل مع نماذج متعددة اللغات، يمكنك إما تحديد قائمة باللغات أو تجاوزها لكل منطقة (انظر لاحقًا).

## الخطوة 3: تحميل الصورة الخاصة بك

Aspose OCR يعمل مع معظم صيغ الصور الشائعة. فقط أشِر إلى مسار الملف، وستحصل على كائن `Image` جاهز للمعالجة.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*حالة حافة:* الصور الكبيرة (أكثر من 5 ميغابايت) قد تبطئ المعالجة. فكر في تغيير حجمها أو ضغطها قبل OCR إذا أصبحت الأداء مشكلة.

## الخطوة 4: تعريف منطقة الجدول (قراءة جدول من صورة)

الآن يأتي الجزء الممتع: إخبار المحرك *أين* يقع الجدول. تزود المحرك بـ `OcrRegion` يحتوي على `Rectangle` (x, y, العرض, الارتفاع). الإحداثيات بوحدات البكسل، لذا قد تحتاج إلى تجربة قليلة.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

لماذا نستخدم منطقة؟ بتحديد OCR على مساحة الجدول فقط، نحن **extract selected text** أسرع ونتجنب الضوضاء من الملصقات أو الرسومات المحيطة. كما أن ذلك يحسن الدقة لأن المحرك يركز على تخطيط موحد.

## الخطوة 5: تشغيل OCR على المنطقة المحددة

بعد ضبط المنطقة، نستدعي `process_region`. تُعيد الطريقة كائن `OcrResult` يحتوي على النص الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

إذا كنت تحتاج لاستخراج جداول متعددة، ببساطة كرّر الخطوتين 4‑5 مع مستطيلات مختلفة.

## الخطوة 6: إخراج نص الجدول المستخرج

أخيرًا، اطبع—أو احفظ—التمثيل النصي للجدول. Aspose OCR يُعيد نصًا عاديًا مع فواصل أسطر عادةً ما تتطابق مع الصفوف، مما يجعل المعالجة اللاحقة بسيطة.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**الناتج المتوقع** (مثال):

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

يمكنك الآن تمرير هذه السلسلة إلى محللات `csv`، أو DataFrames في pandas، أو أي خط أنابيب تحليلي لاحق.

## مثال كامل يعمل

نجمع كل ما سبق في سكريبت كامل يمكنك تشغيله فورًا. استبدل `YOUR_DIRECTORY/form_with_table.png` بالمسار الفعلي لصورتك.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

شغّل السكريبت باستخدام `python extract_table.py`. إذا كان كل شيء مضبوطًا، سترى الجدول يُطبع في وحدة التحكم.

## أسئلة شائعة وتعامل مع حالات الحافة

**ماذا لو لم يكن الجدول مستطيلًا تمامًا؟**  
يمكنك تقسيم الجدول إلى مناطق متداخلة متعددة أو استخدام مستطيل أكبر يغطي كامل المنطقة ثم معالجة النص لاحقًا (مثلاً، التقسيم حسب فواصل الأسطر).

**هل يمكن استخراج أعمدة محددة فقط؟**  
بعد حصولك على النص الكامل للجدول، استخدم `csv` أو `pandas` لتقطيع الأعمدة التي تهمك. خطوة OCR نفسها تُعيد كل ما داخل المستطيل.

**كيف أتعامل مع جداول غير إنجليزية؟**  
اضبط `ocr_engine.language` (أو `region.language`) إلى الـ enum المناسب، مثل `ocr.Language.FRENCH` أو دمج لغات متعددة باستخدام `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**هل يمكن الحصول على إطارات حدود لكل خلية؟**  
Aspose OCR يمكنه إرجاع `region_result.words` حيث يحتوي كل كلمة على إطارات حدود. سيتعين عليك ربط هذه الإطارات بشبكة—مفيد للتحليل المتقدم للتخطيط.

## نصائح لتحسين الدقة

- **نظّف الصورة**: قم بعملية ثنائيات أو زيادة التباين قبل تمريرها إلى OCR. مكتبة Pillow يمكن أن تساعد.
- **تجنّب عيوب الضغط**: احفظ المسحات كملفات PNG عندما يكون ذلك ممكنًا.
- **انتبه إلى DPI**: 300 dpi هو المستوى المثالي؛ القيم الأقل قد تؤدي إلى فقدان أحرف.
- **جرّب أحجام مستطيلات مختلفة**: المستطيلات الأكبر قليلًا غالبًا ما تلتقط الأحرف المتناثرة التي تنتمي للجدول.

## الخطوات التالية

الآن بعد أن أتقنت **how to extract table** باستخدام Aspose OCR، يمكنك استكشاف:

- تحويل النص المستخرج إلى ملف CSV باستخدام وحدة `` في بايثون.
- إدخال البيانات في **pandas** DataFrame للتحليل.
- استخدام OCR لقراءة النماذج المكتوبة يدويًا (يتطلب محركًا مختلفًا أو تدريبًا إضافيًا).
- أتمتة معالجة دفعات من عشرات النماذج الممسوحة باستخدام حلقة `for` بسيطة.

كل هذه الامتدادات تبني على المفاهيم الأساسية التي غطيناها في هذا **python ocr tutorial**، لذا أنت في موقع جيد للتوسع.

---

*برمجة سعيدة! إذا واجهتك أي صعوبات، اترك تعليقًا أدناه—سأكون سعيدًا بمساعدتك على تحسين عملية الاستخراج.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}