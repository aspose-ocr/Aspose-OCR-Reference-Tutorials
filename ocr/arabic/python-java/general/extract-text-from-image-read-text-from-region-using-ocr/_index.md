---
category: general
date: 2026-07-05
description: استخراج النص من الصورة باستخدام OCR في بايثون. تعلم كيفية تحميل الصورة
  للـ OCR، قراءة النص من منطقة معينة، واستخراج النص من الفاتورة ببضع أسطر من الشيفرة.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: ar
og_description: استخراج النص من الصورة باستخدام OCR في بايثون. يوضح هذا الدليل كيفية
  تحميل الصورة للتعرف الضوئي على الأحرف، قراءة النص من منطقة معينة، واستخراج النص
  من الفاتورة بسرعة.
og_title: استخراج النص من الصورة – قراءة النص من المنطقة باستخدام تقنية التعرف الضوئي
  على الأحرف (OCR)
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: استخراج النص من الصورة – قراءة النص من المنطقة باستخدام OCR
url: /ar/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – قراءة النص من منطقة باستخدام OCR

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن الجزء المحدد فقط هو المهم—مثل المبلغ الإجمالي في الفاتورة؟ لست وحدك. في العديد من المشاريع الواقعية ستجد نفسك بحاجة إلى **قراءة النص من منطقة** بدلاً من تحليل الصورة بأكملها. لحسن الحظ، ببضع أسطر من بايثون يمكنك تحميل صورة للـ OCR، تعريف منطقة اهتمام (ROI)، واستخراج الأحرف التي تحتاجها بالضبط.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح كيفية **تحميل صورة للـ OCR**، إعداد ROI، وأخيرًا **استخراج النص من الفاتورة**. في النهاية ستحصل على مقتطف جاهز يمكنك استخدامه مع أي مكتبة OCR شائعة تدعم التعرف القائم على المنطقة.

---

## ما الذي ستحتاجه

- Python 3.8+ (الكود يعمل أيضًا على 3.10)  
- حزمة OCR تُظهر فئة `OcrEngine` (للتجربة سنستخدم وحدة `ocr` خيالية؛ استبدلها بـ `pytesseract` أو `easyocr` أو أي مكتبة تدعم دعم ROI)  
- صورة نموذجية—مثلاً `invoice.png`—تحتوي على نص واضح ومطبوع  
- إلمام أساسي بدوال وفئات بايثون (لا تحتاج خلفية في التعلم العميق)

إذا كان لديك كل ذلك، رائع—لنبدأ. إذا لم يكن كذلك، احصل على أحدث نسخة من بايثون من python.org وقم بتثبيت حزمة OCR عبر `pip install your-ocr-lib`.

![مثال على استخراج النص من الصورة](extract-text-from-image.png "استخراج النص من الصورة – عرض OCR القائم على المنطقة")

*الصورة أعلاه توضح المنطقة (المستطيل الأحمر) التي سنستهدفها **لاستخراج النص من الصورة**.*

---

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولًا، تأكد من أن مكتبة OCR متاحة في بيئتك. نمط الاستيراد أدناه يعمل مع معظم الحزم التي تُظهر فئة `OcrEngine` عالية المستوى.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **نصيحة احترافية:** إذا كنت تستخدم `pytesseract`، ستحتاج إلى تثبيت ملف Tesseract التنفيذي منفصلًا وتعيين `pytesseract.pytesseract.tesseract_cmd` إلى مساره.

---

## الخطوة 2: إنشاء محرك OCR وتحديد اللغة

إنشاء المحرك سهل، لكن تحديد اللغة يحسن الدقة بشكل كبير، خاصةً للفواتير التي تحتوي على أرقام وكلمات إنجليزية.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

لماذا نفعل ذلك؟ يستخدم محرك OCR نماذج اللغة لتوقع الأحرف؛ إخبار المحرك بتوقع الإنجليزية يقلل من الإيجابيات الكاذبة مثل قراءة “0” كـ “O”.

---

## الخطوة 3: تحميل الصورة للـ OCR

الآن نقوم فعليًا **بتحميل صورة للـ OCR**. معظم المكتبات تقبل مسار ملف أو كائن صورة من Pillow. هنا نستخدم أداة التحميل المدمجة في المكتبة لتبسيط العملية.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

تأكد أن المسار يشير إلى الدليل الصحيح؛ الخطأ الشائع هو نسيان المسار النسبي عندما يُشغل السكربت من دليل عمل مختلف.

---

## الخطوة 4: تعريف منطقة الاهتمام (ROI)

تعريف الـ ROI هو جوهر **قراءة النص من منطقة**. فكر فيها كأنك ترسم مستطيلًا حول الجزء من الفاتورة الذي يحتوي على المبلغ الإجمالي.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` و `top` يمثلان إحداثيات X و Y للزاوية العليا اليسرى للمستطيل.  
- `width` و `height` يحددان حجم الصندوق.  
- يمكنك تجربة قيم مختلفة باستخدام عارض صور يُظهر إحداثيات البكسل.

> **لماذا ROI مهم:** تشغيل OCR على الصفحة بأكملها يهدر دورات المعالج وغالبًا ما يُدخل ضوضاء من نصوص غير ذات صلة أو جداول أو رسومات. بالتركيز على منطقة معينة، تحصل على نتائج أنظف ومعالجة أسرع.

---

## الخطوة 5: تنفيذ OCR على المنطقة المحددة

مع إعداد كل شيء، الآن **نستخرج النص من الصورة**—ولكن فقط داخل الـ ROI الذي عرّفناه.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

طريقة `recognize` تُعيد كائنًا يحتوي عادةً على السلسلة الخام، درجات الثقة، وأحيانًا إطارات حدودية لكل كلمة. بالنسبة لنا نحتاج فقط إلى النص العادي.

---

## الخطوة 6: إظهار النص المستخرج

لنطبع النتيجة ونرى ما حصلنا عليه. تُظهر هذه الخطوة **استخراج النص من الفاتورة** في سيناريو واقعي.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### النتيجة المتوقعة

```
Text inside ROI:
Total Amount: $1,245.67
```

إذا كانت فاتورتك تستخدم تخطيطًا مختلفًا، سترى أي نص يقع داخل المستطيل—ربما رقم الفاتورة، التاريخ، أو مرجع طلب الشراء.

---

## الخطوة 7: تجميع كل ذلك في دالة قابلة لإعادة الاستخدام (اختياري)

لجعل الحل قابلًا لإعادة الاستخدام عبر فواتير متعددة، غلف المنطق داخل دالة. هذا أيضًا يوضح **OCR على المنطقة** كأداة عامة.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

يمكنك الآن استدعاء الدالة مع أي فاتورة:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **إخراج فارغ** | الـ ROI لا يغطي أي نص فعليًا (إحداثيات خاطئة). | تحقق من قيم البكسل باستخدام محرر صور؛ أضف طبقة تصحيح بصرية. |
| **حروف غير مفهومة** | دقة الصورة منخفضة أو تباين ضعيف. | عالج الصورة مسبقًا: حوّلها إلى تدرج رمادي، طبّق عتبة (`cv2.threshold`). |
| **لغة خاطئة** | المحرك يستخدم لغة افتراضية لا تحتوي على مجموعة الأحرف المطلوبة. | عيّن صراحةً `ocr_engine.language` إلى `ENGLISH` أو اللغة المناسبة. |
| **بطء الأداء** | تشغيل OCR على صور كبيرة بشكل متكرر. | قلّص حجم الصورة قبل التحميل، أو عالج الـ ROI فقط عن طريق القص أولًا. |

---

## توسيع المثال: عدة مناطق ROI

أحيانًا تحتوي الفاتورة على عدة حقول تحتاجها—مثل **استخراج النص من الفاتورة** لكل من المبلغ الإجمالي وتاريخ الفاتورة. يمكنك التكرار على قائمة من المستطيلات:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

هذا النمط يحافظ على نظافة الكود ويسهل إضافة المزيد من المناطق لاحقًا.

---

## الخلاصة

لقد غطينا الآن سير عمل كامل من البداية إلى النهاية **لاستخراج النص من الصورة** باستخدام OCR في بايثون، مع التركيز على منطقة محددة. عبر **تحميل صورة للـ OCR**، تعريف **منطقة الاهتمام**، واستدعاء المحرك، يمكنك بثقة **قراءة النص من منطقة**—مثالي لاستخراج المبالغ من الفواتير، تواريخ من الإيصالات، أو أي بيانات محلية أخرى.  

لا تتردد في التجربة

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من الصورة – تحسين OCR مع Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية استخراج النص من الصورة بإعداد مستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}