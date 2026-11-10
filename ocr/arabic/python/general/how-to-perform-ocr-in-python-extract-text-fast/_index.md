---
category: general
date: 2026-03-26
description: تعلم كيفية إجراء OCR في بايثون واستخراج النص بسهولة من الصورة، قراءة
  النص من الماسح، أو استخراج النص من الفاتورة باستخدام OcrEngine بسيط.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: ar
og_description: كيف تقوم بتنفيذ التعرف الضوئي على الأحرف (OCR) في بايثون؟ يوضح لك
  هذا الدليل كيفية استخراج النص من الصورة، قراءة النص من المسح الضوئي، واستخراج النص
  من الفاتورة في دقائق.
og_title: كيفية تنفيذ OCR في بايثون – استخراج النص بسرعة
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ OCR في بايثون – استخراج النص بسرعة
url: /ar/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في بايثون – استخراج النص بسرعة

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على إيصال ممسوح أو ملف PDF غير واضح؟ أنت لست وحدك. في العديد من المشاريع تظهر الحاجة إلى **استخراج النص من صورة** في وقت مبكر، والطريقة التقليدية “الكتابة يدويًا كل شيء” ليست قابلة للتوسع.  

في هذا الدرس ستشاهد مثالًا كاملًا وجاهزًا للتنفيذ يوضح **كيفية استخدام OCR** لقراءة النص من مسح ضوئي، سحب البيانات من فاتورة، وحتى التعامل مع تصحيح الميل التلقائي — كل ذلك ببضع أسطر فقط من بايثون.

## ما ستتعلمه

سنستعرض كل ما تحتاج إلى معرفته:

* الاعتمادات والاستيرادات الدقيقة المطلوبة.
* كيفية إنشاء وتكوين كائن `OcrEngine`.
* طرق **استخراج النص من صورة**، **قراءة النص من مسح ضوئي**، و**استخراج النص من فاتورة** باستخدام نفس المحرك.
* الأخطاء الشائعة (اللغة الخاطئة، الملفات المفقودة، الصور الكبيرة) وكيفية تجنبها.
* النتيجة المتوقعة لتتمكن من التحقق من نجاح OCR.

لا توجد حاجة إلى روابط وثائق خارجية — كل شيء متكامل، يمكنك نسخ‑لصق الكود ورؤية النتائج فورًا.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* تثبيت Python 3.8+ (حزمة `ocr` تعمل مع أي نسخة حديثة).
* توفر مكتبة `ocr` (`pip install ocr‑engine` – استبدل باسم الحزمة الفعلي إذا كان مختلفًا).
* ملف صورة تريد معالجته – في المثال سنستخدم `invoice.png` الموجود في مجلد يسمى `YOUR_DIRECTORY`.

هذا كل ما تحتاجه. إذا كان لديك هذه المتطلبات، فأنت جاهز للبدء.

## الخطوة 1: تثبيت واستيراد وحدة OCR

أولًا: نحتاج إلى مكتبة OCR. إذا لم تقم بتثبيتها بعد، نفّذ الأمر التالي في الطرفية:

```bash
pip install ocr-engine
```

الآن نستورد الوحدة في السكريبت الخاص بنا.

```python
# Step 1: Import the OCR module
import ocr
```

> **نصيحة احترافية:** حافظ على بيئة افتراضية نظيفة؛ فهذا يمنع تعارض الإصدارات عندما تضيف حزم معالجة صور أخرى لاحقًا.

## الخطوة 2: إنشاء وتكوين محرك OCR

إنشاء المحرك سهل كاستدعاء المُنشئ، لكن القوة الحقيقية تكمن في تكوينه بشكل صحيح. سنضبط اللغة إلى الإنجليزية ونفعل تصحيح الميل التلقائي، وهو أمر أساسي عند التعامل مع فواتير ممسوحة ليست محاذاة تمامًا.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

لماذا نفعّل `auto_skew`؟ كثير من الماسحات تنتج صورًا بزاوية قليلة. بدون التصحيح قد يفوت المحرك بعض الأحرف، محولًا فاتورة قابلة للقراءة إلى نص غير مفهوم.

## الخطوة 3: تنفيذ OCR على الصورة المستهدفة

الآن نمرّر ملف الصورة إلى المحرك. طريقة `recognize_image` تُعيد كائنًا يحتوي على النص الخام بالإضافة إلى درجات الثقة (إذا كانت المكتبة توفرها).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

إذا كنت تعمل في سيناريو **قراءة النص من مسح ضوئي**، ما عليك سوى استبدال المسار بملف PDF ممسوح تم تحويله إلى PNG أو JPEG. نفس الاستدعاء يعمل مع أي صيغة صورة تدعمها المكتبة الأساسية.

## الخطوة 4: فحص واستخدام النص المستخرج

لنطبع ناتج OCR الخام. في خط أنابيب معالجة الفواتير الواقعي ربما تقوم بتحليل هذه السلسلة، استخراج البنود، الإجماليات، والتواريخ، لكن الآن نظرة سريعة ستؤكد نجاح OCR.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**الناتج المتوقع (مقتطع للت brevity):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

إذا كان الناتج مشوشًا، تحقق من وضوح الصورة وأن `engine.language` يطابق لغة المستند.

## الخطوة 5: التعامل مع الحالات الشائعة

### الصور الكبيرة

معالجة مسح بدقة 5000 × 5000 بكسل قد تستهلك الكثير من الذاكرة. طريقة سريعة للتخفيف هي تقليل حجم الصورة قبل إرسالها إلى المحرك:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### لغات متعددة

إذا احتجت إلى **استخراج النص من صورة** تحتوي على الإنجليزية والإسبانية معًا، يمكنك ضبط قائمة باللغات:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

سيحاول المحرك التعرف على الأحرف من كلا المجموعتين.

### معالجة الأخطاء

لا تفترض وجود الملف دائمًا. احطِ الاستدعاء بكتلة `try‑except` لتقديم رسالة ودية:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## مرجع بصري

فيما يلي لقطة شاشة للفاتورة النموذجية التي استخدمناها في العرض. لاحظ الميل الطفيف — وهو ما يُصححه `auto_skew`.

![how to perform OCR on an invoice](/images/ocr-example.png)

*النص البديل:* كيفية تنفيذ OCR على صورة فاتورة تُظهر تصحيح الميل التلقائي.

## مثال كامل قابل للتنفيذ

بدمج كل ما سبق، إليك سكريبت واحد يمكنك تشغيله من سطر الأوامر. يغطي التثبيت، التكوين، معالجة الأخطاء، وخطوة ما بعد المعالجة البسيطة التي تكتب النص المستخرج إلى ملف باسم `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

تشغيل `python full_ocr_demo.py` سيطبع النص المستخرج على الشاشة ويخزنه في `output.txt`. من هناك يمكنك تطبيق تعبيرات عادية، كُتاب CSV، أو أي منطق آخر تحتاجه لأتمتة **استخراج النص من فاتورة**.

## الخلاصة

أصبح لديك الآن حل شامل من البداية إلى النهاية لـ **كيفية تنفيذ OCR** في بايثون. بإنشاء `OcrEngine`، ضبط اللغة وتصحيح الميل، ومعالجة بعض الحالات العملية، يمكنك بثقة **استخراج النص من صورة**، **قراءة النص من مسح ضوئي**، و**استخراج النص من فاتورة** دون الحاجة للبحث في وثائق متفرقة.

ما الخطوة التالية؟ جرّب معالجة مجموعة من الملفات داخل حلقة، جرب لغات مختلفة، أو اربط الناتج بمكتبة إنشاء PDF لإنشاء ملفات PDF قابلة للبحث. السماء هي الحد، والكود الذي رأيته للتو هو منصة انطلاق قوية.

هل لديك أسئلة حول صيغة ملف معينة أو تحتاج مساعدة في ضبط عتبات الثقة؟ اترك تعليقًا أدناه — سعيد بمساعدتك على تحسين خط أنابيب OCR الخاص بك!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}