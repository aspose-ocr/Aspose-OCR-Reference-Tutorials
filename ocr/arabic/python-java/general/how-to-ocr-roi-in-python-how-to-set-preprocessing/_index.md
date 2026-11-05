---
category: general
date: 2026-03-28
description: كيفية تنفيذ OCR لمنطقة الاهتمام (ROI) في بايثون – تعلّم كيفية ضبط خيارات
  ما قبل المعالجة لاستخراج نص دقيق من مناطق محددة في الصورة.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: ar
og_description: كيفية التعرف الضوئي على الأحرف (OCR) لمنطقة الاهتمام في بايثون – يوضح
  هذا الدليل كيفية إعداد المعالجة المسبقة لاستخراج النص بشكل موثوق من المناطق المحددة
  في الصورة.
og_title: كيفية التعرف الضوئي على الأحرف لمنطقة الاهتمام في بايثون – كيفية ضبط المعالجة
  المسبقة
tags:
- OCR
- Python
- Aspose
title: كيفية إجراء OCR على ROI في بايثون – كيفية ضبط المعالجة المسبقة
url: /ar/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية OCR ROI في بايثون – كيفية ضبط التحضير المسبق

هل تساءلت يومًا **كيفية OCR ROI** في صورة فاتورة مليئة بالضوضاء دون تحميل الصفحة بالكامل في الذاكرة؟ لست وحدك. في العديد من المشاريع الواقعية نحتاج فقط إلى عدد قليل من الحقول — اسم العميل، العنوان، الإجماليات — لذا فإن مسح المستند بالكامل يُعد مبالغة.  

الأخبار السارة؟ مع Aspose OCR يمكنك إخبار المحرك بالضبط **أين يبحث** وحتى إخبارها بتنظيف الصورة أولاً. في هذا الدرس سنستعرض **كيفية ضبط التحضير المسبق**، تعريف مناطق الاهتمام (ROIs)، واستخراج نص نظيف في بضع أسطر فقط من بايثون.

بنهاية هذا الدليل ستحصل على سكريبت جاهز للتنفيذ يستخراج كتل محددة من أي فاتورة أو إيصال أو نموذج. لا تحتاج إلى أدوات إضافية، فقط Aspose OCR وقليل من منطق بايثون.

---

## ما ستحتاجه

- **Python 3.8+** (الكود يعمل على أي نسخة حديثة)  
- **Aspose OCR for Python via .NET** – تثبيت باستخدام `pip install aspose-ocr`  
- صورة نموذجية (مثلاً `invoice.png`) موجودة في مجلد يمكنك الإشارة إليه  
- إلمام أساسي بدوال بايثون وصياغة الكائنات (object‑oriented syntax)  

إذا كان لديك هذه مسبقًا، رائع—لننتقل مباشرة إلى الكود.

![مخطط كيفية OCR ROI](ocr-roi.png "مثال على OCR ROI")

*نص بديل: مخطط يوضح كيفية OCR ROI مع صناديق ROI على صورة فاتورة*

---

## الخطوة 1 – تهيئة محرك OCR (How to OCR ROI)

قبل أن نتمكن من إخبار المحرك *أين* يبحث، نحتاج إلى نسخة من معالج OCR. هذا الكائن يحمل جميع الإعدادات ويقوم بتنفيذ عملية التعرف.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*لماذا هذا مهم*: فئة `OcrEngine` تُجرد الأعمال الثقيلة (اكتشاف الخطوط، تحليل التخطيط، إلخ). بإنشاء محرك واحد تتجنب إعادة تهيئة الموارد الثقيلة لكل صورة، مما يحافظ على سرعة الأداء.

---

## الخطوة 2 – تحميل صورة المصدر (How to OCR ROI)

تجعل Aspose Storage تحميل الصور سهلًا دون عناء. قم بتوجيهه إلى مسار الملف، وستحصل على كائن `Image` جاهز للمعالجة.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*نصيحة*: إذا كنت تتعامل مع تدفقات (مثل الصور المرفوعة عبر واجهة برمجة تطبيقات ويب)، يمكنك تمرير كائن `BytesIO` إلى `Image.load` بدلاً من مسار الملف.

---

## الخطوة 3 – تعريف مناطق الاهتمام (ROIs)

الآن نجيب على السؤال الأساسي **كيفية OCR ROI**: نخبر المحرك بالمستطيلات الدقيقة التي تحتوي على البيانات التي نهتم بها. كل ROI يُعرّف بزاويةه العلوية اليسرى (`x`, `y`) وحجمه (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*لماذا نستخدم ROIs؟*  
- **السرعة** – يتخطى المحرك الأجزاء غير ذات الصلة من الصورة.  
- **الدقة** – بالتركيز على مساحة صغيرة، لا يمكن للضوضاء في أماكن أخرى إرباك أداة التعرف.  
- **المرونة** – يمكنك إضافة عدد أي من ROIs حسب الحاجة؛ يعيد المحرك قائمة بالنتائج بنفس الترتيب.

---

## الخطوة 4 – كيفية ضبط التحضير المسبق لتحسين دقة OCR

الصور الملتقطة مباشرة من الماسحات الضوئية أو الهواتف غالبًا ما تعاني من الانحراف، انخفاض التباين، أو إضاءة غير متساوية. تقدم Aspose OCR كائن `PreprocessingOptions` الذي يتيح لك تفعيل الإصلاحات الشائعة قبل تشغيل عملية التعرف.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*كيف يساعد ذلك*:  
- **Deskew** يزيل الميل الذي يجعل أشكال الحروف غامضة.  
- **Binarize** يقلل من ضوضاء الألوان، مما يمنح محرك OCR صورة ثنائية نظيفة.  
- **Contrast** يعزز الخطوط الخفيفة، وهو مفيد بشكل خاص للإيصالات الباهتة.

يمكنك تجربة هذه العلامات — قم بإيقاف واحدة وانظر إذا تغير الناتج. هذه هي الفكرة وراء **كيفية ضبط التحضير المسبق** بفعالية.

---

## الخطوة 5 – تنفيذ OCR فقط داخل ROIs المحددة

مع وجود المحرك، الصورة، ROIs، والتحضير المسبق جاهزين، حان الوقت لاستدعاء `recognize`. تُعيد الطريقة كائن `OcrResult` يحتوي على مجموعة `regions` — كل إدخال يطابق ترتيب ROI الذي قدمناه.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*خلف الكواليس*: يقوم المحرك بقص كل ROI، يطبق خط أنابيب التحضير المسبق، ويشغل نموذج التعرف على المقتطف المنظف. لأننا مررنا قائمة، يحتفظ الناتج بنفس الترتيب، مما يجعل ما بعد المعالجة بسيطًا.

---

## الخطوة 6 – قراءة واستخدام النص المستخرج (How to OCR ROI)

أخيرًا، قم بالتكرار على قائمة `regions` واطبع — أو احفظ — السلاسل المعترف بها. كائن `Region` يعرض خاصية `text` التي تحمل النتيجة بصيغة Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**الناتج المتوقع (مثال)**:

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

إذا كان النص مشوشًا، أعد النظر في **كيفية ضبط التحضير المسبق**: ربما زيادة `contrast` أو إلغاء تفعيل `binarize` للشعارات الملونة.

---

## المشكلات الشائعة ونصائح الخبراء

| المشكلة | سبب حدوثها | الحل (كيفية ضبط التحضير المسبق) |
|-------|----------------|--------------------------------|
| النص المائل يظهر مشوشًا | `deskew` معطل أو الصورة مائلة جدًا | فعّل `preprocessing_options.deskew = True` |
| الأرقام تتحول إلى نقاط أو علامات عشوائية | انخفاض التباين أو تحويل ثنائي مفرط | قلل `contrast` (مثلاً `1.2`) أو اضبط `binarize = False` |
| إحداثيات ROI غير دقيقة ببضع بكسلات | دقة DPI مختلفة أو مقياس الماسح | استخدم أداة (مثل Paint.NET) لقياس المواقع الدقيقة بالبكسل، أو أضف هامشًا صغيرًا (`+5` بكسل) لكل ROI |
| نتيجة فارغة لمنطقة | ROI خارج حدود الصورة | تحقق من أبعاد الصورة: `source_image.width`, `source_image.height` |

---

## توسيع الحل (How to OCR ROI in Different Scenarios)

- **Dynamic ROIs**: إذا كانت فواتيرك ذات تخطيطات متغيرة، يمكنك أولاً تشغيل OCR سريع للصفحة بالكامل لتحديد الكلمات المفتاحية (“Customer:”, “Address:”) ثم حساب ROIs في الوقت الفعلي.  
- **Batch Processing**: غلف الخطوات السابقة في دالة وكررها على مجلد من الصور. تذكر إعادة استخدام نفس نسخة `ocr_engine` لتقليل استهلاك الذاكرة.  
- **Exporting to JSON**: بدلاً من الطباعة، أنشئ قاموسًا واستخدم `json.dumps` لتفريغه؛ هذا يجعل التكامل اللاحق (مثل تغذية نظام ERP) سهلًا.

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## الخلاصة

أصبح لديك الآن مثال كامل وقابل للتنفيذ يوضح **كيفية OCR ROI** في بايثون مع إتقان **كيفية ضبط التحضير المسبق** لتحقيق أقصى دقة. من خلال تقييد المحرك بالمستطيلات الدقيقة التي تهتم بها وتنظيف الصورة مسبقًا، ستحصل على نتائج أسرع وأكثر نظافة — مثالية لأتمتة الفواتير، رقمنة النماذج، أو أي سيناريو حيث يهم جزء فقط من الصفحة.

هل أنت مستعد للخطوة التالية؟ جرّب تعديل إحداثيات ROI لنوع مستند مختلف، أو جرب علامات تحضير مسبق إضافية مثل `sharpen` أو `noise_reduction`. مرونة Aspose OCR تعني أنك تستطيع تخصيص خط الأنابيب لأي جودة صورة تقريبًا.

إذا واجهت مشكلة، تحقق من مخرجات وحدة التحكم للمنطقات الفارغة وأعد النظر في إعدادات التحضير المسبق. برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}