---
category: general
date: 2026-04-26
description: 'كيفية OCR في بايثون: تعلم استخراج النص من الصورة وقراءة ملف TIFF باستخدام
  بايثون عبر مثال OCR أساسي. كود سريع قابل للتنفيذ مرفق.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: ar
og_description: 'كيفية التعرف الضوئي على الأحرف باستخدام بايثون: دليل خطوة بخطوة يوضح
  كيفية استخراج النص من الصورة، قراءة ملف TIFF باستخدام بايثون، وتحويل نص الصورة الممسوحة
  ضوئياً باستخدام سكريبت بسيط قابل للتنفيذ.'
og_title: كيفية تنفيذ OCR في بايثون – مثال أساسي لاستخراج النص
tags:
- OCR
- Python
- Image Processing
title: كيفية OCR في بايثون – مثال أساسي لاستخراج النص
url: /ar/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيف تستخدم OCR في بايثون – مثال أساسي لاستخراج النص

هل تساءلت يومًا **how to ocr python** عندما يكون لديك ملف TIFF ممسوح ضائع على مكتبك؟ لست الوحيد الذي ينظر إلى مجموعة من ملفات الصور ويسأل: “كيف أحصل على الكلمات من هذا؟” الخبر السار هو أن تحويل صورة إلى نص عادي أمر سهل للغاية مع المكتبة المناسبة وبعض الخطوات الواضحة.

في هذا الدرس سنستعرض **مثال OCR أساسي** يقرأ ملف TIFF، يستخرج النص، ويطبعه على وحدة التحكم. بنهاية الدرس ستعرف بالضبط كيف **extract text from image** من ملفات الصور، وكيفية التعامل مع خصائص تنسيق TIFF، وما الذي يمكنك تعديلّه إذا احتجت **convert scanned image text** إلى شيء أكثر فائدة. لا سحر مخفي—فقط بايثون مباشر يمكنك نسخه‑ولصقه وتشغيله اليوم.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.9+ مثبت (أفضل نسخة مستقرة حديثة).
- مكتبة OCR قابلة للتثبيت عبر pip. في هذا الدليل سنستخدم حزمة خيالية `aocr` تحاكي أدوات شائعة مثل Tesseract؛ يمكنك استبدالها بـ `pytesseract` أو `easyocr` لاحقًا.
- صورة TIFF تريد معالجتها – سميها `input.tiff` وضعها في مجلد ستشير إليه في الكود.
- إلمام أساسي بسطر الأوامر (فقط لتثبيت الحزمة).

هذا كل شيء. لا تبعيات ثقيلة، لا حاويات Docker، فقط بضع أسطر من الكود.

## الخطوة 1 – تثبيت واستيراد الاعتمادات (how to ocr python)

أولًا، احصل على حزمة OCR. افتح الطرفية وشغّل:

```bash
pip install aocr
```

إذا كنت تفضّل مكتبة حقيقية، استبدل `aocr` بـ `pytesseract` وثبّت محرك Tesseract بشكل منفصل.

الآن استورد ما نحتاجه. فئة `Path` من `pathlib` تعطيك طريقة نظيفة للعمل مع مسارات الملفات عبر أنظمة التشغيل.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*لماذا نستخدم `Path`؟* لأنها تُجرد الفروقات بين الشرطتين (`/` مقابل `\`) وتسمح لك بدمج الأدلة دون القلق بشأن نظام التشغيل الأساسي. هذه التفاصيل الصغيرة غالبًا ما توفر صداعًا عندما تنقل السكريبت إلى خادم CI لاحقًا.

## الخطوة 2 – إنشاء نسخة من محرك OCR (basic ocr example)

بعد ذلك، شغّل محرك OCR. فكر في `OcrEngine` كالعقل الذي سيقرأ الصورة ويُخرج الأحرف.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

معظم مكتبات OCR تسمح لك بتعديل اللغة، DPI، أو عتبات الثقة هنا. لهذا **basic OCR example** سنبقى على الإعدادات الافتراضية، لكن يمكنك استكشاف `ocr_engine.config` لاحقًا إذا احتجت معالجة مستندات متعددة اللغات.

## الخطوة 3 – تحميل صورة TIFF الخاصة بك (read tiff file python)

هنا يأتي دور **read tiff file python**. يمكن أن تكون ملفات TIFF متعددة الصفحات، لكن `Image.load` سيجلب الصفحة الأولى افتراضيًا—مناسب للمسح بصفحة واحدة.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

استبدل `"YOUR_DIRECTORY"` بالمجلد الفعلي الذي يحتوي على `input.tiff`. إذا لم تكن متأكدًا من مكان تشغيل السكريبت، فإن `Path.cwd()` يطبع دليل العمل الحالي—مفيد لتصحيح مشاكل المسار.

## الخطوة 4 – تشغيل عملية OCR (extract text from image)

الآن يحدث السحر. استدعاء `process()` يرسل الصورة عبر خط أنابيب OCR ويعيد كائن نتيجة.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

خلف الكواليس قد يقوم المحرك بتحويل الصورة إلى تدرج رمادي، تطبيق عتبة، وإدخالها في شبكة عصبية. لا تحتاج لإدارة هذه الخطوات؛ المكتبة تتولى ذلك.

## الخطوة 5 – طباعة النص المُعترف به (convert scanned image text)

أخيرًا، اعرض النص. في المشاريع الحقيقية قد تكتب النتيجة إلى ملف أو قاعدة بيانات، لكن الطباعة تبقي المثال بسيطًا.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

عند تشغيل السكريبت، يجب أن ترى شيئًا مثل:

```
Hello, world!
This is a sample scanned document.
```

إذا كان الإخراج مشوشًا، تحقق من وضوح الصورة الأصلية وأن لغة OCR تتطابق مع النص.

## السكريبت الكامل العامل

بجمع كل ما سبق، إليك البرنامج الكامل الجاهز للتنفيذ:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

إذا أردت **convert scanned image text** إلى PDF قابل للبحث، يمكنك تمرير `ocr_result.text` إلى مولد PDF مثل `reportlab`—لكن ذلك درس كامل بحد ذاته.

## المشكلات الشائعة والنصائح الاحترافية

- **المسحات منخفضة الدقة**: يواجه OCR صعوبة تحت 150 DPI. إذا كان TIFF غير واضح، قم بزيادة الدقة أولًا باستخدام Pillow (`Image.open(...).resize(...)`).
- **الصفحات المتعددة**: للـ TIFF متعدد الصفحات، كرّر عبر `Image.load_multi_page()` (إن كانت مكتبتك تدعم ذلك) وادمج النتائج.
- **دعم اللغات**: معظم المحركات تفترض الإنجليزية افتراضيًا. عيّن `ocr_engine.language = "spa"` للإسبانية، على سبيل المثال.
- **معالجة الفراغات**: غالبًا ما يضيف OCR فواصل سطر عشوائية. استخدم `str.splitlines()` أو تعبيرات نمطية لتنظيف الإخراج.
- **الأداء**: للمعالجة الجماعية، أعد استخدام نسخة واحدة من `OcrEngine` بدلاً من إنشاء نسخة جديدة لكل ملف.

## توسيع المثال

الآن بعد أن أتقنت **how to ocr python** لصورة واحدة، فكر في الخطوات التالية:

1. **معالجة دفعات** – كرّر عبر مجلد من ملفات TIFF واكتب كل نتيجة إلى ملف `.txt`.
2. **التكامل مع Pandas** – احفظ النص المستخرج مع البيانات الوصفية لتحليل سريع.
3. **نهج هجين** – اجمع OCR مع مكتبات NLP مثل `spaCy` لاستخراج الكيانات (أسماء، تواريخ، مبالغ) من الفواتير الممسوحة.
4. **صيغ ملفات بديلة** – استبدل `Image.load` بـ `Image.from_bytes` للتعامل مع الصور الواردة من API أو قاعدة بيانات.

جميع هذه الأفكار تبني على الفكرة الأساسية لـ **extract text from image** و **convert scanned image text** إلى ما يمكن للآلات فهمه.

## الخلاصة

استعرضنا مثالًا واضحًا وشاملًا لـ **basic OCR example** يوضح **how to ocr python**، وكيف **read tiff file python**، وكيف **extract text from image** باستخدام بضع أسطر فقط. السكريبت مستقل، يتضمن معالجة أخطاء، ويطبع النتيجة مباشرة، مما يجعله أساسًا قويًا لأي مشروع يحتاج إلى تحويل المستندات الممسوحة إلى نص قابل للتحرير.

لا تتردد في التجربة—غيّر محرك OCR، عدّل المعالجة المسبقة، أو اربط الناتج بسير عمل لاحق. السماء هي الحد عندما يمكنك بثقة **convert scanned image text** إلى بيانات قابلة للبحث.

هل لديك أسئلة حول حالات الحافة، حزم اللغات، أو تحسين الأداء؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

![how to ocr python example](/images/ocr-python-example.png "Screenshot of how to ocr python script output")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}