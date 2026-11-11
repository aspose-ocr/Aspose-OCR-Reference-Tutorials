---
category: general
date: 2026-06-25
description: حمّل صورة للتعرف الضوئي على الأحرف وقم بتنفيذ التعرف الضوئي على الأحرف
  على ملف PNG باستخدام دليل Python خطوة بخطوة مع aocr. تعلم تصحيح الأخطاء وتسجيل الأحداث
  وأفضل الممارسات.
draft: false
keywords:
- load image for OCR
- perform OCR on PNG
- aocr logging setup
- OCR debugging Python
- image preprocessing OCR
language: ar
og_description: تحميل الصورة للتعرف الضوئي على الأحرف وتنفيذ التعرف الضوئي على الأحرف
  لملف PNG باستخدام aocr. يوضح هذا الدليل عملية التسجيل، تحميل الصورة، والتعرف مع
  الكود الكامل.
og_title: تحميل الصورة للتعرف الضوئي على الأحرف – دليل بايثون خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Load image for OCR and perform OCR on PNG with a step‑by‑step Python
    tutorial using aocr. Learn debugging, logging, and best practices.
  headline: Load Image for OCR – Complete Guide to Perform OCR on PNG Files
  type: TechArticle
- questions:
  - answer: Usually not. `aocr` handles PNG natively, but if the image is huge (>10
      MP) you might want to downscale first to speed up processing.
    question: Do I need to convert the PNG to another format?
  - answer: Rotate the log after each run or limit the level to `INFO` once you’re
      confident the pipeline works.
    question: What if the logger file grows too large?
  - answer: Absolutely. Just call `ocr_png` for each file; the function creates a
      fresh logger each time, keeping logs isolated.
    question: Can I process multiple images in a loop?
  - answer: Yes – `engine.result` also contains `boxes` and `confidences`. Explore
      the `aocr` docs for `result.boxes` if you need layout information.
    question: Is there a way to get bounding boxes instead of plain text?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: تحميل الصورة للتعرف الضوئي على الأحرف – دليل كامل لإجراء التعرف الضوئي على
  الأحرف على ملفات PNG
url: /ar/python/general/load-image-for-ocr-complete-guide-to-perform-ocr-on-png-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحميل صورة لإجراء OCR – دليل شامل لأداء OCR على ملفات PNG

هل احتجت يوماً إلى **تحميل صورة لإجراء OCR** لكنك لم تكن متأكدًا من طريقة إعداد التصحيح المناسب؟ لست وحدك. في العديد من المشاريع، العائق الأول هو إدخال ملف PNG إلى المحرك مع القدرة على رؤية ما يحدث تحت الغطاء.

في هذا الدرس سنرشدك خطوة بخطوة إلى كل ما تحتاجه **لأداء OCR على PNG** باستخدام مكتبة `aocr` – من إعداد مسجل (logger) للحصول على مخرجات مفصلة إلى التعرف الفعلي على النص. بنهاية الدرس ستحصل على سكريبت قابل لإعادة الاستخدام يمكنك وضعه في أي مشروع Python، وستفهم لماذا كل جزء مهم.

## ما ستتعلمه

- كيفية تهيئة مسجل `aocr` لتتبع كل خطوة.
- الكود الدقيق **لتحميل صورة لإجراء OCR** باستخدام `aocr.OcrEngine`.
- كيفية ضبط مستوى التسجيل للحصول على معلومات تصحيح دقيقة.
- تشغيل المحرك **لأداء OCR على PNG** واسترجاع النتائج.
- نصائح للتعامل مع المشكلات الشائعة مثل الملفات المفقودة أو الصيغ غير المدعومة.

لا تحتاج إلى خبرة سابقة مع `aocr`؛ فقط تثبيت Python 3 يعمل وصورة تريد قراءتها. لنبدأ.

![مثال تحميل صورة لإجراء OCR](assets/load-image-ocr.png "توضيح تحميل صورة لإجراء OCR في Python")

## المتطلبات المسبقة

| المتطلب | لماذا هو مهم |
|-------------|----------------|
| Python 3.8+ | تستهدف `aocr` المفسرات الحديثة وتستخدم تلميحات النوع. |
| مكتبة `aocr` مثبتة (`pip install aocr`) | بدون الحزمة لن تكون الفئات التي نستخدمها موجودة. |
| صورة PNG تريد قراءتها | يركز الدرس على **أداء OCR على PNG**، لذا فإن PNG ضروري. |
| صلاحية كتابة إلى دليل السجلات | يحتاج المسجل لإنشاء `ocr_debug.log`. |

إذا كان أي من هذه غير متوفر، قم بتثبيته الآن – يستغرق الأمر دقيقة واحدة فقط.

```bash
pip install aocr
```

## الخطوة 1: تحميل صورة لإجراء OCR – تهيئة التسجيل

قبل أن تلمس الصورة، قم بإعداد مسجل. تصحيح أخطاء OCR قد يكون كابوسًا إذا كنت غير قادر على رؤية ما يفعله المحرك. فئة `aocr.Logging` تكتب كل شيء إلى ملف، وبضبط المستوى إلى `DEBUG` ستظهر لك كل استدعاء داخلي.

```python
import aocr

# Create a logger instance
ocr_logger = aocr.Logging()
# Choose where the log file will live – adjust the path to suit your project
ocr_logger.set_output_file("logs/ocr_debug.log")

# DEBUG gives you the most detail; you can switch to INFO for less noise
ocr_logger.set_level(aocr.LoggingLevel.DEBUG)
```

**لماذا هذا مهم:**  
إذا لم يتمكن محرك OCR من العثور على الملف أو كان تنسيق الصورة غير مدعوم، سيسجل المسجل تتبع الاستثناء. هذا يوفر عليك التخمين المستمر لاحقًا.

## الخطوة 2: أداء OCR على PNG – ضبط المحرك

الآن بعد أن أصبح المسجل جاهزًا، اربطه بمحرك OCR. هذه الخطوة تربط الاثنين معًا بحيث يتم تسجيل كل فعل للمحرك.

```python
# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
# Plug the logger into the engine
ocr_engine.logging = ocr_logger
```

**نصيحة احترافية:**  
يمكنك إعادة استخدام نفس كائن `ocr_engine` لعدة صور. فقط تذكر مسح أي حالة سابقة إذا كنت تعالج دفعة من الصور.

## الخطوة 3: تحميل صورة لإجراء OCR – إمداد ملف PNG

هذا هو جوهر الدرس: **تحميل صورة لإجراء OCR** فعليًا. طريقة `load_image` تقبل مسار الملف؛ وستقوم داخليًا بفك تشفير PNG إلى bitmap يمكن للمحرك فهمه.

```python
# Path to the PNG you want to read
image_path = "samples/invoice.png"

# Load the image – this is where we “load image for OCR”
ocr_engine.load_image(image_path)
```

### حالات حافة يجب مراقبتها

1. **الملف غير موجود** – إذا كان المسار خاطئًا، ترفع `aocr` استثناء `FileNotFoundError`. سيسجل المسجل ذلك، لكن يمكنك أيضًا التقاطه:

   ```python
   try:
       ocr_engine.load_image(image_path)
   except FileNotFoundError as e:
       print(f"❌ Could not locate {image_path}: {e}")
       raise
   ```

2. **صيغة غير مدعومة** – رغم أن PNG مدعومة على نطاق واسع، قد يتسبب ملف تالف في رفع `UnsupportedFormatError`. في هذه الحالة، فكر في تحويل الصورة إلى PNG نظيفة باستخدام Pillow قبل التحميل.

## الخطوة 4: أداء OCR على PNG – تشغيل التعرف

الآن بعد أن أصبحت الصورة في الذاكرة، يمكنك أخيرًا **أداء OCR على PNG**. طريقة `recognize` تشغل خطوط أنابيب المحرك (المعالجة المسبقة، التجزئة، التصنيف) وتملأ كائن النتيجة.

```python
# Execute the OCR process
ocr_engine.recognize()
```

بعد هذه الاستدعاء، يحتفظ المحرك بالنص المعترف به. يمكنك الوصول إليه عبر الخاصية `result`:

```python
# Retrieve the plain text output
recognized_text = ocr_engine.result.text
print("📝 OCR Result:")
print(recognized_text)
```

**لماذا يجب فحص النتيجة:**  
بعض محركات OCR تُعيد سلاسل فارغة للصور ذات التباين المنخفض. رؤية النتيجة فورًا تسمح لك بتحديد ما إذا كنت بحاجة إلى معالجة مسبقة (مثل زيادة التباين) قبل إعادة التشغيل.

## الخطوة 5: تجميع كل شيء – دالة قابلة لإعادة الاستخدام

دمج الأجزاء في دالة واحدة يجعل من السهل استدعاؤها من سكريبتات أخرى أو خدمة ويب. هذا أيضًا يوضح كيفية **تحميل صورة لإجراء OCR** و**أداء OCR على PNG** في حزمة واحدة منظمة.

```python
def ocr_png(image_path: str, log_dir: str = "logs") -> str:
    """
    Load a PNG image, run aocr OCR, and return the extracted text.
    
    Parameters
    ----------
    image_path : str
        Full path to the PNG file.
    log_dir : str, optional
        Directory where the debug log will be written.
    
    Returns
    -------
    str
        The plain‑text OCR result.
    """
    import os
    import aocr

    # Ensure the log directory exists
    os.makedirs(log_dir, exist_ok=True)

    # ---------- Logging ----------
    logger = aocr.Logging()
    logger.set_output_file(os.path.join(log_dir, "ocr_debug.log"))
    logger.set_level(aocr.LoggingLevel.DEBUG)

    # ---------- Engine ----------
    engine = aocr.OcrEngine()
    engine.logging = logger

    # ---------- Load Image ----------
    try:
        engine.load_image(image_path)
    except Exception as exc:
        logger.error(f"Failed to load image {image_path}: {exc}")
        raise

    # ---------- Recognize ----------
    engine.recognize()
    return engine.result.text

# Example usage
if __name__ == "__main__":
    txt = ocr_png("samples/invoice.png")
    print("\n--- Extracted Text ---\n")
    print(txt)
```

تشغيل السكريبت سينتج ملف `ocr_debug.log` مفصل في مجلد `logs`، ثم يطبع النص المعترف به إلى وحدة التحكم. الآن لديك أداة **أداء OCR على PNG** يمكنك استيرادها في أي مكان.

## أسئلة شائعة ومشكلات محتملة

- **هل أحتاج إلى تحويل PNG إلى صيغة أخرى؟**  
  عادة لا. `aocr` تتعامل مع PNG أصلاً، لكن إذا كانت الصورة ضخمة (>10 MP) قد ترغب في تقليل حجمها أولًا لتسريع المعالجة.

- **ماذا لو نما ملف السجل كثيرًا؟**  
  قم بتدوير السجل بعد كل تشغيل أو قلل المستوى إلى `INFO` بمجرد أن تكون واثقًا من عمل الخط الأنابيب.

- **هل يمكنني معالجة عدة صور في حلقة؟**  
  بالتأكيد. فقط استدعِ `ocr_png` لكل ملف؛ الدالة تنشئ مسجلًا جديدًا في كل مرة، مما يحافظ على عزل السجلات.

- **هل هناك طريقة للحصول على الصناديق المحيطة بدلاً من النص العادي؟**  
  نعم – `engine.result` يحتوي أيضًا على `boxes` و `confidences`. استكشف توثيق `aocr` للخاصية `result.boxes` إذا كنت تحتاج معلومات تخطيطية.

## الخاتمة

أنت الآن تعرف كيف **تحمل صورة لإجراء OCR** و**تؤدي OCR على PNG** باستخدام مكتبة `aocr`، مع إعداد تسجيل قوي يجعل تصحيح الأخطاء سهلًا. الدالة النموذجية تغلف سير العمل بالكامل، بحيث يمكنك وضعها في أي مشروع والبدء في استخراج النص فورًا.

ما الخطوات التالية؟ جرّب إمداد المحرك بأنواع صور مختلفة (JPEG, TIFF) لترى كيف تتغير الدقة، أو جرب تقنيات معالجة مسبقة مثل العتبة لزيادة النتائج على المسحات الضوضائية. وإذا كنت مهتمًا باستخراج بيانات منظمة (جداول، نماذج)، اطلع على أقسام `aocr` الخاصة بتحليل التخطيط – فهي تتكامل بشكل جيد مع ما أنشأته للتو.

برمجة سعيدة، ولتكن خطوط OCR الخاصة بك خالية من الأخطاء دائمًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم استعراضها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية إجراء OCR على صورة – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}