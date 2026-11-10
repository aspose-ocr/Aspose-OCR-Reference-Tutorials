---
category: general
date: 2026-01-12
description: استخراج النص من صورة باستخدام بايثون و Aspose OCR. تعلم كيفية تحويل الصورة
  الممسوحة ضوئياً إلى نص باستخدام الكود غير المتزامن في دقائق قليلة.
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: ar
og_description: استخراج النص من صورة باستخدام بايثون و Aspose OCR. يوضح هذا الدرس
  كيفية تحويل الصورة الممسوحة ضوئياً إلى نص باستخدام الدوال غير المتزامنة.
og_title: استخراج النص من صورة بايثون – دليل OCR غير المتزامن
tags:
- python
- ocr
- async
title: استخراج النص من الصورة باستخدام بايثون – دليل OCR غير المتزامن
url: /ar/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة Python – دليل OCR غير المتزامن

هل احتجت يوماً إلى **استخراج النص من صورة Python** في سكريبتاتك لكن شعرت بأنك عالق في جزء OCR؟ لست وحدك. يواجه العديد من المطورين جداراً عندما يكون لديهم مستند ممسوح ضوئياً ويرغبون في تحويله إلى نص قابل للبحث دون أن يفتتحوا شعرهم.

في هذا الدليل سنستعرض مثالاً كاملاً قابلاً للتنفيذ يوضح لك كيفية **تحويل الصورة الممسوحة إلى نص** باستخدام واجهة Aspose OCR غير المتزامنة. في النهاية ستحصل على دالة واحدة يمكنك إدراجها في أي مشروع، وستفهم لماذا يمكن للمعالجة غير المتزامنة أن تبقي تطبيقك مستجيباً حتى عندما يستغرق OCR بضع ثوانٍ.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.8+ مثبت (ميزات async تحتاج على الأقل إلى 3.7)
- حزمة `asposeocr` (`pip install asposeocr`) – هذه هي المكتبة التي سنستخدمها
- ملف صورة ممسوح ضوئياً (TIFF, PNG, JPEG – أي شيء يدعمه Aspose OCR)
- إلمام أساسي بـ `asyncio` (إذا لم يكن لديك، لا تقلق – سنشرح كل خطوة)

لا توجد تبعيات نظام إضافية مطلوبة؛ Aspose OCR يجمع كل ما تحتاجه في حزمة واحدة.

![مخطط يوضح تدفق OCR غير المتزامن – استخراج النص من صورة python](https://example.com/async-ocr-diagram.png "تدفق OCR غير المتزامن – استخراج النص من صورة python")

## الخطوة 1 – إعداد الدالة المساعدة غير المتزامنة  

قلب الحل هو دالة `async` تقوم بتحميل الصورة، بدء OCR، ثم انتظار النتيجة. إبقاء الدالة غير متزامنة يعني أنه يمكنك تشغيل كوروتينات أخرى (مثل تنزيل ملفات إضافية) بينما يعمل محرك OCR في الخلفية.

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**لماذا هذا مهم:** بإرجاع `Future`، يقوم Aspose OCR بالعمل الثقيل في مجموعة خيوط منفصلة. `await` يحرّر حلقة الأحداث، لذا يظل تطبيقك سريع الاستجابة. إذا احتجت إلى معالجة العديد من الصور في وقت واحد، يمكنك ببساطة جدولة عدة استدعاءات `async_ocr` باستخدام `asyncio.gather`.

## الخطوة 2 – تشغيل Coroutine في حلقة الأحداث  

الآن بعد أن لدينا الدالة المساعدة، نحتاج إلى تنفيذها. `asyncio.run` ينشئ حلقة أحداث جديدة، يشغّل الـ coroutine، ثم يغلق كل شيء بنظافة.

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**نصيحة احترافية:** إذا كنت تدمج هذا في تطبيق async أكبر (مثل FastAPI)، ستستدعي `await async_ocr(...)` مباشرةً بدلاً من `asyncio.run`.

## الخطوة 3 – التحقق من الناتج  

عند تشغيل السكريبت، يجب أن ترى شيئاً مشابهًا لـ:

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

إذا كان الناتج مشوشًا، تحقق من التالي:

1. الصورة واضحة وليست مضغوطة بشكل مفرط.  
2. لقد اخترت اللغة الصحيحة (`ocr.Language.ENGLISH` تعمل لمعظم النصوص اللاتينية).  
3. مسار الملف صحيح والملف قابل للقراءة.

## الخطوة 4 – معالجة الحالات الحدية  

### لغات متعددة  

إذا كنت بحاجة إلى **تحويل الصورة الممسوحة إلى نص** بلغة غير الإنجليزية، فقط غيّر خاصية اللغة:

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### ملفات كبيرة  

بالنسبة لملفات TIFF الكبيرة جدًا، فكر في تغيير حجمها أو تحويلها إلى PNG منخفض الدقة قبل تمريرها إلى OCR. هذا يقلل من ضغط الذاكرة ويسرّع المعالجة.

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### معالجة الأخطاء  

احطِ استدعاء OCR بكتلة `try/except` لالتقاط الأخطاء المتعلقة بالشبكة أو الترخيص.

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## الخطوة 5 – التوسع: معالجة العديد من الصور بشكل متزامن  

نظرًا لأن الدالة غير متزامنة، يمكنك إطلاق عشرات مهام OCR في آن واحد:

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

هذا النمط يبقي وحدة المعالجة المركزية مشغولة بينما يعمل محرك OCR بالتوازي، مما يقلل بشكل كبير من الوقت الإجمالي للمعالجة.

## الخلاصة  

أصبح لديك الآن حل قوي لـ **استخراج النص من صورة Python** يستفيد من واجهة Aspose OCR غير المتزامنة. المثال الكامل يوضح كيف:

1. تهيئة محرك OCR واختيار اللغة.  
2. إطلاق OCR بشكل غير متزامن باستخدام `process_async`.  
3. انتظار النتيجة دون حجز حلقة الأحداث.  
4. معالجة المشكلات الشائعة مثل الملفات الكبيرة ودعم متعدد اللغات.  

لا تتردد في تعديل الكود ليتناسب مع خطوط عملك—سواء كنت تبني نظام إدارة مستندات، فهرس بحث، أو أداة سطر أوامر بسيطة. الخطوات التالية قد تشمل:

- تخزين النص المستخرج في قاعدة بيانات للبحث النصي الكامل.  
- إضافة توليد PDF (مثلاً باستخدام `PyPDF2`) لإنشاء ملفات PDF قابلة للبحث.  
- دمج مع إطار ويب مثل FastAPI لتوفير خدمة OCR RESTful.

برمجة سعيدة، واستمتع بتحويل تلك الصور الممسوحة إلى نص قابل للبحث والتحرير!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}