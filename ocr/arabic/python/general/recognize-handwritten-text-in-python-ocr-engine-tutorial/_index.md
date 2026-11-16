---
category: general
date: 2026-04-26
description: التعرف على النص المكتوب بخط اليد باستخدام محرك OCR في بايثون. تعلم كيفية
  استخراج النص من الصورة، وتفعيل وضع الخط اليدوي، وقراءة الملاحظات المكتوبة بخط اليد
  بسرعة.
draft: false
keywords:
- recognize handwritten text
- extract text from image
- read handwritten notes
- turn on handwritten mode
- create OCR engine python
language: ar
og_description: التعرف على النص المكتوب بخط اليد باستخدام بايثون. يوضح هذا الدرس كيفية
  استخراج النص من الصورة، وتفعيل وضع الخط اليدوي، وقراءة الملاحظات المكتوبة بخط اليد
  باستخدام محرك OCR بسيط.
og_title: التعرف على النص المكتوب بخط اليد في بايثون – دليل OCR الكامل
tags:
- OCR
- Python
- Handwriting Recognition
title: التعرف على النص المكتوب بخط اليد في بايثون – دليل محرك OCR
url: /ar/python/general/recognize-handwritten-text-in-python-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص المكتوب بخط اليد في بايثون – دليل محرك OCR

هل احتجت يومًا إلى **التعرف على النص المكتوب بخط اليد** لكن شعرت بالحيرة عند سؤال “من أين أبدأ؟”؟ لست وحدك. سواءً كنت تقوم برقمنة ملاحظات الاجتماعات أو استخراج البيانات من نموذج ممسوح ضوئيًا، فإن الحصول على نتيجة OCR موثوقة قد يبدو كمطاردة وحيد القرن.  

خبر سار: ببضع أسطر فقط من بايثون يمكنك **استخراج النص من صورة**، **تفعيل وضع الخط اليدوي**، وأخيرًا **قراءة الملاحظات المكتوبة بخط اليد** دون الحاجة للبحث عن مكتبات غامضة. في هذا الدليل سنستعرض العملية بالكامل، من إعداد على نمط **create OCR engine python** إلى طباعة النتيجة على الشاشة.

## ما ستتعلمه

- كيفية إنشاء مثيل **create OCR engine python** باستخدام حزمة `ocr`.  
- أي إعداد لغة يوفّر لك دعمًا مدمجًا للخط اليدوي.  
- النداء الدقيق لتفعيل **turn on handwritten mode** حتى يعرف المحرك أنك تتعامل مع الخط المتصل.  
- كيفية إمداد صورة ملاحظة و**التعرف على النص المكتوب بخط اليد** منها.  
- نصائح للتعامل مع صيغ الصور المختلفة، استكشاف الأخطاء الشائعة، وتوسيع الحل.

بدون إطالة، دون “انظر إلى الوثائق” المميتة—فقط سكريبت كامل قابل للتنفيذ يمكنك نسخه ولصقه واختباره اليوم.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

1. Python 3.8+ مثبت (الكود يستخدم f‑strings).  
2. مكتبة `ocr` الافتراضية (`pip install ocr‑engine` – استبدلها باسم الحزمة الفعلية التي تستخدمها).  
3. ملف صورة واضح لملاحظة مكتوبة بخط اليد (JPEG، PNG، أو TIFF).  
4. قليل من الفضول—كل ما تبقى مغطى أدناه.

> **نصيحة احترافية:** إذا كانت صورتك مشوشة، قم بخطوة تمهيد سريعة باستخدام Pillow (مثال: `Image.open(...).convert('L')`) قبل إرسالها إلى محرك OCR. غالبًا ما يحسن ذلك الدقة.

## كيفية التعرف على النص المكتوب بخط اليد باستخدام بايثون

فيما يلي السكريبت الكامل الذي **creates OCR engine python** كائنات، يضبطها للخط اليدوي، ويطبع السلسلة المستخرجة. احفظه باسم `handwriting_ocr.py` وشغّله من الطرفية.

```python
# handwriting_ocr.py
import ocr                     # The OCR library that provides OcrEngine
import os

def main():
    # Step 1: Create an OCR engine instance
    # This is the core object that will do all the heavy lifting.
    ocr_engine = ocr.OcrEngine()

    # Step 2: Choose a language that includes handwritten support.
    # EXTENDED_LATIN covers most Western alphabets and knows how to
    # handle cursive strokes.
    ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)

    # Step 3: Turn on handwritten mode.
    # Without this flag the engine assumes printed text and will miss
    # most of the nuances in a scribble.
    ocr_engine.enable_handwritten_mode(True)

    # Step 4: Define the path to your handwritten image.
    # Replace the placeholder with the actual location of your file.
    image_path = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")

    # Basic validation – makes debugging easier.
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 5: Recognize text from the image.
    # The recognize_image method returns a result object that holds
    # both the raw text and confidence scores.
    handwritten_result = ocr_engine.recognize_image(image_path)

    # Step 6: Display the extracted text.
    # This is where you finally **read handwritten notes** programmatically.
    print("=== Extracted Text ===")
    print(handwritten_result.text)

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

عند تشغيل السكريبت بنجاح، سترى شيئًا مشابهًا لـ:

```
=== Extracted Text ===
Meeting notes:
- Discuss quarterly targets
- Assign tasks to Alice & Bob
- Follow‑up email by Friday
```

إذا لم يتمكن محرك OCR من اكتشاف أي أحرف، سيكون حقل `text` سلسلة فارغة. في هذه الحالة، تحقق مرة أخرى من جودة الصورة أو جرّب مسحًا بدقة أعلى.

## شرح خطوة بخطوة

### الخطوة 1 – مثيل **create OCR engine python**

فئة `OcrEngine` هي نقطة الدخول. فكر فيها كدفتر ملاحظات فارغ—لا يحدث شيء حتى تخبره بأي لغة تتوقعها وما إذا كنت تتعامل مع الخط اليدوي.

### الخطوة 2 – اختر لغة تدعم الخط اليدوي

`ocr.Language.EXTENDED_LATIN` ليست مجرد “إنجليزية”. إنها تجمع مجموعة من الخطوط المستندة إلى اللاتينية، وتضم نماذج مدربة على عينات من الخط المتصل. تخطي هذه الخطوة غالبًا ما يؤدي إلى مخرجات مشوشة لأن المحرك ي default إلى نموذج النص المطبوع.

### الخطوة 3 – **turn on handwritten mode**

استدعاء `enable_handwritten_mode(True)` يغيّر علامة داخلية. ثم يتحول المحرك إلى شبكته العصبية التي تم ضبطها للتباعد غير المنتظم وعرض الضربات المتغيرة التي تراها في ملاحظات العالم الحقيقي. نسيان هذا السطر خطأ شائع؛ سيتعامل المحرك مع خربشاتك كضوضاء.

### الخطوة 4 – قدم الصورة و**recognize handwritten text**

`recognize_image` يقوم بالعمل الشاق: يسبق معالجة البت ماب، يمرره عبر نموذج الخط اليدوي، ويعيد كائنًا يحتوي على الخاصية `text`. يمكنك أيضًا فحص `handwritten_result.confidence` إذا كنت بحاجة إلى مقياس جودة.

### الخطوة 5 – اطبع النتيجة و**read handwritten notes**

`print(handwritten_result.text)` هو أبسط طريقة للتحقق من أنك نجحت في **extract text from image**. في بيئة الإنتاج ربما تخزن السلسلة في قاعدة بيانات أو تمررها إلى خدمة أخرى.

## معالجة الحالات الحدية والاختلافات الشائعة

| الحالة | ما الذي يجب فعله |
|-----------|------------|
| **الصورة مائلة** | استخدم Pillow لتدوير الصورة (`Image.rotate(angle)`) قبل استدعاء `recognize_image`. |
| **تباين منخفض** | حوّل إلى تدرج الرمادي وطبق العتبة التكيفية (`Image.point(lambda p: p > 128 and 255)`). |
| **صفحات متعددة** | تكرار عبر قائمة مسارات الملفات وربط النتائج. |
| **خطوط غير لاتينية** | استبدل `EXTENDED_LATIN` بـ `ocr.Language.CHINESE` (أو ما يناسب) واحتفظ بـ `enable_handwritten_mode(True)`. |
| **مخاوف الأداء** | أعد استخدام نفس مثيل `ocr_engine` عبر العديد من الصور؛ تهيئته في كل مرة يضيف عبئًا. |

### نصيحة احترافية حول استهلاك الذاكرة

إذا كنت تعالج مئات الملاحظات دفعة واحدة، استدعِ `ocr_engine.dispose()` بعد الانتهاء. يحرّر ذلك الموارد الأصلية التي قد يحتفظ بها غلاف بايثون.

## ملخص بصري سريع

![مثال على التعرف على النص المكتوب بخط اليد](https://example.com/handwritten-note.png "مثال على التعرف على النص المكتوب بخط اليد")

*الصورة أعلاه تُظهر ملاحظة مكتوبة بخط اليد نموذجية يمكن لسكريبتنا تحويلها إلى نص عادي.*

## مثال كامل يعمل (سكريبت ملف واحد)

لمن يحب بساطة النسخ‑اللصق، إليكم كل شيء مرة أخرى دون التعليقات التوضيحية:

```python
import ocr, os

ocr_engine = ocr.OcrEngine()
ocr_engine.set_language(ocr.Language.EXTENDED_LATIN)
ocr_engine.enable_handwritten_mode(True)

img = os.path.join("YOUR_DIRECTORY", "handwritten_note.jpg")
if not os.path.isfile(img):
    raise FileNotFoundError(f"Image not found: {img}")

result = ocr_engine.recognize_image(img)
print("=== Extracted Text ===")
print(result.text)
```

شغّله باستخدام:

```bash
python handwriting_ocr.py
```

يجب الآن أن ترى ناتج **recognize handwritten text** في وحدة التحكم.

## الخلاصة

لقد غطينا الآن كل ما تحتاجه لـ **recognize handwritten text** في بايثون—بدءًا من استدعاء **create OCR engine python** جديد، اختيار اللغة المناسبة، **turn on handwritten mode**، وأخيرًا **extract text from image** إلى **read handwritten notes**.  

في سكريبت واحد مستقل يمكنك الانتقال من صورة ضبابية لرسمة اجتماع إلى نص نظيف قابل للبحث. بعد ذلك، فكر في إمداد الناتج إلى خط أنابيب للغة الطبيعية، تخزينه في فهرس قابل للبحث، أو حتى إعادته إلى خدمة تفريغ لتوليد التعليق الصوتي.

### إلى أين تتجه من هنا؟

- **معالجة دفعات:** غلف السكريبت في حلقة للتعامل مع مجلد من المسحات.  
- **تصفية الثقة:** استخدم `result.confidence` لتجاهل القراءات منخفضة الجودة.  
- **مكتبات بديلة:** إذا لم يكن `ocr` مناسبًا تمامًا، استكشف `pytesseract` مع `--psm 13` لوضع الخط اليدوي.  
- **دمج واجهة المستخدم:** اجمع مع Flask أو FastAPI لتقديم خدمة رفع عبر الويب.  

هل لديك أسئلة حول صيغة صورة معينة أو تحتاج مساعدة في ضبط النموذج؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}