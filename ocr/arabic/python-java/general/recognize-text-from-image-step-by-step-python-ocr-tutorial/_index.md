---
category: general
date: 2026-03-26
description: تعرّف على النص من الصورة بسرعة من خلال تعلم كيفية تحميل الصورة للتعرف
  الضوئي على الأحرف واستخراج البيانات من منطقة محددة. اتبع هذا الدليل العملي.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: ar
og_description: التعرف على النص من صورة في بايثون عن طريق تحميل الصورة للتعرف الضوئي
  على الأحرف، تحديد منطقة الاهتمام، واستخراج نص نظيف. تعلّم سير العمل الكامل.
og_title: التعرف على النص من الصورة – دليل شامل لتقنية OCR باستخدام بايثون
tags:
- OCR
- Python
- Image Processing
title: التعرف على النص من الصورة – دليل OCR خطوة بخطوة باستخدام بايثون
url: /ar/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة – دليل Python OCR كامل

هل احتجت يوماً إلى **التعرف على النص من الصورة** لكن لم تعرف من أين تبدأ؟ ربما لديك نموذج ممسوح ضوئياً، أو إيصال، أو لقطة شاشة وتريد فقط الكلمات داخل صندوق معين. الخبر السار هو أنه ببضع أسطر من Python يمكنك تحميل الصورة للـ OCR، التركيز على منطقة واحدة، واستخراج النص الدقيق الذي تحتاجه—دون الحاجة إلى النسخ اليدوي.

في هذا الدرس سنستعرض العملية بالكامل: تحميل الصورة، تعريف منطقة الاهتمام (ROI)، تشغيل محرك الـ OCR، وطباعة النتيجة. في النهاية ستتمكن من دمج هذا المقتطف في أي مشروع يحتاج إلى استخراج نص من جزء محدد من صورة. لا تحتاج إلى خطوط معالجة صور معقدة، فقط كود نظيف وقابل للقراءة يعمل الآن.

## المتطلبات المسبقة

- تثبيت Python 3.8+  
- حزمة `ocr` (أو أي مكتبة OCR متوافقة) – تثبيت عبر `pip install ocr-lib` (استبدل باسم الحزمة الفعلية التي تستخدمها)  
- صورة PNG/JPEG تحتوي على النموذج الذي تريد قراءته  
- إلمام أساسي بدوال وفئات Python  

إذا كنت مرتاحاً مع هذه المتطلبات، رائع—يمكنك المتابعة مباشرة. وإلا، خذ فنجان قهوة سريع وتأكد من جاهزية العناصر أعلاه؛ الخطوات التالية تفترض توافرها.

## الخطوة 1: إنشاء كائن محرك OCR – نواة “التعرف على النص من الصورة”

أول شيء نحتاجه هو كائن يعرف كيف يتواصل مع محرك الـ OCR. فكر فيه كالعقل الذي سيقوم لاحقاً **بالتعرف على النص من الصورة**.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** تهيئة المحرك مرة واحدة تسمح لك بإعادة استخدام الإعدادات (مثل حزم اللغات) عبر صور متعددة، ما يحسن الأداء ويحافظ على نظافة الكود.

## الخطوة 2: تحميل الصورة للـ OCR – جلب الصورة إلى الذاكرة

الآن نقوم فعلياً **بتحميل الصورة للـ OCR**. توفر المكتبة طريقة ثابتة مريحة تقرأ الملف وتعيد كائنًا يمكن للمحرك فهمه.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **نصيحة احترافية:** إذا كانت صورتك كبيرة، فكر في تصغير حجمها قبل التحميل. الصور الأصغر تسرّع الـ OCR دون التضحية بالدقة لمعظم النصوص المطبوعة.

## الخطوة 3: تعريف منطقة الاهتمام للـ OCR (ROI)

غالباً لا تحتاج إلى الصفحة بأكملها—فقط صندوق محدد حيث أدخل المستخدم البيانات. تعريف **منطقة اهتمام الـ OCR** يخبر المحرك بتجاهل كل ما هو خارجها، ما يقلل الضوضاء ويسرّع المعالجة.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **لماذا التركيز على ROI؟**  
> - **السرعة:** المحرك يفحص عددًا أقل من البكسلات.  
> - **الدقة:** الرسومات الخلفية خارج ROI قد تشوش على التعرف على الأحرف.  
> - **البساطة:** تحصل على سلسلة نظيفة تتطابق تمامًا مع الحقل الذي يهمك.

## الخطوة 4: تشغيل عملية الـ OCR – لحظة الحقيقة

بعد إعداد كل شيء، ن finally **نتعرف على النص من الصورة** داخل ROI المحدد.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

إذا كان المحرك يدعم مناطق متعددة، فإن `ocr_result` سيحتوي على قائمة؛ في حالتنا ذات الـ ROI الواحدة يكون كائنًا بسيطًا يحتوي على طريقة `get_text()`.

## الخطوة 5: استخراج النص وطبع النتيجة – الحصول على المخرجات النهائية

الآن نستخرج السلسلة النصية من كائن النتيجة ونعرضها. هنا يمكنك ربط المخرجات بقاعدة بيانات، ملف CSV، أو أي منطق لاحق.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**المخرجات المتوقعة** (مثال لحقل اسم مملوء):

```
Text inside ROI:
 John Doe
```

إذا أعاد محرك الـ OCR مسافات أو فواصل سطر إضافية، يمكنك تنظيفها باستخدام `.strip()` أو تعبير نمطي.

## التعامل مع الحالات الشائعة

| الحالة                                 | ما الذي يجب فعله                                                       |
|----------------------------------------|------------------------------------------------------------------------|
| **صورة منخفضة الدقة**                  | قم بزيادة الدقة باستخدام `Pillow` (`Image.resize`) قبل التحميل.        |
| **نص مائل أو مدور**                    | طبّق تصحيح دوران (`ocr.Imaging.Image.rotate`).                        |
| **عدة لغات**                           | عيّن حزمة اللغة على المحرك: `ocr_engine.set_language('eng+spa')`.      |
| **عدم تعريف ROI**                     | تخطّ `add_region_of_interest`؛ سيعالج المحرك الصورة بالكامل.          |
| **حروف غير متوقعة (مثل الفواصل)**      | عالج السلسلة بعد الاستخراج: `extracted_text.replace(',', '')`.        |

هذه النصائح تجعل خط أنابيب **تحميل الصورة للـ OCR** قويًا حتى عندما لا تكون المادة المصدرية مثالية.

## مثال كامل يعمل – انسخ، الصق، شغّل

فيما يلي السكربت الكامل الذي يمكنك وضعه في ملف `.py` وتشغيله. يتضمن جميع الاستيرادات، معالجة الأخطاء، ومساعد صغير يتحقق من وجود الصورة.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

تشغيل هذا السكربت يطبع السلسلة المنقحة من ROI، لتمنحك قطعة بيانات جاهزة للاستخدام.

## الخلاصة

أصبح لديك الآن طريقة واضحة من البداية إلى النهاية **للتعرف على النص من الصورة** عبر **تحميل الصورة للـ OCR**، تعريف **منطقة اهتمام الـ OCR** بدقة، وأخيراً استخراج نص نظيف. النهج يعمل مع أي مكتبة OCR للـ Python تتبع النمط الموضح أعلاه، ويمكنك بسهولة توسيعه للتعامل مع عدة ROIs، لغات مختلفة، أو خطوات ما قبل المعالجة.

بعد ذلك، قد ترغب في استكشاف:

- **معالجة الصورة للـ OCR** (العتبة، إزالة الضوضاء) لتحسين الدقة على المسحات الضوضائية.  
- استخدام نتيجة **استخراج النص من ROI** لملء DataFrame من pandas لتحليل بيانات جماعي.  
- الانتقال إلى خدمة OCR سحابية (Google Vision، Azure Computer Vision) عندما تحتاج إلى موثوقية أعلى على نطاق واسع.

جرّبه، عدّل إحداثيات المستطيل لتتناسب مع نماذجك، وشاهد الأتمتة تعمل. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}