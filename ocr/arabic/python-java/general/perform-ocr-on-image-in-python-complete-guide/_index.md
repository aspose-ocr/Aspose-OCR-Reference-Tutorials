---
category: general
date: 2026-06-22
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون في
  بضع أسطر فقط. تعلّم كيفية تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص من
  ملف PNG، واستخدام محرك OCR بكفاءة.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: ar
og_description: قم بإجراء التعرف الضوئي على الأحرف (OCR) على الصورة بسرعة باستخدام
  بايثون. يوضح هذا الدرس كيفية تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على
  النص من ملف PNG، واستخدام محرك OCR بثقة.
og_title: إجراء التعرف الضوئي على الأحرف في صورة باستخدام بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام بايثون – دليل شامل
url: /ar/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تنفيذ OCR على صورة في بايثون – دليل كامل

هل احتجت يومًا إلى **تنفيذ OCR على صورة** لكنك توقفت عند السطر الأول من الكود؟ لست وحدك. في هذا الشرح سنوضح لك بالضبط كيف **تحمّل صورة لـ OCR**، وتُعدّ محرك **OCR خفيف الوزن**، وأخيرًا **تتعرف على النص من PNG** باستخدام عدد قليل من الأوامر.

سنغطي كل شيء من تثبيت المكتبة إلى تعديل القائمة البيضاء بحيث تُعالج الأرقام والحروف الكبيرة فقط. في النهاية ستحصل على سكريبت جاهز للتنفيذ يمكنك وضعه في أي مشروع—بدون غموض ولا إضافات غير ضرورية.

## ما ستتعلمه

- كيفية **استخدام محرك OCR** برمجياً في بايثون.  
- الخطوات الدقيقة لـ **تحميل صورة لـ OCR** من مجلد محلي.  
- لماذا وكيفية تقييد التعرف على مجموعة أحرف مخصصة.  
- كيفية **التعرف على النص من PNG** ومعالجة النتيجة بأمان.  

**المتطلبات المسبقة:** Python 3.7+ مُثبت، طرفية (Terminal) أنت مرتاح معها، وصورة (مثال: `serial-number.png`) تريد قراءتها. لا تحتاج إلى خبرة سابقة في OCR.

---

## تنفيذ OCR على صورة – تهيئة محرك OCR

أول شيء عليك فعله هو إنشاء نسخة من محرك OCR. فكر في المحرك كالعقل الذي سيحلل البكسلات ويحوّلها إلى أحرف.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*لماذا هذا مهم:* بدون محرك لا شيء يعالج الصورة. فئة `OcrEngine` تجمع كل الأعمال الثقيلة—المعالجة المسبقة، التجزئة، وتصنيف الأحرف—في كائن واحد يمكنك إعادة استخدامه.

---

## تحميل صورة لـ OCR – توفير ملف PNG

الآن بعد أن أصبح المحرك موجودًا، تحتاج إلى إمداده بالصورة التي تريد قراءتها. المكتبة تتوقع كائن `ImageStream`، والذي يمكنك إنشاؤه مباشرةً من مسار الملف.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*نصيحة احترافية:* احفظ الصورة بصيغة ذات تباين عالي (نص أسود على خلفية بيضاء) وتجنب عيوب الضغط؛ فهذه العيوب قد تُعطّل خوارزمية OCR.

---

## تقييد الأحرف – القائمة البيضاء للأرقام والحروف الكبيرة

غالبًا ما يهمك فقط مجموعة فرعية من الأحرف—مثلاً رقم تسلسلي يحتوي على A‑Z و0‑9 فقط. بتحديد قائمة بيضاء تخبر المحرك بتجاهل كل ما هو آخر، مما يحسّن الدقة بشكل كبير.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*ما الذي يحدث في الخلفية؟* يبني المحرك مرشحًا يتخلص من أي رموز غير موجودة في القائمة البيضاء قبل مرحلة التصنيف النهائية. هذا مفيد خصوصًا عندما تحتوي الصورة على ضوضاء أو نص زخرفي لا تحتاجه.

---

## التعرف على النص من PNG – تشغيل عملية OCR

مع تحضير المحرك وتحميل الصورة، يمكنك أخيرًا **تنفيذ OCR على صورة**. استدعاء `recognize()` يُشغّل الخط الأنابيب الكامل ويعيد كائن نتيجة.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

إذا كنت مهتمًا بالأداء، فإن الطريقة عادةً ما تنتهي خلال بضع مئات من المللي ثانية لصورة PNG بحجم 300 × 200 بيكسل على حاسوب محمول حديث.

---

## الإخراج والتحقق – الحصول على النص المعترف به

الخطوة الأخيرة هي استخراج النص الصافي من كائن النتيجة. أي شيء لم يطابق القائمة البيضاء يُحذف تلقائيًا، فتُحصل على سلسلة نظيفة جاهزة للمعالجة الإضافية.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*الإخراج النموذجي:* `AB12C3D4E5` (بافتراض أن الصورة تحتوي على هذا الرقم التسلسلي بالضبط).  

إذا كان الإخراج فارغًا أو مشوّهًا، تحقق من جودة الصورة والقائمة البيضاء؛ فخطأ شائع هو حذف أحرف ضرورية عن طريق الخطأ.

---

## الحالات الخاصة والأخطاء الشائعة

| الحالة | ما الذي يجب التحقق منه | الحل المقترح |
|-----------|---------------|---------------|
| **الملف غير موجود** | خطأ إملائي في المسار أو ملف مفقود | استخدم `os.path.abspath` للتحقق من المسار الكامل قبل استدعاء `set_image`. |
| **صورة منخفضة التباين** | النص يندمج مع الخلفية | طبّق عتبة بسيطة (`Pillow` أو `OpenCV`) قبل تمرير الصورة إلى المحرك. |
| **أحرف غير متوقعة** | القائمة البيضاء مقيدة جدًا | أضف الأحرف المفقودة إلى سلسلة القائمة البيضاء. |
| **صور كبيرة** | بطء في التعرف | قلل حجم الصورة إلى أقصى عرض 1024 بيكسل؛ عادةً ما تظل جودة OCR عالية. |

---

## السكريبت الكامل – جاهز للتنفيذ

فيما يلي السكريبت الكامل المستقل الذي يجمع جميع الأجزاء معًا. احفظه باسم `ocr_demo.py`، استبدل `YOUR_DIRECTORY` بالمجلد الفعلي، ثم شغّله بـ `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*الإخراج المتوقع في الطرفية* (عندما يحتوي PNG على `SN12345`):

```
Recognized text: SN12345
```

---

## الخلاصة

أنت الآن تعرف بالضبط كيف **تنفّذ OCR على صورة** في بايثون، من **تحميل صورة لـ OCR** إلى **التعرف على النص من PNG** وأخيرًا استخراج نتيجة نظيفة باستخدام **محرك OCR** قابل للتخصيص. النهج بسيط، قابل للتوسيع، ويعمل مباشرةً لمعظم عمليات المسح التي تشبه الأرقام التسلسلية.

ما الخطوة التالية؟ جرّب استبدال القائمة البيضاء بحروف صغيرة، أو جرب صيغ صور مختلفة (JPEG، BMP)، أو دمج السكريبت في خط معالجة دفعي. النمط نفسه—محرك → صورة → إعدادات → تعرف → إخراج—ينطبق على أي مهمة OCR ستواجهها.

هل لديك أسئلة أو صورة غريبة ترفض التعاون؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة! 

![مخطط يوضح خطوات تنفيذ OCR على صورة باستخدام بايثون](https://example.com/ocr-flow.png "مخطط يوضح كيفية تنفيذ OCR على صورة باستخدام محرك OCR بايثون")


## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف طرق تنفيذ بديلة في مشاريعك.

- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [كيفية استخدام AspOCR: مرشحات ما قبل معالجة صورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [كيفية استخراج النص من صورة عبر إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}