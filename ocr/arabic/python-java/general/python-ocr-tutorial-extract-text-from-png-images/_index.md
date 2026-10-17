---
category: general
date: 2026-06-25
description: دروس OCR بلغة بايثون تُظهر لك كيفية استخراج النص من ملفات PNG، قراءة
  النص في الصورة، والتعرف على نص الصورة باستخدام محرك بسيط خالٍ من الترخيص.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: ar
og_description: يُعلِّمك برنامج Python OCR كيفية تحميل الصورة للتعرف الضوئي على الأحرف،
  استخراج النص من ملفات PNG، والتعرف على نص الصورة في بضع أسطر من الشيفرة فقط.
og_title: دروس بايثون للتعرف الضوئي على الأحرف – استخراج النص من PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'دورة OCR بايثون: استخراج النص من صور PNG'
url: /ar/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل Python OCR – استخراج النص من صور PNG

هل تساءلت يومًا كيف يمكن لـ **python ocr tutorial** تحويل لقطة شاشة لإيصال إلى نص قابل للتحرير؟ لست وحدك. في العديد من المشاريع الواقعية نحتاج إلى *read text image* بسرعة، والقيام بذلك بنفسك أفضل من النسخ واللصق من واجهة المستخدم في كل مرة.  

في هذا الدليل سنستعرض مثالًا عمليًا **extracts text PNG**، يوضح لك كيفية *load image for OCR*، وأخيرًا يطبع نتيجة *recognize image text*—كل ذلك باستخدام محرك OCR مجاني للتقييم فقط. لا مفاتيح ترخيص، لا تبعيات ثقيلة—فقط بايثون عادي وقليل من الحزم الصغيرة.

## ما ستتعلمه

- كيفية تثبيت واستيراد مكتبة OCR الخفيفة.
- الخطوات الدقيقة **load image for OCR** ومعالجة المشكلات الشائعة.
- طرق **read text image** لملفات ذات جودة متفاوتة.
- نصائح لتحسين الدقة عند **extract text png**.
- كيفية عرض السلسلة المعترف بها واختياريًا كتابتها إلى القرص.

بنهاية هذا الدليل ستحصل على سكربت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع يحتاج إلى **recognize image text** في الوقت الفعلي. لا سحر، فقط كود واضح وشروحات.

### المتطلبات المسبقة

- Python 3.8 أو أحدث (المكتبة تعمل مع 3.7+ لكن يُفضَّل 3.8+).
- إلمام أساسي بـ pip وبيئات افتراضية.
- ملف صورة باسم `sample.png` (أو أي PNG تريد اختباره) محفوظ في مجلد يمكنك الإشارة إليه.

إذا كان أي من ذلك غير مألوف لك، خذ دقيقة لتعديله—ستجد الفائدة تستحق الجهد.

---

## Python OCR Tutorial – إعداد المحرك

أولًا: نحتاج إلى كائن محرك OCR. المكتبة التي سنستخدمها هي غلاف صغير حول محرك OCR أصلي يعمل مباشرةً للتقييم. لا تحتاج إلى مفتاح ترخيص، ما يجعل *python ocr tutorial* مثاليًا للنماذج الأولية السريعة.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**لماذا هذا مهم:** إنشاء المحرك يعزل وقت تشغيل OCR عن باقي الكود، مما يسمح لك بإعادة استخدامه لعدة صور دون إعادة تهيئة الموارد الثقيلة في كل مرة.

---

## Load Image for OCR – قراءة ملف PNG

الآن بعد أن تم إنشاء المحرك، علينا *load image for OCR*. طريقة `Image.load` في المكتبة تقبل مسارًا وتفك تشفير PNG وJPEG وBMP وبعض الصيغ الأخرى تلقائيًا.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **نصيحة محترف:** إذا كان PNG يحتوي على قناة ألفا، ستقوم المكتبة بإزالتها تلقائيًا. ومع ذلك، للحصول على أفضل النتائج في مهام *read text image*، احفظ الصورة بتدرج الرمادي—هذا يقلل الضوضاء ويسرّع التعرف.

---

## Recognize Image Text – تشغيل محرك OCR

مع وجود كائن الصورة جاهز، يمكننا أخيرًا **recognize image text**. هذا هو جوهر *python ocr tutorial* ولا يتطلب سوى سطر واحد من الكود.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**ماذا يحدث خلف الكواليس؟** يقوم المحرك بتطبيق سلسلة من الفلاتر المسبقة (تصحيح الميل، ثنائيات) قبل تمرير البت ماب إلى شبكة عصبية تم تدريبها على ملايين الأحرف. لهذا تحصل غالبًا على مخرجات دقيقة حتى على PNG منخفض الدقة.

---

## عرض وحفظ النص المستخرج

وجود النتيجة رائع، لكن ربما تريد رؤيتها أو تخزينها. كائن `result` يوفّر خاصية `text` التي تحتوي على النص الصافي.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**الناتج المتوقع** (بافتراض أن `sample.png` يحتوي على “Hello, OCR!”):

```
Eval-mode result: Hello, OCR!
```

إذا حصلت على رموز غير مفهومة بدلًا من أحرف قابلة للقراءة، راجع القسم التالي لإصلاح المشكلات الشائعة.

---

## معالجة المشكلات الشائعة عند استخراج نص PNG

حتى أفضل محركات OCR قد تواجه صعوبات مع بعض الصور. إليك العقبات النموذجية وكيفية تجاوزها.

### 1. تباين منخفض أو خلفيات داكنة

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. خطوط مائلة

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. أحرف غير إنجليزية

إذا كان PNG يحتوي على حروف مُعَلَّقة أو سكريبتات غير لاتينية، قم بتهيئة المحرك بحزمة اللغة المناسبة:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. صور كبيرة جدًا

معالجة PNG بحجم 4000×3000 قد تكون بطيئة. قلل حجمها مع الحفاظ على قابلية القراءة:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

هذه التعديلات جزء من *python ocr tutorial* قوي يعمل خارج سيناريو “المسار السعيد”.

---

## السكربت الكامل – حل بملف واحد

فيما يلي السكربت الكامل الجاهز للتنفيذ والذي يدمج جميع الخطوات والتحسينات الاختيارية التي نوقشت. انسخه إلى `ocr_extract.py` وشغّله باستخدام `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**تشغيله:**  
```bash
python ocr_extract.py ./sample.png
```

سترى السلسلة المعترف بها مطبوعةً وسيتم إنشاء ملف `sample_extracted.txt` بجوار الصورة.

---

## نظرة بصرية عامة

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*النص البديل:* *مخطط دليل Python OCR يوضح التدفق من تحميل صورة للـ OCR إلى استخراج نص PNG.*

المخطط يوضح التدرج الخطي من **load image for OCR** → **recognize image text** → **extract text PNG** ويبرز الأماكن التي يمكنك فيها إضافة خطوات معالجة مسبقة.

---

## الخلاصة

لقد أكملنا للتو **python ocr tutorial** يوضح كيفية *load image for OCR*، *recognize image text*، وأخيرًا **extract text png** باستخدام عدد قليل من أوامر بايثون. السكربت يعمل بالكامل، يتعامل مع الحالات الطرفية الشائعة، ويمكن توسيعه للمعالجة الدفعية أو الدعم متعدد اللغات.

هل أنت مستعد للتحدي التالي؟ جرّب تحويل ملفات PDF إلى صور، جرب حزم لغات مختلفة، أو دمج خطوة OCR في API باستخدام Flask حتى يتمكن تطبيق الويب الخاص بك من قراءة لقطات الشاشة المرفوعة مباشرة. إمكانيات أتمتة *read text image* لا حدود لها.

هل لديك أسئلة أو صورة صعبة لا تستطيع فك شفرتها؟ اترك تعليقًا أدناه، ولنحلها معًا. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي عرضناها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}