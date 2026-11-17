---
category: general
date: 2026-09-29
description: تعرّف على كيفية استخراج النص من صورة JPG باستخدام OCR في بايثون ومعالجة
  ما بعد AsposeAI لتحويل موثوق من الصورة إلى النص.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from JPG image
- Python OCR
- AsposeAI post‑processing
- image to text conversion
- optical character recognition python
language: ar
lastmod: 2026-09-29
og_description: استخراج النص من صورة JPG باستخدام OCR في بايثون ومعالجة ما بعد AsposeAI.
  اتبع هذا الدليل الكامل للحصول على تحويل دقيق من الصورة إلى النص.
og_image_alt: Python code extracting text from a JPG image with OCR and AI post‑processing
og_title: استخراج النص من صورة JPG باستخدام OCR في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-09-29'
  description: Learn how to extract text from JPG image with Python OCR and AsposeAI
    post‑processing for reliable image‑to‑text conversion.
  headline: How to extract text from JPG image using Python OCR
  type: TechArticle
tags:
- OCR
- Python
- AsposeAI
title: كيفية استخراج النص من صورة JPG باستخدام بايثون OCR
url: /ar/python/general/how-to-extract-text-from-jpg-image-using-python-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج النص من صورة JPG باستخدام Python OCR

إذا كنت بحاجة إلى **استخراج النص من صورة JPG** بسرعة، فإن هذا الدليل يوضح لك سير عمل كامل بلغة Python يجمع بين OCR الأساسي وتصحيح مدفوع بالذكاء الاصطناعي. بنهاية البرنامج التعليمي ستحصل على سكريبت جاهز للتنفيذ ينتج نصًا نظيفًا وقابلًا للبحث من أي صورة JPG.

استخراج النص من صور JPG هو طلب شائع لتحويل الإيصالات، الفواتير، أو المستندات الممسوحة ضوئيًا إلى صيغة رقمية. يغطي هذا الدليل كل ما تحتاجه: تثبيت SDK، تشغيل التعرف الضوئي على الأحرف (OCR) في Python، وتطبيق معالجة ما بعد AsposeAI لتحسين الدقة.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- Python 3.8 أو أحدث مثبت.
- رخصة سارية لحزمة Aspose.OCR for Python via .NET (أو نسخة تجريبية مجانية).
- ملف JPG تريد معالجته (ضعه في مجلد مثل `YOUR_DIRECTORY/sample.jpg`).
- إلمام أساسي بسطر الأوامر وبيئات Python الافتراضية.

لا تحتاج إلى أي أدوات معالجة صور إضافية؛ محرك Aspose OCR يتعامل مع فك ترميز JPEG داخليًا.

## الخطوة 1: تشغيل OCR لاستخراج النص من صورة JPG

الخطوة الأولى هي تحميل الصورة وتشغيل محرك OCR المدمج. سيعطيك ذلك سلسلة نصية أولية قد تحتوي على أخطاء، خاصةً في الصور منخفضة الجودة.

```python
# Step 1: Load the image and run basic OCR
from aspose.ocr import OcrEngine

# Create an OcrEngine instance
ocr_engine = OcrEngine()

# Load the JPG file you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample.jpg")

# Perform optical character recognition (OCR)
raw_result = ocr_engine.recognize()          # raw_result.text holds the initial recognition
print("Raw OCR output:", raw_result.text)
```

**لماذا يعمل هذا:** `OcrEngine` ينفذ منطق التعرف الضوئي على الأحرف في Python الذي يمسح كل بكسل، يحدد حدود الأحرف، ويحولها إلى رموز Unicode. استدعاء `recognize()` يُعيد كائن يحتوي على الخاصية `text` التي تضم النسخة الأولية من النص.

## الخطوة 2: إعداد AsposeAI للمعالجة اللاحقة

غالبًا ما يترك OCR الأساسي أحرفًا غريبة أو كلمات غير مكتشفة بشكل صحيح. توفر AsposeAI نموذجًا عصبيًا خفيفًا يصحح هذه الأخطاء تلقائيًا. تمكين التحميل التلقائي يضمن جلب النموذج في المرة الأولى التي تشغل فيها السكريبت.

```python
# Step 2: Prepare AsposeAI for post‑processing (auto‑download ensures the model is present)
from aspose.ai import AsposeAI

post_processor = AsposeAI()
post_processor.allow_auto_download = "true"
```

**لماذا هذا مهم:** فئة `AsposeAI` تُحمِّل نموذج لغة مدرب مسبقًا يفهم السياق، علامات الترقيم، والأخطاء الشائعة في OCR. ضبط `allow_auto_download` إلى `"true"` يلغي الحاجة إلى تحميل النموذج يدويًا، مما يجعل السكريبت قابلًا للنقل.

## الخطوة 3: تطبيق تصحيح مدفوع بالذكاء الاصطناعي لتحسين مخرجات OCR

الآن قم بتمرير نتيجة OCR الأولية إلى معالج ما بعد AI. سيعيد النموذج نسخة منقحة من النص، مُصححةً الأخطاء النموذجية مثل تبديل الأحرف، فقدان الفراغات، أو الحالة غير الصحيحة.

```python
# Step 3: Apply AI‑based correction to improve the OCR output
clean_result = post_processor.run_postprocessor(raw_result)
```

**كيف يعمل:** `run_postprocessor` يحلل السلسلة الأولية، يطبق استدلال نموذج اللغة، ويُخرج كائن نتيجة جديد. الخاصية `text` في `clean_result` تحتوي على النسخة المصححة من النص، والتي تكون عادةً أكثر دقة من مخرجات OCR الأولية.

## الخطوة 4: عرض النتيجة المصححة

اطبع النص النهائي المُحسّن بالذكاء الاصطناعي للتحقق من التحويل. يمكنك أيضًا كتابة النتيجة إلى ملف للمعالجة لاحقًا.

```python
# Step 4: Display the corrected text
print("Corrected text:", clean_result.text)

# Optional: Save the result to a .txt file
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(clean_result.text)
```

**النتيجة المتوقعة:** بالنسبة لصورة إيصال واضحة، قد ترى شيئًا مثل:

```
Corrected text: Total: $23.45
Date: 2026-09-28
Item 1  Apple   $1.20
Item 2  Bread   $2.50
...
```

معالج AI عادةً ما يزيل الرموز العشوائية (`#`, `@`) ويعيد تنسيق الفواصل السطرية بشكل صحيح.

## الخطوة 5: تحرير الموارد

عند انتهاء السكريبت، حرّر أي موارد أصلية يحتفظ بها محرك AsposeAI. هذا يمنع تسرب الذاكرة في التطبيقات التي تعمل لفترات طويلة.

```python
# Step 5: Release AI resources when done
post_processor.free_resources()
```

**أفضل ممارسة:** دائمًا استدعِ `free_resources()` داخل كتلة `finally` أو استخدم مدير سياق إذا دمجت هذا الكود في خدمة أكبر.

## المشكلات الشائعة والنصائح

| المشكلة | سبب حدوثها | كيفية الإصلاح |
|-------|----------------|---------------|
| **صورة JPG غير واضحة** | انخفاض التباين يقلل من دقة OCR. | قم بمعالجة الصورة مسبقًا باستخدام `opencv` لزيادة التباين قبل الخطوة 1. |
| **نموذج اللغة مفقود** | تم تعطيل التحميل التلقائي أو لا يوجد إنترنت. | قم بتعيين `post_processor.allow_auto_download = "false"` وضع النموذج يدويًا في المجلد المتوقع. |
| **ملفات PDF الكبيرة مقسمة إلى العديد من JPGs** | كل صفحة تحتاج إلى استدعاء OCR منفصل. | قم بالتكرار عبر الملفات في دليل ودمج نتائج `clean_result.text`. |
| **حروف غير لاتينية** | النموذج الافتراضي مدرب على اللغة الإنجليزية. | استخدم `post_processor.set_language("es")` (أو لغة مدعومة أخرى) قبل تشغيل المعالج اللاحق. |

تستفيد هذه النصائح من قدرات **Python OCR** و **AsposeAI post‑processing** لجعل خط أنابيب **تحويل الصورة إلى نص** بالكامل قويًا.

## السكريبت الكامل يمكنك نسخه ولصقه

فيما يلي البرنامج الكامل القابل للتنفيذ الذي يدمج جميع الخطوات ومعالجة الأخطاء.

```python
# extract_text_from_jpg.py
import sys
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI

def extract_text(image_path: str, output_path: str = "extracted_text.txt"):
    # Initialize OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.load_image(image_path)

    # Perform basic OCR
    raw_result = ocr_engine.recognize()
    print("Raw OCR output:", raw_result.text)

    # Set up AsposeAI post‑processor
    post_processor = AsposeAI()
    post_processor.allow_auto_download = "true"

    # Run AI correction
    clean_result = post_processor.run_postprocessor(raw_result)

    # Show corrected text
    print("Corrected text:", clean_result.text)

    # Save to file
    with open(output_path, "w", encoding="utf-8") as f:
        f.write(clean_result.text)

    # Release resources
    post_processor.free_resources()

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python extract_text_from_jpg.py <path_to_jpg>")
        sys.exit(1)

    image_file = sys.argv[1]
    extract_text(image_file)
```

شغّل السكريبت من سطر الأوامر:

```bash
python extract_text_from_jpg.py YOUR_DIRECTORY/sample.jpg
```

يقوم البرنامج بطباعة كل من النص الأولي والنص المصحح، ثم يكتب النتيجة النظيفة إلى `extracted_text.txt`.

## الخلاصة

أنت الآن تعرف كيف **استخراج النص من صورة JPG** باستخدام سير عمل موثوق لـ Python OCR مدعوم بمعالجة ما بعد AsposeAI. غطى الدليل تثبيت SDK، تشغيل التعرف الضوئي على الأحرف في Python، تطبيق تصحيح مدفوع بالذكاء الاصطناعي، وتنظيف الموارد.

من هنا يمكنك:

- دمج السكريبت في معالج دفعي لمئات الصور.
- تجربة مكتبات **تحويل الصورة إلى نص** أخرى مثل Tesseract للمقارنة.
- استكشاف ميزات إضافية في AsposeAI مثل نماذج لغات محددة أو مفردات مخصصة.

برمجة سعيدة، واستمتع بتحويل الصور إلى نص قابل للبحث!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [How to Run OCR on Invoices – Extract Text from Image with Python](/ocr/english/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}