---
category: general
date: 2026-03-26
description: 'دروس OCR بلغة بايثون: تعلم كيفية استخراج النص من الصورة، تحميل الصورة
  للتعرف الضوئي على الأحرف، والتعرف على النص من الفاتورة باستخدام Aspose OCR في بضع
  خطوات فقط.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: ar
og_description: 'دورة Python OCR: تعلم بسرعة استخراج النص من الصورة، تحميل الصورة
  للتعرف الضوئي على الأحرف، وتعرف على النص من الإيصال باستخدام Aspise OCR.'
og_title: دورة OCR في بايثون – استخراج النص من الصورة
tags:
- OCR
- Aspose
- Python
title: دورة OCR بايثون – استخراج النص من الصورة باستخدام Aspose
url: /ar/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# برنامج Python OCR – استخراج النص من صورة باستخدام Aspose

هل تساءلت يومًا كيف تستخرج النص من إيصال غير واضح أو نموذج ممسوح ضوئيًا دون قضاء ساعات في كتابة تعبيرات regex مخصصة؟ لست وحدك. في هذا **python ocr tutorial** سنستعرض تحميل صورة لـ OCR، تنفيذ OCR في Python، وأخيرًا التعرف على النص من ملفات الإيصالات باستخدام مكتبة Aspose OCR.  

بنهاية هذا الدليل ستحصل على سكربت جاهز للتنفيذ يقرأ أي صيغة صورة مدعومة، يستخرج المحتوى النصي، ويطبعه في وحدة التحكم. لا خدمات خارجية، لا مفاتيح API—فقط Python خالص ومحرك OCR قوي.  

## ما ستحتاجه

- Python 3.8 أو أحدث (الكود يستخدم تلميحات الأنواع، لذا يُفضَّل مفسّر حديث)
- حزمة `asposeocrjava` مثبتة عبر `pip install aspose-ocr`
- صورة نموذجية – على سبيل المثال `receipt_noisy.jpg` التي تحتوي على إيصال متجر نموذجي
- (اختياري) بيئة افتراضية للحفاظ على تنظيم الاعتمادات

إذا كنت قد تحققت من هذه المتطلبات، يمكننا القفز مباشرة إلى الكود.  

## الخطوة 1: تثبيت واستيراد فئات Aspose OCR

أولاً، تأكد من توفر حزمة Aspose OCR. ثم استورد الفئات التي سنحتاجها.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**لماذا هذا مهم:** استيراد الرموز الضرورية فقط يحافظ على نظافة مساحة الاسم ويُشير إلى المفسّر أي أجزاء المكتبة نستخدمها فعليًا. كما يُقصر أسطر الكود لاحقًا، مما يجعل الشرح أسهل للمتابعة.

> **نصيحة احترافية:** إذا كنت تستخدم دفتر Jupyter، أضف `!` قبل سطر التثبيت لتشغيله داخل الخلية.

## الخطوة 2: إنشاء محرك OCR وتفعيل وضع التعلم العميق

توفر Aspose عدة أوضاع للمحرك. بالنسبة لمعظم الإيصالات الواقعية، يوفر نموذج التعلم العميق أعلى دقة، خاصةً على المسحات الضوضائية.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**لماذا التعلم العميق؟** يمكن لتقنية OCR القائمة على القواعد التقليدية أن تتعثر مع الأحرف ذات التباين المنخفض أو المشوهة. نموذج التعلم العميق، المدرب على ملايين الرموز، يتكيف بشكل أفضل مع الاختلافات — وهذا بالضبط ما تحتاجه عندما *تجري OCR في Python* على الإيصالات الملتقطة بكاميرا الهاتف.

## الخطوة 3: تحميل الصورة لـ OCR

الآن نقوم فعليًا **بتحميل الصورة لـ OCR**. تدعم Aspose.Imaging صيغ PNG، JPEG، BMP، TIFF، وأكثر، لذا يمكنك توجيهها إلى أي صورة تقريبًا لوثيقة.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**خطأ شائع:** نسيان ضبط الصورة على المحرك يؤدي إلى حدوث `NullReferenceException` أثناء التشغيل. احرص دائمًا على استدعاء `set_image` بعد تحميل الملف.

## الخطوة 4: تنفيذ OCR واستخراج النص

مع تحضير المحرك وإرفاق الصورة، يمكننا أخيرًا **تنفيذ OCR في Python** واسترجاع النتيجة النصية.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

طريقة `recognize()` تُعيد كائن `OcrResult` الذي يحتوي ليس فقط على النص الخام بل أيضًا على درجات الثقة، ومربعات الإحاطة، ومعلومات اللغة. لحالة استخدام سريعة **استخراج النص من صورة** نحتاج فقط إلى `get_text()`.

## الخطوة 5: عرض النص المُعترف به

دعونا نرى ما قرأه المحرك فعليًا من الإيصال.

```python
print("Recognized text:\n", recognized_text)
```

المخرجات النموذجية تبدو كالتالي:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

إذا احتوت المخرجات على أحرف مشوشة، فكر في معالجة الصورة مسبقًا (مثل زيادة التباين أو تطبيق مرشح لتصحيح الميل) قبل تحميلها إلى محرك OCR. توفر Aspose.Imaging مجموعة كاملة من أدوات تحسين الصور يمكنك ربطها معًا.

## التعامل مع الحالات الخاصة ونصائح لتحسين الدقة

### 1. التعامل مع الإيصالات الضوضائية جدًا
إذا كان الإيصال ملطخًا بشدة، قد ترغب في التحويل إلى وضع `OcrEngineMode.HIGH_SPEED` للحصول على تمريرة أسرع، وإن كانت أقل دقة، ثم تشغيل تمريرة ثانية في `DEEP_LEARNING` على الصورة المُنقّاة.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. تحديد اللغة
بشكل افتراضي، تحاول Aspose اكتشاف اللغة تلقائيًا. بالنسبة لإيصالات اللغة الإنجليزية يمكنك تثبيتها يدويًا:

```python
ocr_engine.set_language("eng")
```

### 3. إدارة الذاكرة
عند معالجة العديد من الصور في حلقة، حرّر الموارد صراحةً:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. حفظ نتائج OCR إلى ملف
أحيانًا تحتاج إلى حفظ النص المستخرج للاستخدام لاحقًا في التحليل.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## مثال عملي كامل

فيما يلي السكربت الكامل الذي يجمع كل شيء معًا. انسخه والصقه في ملف باسم `receipt_ocr.py`، عدّل مسار الصورة، ثم شغّله باستخدام `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

تشغيل السكربت يجب أن يعرض محتويات الإيصال في وحدة التحكم الخاصة بك، كما سيُنشئ ملف `receipt_output.txt` بنفس البيانات.

![Python OCR tutorial – عينة مخرجات الإيصال](https://example.com/receipt_output.png "مثال python ocr tutorial")

*نص بديل للصورة:* **python ocr tutorial – sample receipt output**

## ملخص وخطوات مستقبلية

لقد استعرضنا للتو **python ocr tutorial** الذي يوضح كيفية **load image for OCR**، **perform OCR in Python**، وأخيرًا **recognize text from receipt** باستخدام Aspose. النقاط الرئيسية هي:

- اختر وضع المحرك المناسب (التعلم العميق للدقة)
- احرص دائمًا على إرفاق الصورة قبل استدعاء `recognize()`
- استخدم كائن `OcrResult` لاستخراج النص النظيف، ثم احفظه أو عالجه حسب الحاجة

ما التالي؟ فكر في ربط مرشحات Aspose Imaging لتحسين المسحات منخفضة التباين، أو دمج السكربت في واجهة Flask API لتتمكن من رفع الإيصالات عبر نموذج ويب. يمكنك أيضًا استكشاف تصدير بيانات OCR إلى CSV لأتمتة المحاسبة.

هل لديك أسئلة حول معالجة ملفات PDF متعددة الصفحات أو النصوص غير اللاتينية؟ اترك تعليقًا—سأكون سعيدًا بالمساعدة!  

**هل أنت مستعد للارتقاء بأتمتة مستنداتك؟** احصل على الكود، جرب صورًا مختلفة، ودع محرك OCR يقوم بالعمل الشاق. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}