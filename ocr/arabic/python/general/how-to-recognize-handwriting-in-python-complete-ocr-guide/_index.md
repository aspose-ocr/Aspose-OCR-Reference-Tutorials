---
category: general
date: 2026-06-25
description: تعلم كيفية التعرف على الخط اليدوي باستخدام OCR في بايثون. يوضح لك هذا
  المثال في بايثون OCR كيفية استخراج النص المكتوب يدويًا وتحميل الصورة للتعرف الضوئي
  على الأحرف.
draft: false
keywords:
- how to recognize handwriting
- extract handwritten text
- convert handwritten image
- python ocr example
- load image for ocr
language: ar
og_description: كيفية التعرف على الخط اليدوي في بايثون باستخدام مكتبة OCR بسيطة. اتبع
  هذا الدليل خطوة بخطوة لاستخراج النص المكتوب يدويًا من أي صورة.
og_title: كيفية التعرف على الخط اليدوي في بايثون – دليل OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to recognize handwriting with Python OCR. This python ocr
    example walks you through extracting handwritten text and loading image for OCR.
  headline: How to Recognize Handwriting in Python – Complete OCR Guide
  type: TechArticle
- questions:
  - answer: Convert the first page to PNG using `pdf2image` before feeding it to `aocr`.
    question: What if my image is a PDF?
  - answer: Try increasing the DPI when you scan (300 dpi or higher) and ensure good
      lighting—shadows trick the model.
    question: Can I improve accuracy on cursive notes?
  - answer: Wrap the script in a loop that iterates over a directory, reusing the
      same `engine` instance for speed.
    question: Is there a way to batch‑process many files?
  - answer: As of v23.12 `aocr` supports English only; for other languages you’ll
      need a different library (e.g., Tesseract with language packs).
    question: What about non‑English handwriting?
  type: FAQPage
tags:
- OCR
- Python
- Handwriting Recognition
title: كيفية التعرف على الخط اليدوي في بايثون – دليل OCR الكامل
url: /ar/python/general/how-to-recognize-handwriting-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف على الخط اليدوي في بايثون – دليل OCR كامل

هل تساءلت يوماً **كيف تتعرف على الخط اليدوي** في صورة التقطتها بهاتفك؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة عندما يحتاجون لاستخراج الملاحظات المكتوبة بخط اليد أو التوقيعات أو الخربشات لإدخال البيانات. الخبر السار؟ ببضع أسطر من بايثون يمكنك تحويل مسح ضوئي فوضوي إلى نص نظيف قابل للبحث.

في هذا الدرس سنستعرض **مثال python ocr** يوضح لك بالضبط كيف **استخراج النص المكتوب بخط اليد**، **تحويل صورة الخط اليدوي** إلى سلاسل نصية، و**تحميل الصورة لـ OCR** باستخدام مكتبة `aocr`. في النهاية ستحصل على سكريبت جاهز للتنفيذ يمكنك وضعه في أي مشروع—بدون سحر، فقط كود واضح وتوضيحات لماذا يعمل.

## المتطلبات المسبقة والإعداد

قبل أن نبدأ، تأكد من وجود ما يلي:

- Python 3.8+ مثبت (المكتبة تعمل على جميع الإصدارات الحديثة).
- طرفية أو موجه أوامر تشعر بالراحة في استخدامه.
- ملف صورة يحتوي على نص مكتوب بخط يد مختلط (سنسميه `handwritten_mixed.png`).

إذا كان أي من ذلك غير مألوف لك، توقف هنا واحصل عليه—وإلا ستشعر أن الخطوات التالية كخبز كعكة بدون طحين.

### تثبيت مكتبة OCR

حزمة `aocr` ليست جزءًا من المكتبة القياسية، لذا احصل عليها من PyPI:

```bash
pip install aocr
```

> **نصيحة محترف:** استخدم بيئة افتراضية (`python -m venv venv`) للحفاظ على نظافة الاعتماديات.

## الخطوة 1: استيراد مكتبة OCR وإنشاء كائن المحرك

إنشاء المحرك هو أول شيء تقوم به عندما تريد **التعرف على الخط اليدوي**. فكر في المحرك كالعقل الذي سيُمعن النظر في صورتك ويبدأ في تخمين الحروف.

```python
# Step 1: Import the OCR library and instantiate the engine
import aocr

# The OcrEngine object holds all configuration and state
engine = aocr.OcrEngine()
```

لماذا نحتاج كائنًا؟ يسمح لك `OcrEngine` بتعديل الإعدادات—مثل التبديل بين وضع النص المطبوع ووضع الخط اليدوي—دون الحاجة لإعادة إنشاء خط الأنابيب بالكامل في كل مرة.

## الخطوة 2: تحميل الصورة لـ OCR

الآن نقوم فعليًا **بتحميل الصورة لـ OCR**. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف.

```python
# Step 2: Load the image containing mixed handwritten text
image_path = "YOUR_DIRECTORY/handwritten_mixed.png"
engine.load_image(image_path)
```

إذا كانت الصورة كبيرة، سيقوم `aocr` تلقائيًا بتقليص حجمها إلى حجم معقول، لكن يمكنك أيضًا تمرير وسائط إضافية للتحكم في DPI أو وضع اللون. هذه المرونة مفيدة عندما تحتاج **تحويل صورة الخط اليدوي** التي تأتي من مصادر مختلفة (ماسحات، هواتف، ملفات PDF).

## الخطوة 3: تفعيل وضع التعرف على الخط اليدوي

التعرف على الخط اليدوي ليس مفعلاً دائمًا بشكل افتراضي. بدءًا من الإصدار 23.12 أضافت المكتبة وضعًا مخصصًا، يحسن الدقة بشكل كبير على الخطوط المتصلة أو المائلة.

```python
# Step 3: Turn on handwritten mode (available from v23.12)
engine.recognition_mode = aocr.RecognitionMode.HANDWRITTEN
```

خلف الكواليس، يبدل المحرك نموذجه الداخلي بنموذج مدرب على ملايين الضربات بالقلم. إذا تخطيت هذه الخطوة، ستحصل على نتائج نص مطبوع تبدو كهراء.

## الخطوة 4: تنفيذ OCR والحصول على النتيجة

بعد ضبط كل شيء، اطلب من المحرك أداء مهمته. استدعاء `recognize()` متزامن—يُحجب التنفيذ حتى يصبح النص جاهزًا.

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize()
```

المتغير `result` هو سلسلة بايثون عادية، لذا يمكنك التعامل معه كأي نص آخر—تخزينه، البحث فيه، أو تمريره إلى نظام آخر.

## الخطوة 5: عرض النص المستخرج من الخط اليدوي

أخيرًا، اطبع النتيجة لتتحقق من أن خطوة **استخراج النص المكتوب بخط اليد** نجحت.

```python
# Step 5: Show the recognized handwriting
print("Handwritten mixed text:")
print(result)
```

### النتيجة المتوقعة

إذا كان `handwritten_mixed.png` يحتوي على شيء مثل:

```
Dear Alice,
Meet me at 5pm.
- Bob
```

يجب أن ترى:

```
Handwritten mixed text:
Dear Alice,
Meet me at 5pm.
- Bob
```

لاحظ كيف تم الحفاظ على فواصل الأسطر—`aocr` يحترم التخطيط الأصلي، وهو مفيد عندما تحتاج لاحقًا إلى إعادة تنسيق البيانات.

## السكريبت الكامل – تشغيل بنقرة واحدة

بجمع كل ما سبق، إليك المثال الكامل القابل للتنفيذ. انسخه إلى ملف باسم `handwriting_ocr.py` وشغّله بالأمر `python handwriting_ocr.py`.

```python
import aocr

def main():
    # 1️⃣ Create the OCR engine
    engine = aocr.OcrEngine()

    # 2️⃣ Load the target image
    image_path = "YOUR_DIRECTORY/handwritten_mixed.png"
    engine.load_image(image_path)

    # 3️⃣ Switch to handwritten mode (v23.12+)
    engine.recognition_mode = aocr.RecognitionMode.HANDWRITTEN

    # 4️⃣ Run the recognition process
    result = engine.recognize()

    # 5️⃣ Print the extracted text
    print("Handwritten mixed text:")
    print(result)

if __name__ == "__main__":
    main()
```

> **ملاحظة حول الحالات الحدية:** إذا كانت الصورة فارغة تمامًا أو تحتوي على نص مطبوع فقط، سيُعيد المحرك سلسلة فارغة أو نتيجة ذات ثقة منخفضة. يمكنك فحص `engine.last_confidence` (إذا كانت المكتبة تُظهرها) لتقرر ما إذا كنت ستعيد المحاولة مع خطوة تمهيدية مختلفة.

## أسئلة شائعة ونصائح

- **ماذا لو كانت صورتي ملف PDF؟** حوّل الصفحة الأولى إلى PNG باستخدام `pdf2image` قبل تمريرها إلى `aocr`.
- **هل يمكن تحسين الدقة على الملاحظات المتصلة؟** جرّب زيادة DPI عند المسح (300 dpi أو أعلى) وتأكد من إضاءة جيدة—الظلال تُربك النموذج.
- **هل هناك طريقة لمعالجة مجموعة ملفات دفعة واحدة؟** غلف السكريبت بحلقة تتنقل عبر مجلد، مع إعادة استخدام نفس كائن `engine` لتسريع العملية.
- **ماذا عن الخط اليدوي غير الإنجليزي؟** اعتبارًا من الإصدار v23.12 يدعم `aocr` اللغة الإنجليزية فقط؛ للغات أخرى ستحتاج مكتبة مختلفة (مثل Tesseract مع حزم اللغات).

## ملخص بصري

![مثال على إخراج التعرف على الخط اليدوي](/images/handwriting_ocr_output.png)

*النص البديل:* مثال على التعرف على الخط اليدوي يُظهر النص المستخرج من صورة مختلطة مكتوبة بخط يد.

## الخلاصة

أنت الآن تعرف **كيفية التعرف على الخط اليدوي** في بايثون باستخدام مكتبة OCR بسيطة. باتباعك لهذا **مثال python ocr** يمكنك **استخراج النص المكتوب بخط اليد**، **تحويل صورة الخط اليدوي** إلى سلاسل نصية قابلة للاستخدام، و**تحميل الصورة لـ OCR** ببضع أسطر فقط.

هل أنت مستعد للتحدي التالي؟ جرّب تمرير الناتج إلى محلل لغة طبيعية، خزنها في قاعدة بيانات، أو اربطها بمحرك تحويل النص إلى كلام لقراءة ملاحظاتك بصوت عالٍ. الاحتمالات لا حدود لها مثل الخربشات على منديل.

---

*برمجة سعيدة! إذا واجهت أي صعوبات، اترك تعليقًا أدناه وسنحل المشكلة معًا.*

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}