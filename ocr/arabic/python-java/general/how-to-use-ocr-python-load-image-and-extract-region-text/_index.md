---
category: general
date: 2026-06-25
description: كيفية استخدام OCR في بايثون – تعلم كيفية تحميل الصورة للـ OCR، التعرف
  على النص في المنطقة، واستخراج نص المنطقة بسرعة.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: ar
og_description: كيفية استخدام OCR في بايثون – دليل خطوة بخطوة لتحميل صورة، التعرف
  على النص في منطقة محددة، واستخراج رقم الفاتورة.
og_title: 'كيفية استخدام OCR في بايثون: تحميل الصورة واستخراج نص المنطقة'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'كيفية استخدام OCR في بايثون: تحميل الصورة واستخراج نص المنطقة'
url: /ar/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في بايثون: تحميل الصورة واستخراج نص المنطقة

**كيفية استخدام OCR في بايثون** أسهل مما تتصور. هل سبق وأن نظرت إلى فاتورة ممسوحة ضوئياً وتساءلت كيف تستخرج رقم الفاتورة فقط دون تحليل الصفحة بأكملها؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يبدؤون أول مرة مع التعرف الضوئي على الأحرف. في هذا الدليل سنستعرض خطوات تحميل صورة للـ OCR، تعريف مستطيل، التعرف على النص داخل تلك المنطقة، وأخيراً استخراج نص المنطقة. في النهاية ستحصل على سكريبت جاهز للتنفيذ يعزل أي قطعة نص تحتاجها.

> *نصيحة احترافية:* إذا كنت تتعامل مع ملفات PDF، حوّل كل صفحة إلى صورة أولاً—معظم مكتبات OCR تتعامل مع PNG/JPEG بأفضل شكل.

## ما الذي ستحتاجه

- بايثون 3.8+ (يوصى بأحدث إصدار ثابت)  
- مكتبة OCR تُوفر فئة `OcrEngine` (مثال: **ocr** من `pip install ocr-lib`)  
- صورة نموذجية—سنستخدم هنا `invoice.png` موجودة في مجلد تتحكم به  
- معرفة أساسية بالمستطيلات (x, y, العرض, الارتفاع)  

لا توجد تبعيات ثقيلة، ولا حاجة لمعالج رسومي (GPU)—كل شيء يعمل على CPU، مما يجعل الحل محمولاً.

---

## كيفية استخدام OCR: تهيئة المحرك (الخطوة 1)

قبل أن يتم قراءة أي نص، تحتاج إلى إنشاء نسخة من محرك OCR. فكر فيه كالعقل الذي سيحلل أنماط البكسل.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*لماذا هذا مهم:* تهيئة المحرك تقوم بتحميل نماذج اللغات وتعيين الإعدادات الافتراضية. تخطي هذه الخطوة سيتسبب في رفع استثناء في اللحظة التي تستدعي فيها `recognize_region`.

---

## تحميل الصورة للـ OCR (الخطوة 2)

الآن بعد أن أصبح المحرك جاهزاً، نمرره صورة. طريقة `Image.load` في المكتبة تتعامل مع الصيغ الشائعة وتُعِدّ البت ماب إلى صيغة موحدة.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

إذا لم يتم العثور على الملف، سيُطلق بايثون استثناء `FileNotFoundError`. تأكد من أن المسار مطلق أو نسبياً إلى دليل تشغيل السكريبت.  

*حالة خاصة:* بعض محركات OCR تتطلب صورة بتدرج الرمادي. إذا لاحظت دقة منخفضة، حوّل الصورة أولاً:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## التعرف على النص في المنطقة (الخطوة 3)

تعريف المنطقة هو ما تخبر فيه المحرك *أين* يبحث. فئة `Rectangle` تقبل قيمًا عائمة للحصول على دقة تحت البكسل، وهو مفيد عند التعامل مع مسحات عالية الدقة.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – إحداثيات الزاوية العلوية اليسرى للمستطيل (بالبكسل)  
- **العرض, الارتفاع** – حجم الصندوق  

قد تتساءل كيف تحصل على هذه الأرقام. طريقة سريعة هي فتح الصورة في أي محرر (مثل GIMP أو Paint.NET) واستخدام أداة التحديد لقراءة الإحداثيات.  

*لماذا لا تقوم بعمل OCR للصفحة بأكملها؟* تحديد المنطقة يقلل الضوضاء، يسرّع المعالجة، ويحسّن الدقة بشكل كبير للحقول الصغيرة مثل أرقام الفواتير.

---

## كيفية استخراج نص المنطقة (الخطوة 4)

بعد ضبط المنطقة، اطلب من المحرك التعرف فقط على تلك القطعة. كائن النتيجة يحتوي على النص الخام ونقاط الثقة.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

إذا كان محرك OCR يدعم لغات متعددة، يمكنك تمرير رمز لغة اختياري:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*خطأ شائع:* بعض المحركات تُعيد قائمة من الكلمات بدلاً من سلسلة نصية واحدة. في هذه الحالة، قم بدمجها:

```python
text = " ".join(region_result.words)
```

---

## طباعة رقم الفاتورة المستخرج (الخطوة 5)

أخيراً، اطبع—أو احفظ—النص المستخرج. يمكنك أيضاً معالجة السلسلة لإزالة المسافات الزائدة أو الأحرف غير الرقمية.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

تشغيل السكريبت مع مستطيل مُحاذٍ بشكل صحيح يجب أن ينتج شيئًا مثل:

```
Invoice number: 20231578
```

إذا حصلت على رموز غير مفهومة، تحقق مرة أخرى من إحداثيات المستطيل أو فكر في زيادة دقة الصورة.

---

## مثال كامل يعمل

بجمع كل ما سبق، إليك سكريبت مستقل يمكنك نسخه ولصقه وتشغيله:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

احفظ الملف باسم `extract_invoice.py`، استبدل `YOUR_DIRECTORY` بالمجلد الفعلي، ثم شغّله:

```bash
python extract_invoice.py
```

يجب أن ترى رقم الفاتورة يُطبع في وحدة التحكم.

---

## الأسئلة المتكررة

**س: ماذا لو كان رقم الفاتورة مطبوعًا بخط مزخرف؟**  
ج: معظم محركات OCR الحديثة تدعم مجموعة واسعة من الخطوط، لكن يمكنك تحسين الدقة بتدريب نموذج لغة مخصص أو بتمهيد الصورة مسبقًا (مثال: تطبيق مرشح عتبة).

**س: هل يمكن استخراج عدة حقول في آن واحد؟**  
ج: بالتأكيد. عرّف قائمة من كائنات `Rectangle`—واحد لكل حقل—واستخدم حلقة لتكرارها، مع تخزين كل نتيجة في قاموس.

**س: هل يعمل هذا على ملفات PDF متعددة الصفحات؟**  
ج: حوّل كل صفحة إلى صورة أولاً (باستخدام `pdf2image` أو ما شابه)، ثم طبّق نفس طريقة الاستخراج القائمة على كل صفحة.

---

## الخلاصة

في هذا الدليل غطينا **كيفية استخدام OCR** في بايثون لتحميل صورة، التعرف على نص في منطقة محددة، واستخراج نص تلك المنطقة—مثالي لاستخراج أرقام الفواتير، معرفات الطلبات، أو أي قطعة بيانات صغيرة من المستندات الممسوحة. من خلال عزل منطقة الاهتمام تحصل على سرعة، دقة، وأقل جهد في ما بعد المعالجة.

هل أنت مستعد للخطوة التالية؟ جرّب توسيع السكريبت ليُحمّل الصور للـ OCR من مجلد يحتوي على دفعات من الفواتير، أو جرب **recognize text in region** لحقول مختلفة مثل التواريخ والمجموعات. النمط نفسه يُطبق—فقط غيّر إحداثيات المستطيل.

إذا واجهت أي مشاكل أو لديك أفكار للتحسين، اترك تعليقًا أدناه. برمجة سعيدة، ولتكن خطوط أنابيب OCR دقيقة دائمًا!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}