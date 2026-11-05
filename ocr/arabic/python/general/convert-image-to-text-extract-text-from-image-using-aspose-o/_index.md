---
category: general
date: 2026-01-02
description: حوّل الصورة إلى نص بسرعة—تعلم كيفية استخراج النص من الصورة والتعرف على
  النص من ملفات PNG باستخدام Aspose OCR في بايثون. دليل خطوة بخطوة.
draft: false
keywords:
- convert image to text
- extract text from image
- recognize text from png
- how to extract text
- load image for ocr
language: ar
og_description: تحويل الصورة إلى نص في ثوانٍ. يوضح هذا البرنامج التعليمي كيفية استخراج
  النص من الصورة، والتعرف على النص من ملف PNG، وتحميل الصورة لاستخدام OCR باستخدام
  Aspose OCR.
og_title: تحويل الصورة إلى نص باستخدام Aspose OCR – دليل بايثون الكامل
tags:
- ocr
- python
- aspose
- image-processing
title: 'تحويل الصورة إلى نص: استخراج النص من الصورة باستخدام Aspose OCR (Python)'
url: /ar/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل الصورة إلى نص – دليل بايثون الكامل

هل احتجت يومًا إلى **تحويل الصورة إلى نص** لكن لم تكن متأكدًا من أي مكتبة تثق بها؟ لست وحدك. كثير من المطورين يواجهون صعوبة في استخراج النص من ملفات الصور، خاصةً عندما يكون المصدر PNG أو مستندًا ممسوحًا. الخبر السار هو أن Aspose OCR يجعل العملية بأكملها سهلة للغاية.

في هذا الدرس سنستعرض **كيفية استخراج النص** من ملف PNG، ونوضح لك كيفية **تحميل الصورة لـ OCR**، وسننتهي بمثال نظيف قابل للتنفيذ يمكنك إدراجه في أي مشروع بايثون. في النهاية ستتمكن من التعرف على النص من ملفات PNG وتحويله إلى سلاسل قابلة للبحث—بدون الحاجة إلى النسخ واللصق اليدوي.

## ما ستتعلمه

- تثبيت وإعداد حزمة Aspose OCR للبايثون.  
- **تحميل الصورة لـ OCR** باستخدام استدعاء API بسيط.  
- **استخراج النص من الصورة** ومعالجة كائن النتيجة.  
- المشكلات الشائعة عند محاولة **التعرف على النص من PNG**.  
- نصائح لتحسين الدقة ومعالجة الحالات الخاصة.

لا تحتاج إلى أي خبرة سابقة مع Aspose؛ فقط بيئة بايثون 3 تعمل وصورة تريد تحويلها.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. تثبيت Python 3.8+ (يفضل أحدث إصدار مستقر).  
2. إمكانية الوصول إلى `pip` لتثبيت الحزم الخارجية.  
3. صورة نموذجية—لنسميها `sample.png`—تقع في مجلد يمكنك الإشارة إليه (مثال: `YOUR_DIRECTORY/sample.png`).  
4. اختياري لكن مفيد: بيئة افتراضية للحفاظ على نظافة الاعتمادات.

إذا كنت مرتاحًا بالفعل مع `pip install`، يمكنك تخطي ملاحظة البيئة الافتراضية. وإلا، نفّذ:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # on Windows: ocr-env\Scripts\activate
```

## الخطوة 1: تثبيت مكتبة Aspose OCR

توفر Aspose حزمة بايثون صافية تغلف محرك OCR القوي الخاص بها. قم بتثبيتها بأمر واحد:

```bash
pip install asposeocr
```

هذا كل شيء—لا ملفات تنفيذية مُجمَّعة، ولا DLLs إضافية. الحزمة تجلب ملفات التشغيل اللازمة تلقائيًا.

> **نصيحة احترافية:** إذا واجهت مهلة شبكة، جرّب إضافة `--upgrade` أو استخدم مرآة موثوقة (`pip install --trusted-host pypi.org asposeocr`).

## الخطوة 2: استيراد الوحدة وإنشاء محرك (تحويل الصورة إلى نص)

الآن بعد أن أصبحت المكتبة على نظامك، يمكننا البدء بكتابة الكود. أول شيء نقوم به هو **استيراد وحدة Aspose OCR** وإنشاء كائن محرك. هذا الكائن هو قلب سير عمل **تحويل الصورة إلى نص**.

```python
# Step 2: Import Aspose OCR and create an engine instance
import asposeocr as ocr

# Create the OCR engine – this object will handle all subsequent operations
ocr_engine = ocr.OcrEngine()
```

لماذا نحتاج إلى محرك؟ فكر فيه كـ “العقل” الذي يعرف كيف يقرأ البكسلات ويحولها إلى أحرف. بإنشاء نسخة واحدة من `OcrEngine`، يمكنك إعادة استخدامها لعدة صور دون إعادة تهيئة الموارد الثقيلة—مفيد للمهام الدفعية.

## الخطوة 3: تحميل الصورة لـ OCR (استخراج النص من الصورة)

مع جاهزية المحرك، حان الوقت لـ **تحميل الصورة لـ OCR**. تقبل Aspose OCR مسار ملف، أو تدفق، أو حتى مصفوفة NumPy. للتبسيط، سنستخدم مسار ملف.

```python
# Step 3: Load the image you want to recognize
image_path = "YOUR_DIRECTORY/sample.png"   # <-- replace with your actual path
ocr_engine.load_image(image_path)
```

إذا كانت الصورة موجودة في الذاكرة (مثلاً تم جلبها من API)، يمكنك استخدام `ocr_engine.load_image(BytesIO(data))`. يكتشف المحرك الصيغة تلقائيًا، لذا لا داعي للقلق إذا كانت PNG أو JPEG أو BMP.

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح هو أساس **التعرف على النص من png**. أي صيغة تالفة أو غير مدعومة ستتسبب في رمي استثناء من قبل المحرك، مما يوقف التحويل.

## الخطوة 4: تنفيذ OCR – التعرف على النص من PNG

الآن الجزء الممتع—فعليًا **التعرف على النص من PNG**. يقوم المحرك بمسح البت ماب، وتطبيق نماذج اللغة، وإنتاج كائن نتيجة يحتوي على السلسلة المستخرجة، درجات الثقة، ومعلومات تخطيطية اختيارية.

```python
# Step 4: Run the OCR operation
ocr_result = ocr_engine.recognize()
```

استدعاء `recognize()` متزامن ويعيد كائن `OcrResult`. إذا كنت تحتاج إلى معالجة غير متزامنة لمجموعات كبيرة، توفر Aspose أيضًا طريقة `recognize_async()`، لكن ذلك خارج نطاق هذا الدليل السريع.

## الخطوة 5: إخراج النص المتعرف عليه (تحويل الصورة إلى نص)

أخيرًا، نقوم **بتحويل الصورة إلى نص** عبر طباعة أو تخزين الخاصية `text`. تحتوي الخاصية على نص Unicode عادي، مع الحفاظ على فواصل الأسطر حيث اكتشفها المحرك.

```python
# Step 5: Output the recognized text
print(ocr_result.text)   # plain OCR output
```

المخرجات النموذجية تبدو هكذا:

```
Hello, world!
This is a sample image.
```

إذا كنت تحتاج النص بترميز مختلف (مثلاً بايتات UTF‑8)، ببساطة استدعِ `ocr_result.text.encode('utf-8')`.

### التعامل مع الثقة المنخفضة

أحيانًا قد يواجه محرك OCR صعوبة مع الخلفيات المشوشة. يمكنك فحص درجة الثقة:

```python
if ocr_result.confidence < 0.8:
    print("Warning: Low confidence ({:.2f}). Consider preprocessing the image.".format(ocr_result.confidence))
```

تشمل حيل ما قبل المعالجة:

- التحويل إلى تدرج الرمادي (`cv2.cvtColor` مع OpenCV).  
- تطبيق عتبة ثنائية (`cv2.threshold`).  
- تكبير الصورة لتصل على الأقل إلى 300 dpi.

## مثال كامل يعمل

فيما يلي السكربت الكامل الذي يجمع كل شيء معًا. احفظه باسم `convert_image_to_text.py` وشغّله من سطر الأوامر.

```python
#!/usr/bin/env python3
"""
convert_image_to_text.py
A minimal example that demonstrates how to convert image to text using Aspose OCR.
"""

import asposeocr as ocr
import os
import sys

def main(image_path: str):
    # Verify that the file exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found → {image_path}")

    # 1️⃣ Create the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (load image for OCR)
    engine.load_image(image_path)

    # 3️⃣ Recognize text (recognize text from png)
    result = engine.recognize()

    # 4️⃣ Print the plain text (convert image to text)
    print("\n--- OCR Result ---")
    print(result.text)

    # 5️⃣ Optional: Show confidence and suggest improvements
    if hasattr(result, "confidence"):
        print(f"\nConfidence: {result.confidence:.2%}")
        if result.confidence < 0.80:
            print("⚠️ Low confidence – try image preprocessing or higher DPI.")

if __name__ == "__main__":
    # Change this path to point at your PNG/JPEG/etc.
    SAMPLE_IMAGE = "YOUR_DIRECTORY/sample.png"
    main(SAMPLE_IMAGE)
```

**المخرجات المتوقعة** (مع افتراض صورة نظيفة):

```
--- OCR Result ---
Hello, world!
This is a sample image.

Confidence: 96.45%
```

شغّل السكربت:

```bash
python convert_image_to_text.py
```

يجب أن ترى النص المستخرج مطبوعًا في وحدة التحكم. إذا حصلت على تحذير بثقة منخفضة، راجع اقتراحات ما قبل المعالجة أعلاه.

## الحالات الخاصة والأسئلة الشائعة

### 1. *ماذا لو كانت صورتي JPEG بدلاً من PNG؟*

تكتشف Aspose OCR الصيغة تلقائيًا، لذا يمكنك تمرير `load_image()` لأي نوع نقطي مدعوم (PNG, JPEG, BMP, TIFF). لا حاجة لتغيير الكود.

### 2. *هل يمكنني استخراج النص من صفحة PDF؟*

ليس مباشرةً باستخدام محرك OCR، لكن يمكنك تحويل صفحة PDF إلى صورة (باستخدام `asposepdf` أو `PyMuPDF`) ثم تمرير تلك الصورة إلى خط أنابيب OCR—وبالتالي **تحويل الصورة إلى نص** بعد خطوة التحويل.

### 3. *كيف أتعامل مع مستندات متعددة اللغات؟*

قم بتعيين خاصية `language` على المحرك قبل استدعاء `recognize()`:

```python
engine.language = ocr.Language.French | ocr.Language.English
```

هذا يخبر المحرك بالبحث عن أحرف الفرنسية والإنجليزية معًا، مما يحسن الدقة للمحتوى المختلط اللغات.

### 4. *هل هناك طريقة للحصول على إطارات حدودية لكل كلمة؟*

نعم. يحتوي كائن `OcrResult` على مجموعة `words`، كل عنصر منها يتضمن `text`، `rectangle`، و `confidence`. يمكنك التكرار عليها إذا كنت بحاجة إلى معلومات تخطيطية لإنشاء PDF أو PDF قابل للبحث.

## نصائح لتحسين الدقة (كيفية استخراج النص بفعالية)

- **الدقة DPI مهمة**: استهدف على الأقل 300 dpi. الدقة الأعلى تقلل من غموض البكسل.  
- **التباين هو الملك**: النص الداكن على خلفية فاتحة يعطي أفضل النتائج. استخدم أدوات تحرير الصور لزيادة التباين إذا لزم الأمر.  
- **تجنب تشوهات الضغط**: احفظ PNGs بضغط غير فقدان (lossless)؛ تشوهات JPEG قد تربك محرك OCR.  
- **إزالة الفراغات البيضاء**: قص الحدود الزائدة يقلل مساحة المسح التي يحتاجها المحرك، مما يسرّع عملية **تحويل الصورة إلى نص**.

## الخلاصة

لقد غطينا كل ما تحتاجه **لتحويل الصورة إلى نص** باستخدام Aspose OCR في بايثون—بدءًا من التثبيت، مرورًا بتحميل الصورة، التعرف على النص، ومعالجة النتائج. الآن تعرف كيف **استخراج النص من الصورة**، **التعرف على النص من png**، و**تحميل الصورة لـ OCR** في سكربت نظيف وقابل لإعادة الاستخدام.

هل أنت مستعد للخطوة التالية؟ جرّب تمرير مجلد من الإيصالات الممسوحة إلى السكربت، أو دمج مخرجات OCR في قاعدة بيانات SQLite قابلة للبحث. الاحتمالات لا حصر لها، ومع Aspose OCR لديك محرك موثوق تحت الغطاء.

إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع وثائق Aspose OCR للحصول على خيارات تكوين متقدمة. برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}