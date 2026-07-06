---
category: general
date: 2026-05-03
description: استخرج النص من الصورة فورًا باستخدام Aspose OCR. تعلم كيفية تحديد منطقة
  الاهتمام، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص من الفاتورة في دقائق
  قليلة.
draft: false
keywords:
- extract text from image
- define region of interest
- load image for ocr
- extract text from invoice
- process image with ocr
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR. يوضح هذا الدليل كيفية
  تحديد منطقة الاهتمام، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص من الفاتورة
  بكفاءة.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل كامل
tags:
- ocr
- python
- image-processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة
url: /ar/python-java/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة

هل تحتاج إلى **استخراج النص من الصورة** بسرعة؟ لست وحدك—المطورون يواجهون باستمرار مسحًا ضوضائيًا، وإيصالات، وفواتير. في هذا الدرس سنستعرض حلًا كاملاً لا يوضح فقط كيفية *استخراج النص من الصورة* بل يُظهر أيضًا كيفية **تحديد منطقة الاهتمام**، **تحميل الصورة للـ OCR**، واستخراج السطر الدقيق الذي تحتاجه من الفاتورة.  

سنغطي كل شيء من تثبيت مكتبة Aspose OCR إلى معالجة الحالات الخاصة مثل الصفحات المائلة. في النهاية ستحصل على سكريبت قابل للتنفيذ يستخرج النص المطلوب في استدعاء واحد—دون الحاجة إلى قص يدوي.  

## ما ستتعلمه

- كيفية **تحميل الصورة للـ OCR** باستخدام واجهة برمجة تطبيقات Aspose للـ Python.  
- أفضل طريقة لـ **تحديد منطقة الاهتمام** (ROI) بحيث تعالج فقط الجزء المهم من الصورة.  
- كيفية **استخراج النص من حقل الفاتورة** دون سحب الصفحة بأكملها.  
- نصائح لـ **معالجة الصورة بالـ OCR** بفعالية وتجنب المشكلات الشائعة.  

**المتطلبات المسبقة** – بيئة Python 3.9+ حديثة، ملف ترخيص Aspose OCR صالح، وصورة (مثل PNG للفاتورة). لا توجد أدوات خارجية أخرى مطلوبة.

---

## الخطوة 1 – تهيئة محرك OCR (الإعداد الأساسي)

قبل أن تتمكن من **معالجة الصورة بالـ OCR**، تحتاج إلى كائن محرك يحمل الترخيص الخاص بك. هذه الخطوة حاسمة لأن المحرك غير المرخص سيعيد مجموعة نتائج محدودة.

```python
import aspose.ocr as ocr  # Make sure you installed aspose-ocr via pip

# Create the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with your actual .lic file location
ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")
```

*لماذا هذا مهم*: كائن `OcrEngine` هو قلب المكتبة؛ يدير نماذج اللغة، ومعالجة ما قبل الصورة، والترخيص. ضبط الترخيص مسبقًا يضمن لك الدقة الكاملة وعدم ظهور العلامات المائية.

---

## الخطوة 2 – تحميل الصورة للـ OCR

الآن بعد أن أصبح المحرك جاهزًا، نحتاج إلى **تحميل الصورة للـ OCR**. يدعم Aspose العديد من الصيغ (PNG، JPEG، TIFF)، لكن استخدام `Image.from_file` يضمن فك ترميز الصورة بشكل صحيح.

```python
# Load the target image – change the path to point at your invoice file
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.from_file(image_path)
```

> **نصيحة احترافية**: احفظ ملفات الصور بأقل من 5 ميغابايت لأسرع معالجة. يمكن تقليل حجم الملفات الكبيرة باستخدام `image.resize(width, height)` قبل الـ OCR.

---

## الخطوة 3 – تحديد منطقة الاهتمام (ROI)

تحتوي معظم الفواتير على الكثير من النص غير ذي الصلة—كتل العناوين، التذييلات، إلخ. من خلال **تحديد منطقة الاهتمام** نخبر المحرك بالتركيز فقط على المكان الذي يوجد فيه المبلغ أو التاريخ، مما يحسن السرعة والدقة.

```python
# Define ROI: (x, y, width, height) in pixels
# Adjust these numbers based on the layout of your specific invoice
roi = ocr.Rectangle(150, 300, 400, 120)
```

*كيف يعمل*: فئة `Rectangle` تقص الصورة افتراضيًا؛ محرك الـ OCR لا يرى البكسلات خارج المستطيل، لذا يتم تجاهل الضوضاء خارج الـ ROI.

---

## الخطوة 4 – التعرف على النص داخل الـ ROI

مع المحرك، الصورة، والـ ROI جاهزين، ن finally **استخراج النص من الصورة**. تُعيد طريقة `recognize` كائن `OcrResult` يحتوي على السلسلة المكتشفة ودرجات الثقة.

```python
# Perform OCR only within the defined ROI
ocr_result = ocr_engine.recognize(image, roi=roi)

# Print the raw extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

**الناتج المتوقع** (مثال لسطر إجمالي فاتورة نموذجي):

```
Text inside ROI:
Total Amount: $1,245.67
```

إذا تم وضع الـ ROI بشكل صحيح، سترى فقط السطر الذي تحتاجه—بدون أي شيء آخر.

---

## الخطوة 5 – مثال كامل جاهز للنسخ واللصق

فيما يلي السكريبت الكامل الذي يجمع جميع الخطوات السابقة. احفظه باسم `extract_invoice_roi.py` وشغّله باستخدام `python extract_invoice_roi.py`.

```python
# extract_invoice_roi.py
import aspose.ocr as ocr

def main():
    # 1️⃣ Initialize OCR engine and apply license
    ocr_engine = ocr.OcrEngine()
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image you want to process
    image = ocr.Image.from_file("YOUR_DIRECTORY/invoice.png")

    # 3️⃣ Define the region of interest (ROI) – rectangle where the text lives
    roi = ocr.Rectangle(150, 300, 400, 120)   # (x, y, width, height)

    # 4️⃣ Recognize text only inside the ROI
    ocr_result = ocr_engine.recognize(image, roi=roi)

    # 5️⃣ Display the extracted text
    print("Text inside ROI:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

شغّل السكريبت ويجب أن ترى السطر المستهدف يُطبع في وحدة التحكم. إذا حصلت على سلسلة فارغة، تحقق من إحداثيات الـ ROI—فقد يؤدي الانحراف بضع بكسلات إلى استبعاد النص تمامًا.

---

## الخطوة 6 – الاختلافات الشائعة والحالات الخاصة

### أ) تخطيطات فواتير مختلفة  
تختلف صناديق المبلغ الإجمالي بين البائعين. لت **معالجة الصورة بالـ OCR** عبر تخطيطات متعددة، ضع في اعتبارك:

- **مناطق ROI متعددة**: شغّل المحرك تسلسليًا مع عدة مستطيلات واختر النتيجة ذات أعلى ثقة.  
- **اكتشاف ROI ديناميكي**: استخدم مكتبة معالجة صور خفيفة (مثل OpenCV) لتحديد تسمية “Total” أولاً، ثم احسب الـ ROI نسبةً إليها.

### ب) صور مائلة أو منحرفة  
إذا كان المسح مائلًا، استدعِ `image.rotate(angle)` قبل التعرف:

```python
image = image.rotate(2.5)  # Rotate 2.5 degrees clockwise
```

يوفر Aspose OCR أيضًا تصحيحًا تلقائيًا للانحراف، لكن الدوران اليدوي يمنحك تحكمًا أدق.

### ج) أحرف غير لاتينية  
نموذج اللغة الافتراضي هو الإنجليزية. لت **استخراج النص من الفاتورة** المكتوبة بلغة أخرى، اضبط اللغة قبل التعرف:

```python
ocr_engine.language = ocr.Language.French  # Example for French invoices
```

### د) ملفات PDF كبيرة  
عند التعامل مع ملفات PDF متعددة الصفحات، استخرج كل صفحة كصورة أولًا (Aspose PDF → Image) ثم طبّق نفس منطق الـ ROI على كل صفحة.

---

## الخطوة 7 – نصائح الأداء والنصائح الاحترافية

- **تخزين المحرك في الذاكرة**: إنشاء `OcrEngine` مرارًا داخل حلقة يبطئ الأداء. أنشئه مرة واحدة وأعد استخدامه.  
- **المعالجة الدفعية**: إذا كان لديك العشرات من الفواتير، غلف استدعاء الـ OCR داخل `ThreadPoolExecutor` لتوازي العمل المرتبط بـ I/O.  
- **التحقق من الثقة**: `ocr_result.confidence` يعطى قيمة عائمة بين 0 و 1. رفض النتائج التي تقل عن 0.85 واستخدم ROI أكبر أو مراجعة يدوية كبديل.  

> **احذر**: ضبط الـ ROI صغيرًا جدًا قد يقطع الأحرف، مما ينتج مخرجات مشوشة. اختبر دائمًا على عدد قليل من الفواتير قبل التعميم.

---

## الخلاصة

أصبح لديك الآن طريقة قوية وجاهزة للإنتاج **لاستخراج النص من الصورة** باستخدام Aspose OCR، مع إمكانية **تحديد منطقة الاهتمام**، **تحميل الصورة للـ OCR**، واستخراج النص من حقول الفاتورة بثقة. بتقليل نطاق الـ OCR إلى ROI ضيق، تعزز كلًا من السرعة والدقة—مثالي لمعالجة دفعات من آلاف الإيصالات.  

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا السكريبت في واجهة Flask API حتى يتمكن تطبيق الويب الخاص بك من رفع فاتورة وإرجاع المبلغ الإجمالي فورًا. أو جرب استخدام عدة ROIs لاستخراج التاريخ، رقم الفاتورة، واسم البائع في آنٍ واحد. الاحتمالات لا حصر لها، ومع الأساسيات التي غطيناها، أنت مجهّز جيدًا لمواجهة أي تحدي OCR.

برمجة سعيدة، ولتكن النصوص المستخرجة دائمًا نظيفة!  

![مخطط تدفق يوضح كيفية استخراج النص من الصورة باستخدام Aspose OCR](workflow.png){: .center-image alt="مخطط تدفق يوضح كيفية استخراج النص من الصورة باستخدام Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}