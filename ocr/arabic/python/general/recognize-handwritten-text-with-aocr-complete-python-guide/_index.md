---
category: general
date: 2026-05-31
description: تعرّف على النص المكتوب بخط اليد بسرعة باستخدام Aocr. تعلّم كيفية تمكين
  إضافة النص المكتوب بخط اليد، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج النص
  من الصورة.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- load image for ocr
- handwritten text extraction
- how to enable handwritten
language: ar
og_description: التعرف على النص المكتوب بخط اليد في بايثون باستخدام Aocr. يوضح هذا
  الدليل كيفية تمكين إضافة الخط اليدوي، تحميل الصورة للتعرف الضوئي على الأحرف، واستخراج
  النص من الصورة.
og_title: التعرف على النص المكتوب بخط اليد باستخدام Aocr – دليل بايثون الكامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize handwritten text quickly using Aocr. Learn how to enable
    handwritten add‑on, load image for OCR, and extract text from image.
  headline: recognize handwritten text with Aocr – Complete Python Guide
  type: TechArticle
- description: recognize handwritten text quickly using Aocr. Learn how to enable
    handwritten add‑on, load image for OCR, and extract text from image.
  name: recognize handwritten text with Aocr – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If the image contains a clear note like:'
  - name: Running the Script
    text: '```bash python handwritten_ocr.py ```'
  - name: 1. Blurry or Low‑Contrast Images
    text: 'Handwritten OCR struggles with low‑quality scans. Before feeding the image
      to Aocr, consider:'
  - name: 2. Multi‑Page PDFs
    text: Aocr works on single images. If you have a multi‑page PDF, split it into
      individual pages (e.g., using `pdf2image`) and loop over each page, feeding
      them to the same engine instance.
  - name: 3. Non‑English Handwriting
    text: The default model focuses on English characters. For other alphabets, you’ll
      need to load language‑specific models (if available) via `ocr.set_language("es")`
      or similar.
  type: HowTo
- questions:
  - answer: Absolutely. The core engine handles printed text out of the box; you can
      toggle the handwritten add‑on on or off depending on your use case.
    question: Does this work with printed text too?
  - answer: Check the image path, ensure the file exists, and verify that the handwriting
      is legible. Pre‑processing (contrast boost) often fixes empty results.
    question: What if I get an empty string?
  - answer: 'Aocr’s `recognize()` returns plain text, but the library also offers
      `recognize_with_boxes()` which yields coordinates for each detected token—useful
      for highlighting in UI. ## Conclusion We’ve just **recognize handwritten text**
      using Aocr, from installing the package to printing the final string. '
    question: Can I get bounding boxes for each word?
  type: FAQPage
tags:
- OCR
- Python
- HandwritingRecognition
title: التعرف على النص المكتوب بخط اليد باستخدام Aocr – دليل بايثون الكامل
url: /ar/python/general/recognize-handwritten-text-with-aocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص المكتوب بخط اليد باستخدام Aocr – دليل بايثون كامل

هل تساءلت يومًا كيف يمكنك **التعرف على النص المكتوب بخط اليد** في صورة دون أن تشعر بالإحباط؟ لست وحدك. سواء كنت تقوم برقمنة ملاحظات الاجتماعات، أو معالجة النماذج، أو مجرد تجربة الذكاء الاصطناعي للمتعة، فإن الحصول على نص نظيف وقابل للبحث من خربشة قد يبدو كالسحر.  

الخبر السار؟ Aocr يجعل الأمر سهلًا للغاية. في هذا الدرس سنستعرض كل خطوة — *كيفية تمكين التعرف على الخط اليدوي*، *تحميل الصورة للـ OCR*، وأخيرًا *استخراج النص من الصورة* ببضع أسطر من بايثون فقط. بنهاية الدرس ستحصل على سكريبت جاهز للتنفيذ يحول ملاحظة مكتوبة بخط اليد إلى نص عادي.

## ما يغطيه هذا الدرس

- تثبيت حزمة Aocr للبايثون  
- إنشاء مثيل لمحرك OCR  
- **كيفية تمكين التعرف على الخط اليدوي** الإضافة  
- تحميل الصورة للـ OCR بشكل صحيح (مع مراعاة تفاصيل المسار)  
- تشغيل المحرك و**استخراج النص من الصورة**  
- الأخطاء الشائعة ونصائح لاستخراج **النص المكتوب بخط اليد** بشكل موثوق  

لا تحتاج إلى خبرة سابقة في Aocr، فقط إعداد بسيط للبايثون. هيا نبدأ.

## المتطلبات السابقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. تثبيت Python 3.8+ (أي نسخة حديثة).  
2. الوصول إلى الطرفية أو موجه الأوامر.  
3. ملف صورة يحتوي على ملاحظات مكتوبة بخط يد واضح (JPEG أو PNG).  
4. اتصال بالإنترنت لتثبيت الحزمة عبر `pip`.

إذا كان أي من هذه العناصر مفقودًا، توقف لحل المشكلة قبل المتابعة—وإلا سيتسبب الكود في أخطاء غير واضحة.

## الخطوة 1: تثبيت حزمة Aocr

أولًا وقبل كل شيء: تحتاج إلى مكتبة Aocr. هي متوفرة على PyPI، لذا أمر `pip` بسيط يكفي.

```bash
pip install aocr
```

> **نصيحة احترافية:** إذا كنت تستخدم بيئة افتراضية (مستحسن جدًا)، فعّلها قبل تشغيل أمر التثبيت. هذا يحافظ على تنظيم الاعتمادات ويتجنب تعارض الإصدارات.

## الخطوة 2: استيراد الوحدات وإنشاء مثيل لمحرك OCR

الآن سنستورد المكتبة وننشئ محركًا. فكر في المحرك كالعقل الذي سيقوم بالمعالجة الثقيلة.

```python
# Step 2: Import Aocr and create the engine
import aocr

# Create an OCR engine instance – this is where the magic begins
ocr = aocr.OcrEngine()
```

لماذا نحتاج إلى مثيل؟ كائن `OcrEngine` يحمل الإعدادات—مثل نماذج اللغة والإضافات—حتى يمكنك تعديلها حسب المشروع دون الحاجة لإعادة تهيئة كل شيء.

## الخطوة 3: **كيفية تمكين التعرف على الخط اليدوي** الإضافة

تأتي Aocr بمحرك OCR أساسي يدعم النص المطبوع مباشرة. أما التعرف على الخط اليدوي فموجود في إضافة اختيارية يجب تفعيلها صراحةً.

```python
# Step 3: Enable the handwritten‑recognition add‑on
# Passing True activates the feature; False would disable it.
ocr.enable_handwritten_recognition(True)
```

> **لماذا هذا مهم:** تفعيل الإضافة يحمل شبكة عصبية متخصصة تم تدريبها على الخطوط المتصلة والكتابة الكتلية. تخطي هذه الخطوة سيجعل المحرك يتعامل مع خربشاتك كضوضاء، فيعيد إما سلاسل فارغة أو نصًا غير مفهوم.

## الخطوة 4: تحميل الصورة للـ OCR بشكل صحيح

تحميل الصورة يبدو بسيطًا، لكن معالجة المسارات تُربك الكثير من المبتدئين—خاصة على Windows حيث تُعامل الشرطات العكسية كحروف هروب. استخدم السلاسل الخام (`r"..."`) أو الشرطات المائلة للأمام لتجنب الأخطاء الخفية.

```python
# Step 4: Load the image containing handwritten text
image_path = r"YOUR_DIRECTORY/handwritten_note.jpg"  # Replace with your actual path
ocr.load_image(image_path)
```

إذا كنت على macOS أو Linux، فإن نفس السلسلة الخام تعمل دون مشاكل. فقط تأكد من وجود الملف؛ وإلا سيظهر استثناء `FileNotFoundError`.

## الخطوة 5: تشغيل المحرك و**استخراج النص من الصورة**

مع جاهزية المحرك وتحميل الصورة، حان وقت التعرف على المحتوى. طريقة `recognize()` تُعيد سلسلة نصية عادية تحتوي جميع الأحرف المكتشفة.

```python
# Step 5: Perform OCR to recognize the handwritten content
result = ocr.recognize()

# Step 6: Output the recognized text
print("Recognized Handwritten Text:")
print(result)
```

### النتيجة المتوقعة

إذا كانت الصورة تحتوي على ملاحظة واضحة مثل:

```
Buy milk
Call Alice at 5pm
```

يجب أن ترى شيئًا مشابهًا يُطبع في سطر الأوامر:

```
Recognized Handwritten Text:
Buy milk
Call Alice at 5pm
```

قد تحدث اختلافات إملائية بسيطة—الخط اليدوي بطبيعته غير واضح تمامًا—لكن البنية العامة يجب أن تكون قابلة للتعرف.

## البرنامج الكامل – جاهز للتنفيذ

فيما يلي السكريبت الكامل المستقل الذي يجمع جميع الخطوات. انسخه إلى ملف باسم `handwritten_ocr.py`، استبدل `image_path`، ثم نفّذ `python handwritten_ocr.py`.

```python
"""
Handwritten Text Recognition with Aocr
--------------------------------------
This script demonstrates how to:
- enable the handwritten add‑on,
- load an image for OCR,
- and extract text from image.
"""

import aocr

def main():
    # 1️⃣ Create OCR engine
    ocr = aocr.OcrEngine()

    # 2️⃣ Enable handwritten recognition (the crucial add‑on)
    ocr.enable_handwritten_recognition(True)

    # 3️⃣ Load your handwritten image
    image_path = r"YOUR_DIRECTORY/handwritten_note.jpg"  # 👉 Update this line
    ocr.load_image(image_path)

    # 4️⃣ Perform recognition
    result = ocr.recognize()

    # 5️⃣ Print the extracted text
    print("\n=== Recognized Handwritten Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

### تشغيل السكريبت

```bash
python handwritten_ocr.py
```

إذا تم إعداد كل شيء بشكل صحيح، ستظهر النصوص المستخرجة في سطر الأوامر. 🎉

## التعامل مع الحالات الخاصة الشائعة

### 1. الصور الضبابية أو منخفضة التباين

يواجه OCR للخط اليدوي صعوبة مع المسحات منخفضة الجودة. قبل تمرير الصورة إلى Aocr، فكر في:

- تحويلها إلى تدرج الرمادي (`cv2.cvtColor`)  
- تطبيق تمويه غاوسي خفيف لتقليل الضوضاء  
- تعديل التباين باستخدام Pillow (`ImageEnhance.Contrast`)

هذه الخطوات المسبقة يمكن أن تحسّن بشكل كبير دقة **استخراج النص المكتوب بخط اليد**.

### 2. ملفات PDF متعددة الصفحات

تعمل Aocr على صورة واحدة فقط. إذا كان لديك PDF متعدد الصفحات، قسّمه إلى صفحات منفصلة (مثلاً باستخدام `pdf2image`) وكرر العملية على كل صفحة، مع تمريرها إلى نفس مثيل المحرك.

### 3. الخط اليدوي غير الإنجليزي

النموذج الافتراضي يركز على الأحرف الإنجليزية. للغات أخرى، ستحتاج إلى تحميل نماذج مخصصة للغة (إن وجدت) عبر `ocr.set_language("es")` أو ما شابه.

## نصائح احترافية لاستخراج **النص المكتوب بخط اليد** بشكل موثوق

- **حافظ على حجم الصورة معقولًا**: الصور الكبيرة جدًا تستهلك ذاكرة أكثر وتبطئ عملية التعرف. قلّص العرض إلى حوالي 1200 px مع الحفاظ على نسبة الأبعاد.  
- **تجنّب النص المائل**: تتوقع Aocr النص في وضعية عمودية. استخدم `ocr.rotate_image(angle)` إذا كانت ملاحظتك مائلة.  
- **معالجة دفعات**: عند التعامل مع عشرات الملاحظات، أعد استخدام نفس مثيل `OcrEngine`—فإن تهيئته مرة واحدة يقلل من استهلاك الوقت.

## الأسئلة المتكررة

**س: هل يعمل هذا مع النص المطبوع أيضًا؟**  
ج: بالطبع. المحرك الأساسي يدعم النص المطبوع مباشرة؛ يمكنك تشغيل أو إيقاف إضافة الخط اليدوي حسب الحاجة.

**س: ماذا أفعل إذا حصلت على سلسلة فارغة؟**  
ج: تحقق من مسار الصورة، تأكد من وجود الملف، وتأكد من وضوح الخط اليدوي. غالبًا ما يحل تحسين التباين المشكلة.

**س: هل يمكنني الحصول على إطارات حدودية لكل كلمة؟**  
ج: تُعيد `recognize()` نصًا عاديًا، لكن المكتبة توفر أيضًا `recognize_with_boxes()` التي تُعيد إحداثيات لكل رمز مكتشف—مفيد لتسليط الضوء في واجهة المستخدم.

## الخلاصة

لقد قمنا للتو **بالتعرف على النص المكتوب بخط اليد** باستخدام Aocr، من تثبيت الحزمة إلى طباعة السلسلة النهائية. باتباع الخطوات—**كيفية تمكين الإضافة للخط اليدوي**، تحميل الصورة للـ OCR بشكل صحيح، وأخيرًا **استخراج النص من الصورة**—أصبح لديك أساس قوي لأي مشروع يحتاج إلى **استخراج النص المكتوب بخط اليد**.  

الخطوة التالية: جرّب تمرير دفعة من الملاحظات إلى المحرك، جرب معالجة الصور مسبقًا، أو استكشف واجهة إطارات الحدود للحصول على مخرجات أغنى. الإمكانيات لا حصر لها، ومع تصميم Aocr المرن، ستجد أن تحويل الخربشات إلى بيانات قابلة للبحث لم يعد مصدر صداع.

هل لديك أسئلة إضافية أو تريد مشاركة نتائجك؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [كيفية استخراج النص من الصورة عبر إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [استخراج النص من صورة Java باستخدام Aspose.OCR وضعية اكتشاف المناطق](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}