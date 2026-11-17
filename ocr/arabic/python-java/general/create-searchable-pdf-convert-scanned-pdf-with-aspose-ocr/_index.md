---
category: general
date: 2026-03-18
description: إنشاء ملف PDF قابل للبحث من ملفاتك الممسوحة ضوئياً باستخدام Aspose OCR.
  تعلّم كيفية تحويل PDF الممسوح ضوئياً، استخراج النص من PDF، والتعرف على نص PDF بسرعة.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: ar
og_description: إنشاء ملف PDF قابل للبحث على الفور. اتبع هذا الدليل لتحويل PDF الممسوح
  ضوئياً، واستخراج النص من PDF، والتعرف على نص PDF باستخدام Aspose OCR.
og_title: إنشاء ملف PDF قابل للبحث – خطوة بخطوة مع Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: إنشاء ملف PDF قابل للبحث – تحويل PDF الممسوح ضوئياً باستخدام Aspose OCR
url: /ar/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث – دليل خطوة بخطوة  

هل احتجت يومًا إلى **إنشاء ملف PDF قابل للبحث** من مجموعة من الصفحات الممسوحة ضوئيًا لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—فمعظم المطورين يواجهون هذه المشكلة عندما تصل أول عملية مسح إلى الخادم الخاص بهم.  

الخبر السار هو أنه باستخدام Aspose OCR يمكنك **convert scanned pdf** في بضع سطور فقط، **extract text from pdf** للتحقق، وحتى **recognize text pdf** في الوقت الفعلي. في هذا الدرس سنستعرض العملية بالكامل، من تثبيت المكتبة إلى حفظ مستند قابل للبحث بالكامل، وسنضيف بعض النصائح للتعامل مع حالات **convert image pdf** الخاصة.  

## ما ستحققه  

* تحميل ملف PDF ممسوح ضوئيًا (أو PDF يحتوي على صور فقط) إلى Aspose OCR.  
* إخبار المحرك بالصفحات التي يجب معالجتها – مفيد عندما تحتاج فقط إلى جزء منها.  
* إدراج نتائج OCR مرة أخرى في الملف الأصلي بحيث يكون الناتج ملف **searchable PDF** حقيقي.  
* التحقق من العملية بطباعة عدد الصفحات، وإذا رغبت، إظهار النص المستخرج.  

لا توجد خدمات خارجية، ولا سحر مخفي—فقط بايثون خالص وAPI الخاص بـ Aspose.  

## المتطلبات المسبقة  

* Python 3.8 أو أحدث.  
* `aspose-ocr` package – install with `pip install aspose-ocr`.  
* ملف PDF ممسوح ضوئيًا (أو PDF يحتوي على صور فقط).  
* إلمام أساسي ببرمجة بايثون.  

إذا كان لديك هذه المتطلبات بالفعل، عظيم—هيا نبدأ.  

<img src="searchable-pdf-workflow.png" alt="مخطط إنشاء ملف PDF قابل للبحث">  

*(رسم توضيحي لأنابيب OCR – غير مطلوب للكود لكنه يساعد المتعلمين البصريين.)*  

## الخطوة 1 – تهيئة محرك OCR  

أولًا وقبل كل شيء: تحتاج إلى نسخة من `OcrEngine`. فكر فيها كالعقل الذي سيقرأ كل بكسل ويحوّله إلى أحرف Unicode.  

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**لماذا هذا مهم:** بدون المحرك لا يمكنك ضبط الخيارات أو تشغيل التعرف. تهيئته مبكرًا يمنحك أيضًا مكانًا لإرفاق أي قواميس مخصصة لاحقًا.  

## الخطوة 2 – تحميل ملف PDF المصدر  

يمكن لـ Aspose OCR قراءة ملفات PDF مباشرة، مما يعني أنك لا تحتاج إلى تحويل كل صفحة إلى صورة بنفسك. فقط وجه المحرك إلى الملف.  

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*نصيحة احترافية:* إذا كان ملف PDF كبيرًا، فكر في تحميله من تدفق (stream) لتجنب حجز الملف على القرص.  

## الخطوة 3 – تكوين خيارات التعرف على PDF  

هنا يبدأ دور الكلمات المفتاحية الثانوية. يمكنك إخبار المحرك بـ **convert scanned pdf** فقط على صفحات معينة، إدراج النص المعترف به، أو حتى ترك الصور الأصلية دون تعديل.  

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**لماذا هذا مهم:**  
* `setEmbedRecognisedText(True)` هو المفتاح لتحويل PDF النقطي إلى **searchable PDF**.  
* `setPageRange` يساعدك على **convert image pdf** بشكل انتقائي—مفيد للمستندات الكبيرة حيث تحتاج فقط إلى عدد قليل من الصفحات التي يتم التعرف عليها.  
* تمكين استخراج النص يتيح لك لاحقًا **extract text from pdf** دون فتح عارض.  

## الخطوة 4 – إرفاق الخيارات بالمحرك  

الآن اربط الخيارات بالمحرك. من السهل تجاهل هذه الخطوة، لكن تخطيها يعني أن المحرك سيعمل بالإعدادات الافتراضية (بدون نص قابل للبحث).  

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## الخطوة 5 – تشغيل OCR على الصفحات المحددة  

مع ربط كل شيء، يصبح التعرف الفعلي استدعاء طريقة واحدة.  

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

إذا كنت تعالج مستندًا متعدد الميغابايت، قد ترغب في تغليف ذلك داخل كتلة try/except لالتقاط `OcrException` وتسجيل الصفحة التي حدثت فيها المشكلة.  

## الخطوة 6 – التحقق من النتيجة  

فحص سريع للتحقق هو طباعة عدد الصفحات التي يعتقد المحرك أنه عالجها. يمكنك أيضًا سحب النص الخام إذا كنت بحاجة إلى **extract text from pdf** لمزيد من التحليل.  

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**لماذا يهمك:** رؤية عدد الصفحات يؤكد أن `setPageRange` عمل، ومقتطف النص المستخرج يثبت أن OCR فعلاً تعرف على الأحرف.  

## الخطوة 7 – حفظ ملف PDF القابل للبحث  

أخيرًا، اكتب الناتج مرة أخرى إلى القرص. الثابت `ImageFormats.PDF` يخبر Aspose بالحفاظ على الملف كـ PDF، الآن مع نص قابل للبحث.  

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

افتح الملف الناتج في أي قارئ PDF وجرب البحث عن نص—ها قد **أنشأت searchable pdf**!  

## التعامل مع الحالات الخاصة الشائعة  

### عندما يكون المصدر PDF يحتوي على *صور فقط*  

إذا كان PDF الإدخال يحتوي فقط على صور (بدون طبقة نص)، فإن نفس الكود يعمل—فقط تأكد من أن `setEmbedRecognisedText(True)` ما زال مفعلاً. قد ترغب أيضًا في زيادة DPI للحصول على دقة أفضل:  

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### التعامل مع لغات متعددة  

يدعم Aspose OCR حزم اللغات. حمّل لغة قبل استدعاء `recognize()`:  

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### مستندات كبيرة  

معالجة PDF ممسوح مكوّن من 500 صفحة قد يستهلك الكثير من الذاكرة. قسّم المهمة:

1. تكرار على نطاقات الصفحات (`setPageRange(start, end)`).  
2. حفظ كل جزء كملف PDF قابل للبحث مؤقت.  
3. دمج الأجزاء باستخدام `PdfMerger` (مكوّن Aspose آخر).  

## مثال كامل يعمل (جميع الخطوات معًا)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

تشغيل هذا السكريبت سيعطيك **searchable PDF** يمكنك فتحه في Adobe Reader أو Chrome أو أي قارئ PDF والبحث عن الكلمات فورًا.  

## الخلاصة  

أنت الآن تمتلك حلًا كاملاً من البداية إلى النهاية لإنشاء ملفات **create searchable PDF** باستخدام Aspose OCR. من تحميل المصدر، تكوين الخيارات التي **convert scanned pdf**، استخراج النص والتحقق منه، وحتى حفظ النتيجة القابلة للبحث، كل خطوة مغطاة.  

بعد ذلك، قد ترغب في استكشاف سيناريوهات **convert image pdf** حيث يكون المصدر سلسلة من ملفات JPEG مدمجة في PDF، أو الغوص أعمق في OCR الخاص باللغات لتحسين الدقة في المستندات متعددة اللغات. في كل الأحوال، يبقى النمط نفسه: ضبط الخيارات، تشغيل `recognize()`، ثم الحفظ.  

لا تتردد في التجربة—غيّر نطاق الصفحات، عدّل DPI، أو أدخل قاموسًا مخصصًا. إذا واجهت أي مشاكل، اترك تعليقًا أدناه أو راجع الوثائق الرسمية لـ Aspose للحصول على أحدث تفاصيل الـ API. OCR سعيد  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}