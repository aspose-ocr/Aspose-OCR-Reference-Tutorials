---
category: general
date: 2026-07-05
description: كيفية تصحيح ميل الصورة بسرعة. تعلم تمهيد الصورة للتعرف الضوئي على الأحرف
  (OCR)، تصحيح دوران الصورة، وتحويل المسح الضوئي إلى نص باستخدام بايثون.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: ar
og_description: كيفية تصحيح انحراف الصورة ومعالجة الصورة مسبقًا للتعرف الضوئي على
  الأحرف (OCR). يوضح هذا الدليل كيفية تصحيح دوران الصورة واستخراج النص من الصورة باستخدام
  بايثون.
og_title: كيفية تصحيح انحراف الصورة – معالجة OCR خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: كيفية إلغاء ميلان الصورة – دليل شامل لمعالجة ما قبل OCR
url: /ar/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تصحيح إمالة الصورة – دليل كامل لمعالجة ما قبل OCR

هل تساءلت يومًا **كيفية تصحيح إمالة الصورة** التي تبدو كأنها مأخوذة من ماسح مائل؟ لست وحدك. في العديد من المشاريع الواقعية، أول شيء يجب القيام به قبل أن تتمكن من **استخراج النص من الصورة** هو تعديل هذا الانحراف.

في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية **يعالج الصورة للـ OCR**، يُصحح الدوران، وأخيرًا **يحوّل المسح إلى نص** باستخدام مكتبة OCR بايثون. لا مراجع غامضة، بل سكريبت يعمل يمكنك نسخه ولصقه، بالإضافة إلى نصائح حول الأخطاء الشائعة.

## ما ستحققه

بنهاية هذا الدليل ستتمكن من:

* تحميل أي صورة JPEG أو PNG ممسوحة ضوئيًا ومائلة قليلًا.  
* تطبيق مرشح تصحيح الإمالة وخطوة التثنائي لزيادة دقة OCR.  
* تشغيل محرك OCR و**استخراج النص من الصورة** بشكل موثوق.  
* فهم لماذا **تصحيح دوران الصورة** مهم لاستخراج النص لاحقًا.  

### المتطلبات المسبقة

* Python 3.9+ مثبت على جهازك.  
* حزمة OCR قابلة للتثبيت عبر pip تحاكي مساحة الاسم `ocr` المستخدمة في المثال (مثلاً، غلاف خفيف حول Tesseract).  
* إلمام أساسي بدوال بايثون ومفاهيم معالجة الصور.  

إذا كان لديك هذه المتطلبات، فلنبدأ.

![how to deskew image example](deskew_before_after.png){alt="كيفية تصحيح إمالة الصورة – قبل وبعد التصحيح"}

## الخطوة 1: إعداد محرك OCR – كيفية تصحيح إمالة الصورة باستخدام بايثون

أولًا: تحتاج إلى محرك OCR يستطيع فهم لغة مستندك. المقتطف أدناه يوضح الحد الأدنى من الشيفرة لإنشاء المحرك وإعلامه بأنك تتعامل مع نص إنجليزي.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*لماذا هذا مهم:* إعداد لغة المحرك يؤثر على مجموعة الأحرف والقاموس المستخدم. تخطي هذه الخطوة قد يتسبب في تفسير OCR لكلمات شائعة بشكل خاطئ، خاصة بعد **تصحيح دوران الصورة**.

## الخطوة 2: تحميل الصورة الممسوحة التي تريد تعديلها

الآن نجلب الملف إلى الذاكرة. استبدل `"YOUR_DIRECTORY/skewed_scan.jpg"` بالمسار إلى صورتك الخاصة.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

إذا كانت الصورة بالفعل في مصفوفة NumPy أو كائن OpenCV `Mat`، يمكنك تعديل عملية التحميل وفقًا لذلك – المفتاح هو أن الكائن يجب أن يوفر طريقة `apply_filter` المستخدمة لاحقًا.

## الخطوة 3: معالجة الصورة للـ OCR – تصحيح الإمالة وتثنائيها

هنا يحدث السحر. نربط مرشحين:

1. **تصحيح الإمالة** – يكتشف تلقائيًا خط النص السائد ويعيد تدوير الصورة إلى الوضع الأفقي.  
2. **التثنائي (Otsu)** – يحول الصورة إلى أبيض وأسود نقي، مما يحسن معدلات التعرف بشكل كبير.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*نصيحة محترف:* إذا لاحظت أن النص لا يزال غير واضح بعد التثنائي، جرّب تعديل التباين أو استخدام طريقة عتبة مختلفة. وحدة `ocr.Filter` غالبًا ما تتضمن `adaptive_threshold()` للحالات الصعبة.

## الخطوة 4: تشغيل OCR – استخراج النص من الصورة

مع لوحة نظيفة ومسطحة، نسلم الصورة إلى المحرك. يحتوي كائن النتيجة على السلسلة المعترف بها، درجات الثقة، وحتى إطارات الحدود إذا احتجتها لاحقًا.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

المخرجات النموذجية تبدو هكذا:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

هل لاحظت أن فواصل الأسطر تتطابق تمامًا؟ هذا هو فائدة **تصحيح دوران الصورة** – لم يعد OCR بحاجة لتخمين اتجاه السطر.

## الخطوة 5: جمع كل شيء معًا – سكريبت ملف واحد لتحويل المسح إلى نص

فيما يلي السكريبت الكامل القابل للتنفيذ الذي يجمع كل الأجزاء التي ناقشناها. احفظه باسم `deskew_ocr.py` وشغّله بالأمر `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### لماذا يعمل هذا

* **تصحيح الإمالة أولًا** – تدوير الصورة قبل التثنائي يضمن أن خوارزمية العتبة تعمل على أفق مستوي.  
* **التثنائي بعد تصحيح الإمالة** – طريقة Otsu تفترض وجود توزيع ثنائي القمم؛ الصفحة المائلة ستفسد هذا الافتراض.  
* **نموذج اللغة الإنجليزية** – يخبر OCR ما هي الأحرف المتوقعة، مما يقلل الإيجابيات الزائفة.  

إذا احتجت لدعم لغات أخرى، استبدل `ocr.Language.ENGLISH` بالعدد المناسب من الـ enum.

## أسئلة شائعة وحالات خاصة

| السؤال | الجواب |
|----------|--------|
| *ماذا لو كان المسح مقلوبًا رأسًا على عقب؟* | عادةً يكتشف مرشح `deskew()` دوران 180° أيضًا. إذا فشل، استدعِ `apply_filter(ocr.Filter.rotate(180))` قبل تصحيح الإمالة. |
| *وثائقي يحتوي على رسومات ملونة – هل سيحذف التثنائي هذه الرسومات؟* | نعم. للمحتوى المختلط، استخدم `ocr.Filter.deskew()` فقط، ثم نفّذ OCR على الصورة الملونة. يمكنك استخراج النص مع الحفاظ على الرسومات. |
| *هل يمكنني معالجة مجموعة من الملفات؟* | ضع المنطق داخل حلقة، اقرأ كل مسار ملف من قائمة، واحفظ كل `result.text` في ملف `.txt` منفصل. |
| *كيف أحسن الدقة في المسحات منخفضة الدقة؟* | قم بتكبير الصورة بمرشح بيكوبيك **قبل** تصحيح الإمالة، ثم طبّق مرشح شحذ. المزيد من البكسلات يمنح محرك OCR دلائل أفضل. |

## إضافي: التحقق البصري من تصحيح الإمالة

إذا أردت رؤية الصورة قبل وبعد جنبًا إلى جنب، أضف مقتطف Matplotlib سريع:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

رؤية المحاذاة المصححة قد تكون مطمئنة، خاصةً عندما تقوم بتصحيح دفعة صعبة من المسحات.

## الخلاصة

غطّينا **كيفية تصحيح إمالة الصورة**، لماذا **معالجة الصورة للـ OCR** أمر أساسي، وكيفية **استخراج النص من الصورة** لتتمكن أخيرًا من **تحويل المسح إلى نص**. سير العمل — تحميل → تصحيح إمالة → تثنائي → التعرف — يضمن أن يرى OCR صفحة نظيفة ومستقيمة، ما يترجم إلى دقة أعلى وتصحيحات يدوية أقل.

ما الخطوة التالية في رحلتك مع OCR؟ جرّب التجربة بـ:

* حزم لغات مختلفة (`ocr.Language.FRENCH`، إلخ).  
* إضافة خطوة تحليل تخطيط لاكتشاف الأعمدة أو الجداول.  
* تصدير نتائج OCR إلى ملفات PDF قابلة للبحث باستخدام مكتبة PDF.

لا تتردد في ترك تعليق إذا واجهت مشكلة، أو مشاركة تعديلاتك الخاصة للتعامل مع المسحات العنيدة. برمجة سعيدة، ولتظل صورك دائمًا مستوية تمامًا!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}