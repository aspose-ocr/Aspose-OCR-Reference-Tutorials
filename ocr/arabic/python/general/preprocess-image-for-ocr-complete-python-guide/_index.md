---
category: general
date: 2026-06-28
description: معالجة مسبقة للصورة لتقنية التعرف الضوئي على الأحرف مع التدوير التلقائي،
  التحويل إلى ثنائي وإزالة الضوضاء باستخدام بايثون. الحصول على مخرجات JSON منظمة باستخدام
  محرك التعرف الضوئي على الأحرف.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: ar
og_description: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف مع التدوير التلقائي،
  والتثنيل، وإزالة الضوضاء في بايثون. تعلم استخراج JSON منظم باستخدام محرك التعرف
  الضوئي على الأحرف.
og_title: معالجة الصورة مسبقًا للتعرف الضوئي على الأحرف – دليل بايثون كامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: معالجة مسبقة للصورة للتعرف الضوئي على الأحرف – دليل بايثون الكامل
url: /ar/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة الصورة قبل OCR – دليل بايثون كامل

هل تساءلت يوماً كيف **تُعالج الصورة قبل OCR** بحيث يقرأ المحرك ما تراه فعلياً؟ لست وحدك—معظم المطورين يواجهون نفس المشكلة عندما تكون المستندات الممسوحة ضبابية. الخبر السار؟ بضع خطوات مُحكمة—التدوير التلقائي، التحويل إلى ثنائي، وإزالة الضوضاء—يمكنها تحويل صورة فوضوية إلى نص نظيف يمكن للآلة قراءته.

في هذا الدرس سنستعرض سير عمل **Python** لا يقتصر فقط على تنظيف الصورة بل يُعيد لك ملف JSON منظم بشكل جميل. بنهاية الدرس ستعرف كيف تُدوّر الصورة تلقائيًا من أجل OCR، وتطبق التحويل إلى ثنائي للـ OCR، وحتى تُزيل الضوضاء من بيانات صورة OCR قبل تمريرها إلى نسخة **OCR engine Python**.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من توفر التالي على جهازك:

- Python 3.9+ (أي نسخة حديثة تعمل)
- `Pillow` لمعالجة الصور (`pip install pillow`)
- `ocrutil` – مكتبة خيالية تُغلف محرك OCR (التثبيت عبر `pip install ocrutil`)
- صورة مائلة تجريبية (`skewed.jpg`) موجودة في مجلد يمكنك الإشارة إليه

هذا كل شيء—بدون أطر عمل ثقيلة، بدون سحر GPU. مجرد بايثون عادي ومكتبتين مفيدتين.

## الخطوة 1: تحميل الصورة – التحضير للـ OCR

أولاً وقبل كل شيء: نحتاج إلى كائن صورة يستطيع بقية الخطوات معالجته.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*لماذا هذا مهم:* تحميل الصورة باستخدام Pillow يضمن الاحتفاظ بجميع بيانات البكسل الأصلية، وهو أمر حاسم عندما نطبق التحويل إلى ثنائي لاحقًا. تخطي هذه الخطوة أو استخدام محمل منخفض الجودة قد يُفسد دقة OCR من البداية.

## الخطوة 2: تدوير الصورة تلقائيًا للـ OCR (auto rotate image OCR)

الصورة الملتقطة بهاتف غالبًا ما تكون مائلة أو مقلوبة. الدالة `ocrutil.auto_rotate` تكتشف خط النص وتدوّر الصورة وفقًا لذلك.

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*نصيحة محترف:* إذا كنت تعلم أن مستنداتك دائمًا في وضعية صحيحة، يمكنك تخطي هذه الخطوة، لكن في الواقع “auto rotate image OCR” يوفر عليك الكثير من التنظيف اليدوي.

## الخطوة 3: معالجة الصورة للـ OCR – ثنائي + إزالة الضوضاء

الآن نصل إلى جوهر الموضوع: **preprocess image for OCR**. أكثر الحيل فعالية هي:

1. **التحويل إلى ثنائي** – تحويل الصورة إلى أبيض وأسود نقي، ما يُحسّن حواف الأحرف.
2. **إزالة الضوضاء** – حذف البقع التي قد يخطئ محرك OCR في اعتبارها أحرفًا.

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

إذا نظرت إلى الصورة بعد هذه الخطوة (مثلاً `img.show()`)، ستلاحظ تباينًا واضحًا مع الخلفية—بالضبط ما يحتاجه محرك OCR الجيد.

## الخطوة 4: إعداد محرك OCR (OCR engine Python)

مع صورة نظيفة في اليد، نقوم بإنشاء كائن محرك OCR. الفئة `ocrutil.OcrEngine` تغلف خلفية OCR مفتوحة المصدر مشهورة (مثل Tesseract) وتوفر واجهة برمجة تطبيقات Python سهلة.

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*لماذا نفعل ذلك:* تمرير الصورة المُعالجة مسبقًا إلى كائن **OCR engine Python** يضمن أن المحرك يعمل بأعلى جودة للبيانات التي يمكنك تقديمها، ما يترجم مباشرة إلى دقة أعلى.

## الخطوة 5: التعرف على النص العادي (اختياري لكن مفيد)

أحيانًا تحتاج فقط إلى النص الخام. هذه الخطوة اختيارية لأن الهدف الأساسي من الدرس هو الحصول على مخرجات مُنظمة، لكنها مفيدة للتحقق السريع.

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

ستظهر لك سلسلة نصية تشبه المستند الأصلي، لكن بدون أي معلومات تخطيطية. إذا كان النص مشوشًا، عد وعدّل معلمات المعالجة المسبقة.

## الخطوة 6: استخراج البيانات المُنظمة وحفظها كـ JSON (OCR structured JSON output)

القوة الحقيقية لمحركات OCR الحديثة هي قدرتها على إرجاع معلومات التخطيط—الجداول، الأعمدة، وحتى حقول النماذج. الدالة `engine.recognize_structured()` تفعل ذلك بالضبط، وسنقوم بتفريغ النتيجة في ملف JSON مرتب.

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

قد يبدو جزء من الـ JSON هكذا:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*ما يقدمه لك هذا:* تمثيل قابل للقراءة آليًا يمكنك إرساله مباشرة إلى قاعدة بيانات، أو API، أو أداة تقارير—بدون الحاجة إلى النسخ واللصق اليدوي.

## إضافي: تأكيد بصري (صورة مع نص بديل)

فيما يلي لقطة قبل وبعد لخط أنابيب المعالجة المسبقة. لاحظ كيف ارتفع التباين واختفت الضوضاء.

![معالجة الصورة للـ OCR – الأصلية مقابل المنقحة](/images/ocr_preprocess_example.png){: .align-center alt="مثال على معالجة الصورة للـ OCR"}

*إذا كنت فضوليًا:* استبدل `ocrutil.preprocess` بإجراء OpenCV الخاص بك وستظل تتبع نفس فلسفة **preprocess image for OCR**—الحدّ، الترشيح، ثم الإرسال.

## الأخطاء الشائعة وكيفية تجنّبها

- **التحويل إلى ثنائي مفرط:** ضبط العتبة عاليًا جدًا قد يمحو الأحرف الخفيفة. إذا لاحظت حروفًا مفقودة، خفّض العتبة في `ocrutil.preprocess`.
- **دقة DPI غير صحيحة:** محركات OCR تفترض ~300 dpi للمستندات المطبوعة. إذا كانت صورتك منخفضة الدقة، فكر في تكبيرها قبل المعالجة.
- **تخطي التدوير التلقائي:** حتى ميل 5 درجات قد يعرقل اكتشاف السطر. خطوة “auto rotate image OCR” رخيصة وتوفر ساعات من التصحيح لاحقًا.

## توسيع سير العمل

الآن بعد أن لديك أساسًا ثابتًا، قد ترغب في:

1. **إضافة حزم لغات** (`engine.set_language('eng+spa')`) للمستندات متعددة اللغات.  
2. **الدمج مع Pandas** لتحويل جداول JSON إلى DataFrames للتحليل.  
3. **معالجة دفعات** عبر حلقة تمر على مجلد من الصور وتضيف النتائج إلى ملف JSON رئيسي.

كل هذه الإضافات لا تزال تعتمد على الفكرة الأساسية: **preprocess image for OCR** قبل استدعاء المحرك.

## الخلاصة

لقد تعلمت الآن كيف **تُعالج الصورة قبل OCR** باستخدام بايثون—تدوير تلقائي، تحويل إلى ثنائي، إزالة الضوضاء، ثم تمرير الصورة النظيفة إلى **OCR engine Python** الذي يُنتج كلًا من النص العادي و**OCR structured JSON output** غني. باتباع هذه الخطوات، ستحسن معدلات التعرف بشكل كبير وستحصل على بيانات جاهزة للمعالجة اللاحقة.

هل أنت مستعد للارتقاء؟ جرّب استبدال `ocrutil.preprocess` بأنابيب OpenCV مخصصة، جرب تقنيات ثنائية مختلفة، أو أدخل الـ JSON في لوحة تقارير. السماء هي الحد، والأساس الذي بنيناه سيمنعك من التعثر مرة أخرى بسبب مشاكل جودة الصورة.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [استخراج النص من صورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من صورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [كيفية ضبط قيمة العتبة في التعرف على صورة OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}