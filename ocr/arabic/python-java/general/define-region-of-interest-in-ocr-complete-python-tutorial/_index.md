---
category: general
date: 2026-06-16
description: حدد منطقة الاهتمام في تقنية التعرف الضوئي على الأحرف لاستخراج النص الإسباني
  من بطاقات الهوية. تعلّم كيفية تحميل الصورة للتعرف الضوئي على الأحرف وتحديد منطقة
  الاهتمام بكفاءة.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: ar
og_description: حدد منطقة الاهتمام في تقنية التعرف الضوئي على الأحرف لاستخراج النص
  الإسباني من بطاقات الهوية. دليل خطوة بخطوة لتحميل الصور وتحديد منطقة الاهتمام.
og_title: تحديد منطقة الاهتمام في التعرف الضوئي على الأحرف – دليل بايثون الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: تحديد منطقة الاهتمام في التعرف الضوئي على الأحرف – دورة بايثون كاملة
url: /ar/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تعريف منطقة الاهتمام في OCR – دليل بايثون كامل

هل تساءلت يومًا كيف **تعرف منطقة الاهتمام في OCR** بحيث تقرأ فقط الجزء من الصورة الذي تحتاجه فعلاً؟ في هذا الدليل سنرشدك إلى ذلك بالضبط، بالإضافة إلى إظهار كيفية **تحميل الصورة لـ OCR** واستخراج النص الإسباني من بطاقة هوية في بضع أسطر من بايثون.  

إذا كنت قد حدقت يومًا في مسح ضوضائي وفكرت، “يجب أن يكون هناك طريقة أنظف للحصول على حقل الاسم”، فأنت في المكان الصحيح. بنهاية هذا الدليل ستتمكن من استخراج نص بطاقة الهوية الذي يهمك دون التعثر في الفوضى الخلفية.

## ما ستتعلمه

- لماذا يجب عليك **تعريف منطقة الاهتمام** قبل تشغيل OCR.  
- الخطوات الدقيقة لـ **تحميل الصورة لـ OCR** باستخدام غلاف بايثون شائع لـ OCR.  
- كيف **تحدد ROI** باستخدام إحداثيات البكسل.  
- طرق **استخراج نص بطاقة الهوية** بشكل موثوق، حتى عندما تكون اللغة المصدر إسبانية.  
- نصائح للتعامل مع الحالات الخاصة مثل البطاقات المائلة أو المسحات منخفضة التباين.  

لا تحتاج إلى خبرة سابقة في OCR — فقط بيئة Python 3 تعمل وصورة JPEG لبطاقة هوية تريد اختبارها.

---

![Define region of interest illustration](placeholder.png){alt="مثال على تعريف منطقة الاهتمام يظهر مستطيلًا مميزًا على صورة بطاقة هوية"}

## الخطوة 1: تثبيت واستيراد مكتبة OCR

أولاً، تحتاج إلى مكتبة تُظهر فئة `OcrEngine` مشابهة للمقتطف الذي رأيته. في هذا الدليل سنستخدم الحزمة الخيالية `ocr`، لكن نفس المفاهيم تنطبق على `pytesseract`، `easyocr`، أو أي غلاف يتيح لك ضبط اللغة و ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*نصيحة محترف:* إذا كنت تستخدم `pytesseract`، تصبح فئة `Rectangle` عبارة عن زوج بسيط `(left, top, width, height)`. بقية العملية تبقى متطابقة.

## الخطوة 2: تحميل الصورة لـ OCR

الآن **نحمّل الصورة لـ OCR**. المحرك يتوقع كائن `ocr.Image`، لذا نشير إليه إلى الملف الذي يحتوي على بطاقة الهوية. تأكد أن المسار مطلق أو نسبي إلى دليل عمل السكريبت الخاص بك.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

إذا كانت الصورة ضخمة، فكر في تصغيرها أولاً؛ محركات OCR تعمل أسرع على الصور التي يقل عرضها عن 1500 px.

## الخطوة 3: كيفية تحديد ROI (تعريف منطقة الاهتمام)

هذا هو جوهر الدليل: **كيفية تحديد ROI**. منطقة الاهتمام هي ببساطة مستطيل يخبر محرك OCR، “انظر فقط داخل هذه الحدود البكسلية.” فكر فيها كأنك ترسم صندوقًا حول حقل الاسم في بطاقة الهوية.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

لماذا هذه الأرقام؟ في صورتنا النموذجية يقع الاسم تقريبًا على بعد 120 px من الحافة اليسرى و80 px من الأعلى. عدّلها لتتناسب مع تخطيط البطاقات التي تعالجها.  

*حالة خاصة:* إذا كانت البطاقة مائلة 90°، قم بتبديل `width` و `height` وضبط `left`/`top` وفقًا لذلك، أو قم بلف الصورة مسبقًا باستخدام Pillow قبل تمريرها إلى المحرك.

## الخطوة 4: تنفيذ OCR داخل ROI

مع تعريف ROI، سيتجاهل المحرك كل ما هو خارج المستطيل. هذا لا يسرّع المعالجة فحسب، بل يقلل أيضًا من الإيجابيات الزائفة التي تسببها الرسومات الخلفية.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

استدعاء `recognize()` يُعيد كائن يحتوي على النص المُعرّف، درجات الثقة، ومربعات الإحاطة لكل كلمة.

## الخطوة 5: استخراج نص بطاقة الهوية (وتحقق من النتيجة الإسبانية)

أخيرًا، **نستخرج نص بطاقة الهوية** من نتيجة ROI ونطبعه. لأننا ضبطنا اللغة إلى الإسبانية مسبقًا، سيستخدم محرك OCR القواميس الخاصة باللغة، مما يحسّن الدقة للأحرف المشكّلة مثل “ñ” أو “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### النتيجة المتوقعة

```
ROI text: JUAN PÉREZ GARCÍA
```

إذا رأيت أحرفًا مشوشة، تحقق مرة أخرى أن الصورة فعلاً بالإسبانية وأن ملفات بيانات لغة OCR مُثبتة.

## المشكلات الشائعة وكيفية تجنّبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| تم إرجاع سلسلة فارغة | ROI لا يتقاطع مع أي نص | تحقق من الإحداثيات باستخدام عارض صور؛ استخدم `engine.debug_draw_roi()` إذا كان متاحًا. |
| الكثير من الأحرف غير المفهومة | حزمة اللغة غير صحيحة | أعد تثبيت بيانات اللغة الإسبانية أو انتقل إلى `ocr.Language.AUTO`. |
| درجات ثقة منخفضة | الصورة غير واضحة أو منخفضة التباين | عالجها مسبقًا باستخدام OpenCV – طبّق `cv2.GaussianBlur` و `cv2.threshold`. |
| يعمل OCR على الصورة بالكامل رغم تحديد ROI | استخدام نسخة قديمة من المكتبة | حدّث إلى أحدث حزمة `ocr`؛ الإصدارات القديمة كانت تتجاهل ROI. |

## توسيع المثال: عدة ROIs

أحيانًا تحتاج إلى استخراج أكثر من حقل (مثل الاسم ورقم الهوية). النمط يبقى نفسه: غيّر `engine.region_of_interest` واستدعِ `recognize()` مرة أخرى.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

يمكنك أيضًا معالجة قائمة من المستطيلات دفعة واحدة إذا كانت المكتبة تدعم ذلك، مما يوفر جولة إضافية إلى محرك OCR.

## سكريبت كامل يعمل

بجمع كل ما سبق، إليك سكريبت جاهز للتنفيذ **يعرف منطقة الاهتمام**، **يحمّل الصورة لـ OCR**، و**يستخرج النص الإسباني** من بطاقة هوية.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

شغّل السكريبت وسترى الاسم يُطبع في وحدة التحكم. غيّر قيم المستطيل لاستهداف حقول أخرى، وستحصل على أداة قابلة لإعادة الاستخدام لأي مستند من نوع بطاقة هوية.

## الخطوات التالية

- **المعالجة الدفعية:** كرّر عبر مجلد من بطاقات الهوية واحفظ كل اسم مستخرج في ملف CSV.  
- **اكتشاف اللغة:** اسمح للمستخدم باختيار اللغة ديناميكيًا؛ `ocr.Language.AUTO` يمكن أن يكون مفيدًا.  
- **ما بعد المعالجة:** طبّق أنماط regex لتنظيف الأخطاء الشائعة في OCR (مثلاً استبدال “0” بـ “O” عندما تظهر في الأسماء).  

بإتقانك كيفية **تعريف منطقة الاهتمام**، فتحت طريقة قوية لـ **استخراج نص بطاقة الهوية** بسرعة ودقة، خاصةً عند التعامل مع مستندات باللغة الإسبانية.

---

### ملخص

أظهرنا لك كيفية **تعريف منطقة الاهتمام في OCR**، **تحميل الصورة لـ OCR**، و**تحديد ROI** لاستخراج **النص الإسباني** من بطاقة هوية. المثال الكامل يعمل في أقل من دقيقة ويمكن تكييفه مع أي تخطيط ببضع تعديلات على الإحداثيات. جرّبه، عدّل المستطيل، وشاهد OCR يركز كالليزر.

برمجة سعيدة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}