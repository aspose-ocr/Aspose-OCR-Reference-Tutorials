---
category: general
date: 2026-05-31
description: إنشاء ملف PDF قابل للبحث من الصور الممسوحة ضوئياً باستخدام Python OCR.
  تعلم كيفية تحويل PDF من صورة ممسوحة ضوئياً، وتحويل TIFF إلى PDF، وإضافة طبقة نص
  OCR في دقائق.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: ar
og_description: إنشاء ملف PDF قابل للبحث على الفور. يوضح هذا الدليل كيفية تشغيل OCR،
  تحويل ملف PDF الممسوح ضوئياً، وإضافة طبقة نص OCR باستخدام سكريبت بايثون واحد.
og_title: إنشاء ملف PDF قابل للبحث باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: إنشاء ملف PDF قابل للبحث باستخدام بايثون – دليل خطوة بخطوة
url: /ar/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء PDF قابل للبحث باستخدام بايثون – دليل خطوة بخطوة

هل تساءلت يومًا كيف تُنشئ **PDF قابل للبحث** من صفحة ممسوحة ضوئيًا دون الحاجة إلى التعامل مع عشرات الأدوات؟ لست وحدك. في العديد من سير عمل المكاتب، يتم وضع ملف TIFF أو JPEG ممسوح على محرك مشاركة، ويتعين على الشخص التالي نسخ‑لصق النص يدويًا—مما يسبب الألم، الأخطاء، وإضاعة الوقت.  

في هذا الدرس سنستعرض حلًا برمجيًا نظيفًا يتيح لك **تحويل PDF صورة ممسوحة**، **تحويل TIFF إلى PDF**، و**إضافة طبقة نص OCR** في خطوة واحدة. بنهاية الدرس ستحصل على سكربت جاهز للاستخدام يقوم بتشغيل OCR، يدمج النص المخفي، ويُنتج PDF قابل للبحث يمكنك فهرسته، البحث فيه، أو مشاركته بثقة.

## ما ستحتاجه

- Python 3.9+ (أي نسخة حديثة تعمل)
- حزم `aspose-ocr` و `aspose-pdf` (تثبيتها عبر `pip install aspose-ocr aspose-pdf`)
- ملف صورة ممسوحة (`.tif`, `.png`, `.jpg`, أو حتى صفحة PDF تحتوي على صورة فقط)
- كمية معتدلة من الذاكرة RAM (محرك OCR خفيف؛ حتى اللاب توب يتعامل معه)

> **نصيحة احترافية:** إذا كنت تستخدم Windows، أسهل طريقة للحصول على الحزم هي تشغيل الأمر في نافذة PowerShell مرتفعة الصلاحيات.

```bash
pip install aspose-ocr aspose-pdf
```

الآن بعد أن انتهينا من المتطلبات المسبقة، دعنا نغوص في الكود.

## الخطوة 1: إنشاء مثيل محرك OCR – *create searchable pdf*

أول شيء نفعله هو تشغيل محرك OCR. فكر فيه كالعقل الذي سيقرأ كل بكسل ويحوّله إلى أحرف.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **لماذا هذا مهم:** تهيئة المحرك مرة واحدة فقط يحافظ على انخفاض استهلاك الذاكرة. إذا قمت باستدعاء `OcrEngine()` داخل حلقة لكل صفحة، ستنفد الموارد سريعًا.

## الخطوة 2: تحميل الصورة الممسوحة – *convert tiff to pdf* & *convert scanned image pdf*

بعد ذلك، وجه المحرك إلى الملف الذي تريد معالجته. الـ API يقبل أي صورة نقطية، لذا فإن TIFF يعمل بنفس كفاءة JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

إذا كان لديك ملف PDF يحتوي فقط على صورة ممسوحة، يمكنك ما زال استخدام `load_image` لأن Aspose سيستخرج الصفحة الأولى تلقائيًا.

## الخطوة 3: إعداد خيارات حفظ PDF – *add OCR text layer*

هنا نقوم بتكوين شكل الـ PDF النهائي. العلامة الحاسمة هي `create_searchable_pdf`؛ ضبطها على `True` يخبر المكتبة بدمج طبقة نص غير مرئية تعكس المحتوى البصري.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **ما تفعله طبقة النص:** عندما تفتح الملف الناتج في Adobe Reader وتحاول تحديد النص، ستظهر الأحرف المخفية. محركات البحث يمكنها أيضًا فهرستها—مثالي للامتثال أو الأرشفة.

## الخطوة 4: تشغيل OCR والحفظ – *how to run OCR* في استدعاء واحد

الآن يحدث السحر. استدعاء طريقة واحدة يشغّل محرك التعرف ويكتب PDF القابل للبحث على القرص.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

طريقة `recognize` تُعيد كائن حالة يمكنك فحصه للبحث عن أخطاء، لكن في معظم السيناريوهات البسيطة يكون الاستدعاء أعلاه كافيًا.

### النتيجة المتوقعة

تشغيل السكربت يطبع:

```
PDF saved as searchable PDF.
```

إذا فتحت `scanned_page_searchable.pdf` ستلاحظ أنك تستطيع تحديد النص، نسخه‑لصقه، وحتى إجراء بحث `Ctrl+F`. هذا هو ما يميز سير عمل **create searchable pdf**.

## السكربت الكامل القابل للتشغيل

فيما يلي السكربت الكامل الجاهز للتنفيذ. فقط استبدل مسارات العناصر النائبة بمواقع ملفاتك الفعلية.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

احفظه باسم `create_searchable_pdf.py` ثم نفّذه:

```bash
python create_searchable_pdf.py
```

## أسئلة شائعة وحالات خاصة

### 1️⃣ هل يمكنني معالجة ملفات PDF متعددة الصفحات؟

نعم. استخدم `ocr_engine.load_image("file.pdf")` ثم كرّر عبر كل صفحة باستخدام `ocr_engine.recognize(pdf_save_options, page_number)`. المكتبة ستولد PDF قابل للبحث متعدد الصفحات تلقائيًا.

### 2️⃣ ماذا لو كان ملف المصدر TIFF عالي الدقة (300 dpi+)؟

كلما ارتفعت DPI زادت دقة OCR لكن استهلاك الذاكرة يصبح أكبر. إذا واجهت `MemoryError`، قلل حجم الصورة أولًا:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ كيف أغيّر لغة OCR؟

عيّن خاصية `language` على المحرك قبل تحميل الصورة:

```python
ocr_engine.language = "fra"   # French
```

قائمة كاملة بأكواد اللغات المدعومة موجودة في وثائق Aspose.

### 4️⃣ ماذا لو أردت الحفاظ على جودة الصورة الأصلية؟

فئة `PdfSaveOptions` تحتوي على خاصية `compression`. اضبطها على `PdfCompression.None` للحفاظ على بيانات الصورة النقطية كما هي تمامًا.

```python
pdf_save_options.compression = "None"
```

## نصائح للنشر في بيئات الإنتاج

- **معالجة دفعات:** غلف المنطق الأساسي في دالة تستقبل قائمة مسارات ملفات. سجّل كل نجاح/فشل في ملف CSV لتتبع التدقيق.
- **التوازي:** استخدم `concurrent.futures.ThreadPoolExecutor` لتشغيل OCR على عدة نوى. فقط تذكّر أن كل خيط يحتاج إلى مثيل `OcrEngine` خاص به.
- **الأمان:** إذا كنت تتعامل مع مستندات حساسة، شغّل السكربت في بيئة معزولة واحذف الملفات المؤقتة فور الانتهاء من المعالجة.

## الخلاصة

أنت الآن تعرف كيف **تنشئ ملفات PDF قابلة للبحث** من صور ممسوحة باستخدام سكربت بايثون مختصر. من خلال تهيئة محرك OCR، تحميل TIFF (أو أي صورة نقطية)، تكوين `PdfSaveOptions` لإ **add OCR text layer**، وأخيرًا استدعاء `recognize`، يصبح خط أنابيب **convert scanned image pdf** و **convert TIFF to PDF** أمرًا واحدًا قابلًا للتكرار.

ما الخطوات التالية؟ جرّب ربط هذا السكربت بمراقب ملفات بحيث أي مسح جديد يُسقط في مجلد يتحول تلقائيًا إلى PDF قابل للبحث. أو جرب لغات OCR مختلفة لدعم أرشيفات متعددة اللغات. السماء هي الحد عندما تجمع بين OCR وإنشاء PDF.

هل لديك أسئلة إضافية حول **how to run OCR** بلغات أو أطر أخرى؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة! 

![مخطط يوضح التدفق من الصورة الممسوحة → محرك OCR → PDF قابل للبحث (create searchable pdf)](searchable-pdf-flow.png "مخطط تدفق إنشاء PDF قابل للبحث")

## ماذا يجب أن تتعلم بعد ذلك؟

- [كيفية التعرف الضوئي على النص في PDF باستخدام .NET مع Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [كيفية التعرف الضوئي على نص الصورة مع اللغة باستخدام Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}