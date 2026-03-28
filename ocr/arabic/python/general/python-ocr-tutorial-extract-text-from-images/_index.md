---
category: general
date: 2026-03-28
description: دروس OCR بلغة Python توضح كيفية استخراج النص من الصورة باستخدام Aspose
  OCR Cloud. تعلم كيفية تحميل الصورة للتعرف الضوئي على الأحرف وتحويل الصورة إلى نص
  عادي في دقائق.
draft: false
keywords:
- python ocr tutorial
- extract text image python
- ocr image to text
- load image for ocr
- convert image plain text
language: ar
og_description: يشرح برنامج تعليمي للـ OCR باستخدام بايثون كيفية تحميل الصورة للـ
  OCR وتحويل النص العادي للصورة باستخدام Aspose OCR Cloud. احصل على الكود الكامل والنصائح.
og_title: دليل بايثون للتعرف الضوئي على الأحرف – استخراج النص من الصور
tags:
- OCR
- Python
- Image Processing
title: دورة بايثون للتعرف الضوئي على الأحرف – استخراج النص من الصور
url: /ar/python/general/python-ocr-tutorial-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – استخراج النص من الصور

هل تساءلت يومًا كيف تحول صورة إيصال غير مرتبة إلى نص نظيف وقابل للبحث؟ لست وحدك. في تجربتي، أكبر عقبة ليست محرك OCR نفسه بل الحصول على الصورة بالتنسيق الصحيح واستخراج النص العادي دون أي مشاكل.  

هذا **python ocr tutorial** يشرح لك كل خطوة — تحميل صورة للـ OCR، تشغيل التعرف، وأخيرًا تحويل النص العادي للصورة إلى سلسلة Python يمكنك تخزينها أو تحليلها. في النهاية ستكون قادرًا على **extract text image python**، ولن تحتاج إلى أي ترخيص مدفوع للبدء.

## ما ستتعلمه

- كيفية تثبيت واستيراد Aspose OCR Cloud SDK للـ Python.  
- الكود الدقيق لـ **load image for OCR** (PNG, JPEG, TIFF, PDF، إلخ).  
- كيفية استدعاء المحرك لإجراء تحويل **ocr image to text**.  
- نصائح للتعامل مع الحالات الشائعة مثل ملفات PDF متعددة الصفحات أو المسحات منخفضة الدقة.  
- طرق للتحقق من النتيجة وماذا تفعل إذا كان النص مشوشًا.

### المتطلبات المسبقة

- Python 3.8+ مثبت على جهازك.  
- حساب Aspose Cloud مجاني (الإصدار التجريبي يعمل بدون ترخيص).  
- إلمام أساسي بـ pip وبيئات virtual environments — لا شيء معقد.

> **نصيحة احترافية:** إذا كنت تستخدم virtualenv بالفعل، فعّله الآن. يحافظ ذلك على نظافة الاعتمادات ويتجنب تعارض الإصدارات.

![Python OCR tutorial screenshot showing recognized text](path/to/ocr_example.png "Python OCR tutorial – extracted plain text display")

## الخطوة 1 – تثبيت Aspose OCR Cloud SDK

أولًا، نحتاج إلى المكتبة التي تتواصل مع خدمة OCR من Aspose. افتح الطرفية واكتب:

```bash
pip install asposeocrcloud
```

هذا الأمر الواحد يجلب أحدث SDK (الإصدار الحالي 23.12). الحزمة تشمل كل ما تحتاجه — لا حاجة لمكتبات معالجة صور إضافية.

## الخطوة 2 – تهيئة محرك OCR (الكلمة المفتاحية الأساسية في العمل)

الآن بعد أن أصبح SDK جاهزًا، يمكننا تشغيل محرك **python ocr tutorial**. المُنشئ لا يحتاج إلى مفتاح ترخيص للتجربة، مما يبسط الأمور.

```python
import asposeocrcloud as ocr

# Initialise the OCR engine – no licence needed for trial use
ocr_engine = ocr.OcrEngine()
```

> **لماذا هذا مهم:** تهيئة المحرك مرة واحدة فقط تجعل الاستدعاءات اللاحقة سريعة. إذا قمت بإنشاء الكائن لكل صورة ستضيع جولات الشبكة.

## الخطوة 3 – تحميل صورة للـ OCR

هنا يبرز دور كلمة **load image for OCR**. طريقة `Image.load` في SDK تقبل مسار ملف أو URL، وتكتشف التنسيق تلقائيًا (PNG، JPEG، TIFF، PDF، إلخ). لنحمّل إيصالًا تجريبيًا:

```python
# Step 3: Load the input image (PNG, JPEG, TIFF, PDF …)
input_image = ocr.Image.load(r"YOUR_DIRECTORY/receipt.png")
```

إذا كنت تتعامل مع PDF متعدد الصفحات، ما عليك سوى الإشارة إلى ملف PDF؛ سيعامل SDK كل صفحة كصورة منفصلة داخليًا.

## الخطوة 4 – تنفيذ تحويل OCR من صورة إلى نص

مع وجود الصورة في الذاكرة، يحدث الـ OCR الفعلي في سطر واحد. طريقة `recognize` تُعيد كائن `OcrResult` يحتوي على النص العادي، درجات الثقة، وحتى إطارات الحدود إذا احتجتها لاحقًا.

```python
# Step 4: Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)
```

> **حالة خاصة:** للصور منخفضة الدقة (أقل من 300 dpi) قد ترغب في تكبير الصورة أولًا. يوفر SDK أداة مساعدة `Resize`، لكن بالنسبة لمعظم الإيصالات الإعداد الافتراضي يعمل جيدًا.

## الخطوة 5 – تحويل النص العادي للصورة إلى سلسلة قابلة للاستخدام

القطعة الأخيرة من اللغز هي استخراج النص العادي من كائن النتيجة. هذه هي خطوة **convert image plain text** التي تحول كتلة الـ OCR إلى شيء يمكنك طباعته، تخزينه، أو إمداده إلى نظام آخر.

```python
# Step 5: Output the recognised plain text
print("Plain OCR:")
print(ocr_result.text)
```

عند تشغيل السكريبت، يجب أن ترى شيئًا مثل:

```
Plain OCR:
Starbucks Coffee
Date: 2026/03/27
Total: $4.75
Thank you!
```

هذه النتيجة الآن سلسلة Python عادية، جاهزة لتصدير CSV، إدخال قاعدة بيانات، أو معالجة اللغة الطبيعية.

## التعامل مع المشكلات الشائعة

### 1. صور فارغة أو مشوشة

إذا كان `ocr_result.text` فارغًا، تحقق مرة أخرى من جودة الصورة. حل سريع هو إضافة خطوة تمهيدية:

```python
# Simple preprocessing – convert to grayscale and increase contrast
processed = input_image.to_grayscale().adjust_contrast(1.2)
ocr_result = ocr_engine.recognize(processed)
```

### 2. ملفات PDF متعددة الصفحات

عند إمداد PDF، تُعيد `recognize` النتائج لكل صفحة. قم بالتكرار عبرها هكذا:

```python
pdf_image = ocr.Image.load("document.pdf")
pages = pdf_image.pages  # collection of page images

for i, page in enumerate(pages, start=1):
    result = ocr_engine.recognize(page)
    print(f"--- Page {i} ---")
    print(result.text)
```

### 3. دعم اللغات

يدعم Aspose OCR أكثر من 60 لغة. لتغيير اللغة، اضبط خاصية `language` قبل استدعاء `recognize`:

```python
ocr_engine.language = "fr"  # French
ocr_result = ocr_engine.recognize(input_image)
```

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك سكريبت كامل جاهز للنسخ واللصق يغطي كل شيء من التثبيت إلى معالجة الحالات الخاصة:

```python
# -*- coding: utf-8 -*-
"""
Python OCR tutorial – complete example using Aspose OCR Cloud.
Demonstrates loading an image, performing OCR, and handling multi‑page PDFs.
"""

import asposeocrcloud as ocr
import os

def ocr_file(filepath: str, language: str = "en"):
    """
    Perform OCR on a given file (image or PDF) and return plain text.
    """
    # Initialise engine (trial licence)
    engine = ocr.OcrEngine()
    engine.language = language

    # Load the file – SDK auto‑detects format
    image = ocr.Image.load(filepath)

    # If it's a PDF, iterate over pages
    if image.is_pdf:
        all_text = []
        for page in image.pages:
            result = engine.recognize(page)
            all_text.append(result.text)
        return "\n".join(all_text)

    # Single‑image case
    result = engine.recognize(image)
    return result.text


if __name__ == "__main__":
    # Example usage – replace with your own path
    sample_path = os.path.join("YOUR_DIRECTORY", "receipt.png")

    if not os.path.exists(sample_path):
        raise FileNotFoundError(f"File not found: {sample_path}")

    extracted = ocr_file(sample_path)
    print("=== Extracted Text ===")
    print(extracted)
```

شغّل السكريبت (`python ocr_demo.py`) وسترى ناتج **ocr image to text** مباشرة في وحدة التحكم.

## ملخص – ما تم تغطيته

- تم تثبيت SDK **Aspose OCR Cloud** (`pip install asposeocrcloud`).  
- **تهيئة محرك OCR** بدون ترخيص (مثالي للتجربة).  
- تم توضيح كيفية **load image for OCR**، سواء كان PNG أو JPEG أو PDF.  
- تم تنفيذ تحويل **ocr image to text** و**convert image plain text** إلى سلسلة Python قابلة للاستخدام.  
- تم معالجة المشكلات الشائعة مثل المسحات منخفضة الدقة، ملفات PDF متعددة الصفحات، واختيار اللغة.

## الخطوات التالية والمواضيع ذات الصلة

الآن بعد أن أتقنت **python ocr tutorial**، فكر في استكشاف:

- **Extract text image python** للمعالجة الدفعية لمجلدات كبيرة من الإيصالات.  
- دمج ناتج OCR مع **pandas** لتحليل البيانات (`df = pd.read_csv(StringIO(extracted))`).  
- استخدام **Tesseract OCR** كخيار احتياطي عندما تكون اتصال الإنترنت محدودًا.  
- إضافة معالجة لاحقة باستخدام **spaCy** لتحديد الكيانات مثل التواريخ، المبالغ، وأسماء التجار.  

لا تتردد في التجربة: جرّب صيغ صور مختلفة، عدّل التباين، أو غيّر اللغات. مجال OCR واسع، والمهارات التي اكتسبتها الآن تشكل أساسًا قويًا لأي مشروع أتمتة مستندات.

برمجة سعيدة، ولتكن نصوصك دائمًا قابلة للقراءة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}