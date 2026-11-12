---
category: general
date: 2026-07-05
description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على صورة في بايثون بسرعة. تعلم
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف، استخراج النص من نموذج ممسوح ضوئياً،
  واستخدام OCR للتعرف على الصورة في بايثون.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: ar
og_description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون. يُظهر
  هذا الدرس كيفية تحميل الصورة للتعرف الضوئي على الأحرف، استخراج النص من نموذج ممسوح
  ضوئياً، واستخدام OCR للتعرف على الصورة في بايثون.
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: تنفيذ التعرف الضوئي على الحروف في الصورة باستخدام بايثون – دليل شامل
url: /ar/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة باستخدام Python – دليل كامل

هل احتجت يومًا إلى **perform OCR on image** للملفات لكنك لم تكن متأكدًا من أين تبدأ في Python؟ لست وحدك. سواءً كنت تقوم برقمنة الإيصالات، أو استخراج البيانات من نموذج استبيان صاخب، أو ببساطة تحويل ملف PDF ممسوح ضوئيًا إلى نص قابل للبحث، فإن القدرة على استخراج النص من نموذج ممسوح ضوئيًا هي نقطة ألم يومية للعديد من المطورين.

في هذا البرنامج التعليمي سنستعرض **how to use OCR Python** خطوة بخطوة، من تحميل الصورة إلى عرض النتيجة المفلترة. بنهاية الدرس ستعرف بالضبط كيف **load image for OCR**، وتضبط عتبات الثقة، وتستدعي طريقة **OCR recognize image Python** التي تقوم بالعمل الفعلي.

> **ما ستحصل عليه:** سكريبت جاهز للتنفيذ يحمل صورة، ينفذ OCR، ويطبع نصًا نظيفًا ومفلترًا حسب الثقة. لا مراجع غامضة، ولا استيرادات مفقودة—فقط حل كامل يمكنك نسخه ولصقه.

## ما ستحتاجه

قبل أن نغوص في التفاصيل، تأكد من وجود ما يلي:

* Python 3.9 أو أحدث مثبت (الكود يعمل على 3.10+ أيضًا).  
* حزمة OCR تتبع واجهة `ocr` المستخدمة أدناه – على سبيل المثال، المكتبة الوهمية `simple-ocr` أو أي غلاف يعرض `OcrEngine` و `Language` و `Image`.  
* ملف صورة (`.png`، `.jpg`، إلخ) يحتوي على النص الذي تريد استخراجَه.  
* طرفية أو بيئة تطوير (IDE) يمكنك من خلالها تشغيل سكريبت Python واحد.

إذا كان لديك كل ذلك بالفعل، عظيم—هيا نبدأ.

## إجراء OCR على الصورة – إعداد المحرك

أول شيء يجب عليك فعله هو إنشاء مثال (instance) لمحرك OCR. فكر في المحرك كالعقل وراء العملية؛ فهو يعرف كيف يفسر البكسلات ويحولها إلى أحرف.

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*لماذا هذا مهم:* بدون محرك لا شيء للمعالجة. كائن `OcrEngine` يحمل كل الإعدادات التي ستضبطها لاحقًا، مثل اللغة وعامل عتبة الثقة.

## تحميل الصورة لـ OCR – تحضير النموذج الممسوح ضوئيًا

الآن بعد أن أصبح المحرك موجودًا، نحتاج إلى **load image for OCR**. طريقة `Image.load()` في المكتبة تقرأ الملف من القرص وتحوّله إلى تمثيل داخلي يستطيع المحرك فهمه.

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **نصيحة:** إذا كنت تتعامل مع ملفات PDF، حوّل كل صفحة إلى صورة أولاً (مثلاً باستخدام `pdf2image`). محرك OCR يقبل فقط الصور النقطية.

## كيفية استخدام OCR Python – ضبط اللغة والثقة

معظم محركات OCR تدعم لغات متعددة وتتيح لك تصفية الأحرف ذات الثقة المنخفضة. ضبط هذه المعلمات مبكرًا يضمن حصولك على نص موثوق فقط.

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*لماذا 85 %؟* عمليًا، عتبة حول 80‑90 % تُزيل معظم النصوص العشوائية مع الحفاظ على المحتوى الجيد. لا تتردد في تعديلها بناءً على جودة المسحات الضوئية.

## استخراج النص من النموذج الممسوح ضوئيًا – التعرف على الصورة

مع جاهزية المحرك وتحميل الصورة، حان الوقت فعليًا لـ **perform OCR on image**. طريقة `recognize()` تُعيد كائن نتيجة يحتوي على النص المستخرج، واختياريًا، بيانات الصناديق المحيطة.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

إذا كانت المكتبة تدعم ذلك، قد يُظهر `result` أيضًا `result.confidences` (قائمة بدرجات الثقة لكل حرف) و `result.words` (كائنات كلمات مُنظمة). في هذا الدليل سنركز على مخرجات النص العادي.

## OCR Recognize Image Python – عرض النتائج المفلترة

أخيرًا، لنطبع النص المفلتر. الرموز ذات الثقة المنخفضة تظهر كعلامة استفهام (`?`) لأننا ضبطنا `min_confidence` إلى 85 %.

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### النتيجة المتوقعة

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

لاحظ كيف تحولت التوقيع غير القابل للقراءة إلى `?`. هذا بالضبط ما صُمم له مرشح الثقة—للحفاظ على نظافة المخرجات للمعالجة اللاحقة.

## المشكلات الشائعة والنصائح الاحترافية

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **إخراج فارغ** | الصورة مظلمة جدًا أو منخفضة الدقة. | قم بالمعالجة المسبقة باستخدام OpenCV: زيادة التباين، وتغيير الحجم إلى ≥300 dpi. |
| **حروف غير مفهومة** | تم اختيار لغة خاطئة. | اضبط `engine.language` لتطابق المستند (مثلاً `ocr.Language.FRENCH`). |
| **الكثير من رموز `?`** | عتبة الثقة مرتفعة جدًا. | قلل `engine.min_confidence` إلى 70‑80 % للمسحات الضوضائية. |
| **أخطاء Unicode** | الإخراج يحتوي على أحرف غير ASCII لكن ترميز الطرفية غير صحيح. | شغّل `python -X utf8` أو اضبط `PYTHONIOENCODING=utf-8`. |

**نصيحة احترافية:** إذا كنت بحاجة لاستخراج الجداول، قم بتمرير ثاني باستخدام محرك OCR يدرك التخطيط (مثل `--psm 6` في Tesseract) بعد أن تقوم بفلترة النص الخام.

## السكريبت الكامل – جاهز للتنفيذ

فيما يلي السكريبت الكامل المستقل الذي يدمج جميع الخطوات التي تم مناقشتها. احفظه باسم `perform_ocr.py`، عدل مسار الصورة، ونفّذ `python perform_ocr.py`.

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

شغّله، وسترى النص المفلتر يُطبع في الطرفية—بالضبط ما وعد به خطوة **extract text from scanned form**.

## ما التالي؟

الآن بعد أن عرفت كيفية **perform OCR on image** و **extract text from scanned form**، قد ترغب في استكشاف:

* **Batch processing** – تكرار عبر دليل يحتوي على صور لإنشاء ملف CSV بالنتائج.  
* **Post‑processing** – استخدم regex أو spaCy لاستخراج حقول مثل التواريخ، المبالغ، أو المعرفات.  
* **Integrations** – إدخال مخرجات OCR إلى قاعدة بيانات، Google Sheets، أو واجهة REST API.  

جميع هذه الأفكار بطبيعتها تتضمن نفس الدوال الأساسية التي غطيناها: تحميل الصورة، ضبط المحرك، واستدعاء طريقة **OCR recognize image Python**.

## الخلاصة

لقد استعرضنا مثالًا كاملًا وجاهزًا للإنتاج حول كيفية **perform OCR on image** باستخدام Python. من **loading image for OCR** إلى ضبط اللغة، وتعيين عتبة الثقة، وأخيرًا **extracting text from scanned form**، تم توضيح كل خطوة بكود واضح وشروحات. الآن لديك أساس قوي لمواجهة سيناريوهات أكثر تعقيدًا—سواء كان ذلك يعني وظائف دفعات، دعم متعدد اللغات، أو استخراج الجداول.

جرّب السكريبت، عدّل العتبات، وشاهد مستنداتك تصبح قابلة للبحث في دقائق. هل لديك أسئلة أو نموذج صعب لا يتعاون؟ اترك تعليقًا أدناه، ولنحل المشكلة معًا. برمجة سعيدة! 

![مثال على إجراء OCR على الصورة](example.png "إجراء OCR على الصورة")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخدام AspOCR: تصفية معالجة الصورة OCR لـ .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}