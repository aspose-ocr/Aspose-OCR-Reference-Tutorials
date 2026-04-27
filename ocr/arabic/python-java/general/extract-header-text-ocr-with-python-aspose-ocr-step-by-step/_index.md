---
category: general
date: 2026-04-26
description: استخراج نص العنوان باستخدام OCR في Python مع Aspose OCR. تعلم كيفية استخراج
  نص منطقة محددة من الصور بسرعة وموثوقية.
draft: false
keywords:
- extract header text ocr
- extract specific area text
- python aspose ocr
- ocr region of interest python
- aspose ocr roi
language: ar
og_description: استخراج نص العنوان باستخدام OCR بسرعة. يوضح هذا الدليل كيفية استخراج
  نص منطقة محددة باستخدام Aspose OCR في بايثون في بضع أسطر فقط.
og_title: استخراج نص العنوان باستخدام OCR في بايثون Aspose OCR – دليل شامل
tags:
- OCR
- Python
- Aspose
title: استخراج نص العنوان باستخدام OCR في بايثون Aspose OCR – دليل خطوة بخطوة
url: /ar/python-java/general/extract-header-text-ocr-with-python-aspose-ocr-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج نص العنوان باستخدام OCR – دليل كامل بلغة Python Aspose OCR

هل احتجت يوماً إلى **استخراج نص العنوان باستخدام OCR** من فاتورة ممسوحة ضوئياً دون الحاجة لمعالجة الصفحة بأكملها؟ لست وحدك. في العديد من خطوط الأنابيب الواقعية يحتوي العنوان على أهم المعلومات—رقم الفاتورة، التاريخ، اسم المورد—واستخرجها بسرعة يمكن أن يوفر الكثير من العمل اللاحق.

في هذا الدرس سنعرض لك حلاً جاهزاً للتنفيذ **يستخرج نص منطقة محددة** باستخدام مكتبة **Python Aspose OCR**. لا مراجع غامضة للوثائق الخارجية، بل سكريبت كامل، شرح واضح لكل سطر، ونصائح ستستفيد منها غداً.

## ما ستتعلمه

- كيفية تثبيت واستيراد حزمة Aspose OCR للغة Python.  
- كيفية تحميل صورة وتعريف **منطقة الاهتمام (ROI)** التي تعزل العنوان.  
- كيفية تشغيل محرك OCR على تلك الـ ROI واسترجاع النص النظيف.  
- الأخطاء الشائعة (مثل عدم توافق DPI) وكيفية تجنبها.  
- ما هو الشكل المتوقع للمخرجات لتتمكن من التحقق من صحة العملية.

بنهاية هذا الدرس ستتمكن من إدراج هذا الكود في أي مشروع يحتاج إلى **استخراج نص العنوان باستخدام OCR** من الفواتير أو الإيصالات أو أي مستند ذو تخطيط متوقع.

## المتطلبات المسبقة

- Python 3.8 أو أحدث مثبت على جهازك.  
- ترخيص صالح لـ Aspose OCR for Python (الإصدار التجريبي المجاني يكفي للتقييم).  
- ملف صورة (`invoice.png`) يحتوي على منطقة عنوان واضحة.  
- إلمام أساسي بدوال Python ومسارات الملفات.

> **نصيحة احترافية:** إذا كنت تختبر على مسح منخفض الدقة، قم بزيادة DPI قبل إرساله إلى Aspose OCR – ذلك يحسن الدقة بشكل كبير.

---

## الخطوة 1: تثبيت حزمة Aspose OCR

أولاً، أضف المكتبة إلى بيئتك. الحزمة الرسمية هي `aspose-ocr`. نفّذ هذا الأمر مرة واحدة:

```bash
pip install aspose-ocr
```

إذا كنت تستخدم بيئة افتراضية (مستحسن جداً)، فعّلها قبل التثبيت. هذا يضمن أن الحزمة لن تتصادم مع مشاريع أخرى.

## الخطوة 2: استيراد الفئات المطلوبة وتحميل الصورة

الآن نستدعي الفئات الضرورية في السكريبت ونحمّل صورة الفاتورة. لاحظ استخدام **المسارات الكاملة**؛ المسارات النسبية تعمل أيضاً، لكن المسارات المطلقة تزيل الغموض عندما يُشغَّل السكريبت على خادم.

```python
# Step 2: Imports and image loading
from asposeocr import OcrEngine, Rectangle, Image

# Create an OCR engine instance – this object holds all settings.
ocr_engine = OcrEngine()

# Load the image that contains the invoice.
# Replace "YOUR_DIRECTORY/invoice.png" with your actual file location.
ocr_engine.image = Image.load(r"C:\Invoices\invoice.png")
```

> **لماذا هذا مهم:** تهيئة `OcrEngine` مرة واحدة وإعادة استخدامها لعدة صور أكثر كفاءة من إنشاء محرك جديد في كل مرة.

## الخطوة 3: تعريف منطقة العنوان (ROI)

عادةً ما يكون العنوان في أعلى الصفحة، لكن إحداثياته قد تختلف. هنا نعرّف مستطيلًا (`x`, `y`, `width`, `height`) يغطي العنوان. عدّل الأرقام لتتناسب مع تخطيط مستندك.

```python
# Step 3: Define the region of interest (ROI) that contains the header.
# Rectangle(x, y, width, height) – all values are in pixels.
header_region = Rectangle(50, 20, 500, 80)   # Example values; tweak as needed.
```

> **كيف يعمل:** عند استدعاء `set_roi`، يقتصر محرك OCR على تحليل هذا المستطيل، ما يسرّع المعالجة بشكل كبير ويقلل الضوضاء من باقي الصفحة.

## الخطوة 4: تطبيق الـ ROI وتشغيل OCR

نخبر المحرك بالتركيز على منطقة العنوان ثم ننفّذ عملية OCR. يحتوي كائن النتيجة على النص المُعترف به وبيانات وصفية إضافية (نقاط الثقة، اللغة، إلخ).

```python
# Step 4: Apply the ROI to the OCR engine.
ocr_engine.set_roi(header_region)

# Step 5: Perform OCR on the defined ROI.
ocr_result = ocr_engine.process()
```

إذا فشل OCR (مثلاً، تنسيق صورة غير مدعوم)، سيكون `ocr_result` مساويًا لـ `None`. يمكن إضافة شرط حماية بسيط لجعل السكريبت أكثر صلابة:

```python
if ocr_result is None:
    raise RuntimeError("OCR processing failed – check image format and ROI.")
```

## الخطوة 5: استرجاع وطباعة نص العنوان المستخرج

أخيرًا، نستخرج النص من كائن النتيجة ونعرضه. يمكنك أيضًا كتابته إلى ملف أو تمريره إلى دالة أخرى لمزيد من التحليل.

```python
# Step 6: Print the extracted header text.
print("Header text:", ocr_result.text)
```

### المخرجات المتوقعة

عند إعداد كل شيء بشكل صحيح، يجب أن ترى شيئًا مشابهًا لـ:

```
Header text: Acme Corp
Invoice #12345
Date: 2026‑04‑20
```

إذا كان المخرجات مشوشة، أعد فحص إحداثيات الـ ROI وتأكد من أن الصورة الأصلية ذات تباين عالي.

---

## التنويعات والحالات الخاصة

### 1. عناوين متعددة في مستند واحد

أحيانًا يحتوي ملف PDF على عدة صفحات، كل منها يحمل عنوانًا خاصًا. يمكن حلقة عبر الصفحات وتعديل الـ ROI لكل صفحة:

```python
for page_number, img_path in enumerate(image_paths, start=1):
    ocr_engine.image = Image.load(img_path)
    # Adjust Y coordinate based on page height if needed.
    ocr_engine.set_roi(Rectangle(50, 20, 500, 80))
    result = ocr_engine.process()
    print(f"Page {page_number} header:", result.text)
```

### 2. التعامل مع المسحات المائلة

إذا كانت الفاتورة مائلة قليلًا، عالج الصورة مسبقًا باستخدام OpenCV قبل تمريرها إلى Aspose OCR:

```python
import cv2
import numpy as np

# Load with OpenCV, correct rotation, then convert back to Aspose Image.
cv_img = cv2.imread(r"C:\Invoices\invoice.png")
# Assume we have a function `deskew` that returns a corrected image.
deskewed = deskew(cv_img)
# Convert back to Aspose Image:
aspose_img = Image.from_array(deskewed)   # Pseudo‑code; actual conversion may vary.
ocr_engine.image = aspose_img
```

### 3. تغيير إعدادات اللغة

يمكن لـ Aspose OCR اكتشاف اللغة تلقائيًا، لكن يمكنك فرض الإنجليزية للحصول على نتائج أسرع:

```python
ocr_engine.language = "en"
```

---

## مثال كامل يعمل

فيما يلي السكريبت الكامل الذي يمكنك نسخه ولصقه في ملف باسم `extract_header.py`. لا تنسَ استبدال مسار الصورة بالمسار الخاص بك.

```python
# extract_header.py
# Complete example: extract header text OCR using Python Aspose OCR

from asposeocr import OcrEngine, Rectangle, Image

def extract_header(image_path: str,
                   roi: Rectangle = Rectangle(50, 20, 500, 80),
                   language: str = "en") -> str:
    """
    Extracts text from the header region of an invoice image.

    :param image_path: Full path to the invoice image (PNG, JPG, etc.).
    :param roi: Rectangle defining the header area (default works for most A4 invoices).
    :param language: OCR language code; default is English.
    :return: Recognized header text.
    :raises RuntimeError: If OCR processing fails.
    """
    engine = OcrEngine()
    engine.language = language
    engine.image = Image.load(image_path)
    engine.set_roi(roi)

    result = engine.process()
    if result is None:
        raise RuntimeError("OCR processing failed – verify image and ROI.")
    return result.text.strip()

if __name__ == "__main__":
    # Example usage
    invoice_path = r"C:\Invoices\invoice.png"
    header_text = extract_header(invoice_path)
    print("Header text:", header_text)
```

تشغيل هذا السكريبت يجب أن يُظهر سطور العنوان تمامًا كما هو موضح أعلاه. لا تتردد في تعديل قيم `roi` لتتناسب مع قالب الفاتورة الخاص بك.

---

## أسئلة شائعة

**س: هل يعمل هذا مع ملفات PDF مباشرة؟**  
ج: ليس مباشرة. حوّل كل صفحة PDF إلى صورة (مثلاً باستخدام `pdf2image`) ثم مرّر PNG/JPG إلى السكريبت.

**س: ماذا إذا كان العنوان يحتوي على شعار ونص معًا؟**  
ج: يركز Aspose OCR على المحتوى النصي. بالنسبة للشعارات، استخدم مكتبة التعرف على الصور مثل `opencv` أو `tesseract` مع نموذج مخصص.

**س: هل التجربة المجانية محدودة؟**  
ج: التجربة تسمح بما يصل إلى 10 صفحات شهريًا. للإنتاج، اشترِ ترخيصًا لإزالة الحد وتفعيل إعدادات دقة أعلى.

---

## الخلاصة

أصبح لديك الآن دليل **متكامل وقابل للاقتباس** لاستخدام **استخراج نص العنوان باستخدام OCR** عبر **Python Aspose OCR**. غطى الدرس كل شيء من التثبيت إلى التعامل مع الحالات الخاصة، وقدّم لك دالة قابلة لإعادة الاستخدام يمكنك إدراجها في سير عمل أكبر.

بعد ذلك، قد تستكشف **استخراج نص مناطق محددة** لأجزاء أخرى مثل التذييل أو بنود الفاتورة، أو تجمع هذا النهج مع محول PDF‑إلى‑صورة لأتمتة خطوط الأنابيب الكاملة. الاحتمالات لا حصر لها—فقط تأكد من دقة إحداثيات الـ ROI وصورك ذات دقة عالية.

هل لديك تخطيط صعب؟ شاركه في التعليقات وسنقوم بضبط الـ ROI معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}