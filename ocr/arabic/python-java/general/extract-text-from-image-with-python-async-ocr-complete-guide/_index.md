---
category: general
date: 2026-05-03
description: استخراج النص من الصورة باستخدام OCR غير المتزامن في بايثون. تعلم كيفية
  تحويل ملفات tif إلى نص، تحميل الصورة للـ OCR، والتعرف على النص من الصورة بكفاءة.
draft: false
keywords:
- extract text from image
- convert tif to text
- load image for ocr
- extract image text
- recognize text from image
language: ar
og_description: استخراج النص من الصورة باستخدام OCR غير المتزامن في بايثون. يوضح هذا
  الدليل كيفية تحويل ملفات tif إلى نص، تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف
  على النص من الصورة.
og_title: استخراج النص من الصورة باستخدام بايثون OCR غير المتزامن – دليل شامل
tags:
- OCR
- Python
- AsyncIO
title: استخراج النص من الصورة باستخدام بايثون OCR غير المتزامن – دليل كامل
url: /ar/python-java/general/extract-text-from-image-with-python-async-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Python Async OCR – دليل كامل

هل تحتاج إلى **استخراج النص من الصورة** بسرعة؟ باستخدام Python Async OCR يمكنك القيام بذلك في بضع أسطر من الشيفرة فقط. سواء كنت تتعامل مع مسح .tif ضخم أو مجموعة من ملفات JPEG، يوضح لك هذا الدليل كيفية تحويل tif إلى نص، **تحميل الصورة لـ OCR**، وأخيرًا التعرف على النص من الصورة دون حجب حلقة الأحداث الخاصة بك.

الأمر هو أن معظم المطورين يلجؤون إلى مكتبة متزامنة، ثم يواجهون واجهة مستخدم متجمدة بينما يقوم المحرك بمعالجة البكسلات. في هذا الدليل سنقلب هذا السيناريو باستخدام Aspose OCR Cloud API غير المتزامن، بحيث يبقى تطبيقك مستجيبًا. في النهاية ستحصل على سكريبت قابل للتنفيذ يخرج النص من أي صيغة صورة مدعومة، وستفهم السبب وراء كل خطوة.

## ما ستتعلمه

- كيفية إعداد Aspose OCR Cloud SDK للبايثون.  
- الشيفرة الدقيقة اللازمة **لتحميل الصورة لـ OCR** وبدء مهمة التعرف غير المتزامنة.  
- نصائح للتعامل مع ملفات .tif الكبيرة وتعقيدات الترخيص.  
- طرق **استخراج نص الصورة** بأمان، حتى عندما تُرجع الخدمة أخطاء.  
- مثال كامل جاهز للنسخ واللصق يمكنك إدراجه في مشروعك.

> **المتطلبات المسبقة**: Python 3.8+ وملف ترخيص Aspose OCR Cloud (`Aspose.OCR.Java.lic`). لا توجد حزم طرف ثالث أخرى مطلوبة.

![extract text from image workflow](workflow.png){: .align-center alt="مخطط استخراج النص من الصورة"}

## استخراج النص من الصورة – نظرة عامة على OCR غير المتزامن

قبل أن نغوص في الشيفرة، دعنا نفكك التدفق. عندما تستدعي `recognize_async` يرسل SDK الصورة إلى سحابة Aspose، يُنشئ مهمة خلفية، ويعطيك كائن `Task`. انتظار هذه المهمة يُعيد لك `OcrResult` يحتوي على تمثيل النص العادي للصورة. لأن الاستدعاء غير متزامن، يمكنك إطلاق مهام متعددة بالتوازي—مثالي لمعالجة دفعات من الأرشيفات الضخمة للمستندات الممسوحة ضوئيًا.

### لماذا نستخدم غير المتزامن؟

- **I/O غير حابِس** – تبقى حلقة الأحداث حرة لمعالجة أعمال أخرى (مثل خدمة طلبات HTTP).  
- **قابلية التوسع** – تشغيل عشرات عمليات التعرف في آن واحد؛ السحابة تقوم بالعمل الشاق.  
- **الاستجابة** – تطبيقات الواجهة لا تتجمد أثناء انتظار محرك OCR.

الآن بعد أن وضّحنا “السبب”، دعنا نرى **كيف**.

## تحويل TIF إلى نص باستخدام Aspose OCR

عقبة شائعة هي الافتراض بأن كل مكتبة OCR تدعم .tif أصلاً. Aspose تدعم ذلك، لكن لا يزال عليك تزويدها بكائن `Image`. SDK يُجرد الصيغة، لذا يمكنك ببساطة الإشارة إلى مسار الملف.

```python
import asyncio
import asposeocrcloud as ocr

async def async_ocr(image_path: str) -> str:
    """
    Asynchronously extract text from the given image file.
    
    Parameters
    ----------
    image_path: str
        Path to the image (e.g., a .tif, .png, or .jpg file).

    Returns
    -------
    str
        The plain‑text OCR result.
    """
    # 1️⃣ Create the OCR engine and apply the license
    ocr_engine = ocr.OcrEngine()
    # The License class reads the .lic file; adjust the path if needed.
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image for OCR – this works for TIF, PNG, JPEG, etc.
    ocr_image = ocr.Image.from_file(image_path)

    # 3️⃣ Start the asynchronous recognition task
    recognition_task = ocr_engine.recognize_async(ocr_image)

    # 4️⃣ Await the task and retrieve the extracted text
    ocr_result = await recognition_task
    return ocr_result.text
```

**شرح السطور الرئيسية**

- `ocr_engine.license = ...` – بدون ترخيص صالح تُعيد السحابة خطأ 403. تأكد من أن ملف `.lic` متاح من دليل عمل السكريبت.  
- `ocr.Image.from_file(image_path)` – هذه الخطوة **تحمل الصورة لـ OCR**؛ SDK يكتشف الصيغة تلقائيًا، لذا لا تحتاج إلى تحويل .tif مسبقًا.  
- `recognize_async` – تُعيد مهمة متوافقة مع الـ coroutine. يمكنك إطلاق عدة منها في استدعاء `gather` إذا كان لديك دفعة.

> **نصيحة احترافية**: إذا كنت تعالج ملفات TIFF بحجم جيجابايت، فكر في تقسيمها إلى صفحات أولاً. يمكن لـ `Image.from_file` في Aspose قبول فهرس صفحة، مما يقلل من ضغط الذاكرة.

## التعرف على النص من الصورة بشكل غير متزامن

دعنا نرى كيف ستستدعي الدالة من سكريبت نموذجي. نقطة الدخول `asyncio.run` هي أبسط طريقة لإطلاق الـ coroutine عندما لا تكون داخل حلقة أحداث (مثل أداة CLI بسيطة).

```python
if __name__ == "__main__":
    # Replace with the actual path to your large TIF file.
    tif_path = "YOUR_DIRECTORY/large_image.tif"

    # Execute the coroutine and capture the output.
    extracted_text = asyncio.run(async_ocr(tif_path))

    # Print the result – this is the final step of **extracting text from image**.
    print("=== OCR Result ===")
    print(extracted_text)
```

**ما المتوقع**

تشغيل السكريبت على مسح واضح وعالي الدقة عادةً ما يُنتج سلسلة متعددة الأسطر تتطابق مع الصفحة المطبوعة. إذا كانت الصورة مشوشة، لا يزال Aspose يحاول تنظيفها، لكن قد ترى أحرفًا مشوهة. في هذه الحالة، فكر في ما قبل المعالجة باستخدام OpenCV (مثل العتبة) قبل تمرير الملف إلى محرك OCR.

### التعامل مع الأخطاء بأناقة

```python
try:
    extracted_text = asyncio.run(async_ocr(tif_path))
except ocr.OcrException as exc:
    print(f"⚠️ OCR failed: {exc}")
    # Fallback: you could retry, log, or switch to a different service.
else:
    print(extracted_text)
```

التقاط `OcrException` يضمن عدم تعطل برنامجك عندما تُرجع السحابة خطأ—وهو ما يوقع الكثير من المبتدئين الذين ينسون مشاكل الشبكة.

## تحميل الصورة لـ OCR – نصائح عملية

1. **مسار الملف مقابل الـ Bytes** – SDK يقبل مسار ملف، لكن يمكنك أيضًا التحميل من كائن `bytes` إذا كانت الصورة موجودة في الذاكرة (`ocr.Image.from_bytes`). هذا مفيد عندما تكون قد جلبت الملف بالفعل من S3 أو قاعدة بيانات.  
2. **الصيغ المدعومة** – بجانب .tif، Aspose يتعامل مع PDF، BMP، GIF، وحتى TIFF متعدد الصفحات. استخدم `Image.from_file("doc.pdf")` لتطبيق OCR مباشرة على ملفات PDF.  
3. **الأداء** – للوظائف الدفعة، أعد استخدام نفس كائن `OcrEngine`؛ إنشاء محرك جديد لكل ملف يضيف عبئًا غير ضروري.

## مثال كامل يعمل (جميع الخطوات في سكريبت واحد)

فيما يلي السكريبت الكامل الجاهز للتنفيذ الذي يدمج الترخيص، معالجة الأخطاء، ومُحلل وسائط سطر الأوامر البسيط. انسخه، عدل مسار الترخيص، وستكون جاهزًا.

```python
# full_async_ocr.py
import asyncio
import argparse
import asposeocrcloud as ocr
import sys
from pathlib import Path

async def async_ocr(image_path: Path) -> str:
    """Extract text from an image file asynchronously."""
    engine = ocr.OcrEngine()
    # Adjust this if your .lic file lives elsewhere
    license_path = Path("Aspose.OCR.Java.lic")
    if not license_path.is_file():
        sys.exit("❌ License file not found. Place Aspose.OCR.Java.lic beside the script.")
    engine.license = ocr.License().set_license(str(license_path))

    # Load the image (supports TIFF, PNG, JPEG, PDF, etc.)
    image = ocr.Image.from_file(str(image_path))

    # Fire off the async recognition
    task = engine.recognize_async(image)

    # Await and return the plain text
    result = await task
    return result.text

def parse_args():
    parser = argparse.ArgumentParser(
        description="Extract text from image using Aspose OCR async API."
    )
    parser.add_argument(
        "image",
        type=Path,
        help="Path to the image file (e.g., .tif, .png, .jpg, .pdf)."
    )
    return parser.parse_args()

def main():
    args = parse_args()
    if not args.image.is_file():
        sys.exit(f"❌ File not found: {args.image}")

    try:
        text = asyncio.run(async_ocr(args.image))
    except ocr.OcrException as e:
        sys.exit(f"⚠️ OCR failed: {e}")

    print("\n=== Extracted Text ===\n")
    print(text)

if __name__ == "__main__":
    main()
```

**الناتج المتوقع**

```
=== Extracted Text ===

Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
...
```

إذا احتوت الصورة على فقرة بسيطة، سيعرض الطرفية نفس الأسطر مع الحفاظ على فواصل الأسطر. بالنسبة لملفات TIFF متعددة الصفحات، يقوم SDK بدمج الصفحات بالترتيب.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع أطر غير متزامنة أخرى مثل FastAPI؟**  
ج: بالتأكيد. استبدل استدعاء `asyncio.run` بـ `await async_ocr(path)` داخل نقطة النهاية الخاصة بك، وستتعامل FastAPI مع حلقة الأحداث تلقائيًا.

**س: ماذا لو احتجت إلى معالجة مئات الملفات في آن واحد؟**  
ج: استخدم `asyncio.gather`:

```python
tasks = [async_ocr(p) for p in list_of_paths]
results = await asyncio.gather(*tasks, return_exceptions=True)
```

**س: هل يمكنني استخراج النص من PDF محمي بكلمة مرور؟**  
ج: ليس مباشرة. ستحتاج إلى فك حماية PDF أولًا (مثلاً باستخدام `pikepdf`) ثم تمرير الـ bytes المفكوكة إلى `ocr.Image.from_bytes`.

**س: كيف أتعامل مع لغات غير الإنجليزية؟**  
ج: اضبط اللغة قبل التعرف:

```python
engine.language = "spa"   # Spanish ISO code
```

Aspose يدعم أكثر من 60 لغة؛ راجع الوثائق للحصول على المعرفات الدقيقة.

## الخلاصة

الآن لديك حل قوي **استخراج النص من الصورة** يستفيد من `asyncio` في بايثون وAspose OCR Cloud API غير المتزامن. باتباع الخطوات أعلاه يمكنك **تحويل tif إلى نص**، **تحميل الصورة لـ OCR**، و**التعرف على النص من الصورة** بطريقة غير حابسة—مثالي لكل من أدوات سطر الأوامر وخدمات الويب عالية الحركة.

ما التالي؟ جرّب تجميع مجلد من المسحات، جرب إعدادات اللغة، أو قم بتمرير ناتج OCR إلى خط أنابيب معالجة اللغة الطبيعية اللاحق. السماء هي

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}