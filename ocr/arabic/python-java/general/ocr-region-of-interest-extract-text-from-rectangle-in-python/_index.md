---
category: general
date: 2026-05-31
description: تعلم كيفية استخدام منطقة الاهتمام في OCR لتحميل الصورة للـ OCR واستخراج
  النص من المستطيل، وهو مثالي للتعرف على المبلغ في الفاتورة.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: ar
og_description: إتقان منطقة الاهتمام في OCR لتحميل الصورة للـ OCR، استخراج النص من
  المستطيل والتعرف على النص من الفاتورة في دليل واحد.
og_title: منطقة الاهتمام في OCR – دليل بايثون خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: منطقة الاهتمام في OCR – استخراج النص من مستطيل باستخدام بايثون
url: /ar/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – استخراج النص من مستطيل في بايثون

هل تساءلت يومًا كيف تقوم بـ **ocr region of interest** لجزء محدد من فاتورة ممسوحة ضوئيًا دون إطعام الصفحة بأكملها إلى المحرك؟ لست أول من يحدق في إيصال غير واضح ويفكر، “كيف أستخرج المبلغ الذي يقع في أسفل اليمين؟” الخبر السار هو أنك تستطيع إخبار مكتبة OCR بالضبط أين تبحث، مما يزيد السرعة والدقة بشكل كبير.

في هذا الدليل سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يوضح لك كيفية **load image for OCR**، تعريف **region of interest**، ثم **extract text from rectangle** وأخيرًا **recognize text from invoice** للإجابة على سؤال “كيفية استخراج المبلغ”. لا مراجع غامضة—فقط كود ملموس، شروحات واضحة، وبعض النصائح الاحترافية التي كنت تتمنى معرفتها مبكرًا.

---

## ما ستبنيه

بنهاية هذا البرنامج التعليمي ستحصل على سكريبت بايثون صغير يقوم بـ:

1. تحميل صورة فاتورة من القرص.  
2. وضع مستطيل ROI حيث يوجد المبلغ الإجمالي.  
3. تشغيل OCR داخل ذلك الـ ROI فقط.  
4. طباعة سلسلة المبلغ المنقحة.  

كل هذا يعمل مع أي مكتبة OCR تدعم الـ ROI—سنستخدم هنا حزمة خيالية تمثيلية `SimpleOCR` تشبه الأدوات الشهيرة مثل Tesseract أو EasyOCR. يمكنك استبدالها بسهولة؛ المفاهيم تبقى نفسها.

---

## المتطلبات المسبقة

- تثبيت Python 3.8+ (`python --version` يجب أن يظهر ≥3.8).  
- حزمة OCR قابلة للتثبيت عبر pip (مثال: `pip install simpleocr`).  
- صورة فاتورة (PNG أو JPEG) موجودة في مجلد يمكنك الإشارة إليه.  
- إلمام أساسي بدوال وفئات بايثون (لا شيء معقد).

إذا كان لديك كل ذلك، رائع—لنبدأ. إذا لم يكن، احصل على الصورة أولًا؛ باقي الخطوات مستقلة عن محتوى الملف الفعلي.

---

## الخطوة 1: Load Image for OCR

أول شيء يحتاجه أي سير عمل OCR هو صورة نقطية للقراءة منها. معظم المكتبات توفر طريقة بسيطة `load_image` تقبل مسار الملف. إليك الطريقة مع محرك `SimpleOCR` الخاص بنا:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **نصيحة احترافية:** استخدم مسارات مطلقة أو `os.path.join` لتجنب مفاجآت “الملف غير موجود” عند تشغيل السكريبت من دليل عمل مختلف.

---

## الخطوة 2: Define OCR Region of Interest

بدلاً من السماح للمحرك بمسح الصفحة بأكملها، نخبره *بالضبط* أين يقع المبلغ. هذه هي خطوة **ocr region of interest**، وهي المفتاح لاستخراج موثوق، خاصة عندما يحتوي المستند على رؤوس أو تذييلات صاخبة.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

لماذا هذه الأرقام؟ `x` و `y` هما إزاحة بالبكسل من الزاوية العلوية اليسرى، بينما `width` و `height` يحددان حجم الصندوق. إذا لم تكن متأكدًا، افتح الصورة في أي محرر، فعّل المسطرة، وسجل الإحداثيات. العديد من بيئات التطوير تسمح لك بطباعة موضع المؤشر أثناء التحويم.

---

## الخطوة 3: Extract Text from Rectangle

الآن بعد ضبط الـ ROI، نطلب من المحرك **recognize text from invoice** لكن مقيدًا بالمستطيل الذي أضفناه. تُعيد الدالة كائن نتيجة يحتوي عادةً على السلسلة الخام، درجات الثقة، وأحيانًا إطارات الحدود.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

خلف الكواليس، `recognize()` يمر على كل ROI، يقتطع تلك القطعة، يشغل نموذج OCR، ويجمع النتائج معًا. لهذا السبب تعريف منطقة **extract text from rectangle** ضيقة يمكن أن يوفر ثوانٍ من وقت المعالجة للوظائف الدفعية.

---

## الخطوة 4: How to Extract Amount – Clean the Output

OCR ليس مثاليًا؛ ستحصل غالبًا على مسافات زائدة، أسطر جديدة، أو حتى أحرف مخطئة (مثل “S” بدلًا من “5”). `strip()` سريع وبعض التعبيرات النمطية الصغيرة عادةً ما تحل المشكلة للقيم المالية.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **لماذا هذا مهم:** إذا كنت تخطط لإدخال المبلغ في قاعدة بيانات أو بوابة دفع، تحتاج إلى تنسيق متوقع. إزالة الفراغات وتصفية الأحرف غير الرقمية يمنع الأخطاء في المراحل اللاحقة.

---

## الخطوة 5: Recognize Text from Invoice – Full Script

بدمج كل ما سبق، إليك السكريبت الكامل الجاهز للتنفيذ. احفظه باسم `extract_amount.py` وشغّله باستخدام `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

```
Amount: 1,245.67
```

إذا كان الـ ROI غير محاذٍ بشكل صحيح، قد ترى شيئًا مثل `Amount: 1245.6S`—لاحظ الـ “S” الزائدة. عدّل إحداثيات المستطيل وأعد التشغيل حتى تصبح النتيجة نظيفة.

---

## المشكلات الشائعة وحالات الحافة

| المشكلة | السبب | الحل |
|--------|-------|------|
| **ROI صغير جدًا** | يتم قطع نص المبلغ، مما يؤدي إلى تعرّف جزئي. | زِد `width`/`height` بنحو 10‑20 % وأعد الاختبار. |
| **دقة DPI غير صحيحة** | المسحات منخفضة الدقة (≤150 dpi) تقلل من دقة OCR. | أعد تحجيم الصورة إلى 300 dpi قبل التحميل، أو اطلب من الماسح دقة أعلى. |
| **عملات متعددة** | التعبير النمطي يلتقط أول مجموعة رقمية، قد تكون رقم الفاتورة. | حسّن التعبير النمطي للبحث عن رموز العملة (`$`, `€`, `£`) قبل الأرقام. |
| **فواتير مائلة** | محركات OCR تفترض نصًا عموديًا؛ الصفحات المائلة تعطل التعرف. | طبّق تصحيح دوران (`ocr_engine.rotate(90)`) قبل إضافة ROI. |
| **ضوضاء في الخلفية** | الظلال أو الختم يربك النموذج. | عالج مسبقًا باستخدام عتبة بسيطة (`cv2.threshold`) أو مرشح إزالة الضوضاء. |

معالجة هذه الحالات مبكرًا توفر لك ساعات من التصحيح لاحقًا.

---

## نصائح احترافية للمشاريع الواقعية

- **معالجة دفعات:** حلق عبر مجلد الفواتير، احسب ROI ديناميكيًا (مثلاً بناءً على اكتشاف القالب)، وخزن النتائج في CSV.  
- **مطابقة القوالب:** إذا كنت تتعامل مع عدة تخطيطات فواتير، احتفظ بخريطة JSON من `template_id → إحداثيات ROI`. غيّر ROI بناءً على مصنف تخطيط سريع.  
- **التنفيذ المتوازي:** استخدم `concurrent.futures.ThreadPoolExecutor` لتشغيل عدة مثيلات OCR متزامنًا—مفيد لخطوط الأنابيب الخلفية ذات الحجم الكبير.  
- **تصفية الثقة:** معظم نتائج OCR تشمل درجة ثقة. تجاهل النتائج التي تقل عن عتبة (مثال: 85 %) وضع علامة عليها للمراجعة اليدوية.

---

## الخلاصة

غطّينا كل ما تحتاجه للقيام بـ **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, وأخيرًا **recognize text from invoice** للإجابة على سؤال **how to extract amount** الشائع. السكريبت صغير، لكنه مرن بما يكفي للتكيف مع صيغ مستندات مختلفة، لغات متعددة، ومزودي OCR مختلفين.

الآن بعد أن أتقنت الأساسيات، فكر في توسيع سير العمل: أضف مسح الباركود، دمج مع محلل PDF، أو إرسال المبلغ المستخرج إلى واجهة برمجة تطبيقات محاسبة. السماء هي الحد، ومع ROI معرف جيدًا ستحصل دائمًا على نتائج أسرع وأنظف.

إذا واجهت أي صعوبة، اترك تعليقًا أدناه—نتمنى لك OCR موفق!

![مثال على منطقة الاهتمام في OCR](https://example.com/ocr_roi_example.png "مثال على منطقة الاهتمام في OCR")


## ماذا يجب أن تتعلم بعد ذلك؟

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}