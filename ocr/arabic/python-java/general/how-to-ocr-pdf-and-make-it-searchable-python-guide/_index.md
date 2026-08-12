---
category: general
date: 2026-01-12
description: تعلم كيفية إجراء التعرف الضوئي على الحروف (OCR) لملفات PDF باستخدام بايثون
  وجعل ملفات PDF قابلة للبحث بسرعة. تحويل ملفات PDF الممسوحة ضوئياً، استخراج نص PDF،
  واستخدام OCR لملفات PDF الممسوحة ضوئياً في بايثون باستخدام Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: ar
og_description: كيفية التعرف الضوئي على النص في ملفات PDF باستخدام بايثون؟ يوضح لك
  هذا الدليل خطوة بخطوة كيفية تحويل ملفات PDF الممسوحة ضوئياً إلى ملفات PDF قابلة
  للبحث واستخراج النص باستخدام Aspose OCR.
og_title: كيفية تحويل PDF إلى نص قابل للبحث باستخدام OCR – دليل بايثون
tags:
- OCR
- Python
- PDF processing
title: كيفية تحويل PDF إلى نص قابل للبحث باستخدام OCR – دليل بايثون
url: /ar/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تحويل PDF إلى نص قابل للبحث باستخدام OCR – دليل بايثون

هل تساءلت يومًا **كيفية تحويل PDF إلى نص باستخدام OCR** دون إنفاق ثروة على برامج تجارية؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى تحويل عقد ممسوح ضوئيًا، أو فاتورة، أو أي PDF يعتمد على الصور إلى مستند قابل للبحث. الخبر السار؟ ببضع أسطر من بايثون و Aspose OCR يمكنك تحويل PDF الممسوح ضوئيًا، استخراج نص PDF، وأخيرًا جعل PDF قابلًا للبحث في دقائق.

في هذا الدرس سنستعرض كل ما تحتاجه: من تثبيت المكتبة، ضبط اللغة، معالجة PDF ممسوح ضوئيًا، إلى حفظ النتيجة كملف PDF قابل للبحث يحتوي على الصورة الأصلية وطبقة نص مخفية. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع—بدون الحاجة إلى النسخ واللصق يدويًا.

---

## ما ستحتاجه

- **Python 3.8+** (الكود يعمل على 3.9، 3.10، والإصدارات الأحدث)
- رخصة **Aspose OCR for Python** سارية (إصدار تجريبي مجاني للتجربة)
- ملف PDF ممسوح ضوئيًا (مثال: `scanned_contract.pdf`) تريد جعله قابلًا للبحث
- إلمام أساسي بسطر الأوامر والبيئات الافتراضية (اختياري لكن يُنصح به)

> **نصيحة احترافية:** إذا لم تكن لديك رخصة بعد، سجّل للحصول على تجربة مجانية لمدة 30 يومًا على موقع Aspose؛ النسخة التجريبية تعمل بكامل الوظائف لأغراض التطوير.

---

## كيفية تحويل PDF إلى نص باستخدام Aspose OCR (الكلمة المفتاحية الأساسية في H2)

الخطوة الأولى هي الحصول على الحزمة المناسبة. توفر Aspose OCR واجهة برمجة تطبيقات عالية المستوى تُبسط تفاصيل معالجة الصور منخفضة المستوى.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

بعد تثبيت الحزمة، يمكنك البدء بكتابة السكريبت.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **لماذا ضبط اللغة؟**  
> تعتمد دقة OCR بشكل كبير على نموذج اللغة. من خلال إخبار المحرك صراحةً أنه يتوقع نصًا إنجليزيًا، تقلل الإيجابيات الكاذبة وتسرّع عملية المعالجة.

---

## الخطوة 2: تحويل PDF الممسوح ضوئيًا إلى PDF قابل للبحث

الآن بعد أن أصبح المحرك جاهزًا، وجهه إلى المستند الممسوح. تُعيد طريقة `process_pdf` كائنًا من نوع `PdfResult` يحتوي على بيانات الصورة الأصلية والنص المُعترف به.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

إذا كنت بحاجة إلى **تحويل ملفات PDF ممسوحة ضوئيًا** دفعة واحدة، ما عليك سوى تكرار العملية على مجلد واستدعاء `process_pdf` لكل ملف. يتعامل المحرك مع ملفات PDF متعددة الصفحات مباشرةً.

---

## الخطوة 3: حفظ النتيجة كملف PDF قابل للبحث (Make PDF Searchable)

القطعة الأخيرة من اللغز هي حفظ النسخة القابلة للبحث. تجعل Aspose OCR ذلك سطرًا واحدًا:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

عند فتح `contract_searchable.pdf` في أي عارض PDF، سترى الصورة الممسوحة الأصلية، لكن الآن يمكنك **البحث عن أي كلمة** تعرفها محرك OCR. طبقة النص المخفية غير مرئية للعين لكنها قابلة للفهرسة بالكامل.

---

### السكريبت الكامل – جاهز للتنفيذ

فيما يلي المثال الكامل القابل للتنفيذ. انسخه والصقه في ملف باسم `make_searchable.py` وعدّل المسارات لتتناسب مع بيئتك.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**الناتج المتوقع:**  
عند تشغيل السكريبت سيطبع سطر تأكيد وينشئ `contract_searchable.pdf`. افتح الملف، اضغط `Ctrl + F`، واكتب أي كلمة تظهر في الصورة الممسوحة الأصلية—ستظهر النتائج فورًا.

---

## أسئلة شائعة وحالات خاصة

### 1. ماذا لو كان PDF يحتوي على لغات متعددة؟

يمكنك تمرير قائمة باللغات إلى المحرك:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

ستحاول Aspose OCR التعرف على النص في كلتا اللغتين على نفس الصفحة.

### 2. كيف أتعامل مع المسحات منخفضة الدقة؟

إذا كانت الصور المصدر أقل من 150 dpi، قد تتأثر دقة OCR. قم بمعالجة PDF مسبقًا باستخدام أداة مثل `pdfimages` لاستخراج الصفحات، ثم قم بزيادة الدقة باستخدام Pillow، وأعد تغذية الصور ذات الدقة الأعلى إلى `process_pdf`.

### 3. هل يمكن استخراج النص العادي دون إنشاء PDF قابل للبحث؟

بالطبع. يُظهر كائن `PdfResult` خاصية `text`:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

هذا يلبي حالة الاستخدام **استخراج نص PDF** عندما تحتاج فقط إلى الأحرف الخام.

### 4. هل هناك طريقة لمعالجة مجموعة من ملفات PDF دفعة واحدة؟

نعم—غلف دالة `ocr_to_searchable` في حلقة بسيطة:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

الآن يمكنك **تحويل ملفات PDF ممسوحة ضوئيًا** جماعيًا بأمر واحد.

---

## نصائح للأداء

- **إعادة استخدام المحرك**: إنشاء كائن `OcrEngine` جديد لكل ملف يضيف عبئًا. أنشئه مرة واحدة وأعد استخدامه عبر عدة استدعاءات.
- **المعالجة المتوازية**: للدفعات الكبيرة، استخدم `concurrent.futures.ThreadPoolExecutor` في بايثون—Aspose OCR آمن للقراءة المتعددة الخيوط.
- **إدارة الذاكرة**: إذا كنت تعالج PDF كبيرًا جدًا (مئات الصفحات)، استدعِ `gc.collect()` بعد كل ملف لتحرير الذاكرة.

---

## الخلاصة

غطينا **كيفية تحويل PDF إلى نص باستخدام OCR** في بايثون، وحولنا تلك المسحات إلى **PDFات قابلة للبحث**، وأظهرنا لك أيضًا كيفية **استخراج نص PDF** مباشرة. مع Aspose OCR تحصل على محرك موثوق يدعم المستندات متعددة الصفحات، اللغات المتعددة، وتعرف عالي الدقة—كل ذلك ببضع أسطر من الكود فقط.

جرّبه على عقودك، فواتيرك، أو أوراق البحث المؤرشفة. بمجرد إتقان الأساسيات، استكشف الميزات المتقدمة—مثل القواميس المخصصة، معالجة الصور المسبقة، أو دمج النتيجة في فهرس بحث نص كامل مثل Elasticsearch.

هل لديك المزيد من الأسئلة حول **ocr scanned pdf python** أو تحتاج مساعدة في حل مشكلة مسح صعبة؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

--- 

![how to ocr pdf example](image-placeholder.png){alt="مثال على كيفية OCR PDF"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}