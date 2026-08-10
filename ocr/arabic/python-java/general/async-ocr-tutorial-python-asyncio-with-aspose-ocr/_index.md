---
category: general
date: 2026-05-31
description: دورة تعليمية عن OCR غير المتزامن تُظهر كيفية استخدام Aspose OCR في بايثون
  مع asyncio لاستخراج النص من الصور بسرعة. تعلم تنفيذ OCR غير المتزامن خطوة بخطوة.
draft: false
keywords:
- async ocr tutorial
- asynchronous OCR with Python
- Aspose OCR library
- Python asyncio OCR
- image text extraction
language: ar
og_description: يُرشدك البرنامج التعليمي لـ OCR غير المتزامن إلى كيفية استخدام Aspose
  OCR في بايثون مع asyncio لاستخراج نص الصور بكفاءة.
og_title: دليل OCR غير المتزامن – Python asyncio مع Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Async OCR tutorial showing how to use Aspose OCR in Python with asyncio
    for fast image text extraction. Learn step‑by‑step async OCR implementation.
  headline: Async OCR Tutorial – Python asyncio with Aspose OCR
  type: TechArticle
- description: Async OCR tutorial showing how to use Aspose OCR in Python with asyncio
    for fast image text extraction. Learn step‑by‑step async OCR implementation.
  name: Async OCR Tutorial – Python asyncio with Aspose OCR
  steps:
  - name: Installed the Aspose OCR library.
    text: Installed the Aspose OCR library.
  - name: Built an `async_ocr` helper that runs recognition without blocking.
    text: Built an `async_ocr` helper that runs recognition without blocking.
  - name: Ran the helper from a clean `asyncio` entry point.
    text: Ran the helper from a clean `asyncio` entry point.
  - name: Demonstrated batch processing with `asyncio.gather`.
    text: Demonstrated batch processing with `asyncio.gather`.
  - name: Added error handling and best‑practice tips.
    text: Added error handling and best‑practice tips.
  type: HowTo
tags:
- OCR
- Python
- asyncio
title: دليل OCR غير المتزامن – Python asyncio مع Aspose OCR
url: /ar/python-java/general/async-ocr-tutorial-python-asyncio-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل OCR غير المتزامن – Python asyncio مع Aspose OCR

هل تساءلت يوماً كيف تشغّل التعرف الضوئي على الحروف دون حجب تطبيقك؟ في **دليل OCR غير المتزامن** ستشاهد ذلك بالضبط — استخراج نص غير حابِس للـ thread باستخدام `asyncio` في بايثون ومكتبة Aspose OCR.  

إذا كنت عالقاً في انتظار معالجة صورة ثقيلة، فإن هذا الدليل يقدّم لك حلاً غير متزامنًا نظيفًا يبقي حلقة الأحداث تعمل بسلاسة.

في الأقسام التالية سنغطي كل ما تحتاجه: تثبيت المكتبة، إعداد مساعد غير متزامن، معالجة النتيجة، وحتى نصيحة سريعة لتوسيع المعالجة إلى عدة صور. بنهاية الدليل ستتمكن من إضافة **دليل OCR غير المتزامن** إلى أي مشروع بايثون يستخدم `asyncio` بالفعل.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.9+ (واجهة `asyncio` التي نستخدمها مستقرة منذ 3.7)  
* رخصة Aspose OCR سارية أو نسخة تجريبية مجانية (المكتبة مكتوبة ببايثون خالص، لا تحتاج إلى ملفات ثنائية)  
* ملف صورة صغير (`.jpg`، `.png`، إلخ) تريد قراءته – احفظه في مجلد معروف  

لا توجد أدوات خارجية أخرى مطلوبة؛ كل شيء يعمل ببايثون خالص.

## الخطوة 1: تثبيت حزمة Aspose OCR

أولاً، احصل على حزمة Aspose OCR من PyPI. افتح الطرفية ونفّذ:

```bash
pip install aspose-ocr
```

> **نصيحة احترافية:** إذا كنت تعمل داخل بيئة افتراضية (مستحسن جدًا)، فعّلها أولاً. هذا يحافظ على عزل الاعتمادات ويتجنب تعارض الإصدارات.

## الخطوة 2: تهيئة محرك OCR بشكل غير متزامن

قلب **دليل OCR غير المتزامن** هو دالة مساعدة غير متزامنة. تُنشئ كائن `OcrEngine`، تُحمّل صورة، ثم تستدعي `recognize_async()`. المحرك نفسه متزامن، لكن طريقة الـ wrapper تُعيد كائنًا قابلًا للانتظار، مما يسمح لحلقة الأحداث بالبقاء مستجيبة.

```python
import asyncio
from asposeocr import OcrEngine

async def async_ocr(image_path: str) -> str:
    """
    Perform OCR on the given image without blocking the event loop.
    
    Args:
        image_path: Path to the image file you want to process.
    
    Returns:
        Recognized text as a string.
    """
    # Initialise the OCR engine – this is cheap, so we do it per call.
    engine = OcrEngine()
    
    # Load the target image into the engine.
    engine.load_image(image_path)
    
    # Start asynchronous recognition and await the result.
    result = await engine.recognize_async()
    
    # Return only the plain text part of the result.
    return result.text
```

**لماذا نفعل ذلك بهذه الطريقة:**  
*إنشاء المحرك داخل الدالة المساعدة يضمن أمان الخيوط إذا قررت تشغيل عدة مهام OCR متوازية لاحقًا. كلمة المفتاح `await` تُعيد التحكم إلى حلقة الأحداث بينما تُجرى المعالجة الثقيلة في مجموعة الخيوط الداخلية للمكتبة.*

## الخطوة 3: تشغيل المساعدة من دالة `async` رئيسية

الآن نحتاج إلى coroutine صغير يُدعى `main()` يستدعي `async_ocr()` ويطبع النتيجة. هذا يعكس نقطة الدخول النموذجية لسكريبت `asyncio`.

```python
async def main():
    # Replace with the path to your own image.
    image_file = "YOUR_DIRECTORY/photo.jpg"
    
    # Await the OCR result – the call is non‑blocking.
    text = await async_ocr(image_file)
    
    # Show the recognized text.
    print("Async OCR result:", text)

# Run the coroutine using asyncio's high‑level API.
if __name__ == "__main__":
    asyncio.run(main())
```

**ماذا يحدث خلف الكواليس؟**  
`asyncio.run()` ينشئ حلقة أحداث جديدة، يجدول `main()`، ويغلق الحلقة بنظافة عندما تنتهي `main()`. هذا النمط هو الطريقة الموصى بها لبدء البرامج غير المتزامنة في بايثون 3.7+.

## الخطوة 4: اختبار السكريبت الكامل

احفظ الكتلتين البرمجيتين أعلاه في ملف واحد، مثلاً `async_ocr_demo.py`. شغّله من سطر الأوامر:

```bash
python async_ocr_demo.py
```

إذا تم الإعداد بشكل صحيح، يجب أن ترى شيئًا مثل:

```
Async OCR result: The quick brown fox jumps over the lazy dog.
```

المخرجات الدقيقة ستعتمد على محتوى `photo.jpg`. النقطة الأساسية هي أن السكريبت ينتهي بسرعة، حتى وإن كانت الصورة كبيرة، لأن عمل OCR يحدث في الخلفية.

## الخطوة 5: التوسيع – معالجة عدة صور بشكل متزامن

سؤال شائع يتبع ذلك هو: *"هل يمكنني تنفيذ OCR على دفعة من الملفات دون إطلاق عملية جديدة لكل واحدة؟"* الجواب نعم. لأن مساعدنا غير متزامن بالكامل، يمكننا جمع عدة coroutines باستخدام `asyncio.gather()`:

```python
async def batch_ocr(image_paths):
    # Build a list of coroutine objects.
    tasks = [async_ocr(path) for path in image_paths]
    
    # Run them concurrently and collect results.
    return await asyncio.gather(*tasks)

# Example usage:
if __name__ == "__main__":
    files = [
        "imgs/img1.jpg",
        "imgs/img2.png",
        "imgs/img3.tif",
    ]
    results = asyncio.run(batch_ocr(files))
    for path, text in zip(files, results):
        print(f"{path}: {text[:50]}...")  # Show first 50 chars of each result
```

**لماذا يعمل هذا:** `asyncio.gather()` يجدول جميع مهام OCR مرة واحدة. مكتبة Aspose OCR لا تزال تستخدم مجموعة خيوطها الخاصة، لكن من منظور بايثون يبقى كل شيء غير حابِس، مما يتيح لك معالجة عشرات الصور في الوقت الذي تستغرقه مكالمة متزامنة واحدة.

## الخطوة 6: معالجة الأخطاء بلطف

عند التعامل مع ملفات خارجية، ستواجه حتماً ملفات مفقودة، صور تالفة، أو مشاكل رخصة. احطّ استدعاء OCR بكتلة `try/except` للحفاظ على حلقة الأحداث حية:

```python
async def safe_async_ocr(image_path):
    try:
        return await async_ocr(image_path)
    except Exception as e:
        # Log the error and return an empty string or a placeholder.
        print(f"Error processing {image_path}: {e}")
        return ""
```

الآن يمكن لـ `batch_ocr()` استدعاء `safe_async_ocr` بدلاً من ذلك، مما يضمن أن ملفًا سيئًا واحدًا لا يوقف الدفعة بأكملها.

## نظرة بصرية

![مخطط دليل OCR غير المتزامن](async-ocr-diagram.png){alt="مخطط تدفق دليل OCR غير المتزامن يوضح مساعد async_ocr، حلقة الأحداث، ومحرك Aspose OCR"}

المخطط أعلاه يوضح التدفق: حلقة الأحداث → `async_ocr` → `OcrEngine` → الخيط الخلفي → النتيجة تعود إلى الحلقة.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | لماذا تحدث | الحل |
|---------|------------|------|
| **إدخال/إخراج حابِس داخل المساعدة** | استخدام `open()` دون `await` يسبب حجب الحلقة. | استخدم `aiofiles` لقراءة الملفات، أو دع `engine.load_image` يتولى ذلك (إنه غير حابِس بالفعل). |
| **إعادة استخدام نفس `OcrEngine` عبر coroutines** | المحرك غير آمن للـ thread؛ الاستدعاءات المتزامنة قد تفسد الحالة. | أنشئ محركًا جديدًا داخل كل استدعاء `async_ocr` (كما هو موضح). |
| **غياب الرخصة** | Aspose OCR يرمي استثناءً متعلقًا بالرخصة أثناء التشغيل. | سجّل رخصتك مبكرًا (`OcrEngine.set_license("license.json")`). |
| **صور كبيرة تسبب ارتفاعًا في استهلاك الذاكرة** | المكتبة تحمل الصورة بالكامل في الذاكرة. | قلل أبعاد الصور قبل OCR إذا كانت الذاكرة تشكل قلقًا. |

## ملخص: ما أنجزناه

في هذا **دليل OCR غير المتزامن** قمنا بـ:

1. تثبيت مكتبة Aspose OCR.  
2. بناء مساعد `async_ocr` يُجري التعرف دون حجب.  
3. تشغيل المساعد من نقطة دخول `asyncio` نظيفة.  
4. توضيح المعالجة الدفعة باستخدام `asyncio.gather`.  
5. إضافة معالجة الأخطاء ونصائح أفضل الممارسات.

كل ذلك ببايثون خالص، لذا يمكنك دمجه في خادم ويب، أداة سطر أوامر، أو خط أنابيب بيانات دون إعادة كتابة الكود غير المتزامن الموجود.

## الخطوات التالية والمواضيع ذات الصلة

* **معالجة الصور مسبقًا بشكل غير متزامن** – استخدم `aiohttp` لتنزيل الصور بشكل متزامن قبل OCR.  
* **تخزين نتائج OCR** – اجمع هذا الدليل مع برنامج تشغيل قاعدة بيانات غير متزامن مثل `asyncpg` لـ PostgreSQL.  
* **تحسين الأداء** – جرّب `engine.recognize_async(max_threads=4)` إذا كانت المكتبة توفر هذا الخيار.  
* **محركات OCR بديلة** – قارن Aspose OCR مع أغطية Tesseract غير المتزامنة لتحليل التكلفة والفائدة.

لا تتردد في التجربة: جرّب معالجة ملفات PDF، عدّل إعدادات اللغة، أو اربط النتائج مع chatbot. السماء هي الحد عندما يكون لديك أساس صلب لـ **دليل OCR غير المتزامن**.

برمجة سعيدة، ولتكن استخراج النصوص سريعًا دائمًا!

## ماذا يجب أن تتعلمه بعد ذلك؟

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [دليل Aspose OCR – التعرف الضوئي على الحروف](/ocr/english/)
- [كيفية تنفيذ OCR لنص الصورة مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}