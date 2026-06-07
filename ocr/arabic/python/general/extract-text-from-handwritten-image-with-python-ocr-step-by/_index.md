---
category: general
date: 2026-06-06
description: استخراج النص من صورة مكتوبة بخط اليد باستخدام OCR في بايثون. تعلم كيفية
  تحويل صورة مكتوبة بخط اليد إلى نص بسرعة وموثوقية.
draft: false
keywords:
- extract text from handwritten image
- convert handwritten photo to text
- how to recognize handwritten text
- python ocr handwritten recognition
language: ar
og_description: استخراج النص من صورة مكتوبة بخط اليد باستخدام بايثون. يوضح هذا الدليل
  كيفية تحويل صورة مكتوبة بخط اليد إلى نص ويجيب عن كيفية التعرف على النص المكتوب بخط
  اليد.
og_title: استخراج النص من صورة مكتوبة بخط اليد – دليل بايثون لتقنية OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from handwritten image using Python OCR. Learn how to
    convert handwritten photo to text quickly and reliably.
  headline: Extract Text from Handwritten Image with Python OCR – Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Handwriting
title: استخراج النص من صورة مكتوبة بخط اليد باستخدام OCR في بايثون – دليل خطوة بخطوة
url: /ar/python/general/extract-text-from-handwritten-image-with-python-ocr-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة مكتوبة بخط اليد باستخدام Python OCR – دليل خطوة بخطوة

هل تساءلت يومًا **كيف تتعرف على النص المكتوب بخط اليد** في صورة التقطتها بهاتفك؟ لست وحدك. في العديد من المشاريع—سواء كان ذلك لتحويل ملاحظات المحاضرات إلى رقمية أو استخراج البيانات من النماذج الموقعة—تحتاج إلى **استخراج النص من صورة مكتوبة بخط اليد** بسرعة وبدون عناء.  

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح لك بالضبط كيف **تحول صورة مكتوبة بخط اليد إلى نص** باستخدام مكتبة OCR شائعة في Python. لا مراجع غامضة، فقط كود ملموس، شروحات، ونصائح يمكنك نسخها ولصقها اليوم.

![extract text from handwritten image](https://example.com/placeholder-handwritten.jpg "extract text from handwritten image")

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

| المتطلب | لماذا يهم |
|---------|-----------|
| Python 3.9 أو أحدث | دعم الصياغة الحديثة والمكتبات |
| `pip` (مدير حزم Python) | لتثبيت حزمة OCR |
| صورة واضحة لملاحظات مكتوبة بخط اليد (JPEG/PNG) | دقة OCR تنخفض مع الصور الضبابية |
| إلمام أساسي بدوال Python | يساعدك على تعديل المثال لاحقًا |

إذا كان أي من هذه غير متوفر، احصل على أحدث نسخة من Python من <https://python.org> وقم بتثبيتها—بدون تعقيدات.

## تثبيت مكتبة OCR للـ Python

المقتطف البرمجي الذي سنستخدمه يعتمد على حزمة `ocr` (غلاف خفيف حول Tesseract يضيف إعدادات مفيدة). ثبّتها بأمر واحد:

```bash
pip install ocr
```

> **نصيحة احترافية:** بعد التثبيت، شغّل `tesseract --version` في الطرفية لتتأكد من وجود المحرك الأساسي. إذا لم يكن لديك Tesseract، اتبع الدليل الرسمي لنظامك—معظم مديري الحزم يحتويونه (`apt-get install tesseract-ocr` على Ubuntu، `brew install tesseract` على macOS).

## الخطوة 1: إنشاء كائن محرك OCR

إنشاء المحرك هو الحجر الأول في جدار **python ocr handwritten recognition**. فكر في المحرك كالعقل الذي سيقرأ الخربشات لاحقًا.

```python
# Step 1: Import the library and instantiate the OCR engine
import ocr

# The OcrEngine class gives us access to all the low‑level settings.
engine = ocr.OcrEngine()
```

لماذا هذا مهم: بدون محرك لا يمكنك تعديل خط أنابيب التعرف. الإعدادات الافتراضية مهيأة للنص المطبوع، لذا سنحتاج لتعديلها في الخطوة التالية.

## الخطوة 2: تفعيل التعرف على الخط اليدوي

بشكل افتراضي يفترض المحرك أن الأحرف مطبوعة. تفعيل وضع الخط اليدوي يغيّر الإعداد ليخبر Tesseract باستخدام نموذج LSTM المدرب على الخطوط المتصلة.

```python
# Step 2: Turn on handwritten mode
engine.ocr_settings.enable_handwritten_recognition = True
```

> **ماذا يحدث إذا تخطيت هذه الخطوة؟** سيعامل OCR الضربات كضوضاء، مما ينتج مخرجات غير مفهومة. تفعيل العلامة هو جوهر **how to recognize handwritten text**.

## الخطوة 3: تحميل صورة الخط اليدوي

الآن نوجه المحرك إلى ملف الصورة. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف.

```python
# Step 3: Load the image containing the handwritten notes
image_path = "YOUR_DIRECTORY/handwritten_note.jpg"
engine.load_image(image_path)
```

تحقق سريعًا: افتح الصورة في عارض النظام. إذا كان النص غير واضح، فكر في ما قبل المعالجة (زيادة التباين، تدوير) قبل تمريرها إلى المحرك—هذه التعديلات غالبًا ما تحسن معدل نجاح **extract text from handwritten image**.

## الخطوة 4: تشغيل عملية التعرف

مع إعداد كل شيء، نطلب من المحرك الآن أداء مهمته. طريقة `recognize()` تُعيد كائن نتيجة يحتوي على السلسلة المستخرجة ودرجات الثقة.

```python
# Step 4: Execute the OCR process
handwritten_result = engine.recognize()
```

خلف الكواليس، يحول المحرك البت ماب إلى سلسلة من متجهات الخصائص، يمررها عبر شبكة LSTM، ثم يجمع الأحرف معًا. هذه هي سحر **python ocr handwritten recognition**.

## الخطوة 5: عرض النص المستخرج

كائن النتيجة يوفّر خاصية `.text` التي تحتوي على سلسلة Unicode صافية. اطبعها، احفظها في ملف، أو مرّرها إلى خط أنابيب آخر—اختيارك.

```python
# Step 5: Print the extracted text to the console
print("=== Extracted Text ===")
print(handwritten_result.text)
```

### النتيجة المتوقعة

إذا كانت الصورة المصدر تحتوي على الملاحظة “Buy milk, eggs, and bread”، فستظهر لك شيء مثل:

```
=== Extracted Text ===
Buy milk, eggs, and bread
```

لاحظ كيف تحافظ النتيجة على علامات الترقيم وفواصل الأسطر (إن وجدت). إذا حصلت على نص غير مفهوم، أعد فحص جودة الصورة وعلامة `enable_handwritten_recognition`.

## معالجة المشكلات الشائعة

| المشكلة | العرض | الحل |
|---------|-------|------|
| درجات ثقة منخفضة | ظهور الكثير من “?” أو أحرف غير منطقية | زيادة DPI الصورة إلى ≥300، تطبيق التحويل إلى ثنائي (`opencv`)، أو قص المنطقة المطلوبة. |
| لغات مختلطة | المخرجات تمزج بين الإنجليزية ونص آخر | عيّن `engine.ocr_settings.language = "eng"` (أو أي رمز ISO آخر) قبل `recognize()`. |
| ملفات كبيرة | وقت معالجة طويل أو خطأ في الذاكرة | قلل أبعاد الصورة إلى حجم معقول (مثلاً عرض أقصى 1200 px) قبل التحميل. |
| عدم وجود Tesseract | `ImportError` أو `FileNotFoundError` | ثبّت Tesseract منفصلًا وتأكد من إضافته إلى PATH النظام. |

هذه التعديلات تجعل سير عمل **convert handwritten photo to text** ثابتًا عبر مجموعات بيانات متنوعة.

## البرنامج الكامل الذي يمكنك تشغيله الآن

فيما يلي البرنامج الكامل المستقل الذي يجمع كل الأجزاء معًا. انسخه إلى ملف باسم `handwritten_ocr.py` وشغّله بالأمر `python handwritten_ocr.py`.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py

A minimal example that demonstrates how to extract text from handwritten image
using Python OCR (handwritten recognition mode). Adjust `image_path` to point
to your own file before running.
"""

import ocr  # pip install ocr

def main():
    # 1️⃣ Create the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Enable the handwritten recognition flag
    engine.ocr_settings.enable_handwritten_recognition = True

    # 3️⃣ Load the target image
    image_path = "YOUR_DIRECTORY/handwritten_note.jpg"
    engine.load_image(image_path)

    # 4️⃣ Run the OCR process
    result = engine.recognize()

    # 5️⃣ Output the extracted text
    print("=== Extracted Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

شغّله، وسترى النص يُطبع في الطرفية—بالضبط النتيجة التي تحتاجها عندما تريد **convert handwritten photo to text**.

## التعمق أكثر

الآن بعد أن أتقنت أساسيات **extract text from handwritten image**، فكر في الخطوات التالية:

- **المعالجة الدفعية:** كرّر العملية على مجلد من الصور واحفظ كل نتيجة في ملف CSV.
- **ما بعد المعالجة:** استخدم تعبيرات نمطية لتنظيف الأخطاء الشائعة في OCR (مثل “1” مقابل “l”).
- **التكامل:** مرّر السلاسل المستخرجة إلى خط أنابيب معالجة لغة طبيعية لتحليل المشاعر أو استخراج الكلمات المفتاحية.
- **مكتبات بديلة:** إذا احتجت دقة أعلى، استكشف `easyocr` أو `pytesseract` مع نماذج LSTM مخصصة—كلاهما يدعم **python ocr handwritten recognition**.

تذكر أن جودة الصورة المصدر غالبًا ما تحدد النجاح، لذا خصص بضع دقائق للمعالجة المسبقة. قليل من الجهد الآن يوفر عليك الكثير من التصحيح لاحقًا.

## الخلاصة

استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح **how to recognize handwritten text**، والأهم من ذلك **extract text from handwritten image** باستخدام Python. عبر تثبيت حزمة `ocr`، تفعيل وضع الخط اليدوي، تحميل الصورة، واستدعاء `recognize()`، يمكنك **convert handwritten photo to text** في بضع أسطر فقط.

جرّبه على ملاحظاتك الخاصة، عدّل خطوات المعالجة المسبقة، ودع OCR يتولى العبء. إذا واجهت أي صعوبات، ارجع إلى جدول “معالجة المشكلات الشائعة” أو جرّب محركات OCR بديلة. برمجة سعيدة، ولتصبح بياناتك المكتوبة بخط اليد قابلة للبحث فورًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/)
- [How to Use OCR - Recognize Image without Text Area Detection](/ocr/english/net/image-and-drawing-recognition/recognize-image-without-text-area-detection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}