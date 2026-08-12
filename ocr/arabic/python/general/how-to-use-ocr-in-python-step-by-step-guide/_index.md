---
category: general
date: 2026-08-12
description: كيفية استخدام OCR في بايثون للتعرف على النص من الصورة، استخراج النص،
  تحويل الصورة إلى نص، وتنظيف نص OCR باستخدام المعالجة اللاحقة بالذكاء الاصطناعي.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: ar
lastmod: 2026-08-12
og_description: كيفية استخدام OCR في بايثون لتحويل الصور إلى نص قابل للتحرير. تعلم
  كيفية التعرف على النص من الصورة، استخراج النص، تحويل الصورة إلى نص، وتنظيف نص OCR
  باستخدام الذكاء الاصطناعي.
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: كيفية استخدام OCR في بايثون – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: كيفية استخدام OCR في بايثون – دليل خطوة بخطوة
url: /ar/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في بايثون – دليل خطوة بخطوة

إذا كنت بحاجة إلى **كيفية استخدام OCR** لتحويل المستندات الممسوحة ضوئياً أو لقطات الشاشة إلى نص قابل للتحرير، فإن هذا الدليل يوضح حلًا كاملاً في بايثون. ستتعلم كيفية التعرف على النص من الصورة، استخراج النص من الصورة، تحويل الصورة إلى نص، وتنظيف نص OCR باستخدام معالج ما بعد المعالجة الذكي الخفيف.

يغطي الدليل كل شيء بدءًا من تثبيت المكتبات المطلوبة إلى التعامل مع الصور منخفضة الجودة، بحيث يمكنك دمج OCR في أي خط أنابيب أتمتة دون التخمين بشأن الخطوة المفقودة.

## ما ستبنيه

بنهاية هذه المقالة ستحصل على سكريبت بايثون واحد يقوم بـ:

1. تحميل ملف صورة (PNG أو JPEG أو TIFF).  
2. التعرف على النص من الصورة باستخدام محرك OCR.  
3. تحسين المخرجات الأولية باستخدام معالج ما بعد المعالجة المدعوم بالذكاء الاصطناعي.  
4. طباعة النص المنقح إلى وحدة التحكم.

لا توجد خدمات خارجية مطلوبة—كل شيء يعمل محليًا، مما يجعل الحل مناسبًا للبيئات غير المتصلة أو المشاريع الحساسة للخصوصية.

## المتطلبات المسبقة

- Python 3.9 أو أحدث.  
- مكتبات `pytesseract` و `Pillow` (`pip install pytesseract pillow`).  
- تثبيت ملف تنفيذ Tesseract‑OCR وجعله متاحًا في `PATH` الخاص بالنظام.  
- فهم أساسي للدوال في بايثون.  

إذا كنت تمتلك هذه العناصر بالفعل، يمكنك القفز مباشرة إلى أول كتلة شفرة.

## كيفية استخدام OCR مع بايثون

الجوهر الأساسي **كيفية استخدام OCR** هو تهيئة محرك OCR وتزويده بصورة. في هذا الدليل نستخدم `pytesseract`، وهو غلاف خفيف حول محرك Tesseract المفتوح المصدر.

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **لماذا هذه الخطوة مهمة** – يتوقع Tesseract صورة نظيفة وموجهة بشكل صحيح. يضمن Pillow أن بيانات الصورة مُعَدلَة قبل تشغيل OCR، مما يحسن دقة عملية **التعرف على النص من الصورة** اللاحقة.

## التعرف على النص من الصورة

الآن نستدعي `pytesseract.image_to_string` لاستخراج السلسلة الأولية. هذه هي الدعوة الكلاسيكية لـ **التعرف على النص من الصورة**.

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **لماذا نفصل الدالة** – عزل خطوة OCR يتيح لك استبدال المحرك لاحقًا (مثلاً، التحويل إلى EasyOCR) دون تعديل باقي خط الأنابيب. كما يجعل اختبار الوحدة أسهل.

## استخراج النص من الصورة وتحسين الجودة

غالبًا ما يحتوي إخراج OCR الخام على فواصل أسطر، أحرف عشوائية، أو كلمات تم التعرف عليها بشكل خاطئ. يمكن لمعالج ما بعد المعالجة الذكي تنظيف هذه العيوب تلقائيًا. أدناه مثال بسيط يستخدم مكتبة `transformers` لتشغيل نموذج لغة صغير محليًا. يمكنك استبداله بأي خدمة مملوكة إذا رغبت.

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **لماذا يساعد معالج ما بعد المعالجة الذكي** – تتفوق محركات OCR التقليدية في التعرف على الأحرف لكنها تكافح مع التخطيط والضوضاء. نموذج اللغة يفهم السياق، لذا يمكنه تحويل “Th1s 1s 4 test.” إلى “This is a test.” هذه الخطوة تلبي مباشرةً متطلب **تنظيف نص OCR**.

## تحويل الصورة إلى نص – السكريبت الكامل

جمع كل الأجزاء معًا ينتج سكريبت قصير يقوم بـ **تحويل الصورة إلى نص** من البداية إلى النهاية.

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### النتيجة المتوقعة

تشغيل السكريبت مع صورة تجريبية (`sample.png`) قد ينتج:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

لاحظ كيف قام معالج الذكاء الاصطناعي بتصحيح الأحرف التي قرأها بشكل خاطئ وإزالة فاصل السطر العشوائي. هذا يوضح سير عمل **استخراج النص من الصورة** بالكامل ويظهر فائدة تنظيف نص OCR.

## معالجة الحالات الشائعة

| الحالة                                 | التعديل الموصى به                                                               |
|----------------------------------------|---------------------------------------------------------------------------------|
| صورة منخفضة التباين                     | تحويلها إلى تدرج رمادي وزيادة التباين باستخدام `ImageEnhance` قبل OCR.        |
| مستند متعدد اللغات                     | تمرير قائمة مفصولة بفواصل إلى `lang` (مثال: `lang='eng+fra'`).                |
| صور كبيرة جدًا ( > 2000 px )           | تقليل الحجم باستخدام `img.thumbnail((2000, 2000))` لتسريع Tesseract.          |
| عدم وجود ملف تنفيذ Tesseract            | التحقق من أن `pytesseract.pytesseract.tesseract_cmd` يشير إلى الملف التنفيذي. |
| معالج ما بعد المعالجة الذكي بطيء        | استخدام نموذج أصغر (`t5-small`) أو تشغيل المعالج على وحدة معالجة رسومية.    |

> **نصيحة احترافية:** احفظ كائن نموذج الذكاء الاصطناعي (`_ai_postprocessor`) عند استيراد الوحدة، كما هو موضح، لتجنب إعادة تحميله في كل استدعاء. هذا يقلل من زمن الاستجابة بشكل كبير عند معالجة العديد من الصور.

## نهج بديلة

- **EasyOCR**: مكتبة OCR مكتوبة بالكامل ببايثون تدعم أكثر من 80 لغة دون الحاجة إلى ملف تنفيذ خارجي. استبدل `ocr_recognize` بـ `EasyOCR.Reader` إذا كنت تفضل حلاً يعتمد على pip فقط.  
- **واجهات برمجة تطبيقات OCR السحابية**: Google Cloud Vision، Azure Computer Vision، أو Amazon Textract توفر دقة أعلى لتخطيطات معقدة لكن تتطلب اتصالًا بالشبكة وفوترة.  
- **معالجة ما بعد المعالجة المخصصة**: للتنظيف الحتمي، يمكن للتعبيرات النمطية (`re.sub`) إصلاح الأنماط الشائعة (مثل إزالة الفواصل المربوطة) دون الحاجة إلى نموذج ذكاء اصطناعي.

## الخلاصة

أنت الآن تعرف **كيفية استخدام OCR** في بايثون للتعرف على النص من الصورة، استخراج النص من الصورة، تحويل الصورة إلى نص، وتنظيف نص OCR باستخدام معالج ما بعد المعالجة الذكي. يوضح السكريبت الكامل خط أنابيب جاهز للإنتاج يمكنك توسيعه بعمليات تمهيد إضافية (تقليل الضوضاء، تصحيح الميل) أو إجراءات لاحقة (حفظ إلى قاعدة بيانات، إمداد فهرس بحث).

### الخطوات التالية

- جرب نماذج ذكاء اصطناعي مختلفة (مثل `gpt‑2`، `flan‑ul2`) لترى أيها يقدم أفضل تنظيف لمجالك.  
- دمج الخط الأنابيب في خدمة ويب باستخدام Flask أو FastAPI، لتحويل السكريبت إلى نقطة نهاية OCR عند الطلب.  
- استكشاف المعالجة الدفعية: التكرار عبر دليل من الصور وكتابة كل ناتج منقح إلى ملف `.txt` مطابق.

لا تتردد في تعديل الكود ليتناسب مع سير عملك الخاص، ودع النص القابل للبحث يعزز المرحلة التالية من تطبيقك. برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}