---
category: general
date: 2026-06-06
description: كيفية التعرف الضوئي على النص في PDF باستخدام Aspose OCR Cloud. تعلم استخراج
  النص من PDF، تحويل صفحة PDF إلى PNG، وحفظ صور صفحات PDF باستخدام Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: ar
og_description: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose OCR Cloud.
  يوضح هذا الدليل كيفية استخراج النص العادي من PDF، وتحويل صفحة PDF إلى PNG، وحفظ
  صور صفحات PDF.
og_title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose OCR Cloud – خطوة
  بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام Aspose OCR Cloud – دليل
  كامل
url: /ar/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية OCR PDF باستخدام Aspose OCR Cloud – دليل كامل

هل تساءلت يومًا **how to OCR PDF** ملفات دون التعامل مع أدوات سطح مكتب ثقيلة؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحتاجون إلى طريقة سريعة برمجية لاستخراج النص من المستندات الممسوحة ضوئيًا. الخبر السار؟ مع Aspose OCR Cloud يمكنك **extract text from PDF**، تحويل كل صفحة إلى PNG، وحتى **save PDF page images** للاستخدام لاحقًا، كل ذلك من خلال سكريبت Python مرتب.

في هذا الدرس سنستعرض كل ما تحتاج معرفته: من تثبيت الـ SDK، ترخيص المحرك، والتعرف على ملفات PDF متعددة الصفحات، إلى استخراج النص العادي، تحويل الصفحات إلى PNG، وحفظ تلك الصور على القرص. في النهاية ستحصل على قطعة شفرة قابلة لإعادة الاستخدام يمكنك إدراجها في أي مشروع يحتاج إلى قدرات **how to OCR PDF**.

## ما ستحتاجه

- **Python 3.8+** (الكود يعمل على 3.10 وما بعده أيضًا)  
- حساب Aspose OCR Cloud – ستحصل على ملف ترخيص تجريبي مجاني (`Aspose.OCR.lic`)  
- حزمة `asposeocrcloud` (`pip install asposeocrcloud`)  
- ملف PDF ممسوح ضوئيًا متعدد الصفحات تريد معالجته  

هذا كل شيء. لا ملفات تنفيذية إضافية، لا تبعيات أصلية، فقط Python نقي.

## كيفية OCR PDF – الإعداد والترخيص

قبل أن تتمكن من استدعاء أي طرق OCR، عليك إبلاغ الـ SDK بهويتك. تستخدم Aspose ملف ترخيص خفيف الوزن تضعه في مكان يمكن للسكريبت الوصول إليه.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*نصيحة احترافية:* إذا تخطيت خطوة الترخيص، سيستمر الـ SDK في العمل لكنه سيضيف علامة مائية صغيرة إلى الصور الناتجة. وهذا ليس مثالياً للإنتاج.

## الخطوة 2: تثبيت Aspose OCR Cloud Python SDK

افتح الطرفية وشغّل:

```bash
pip install asposeocrcloud
```

تجلب الحزمة جميع الاعتمادات المطلوبة (requests, pillow، إلخ) لذا لا تحتاج للبحث عن أي شيء آخر.

## الخطوة 3: إنشاء محرك OCR واختيار لغة

المحرك هو قلب العملية. يمكنك تحديد أي لغة تدعمها Aspose؛ الإنجليزية تعمل في معظم الحالات.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

لماذا نحدد اللغة؟ لأن محرك OCR يستخدم قواميس خاصة باللغة لتحسين الدقة. إذا كنت تعالج ملفات PDF بالفرنسية، استبدل `ENGLISH` بـ `FRENCH`.

## الخطوة 4: الإشارة إلى ملف PDF متعدد الصفحات

امنح المحرك المسار الكامل للملف الذي تريد معالجته. المسارات النسبية مقبولة طالما أنها تُحل من دليل عمل السكريبت.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

تأكد من أن الملف قابل للقراءة؛ وإلا ستظهر لك رسالة `FileNotFoundError`.

## الخطوة 5: تشغيل OCR – ستحصل على قائمة بالنتائج

استدعاء `recognize_pdf` يُعيد قائمة حيث كل عنصر يمثل صفحة واحدة من ملف PDF الأصلي.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

كل `OcrResult` يحتوي على خاصيتين مفيدتين:

* `text` – تمثيل النص العادي للصفحة (مفيد لـ **extract plain text pdf**)
* `image` – كائن Pillow `Image` للصفحة المُرَسَمة (مثالي لـ **convert pdf page png**)

## الخطوة 6: استخراج النص من PDF وتحويل الصفحات إلى PNG

الآن نقوم بالتكرار عبر النتائج، طباعة النص المستخرج، وحفظ نسخة PNG لكل صفحة.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### مخرجات وحدة التحكم المتوقعة

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

ستجد أيضًا `page_1.png`، `page_2.png`، … في `YOUR_DIRECTORY`. هذه هي صور الصفحات المرسومة التي يمكنك تمريرها إلى خطوط معالجة الصور اللاحقة.

## الخطوة 7: حفظ صور صفحات PDF (معالجة لاحقة اختيارية)

إذا كنت تحتاج فقط إلى الصور دون النص، يمكنك تخطي سطر `print(res.text)`. وعلى العكس، إذا أردت تخزين النص في ملفات `.txt` منفصلة، فقط أضف عملية كتابة صغيرة:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

هذه الإضافة الصغيرة توضح مدى سهولة **save PDF page images** مع حفظ المحتوى المستخرج.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك السكريبت الكامل الذي يمكنك نسخه ولصقه في `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

شغّله باستخدام:

```bash
python ocr_pdf.py
```

يجب أن ترى طباعة النص لكل صفحة في وحدة التحكم وسلسلة من ملفات PNG

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية OCR PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [التعرف على نص PDF – عمليات OCR مع Aspose.OCR للـ Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}