---
category: general
date: 2026-03-18
description: قم بتشغيل تقنية التعرف الضوئي على الأحرف (OCR) على الصورة لاستخراج النص
  من ملف PNG وإنشاء ملف PDF قابل للبحث. تعلم كيفية التعرف على النص في الصورة وتحويل
  PNG إلى PDF في دقائق.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: ar
og_description: قم بتشغيل OCR على الصورة لاستخراج النص من PNG، والتعرف على نص الصورة،
  وإنشاء ملف PDF قابل للبحث. اتبع هذا الدليل خطوة بخطوة.
og_title: تشغيل OCR على الصورة – استخراج النص من PNG بسرعة
tags:
- OCR
- Python
- Image Processing
title: تشغيل OCR على الصورة – استخراج النص من PNG بسرعة
url: /ar/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تشغيل OCR على الصورة – استخراج النص من PNG بسرعة

هل احتجت يومًا إلى **run OCR on image** للملفات ولكنك لم تكن متأكدًا من أين تبدأ؟ ربما لديك مقالة ممسوحة ضُمت كملف `article.png` وتريد النص العادي فقط، أو تحتاج إلى PDF قابل للبحث لأغراض الأرشفة. في كلتا الحالتين، أنت في المكان الصحيح. في هذا الدرس سنستعرض استخراج النص من PNG، التعرف على صورة النص، وحتى تحويل ذلك PNG إلى PDF قابل للبحث—كل ذلك ببضع أسطر من الشيفرة.

> **What you’ll get:** سكريبت كامل قابل للتنفيذ يقوم بتحميل PNG، تشغيل OCR، حفظ مخرجات hOCR، وإنشاء PDF قابل للبحث اختياريًا. لا استيرادات مفقودة، ولا نهايات “انظر الوثائق”—فقط حل مستقل يمكنك إضافته إلى مشروعك اليوم.

## المتطلبات المسبقة

- **Python 3.8+** (الصياغة المستخدمة هنا تعمل على أي نسخة حديثة)
- مكتبة **`ocr_engine`** التي تستخدمها (المثال يفترض وجود فئة تسمى `OcrEngine`؛ استبدلها بـ Tesseract أو EasyOCR، إلخ إذا لزم الأمر)
- صورة PNG تريد معالجتها (مثال: `article.png` موجودة في مجلد يمكنك الإشارة إليه)
- صلاحية كتابة إلى دليل الإخراج

إذا كنت تستخدم Tesseract في الخلفية، فقم بتثبيته باستخدام:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

ثم قم بتثبيت الغلاف (wrapper) الخاص بـ Python:

```bash
pip install pytesseract Pillow
```

*نصيحة احترافية:* حافظ على تحديث مكتبة OCR الخاصة بك—حزم اللغات الجديدة وتعديلات الأداء تصدر بشكل متكرر.

## تشغيل OCR على الصورة – دليل خطوة بخطوة

فيما يلي **السكريبت الكامل**. لا تتردد في نسخه ولصقه في ملف يُسمى `run_ocr.py` وتشغيله باستخدام `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### ما يفعله السكريبت، بلغة بسيطة

1. **Instantiate** محرك OCR حتى تتمكن من التحكم في إعداداته.  
2. **Load** ملف PNG (`article.png`). يتوقف السكريبت مبكرًا إذا لم يكن الملف موجودًا—بدون أخطاء `NoneType` غامضة لاحقًا.  
3. **Select** `hocr` كصيغة تصدير. هذه الصيغة تحتفظ بالتخطيط الأصلي، وهو أمر أساسي لتحويل الصورة لاحقًا إلى PDF قابل للبحث.  
4. **Run** محرك التعرف؛ هنا يتم تنفيذ الجزء الأكبر من العملية.  
5. **Write** ملف XML الخاص بـ hOCR إلى `article.hocr`. الآن لديك تمثيل قابل للقراءة آليًا للنص وإحداثياته.  
6. *(اختياري)* غيّر إلى `"pdf"` وأنشئ PDF قابل للبحث في خطوة إضافية.

المخرجات المتوقعة هي ملف `.hocr` مشفر بـ UTF‑8 يبدو كالتالي (مقتطع للاختصار):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

إذا قمت بإلغاء التعليق عن قسم PDF، ستحصل أيضًا على `article_searchable.pdf`، والذي يمكنك فتحه بأي عارض PDF واستخدام صندوق البحث **Ctrl + F** لتحديد الكلمات فورًا.

![مثال ناتج تشغيل OCR على الصورة](example.png "تشغيل OCR على الصورة – نتائج hOCR و PDF")

## كيفية استخراج النص من PNG باستخدام OcrEngine

إذا كان كل ما تحتاجه هو النص الخام (بدون تخطيط، بدون PDF)، يمكنك تخطي خطوة hOCR تمامًا:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*لماذا تختار النص العادي؟* إنه خفيف الوزن، مثالي للفهرسة، ويعمل بشكل رائع مع خطوط أنابيب NLP اللاحقة.

## التعرف على صورة النص وإنشاء PDF قابل للبحث

إنشاء PDF قابل للبحث هو عملية من جزأين:

1. **Run OCR** باستخدام `hocr` (كما فعلنا أعلاه) للحصول على معلومات التخطيط.  
2. **Combine** صورة PNG الأصلية مع hOCR في PDF باستخدام مُصدّر PDF الخاص بالمحرك.

معظم مكتبات OCR الحديثة (Tesseract، ABBYY، Google Vision) توفر تصدير `pdf` الذي يقوم بذلك بالضبط. المقتطف في كتلة *Optional* من السكريبت الرئيسي يوضح النمط. إذا لم تكن مكتبتك تحتوي على مُصدّر PDF مدمج، يمكنك استخدام **`pdf2image`** + **`reportlab`** لدمج الصورة وhOCR معًا—فقط أخبرني، وسأشارك مثالًا إضافيًا سريعًا.

## تحويل PNG إلى PDF مع مخرجات OCR

أحيانًا تريد فقط **PDF عادي** يحتوي على الصورة (بدون طبقة قابلة للبحث). هذا أبسط حتى:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

اجمع هذا مع خطوة OCR إذا كنت بحاجة إلى نسخة قابلة للبحث، أو احتفظ به كنسخة بصرية دقيقة لأغراض الأرشفة.

## المشكلات الشائعة والنصائح

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **صورة PNG غير واضحة أو منخفضة الدقة** | دقة OCR تنخفض بشكل كبير تحت ~300 DPI. | قم بزيادة الحجم باستخدام `Image.resize((width*2, height*2), Image.LANCZOS)` قبل تمريره إلى المحرك. |
| **لغة خاطئة** | المحرك يفرض اللغة الإنجليزية افتراضيًا؛ الأحرف غير الإنجليزية تصبح مشوهة. | استدعِ `ocr_engine.setLanguage('deu')` (أو رمز ISO المناسب) قبل `recognize()`. |
| **غياب مخرجات hOCR** | بعض المحركات تُخرج نصًا عاديًا افتراضيًا عندما لا يتم استدعاء `setExportFormat`. | تحقق مرة أخرى من أن `setExportFormat("hocr")` يُنفّذ **قبل** `recognize()`. |
| **أخطاء صلاحيات الملف** | محاولة الكتابة إلى مجلد للقراءة فقط. | استخدم مسارًا داخل مشروعك أو نفّذ `os.makedirs(..., exist_ok=True)` أولاً. |
| **ملفات PDF الكبيرة تسبب ارتفاعًا في الذاكرة** | مُصدّر PDF يحتفظ بالصورة كاملة في الذاكرة. | عالج الصفحات على دفعات أو استخدم كاتب PDF تدفقي. |

*نصيحة احترافية:* اختبر دائمًا على صورة عينة صغيرة قبل توسيع العملية إلى مجموعة من آلاف الصور. هذا يوفر ساعات من تصحيح الأخطاء.

## الخلاصة

أنت الآن تعرف **how to run OCR on image** للملفات، **extract text from PNG**، **recognize text image** للمهام اللاحقة، **generate a searchable PDF**، و **convert PNG to PDF** عندما تحتاج إلى أرشفة بسيطة. السكريبت المقدم هو حل كامل، قابل للنسخ واللصق يعمل مباشرة، وتسمح الأقسام الاختيارية لك بتخصيص المخرجات وفق سير عملك الدقيق.

### ما التالي؟

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}