---
category: general
date: 2026-06-19
description: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR في بايثون. تعلم كيفية تحويل
  OCR إلى PDF، استخراج النص من الصورة، وإجراء OCR على الصورة بسرعة.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: ar
og_description: إنشاء ملف PDF قابل للبحث من صورة باستخدام OCR في بايثون. يوضح هذا
  الدليل كيفية تحويل OCR إلى PDF، واستخراج النص من الصورة، وإجراء OCR على الصورة.
og_title: إنشاء ملف PDF قابل للبحث في بايثون – دليل برمجي كامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: إنشاء ملف PDF قابل للبحث في بايثون – دليل كامل خطوة بخطوة
url: /ar/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث في بايثون – دليل خطوة‑بخطوة كامل

هل احتجت يومًا إلى **إنشاء ملف PDF قابل للبحث** من إيصال ممسوح ضوئيًا لكنك لم تكن متأكدًا من أين تبدأ؟ لست وحدك — كثير من المطورين يواجهون نفس المشكلة عندما يحاولون لأول مرة تحويل صورة نص إلى ملف PDF يمكنك فعليًا البحث فيه.  

في هذا الدرس سنستعرض حلًا عمليًا يتيح لك **تنفيذ OCR على الصورة**، تحويل نتيجة OCR إلى **PDF قابل للبحث**، وحتى استخراج النص الأصلي إذا كنت تحتاجه لمعالجة إضافية. لا إطالة، مجرد مثال عملي يمكنك نسخه‑ولصقه في مشروعك اليوم.

## ما ستتعلمه

- كيفية إعداد محرك OCR خفيف الوزن في بايثون  
- الخطوات الدقيقة **لتحويل OCR إلى PDF** وحفظه كمستند قابل للبحث  
- طرق **استخراج النص من الصورة** للتحليل اللاحق  
- نصائح للتعامل مع المشكلات الشائعة مثل اتجاه الصورة والملفات الكبيرة  
- برنامج كامل قابل للتنفيذ يمكنك تكييفه مع حالتك الخاصة

### المتطلبات المسبقة

- تثبيت Python 3.8+ على جهازك  
- إلمام أساسي بـ pip وبيئات افتراضية (اختياري لكن يُنصح به)  
- ملف صورة (PNG، JPEG، إلخ) يحتوي على نص واضح يمكن قراءته آليًا  

إذا كان لديك كل ذلك، لنبدأ.

## الخطوة 1: تثبيت المكتبة المطلوبة

المقتطف البرمجي الذي رأيته سابقًا يستخدم حزمة `ocr` خيالية، لكن الفكرة نفسها تنطبق على مكتبات حقيقية مثل **EasyOCR**، **pytesseract**، أو **pdfminer.six**. في هذا الدليل سنستخدم **EasyOCR** لأنها بايثون خالص، تدعم العديد من اللغات، وتوفر طريقة تحويل PDF مفيدة عبر مساعد إضافي.

```bash
pip install easyocr pillow
```

> **نصيحة احترافية:** قم بالتثبيت داخل بيئة افتراضية (`python -m venv venv && source venv/bin/activate`) للحفاظ على نظافة الاعتمادات.

## الخطوة 2: تهيئة محرك OCR – تنفيذ OCR على الصورة

الآن بعد أن أصبحت المكتبة جاهزة، ننشئ محرك OCR ونخبره بالعمل مع النص الإنجليزي. هذا هو المكان الأول الذي **ننفذ فيه OCR على الصورة**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

لماذا نحتاج كائن قارئ مخصص؟ EasyOCR يحمل نماذج اللغات مسبقًا، لذا إعادة استخدام نفس `reader` لعدة صور أكثر كفاءة من إعادة تهيئته في كل مرة.

## الخطوة 3: تحميل الصورة – استخراج النص من الصورة

لنُدخل الصورة إلى الذاكرة. هذه الخطوة هي التي **نستخرج فيها النص من الصورة** لاحقًا، لكن الآن نكتفي بتحميلها.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

إذا كانت صورتك مقلوبة أو مائلة، فكر في استخدام طرق `rotate` أو `transpose` الخاصة بـ Pillow قبل تمريرها إلى محرك OCR. فحص بصري سريع يمكن أن يوفر لك ساعات من تصحيح الأخطاء لاحقًا.

## الخطوة 4: تشغيل محرك OCR والتقاط النتائج

هذا هو جوهر العملية—إرسال الصورة إلى محرك OCR والحصول على بيانات مُنظمة.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

علامة `detail=1` تُعطينا صناديق الإحاطة، والتي سنحتاجها عندما **نحول OCR إلى PDF** لاحقًا. إذا كنت تهتم فقط بالسلاسل النصية الخام، اضبط `detail=0`.

## الخطوة 5: تحويل نتيجة OCR إلى PDF قابل للبحث – تحويل OCR إلى PDF

EasyOCR لا توفر كاتب PDF مباشر، لكن يمكننا تجميع PDF بأنفسنا باستخدام Pillow ومكتبة `reportlab`. لتقليل وزن الدرس، سنستخدم `fpdf2`، التي تسمح لنا بدمج الصورة الأصلية وتراكب نص غير مرئي.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

ماذا حدث للتو؟ وضعنا الصورة الممسوحة كطبقة مرئية، ثم كتبنا الكلمات المُعترف بها فوقها بنص أبيض يندمج مع الخلفية البيضاء. لا تزال أدوات البحث تقرأ الطبقة المخفية، لذا يصبح PDF **قابلًا للبحث** دون تغيير المظهر البصري.

## الخطوة 6: حفظ بايتات PDF – تحويل الصورة إلى PDF

إذا كنت تفضل التعامل مع PDF في الذاكرة (مثلاً إرساله عبر API)، يمكنك التقاط البايتات بدلاً من الكتابة مباشرة إلى القرص.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

هذا السطر يوضح سير عمل **تحويل الصورة إلى PDF** الكلاسيكي: تبدأ بصورة، تشغل OCR، تراكب النص، وأخيرًا تُصدر تدفق PDF.

## الخطوة 7: التحقق من النتيجة – فحوصات سريعة

بعد تشغيل السكريبت، افتح `receipt_searchable.pdf` في أي عارض PDF وجرب صندوق البحث (Ctrl + F). اكتب كلمة تعرف أنها موجودة في الإيصال—إذا انتقل إلى الموضع الصحيح، فقد نجحت في **إنشاء PDF قابل للبحث**!  

إذا فشل البحث، تحقق مرة أخرى من:

1. درجات ثقة OCR (`conf` values). الثقة المنخفضة قد تعني أن الصورة غير واضحة.  
2. إحداثيات صناديق الإحاطة—أحيانًا تُبلغ EasyOCR عنها بزاوية مختلفة.  
3. أن عارض PDF ليس في وضع “صورة‑فقط” (نادر، لكن بعض العارضات لديها هذا الخيار).

## البرنامج الكامل القابل للتنفيذ

بتجميع كل شيء معًا، إليك ملف بايثون الكامل الجاهز للتنفيذ:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

احفظه باسم `searchable_pdf.py`، استبدل القيم `YOUR_DIRECTORY` بالمسارات الفعلية، ثم شغّله:

```bash
python searchable_pdf.py
```

ستظهر لك رسالة تأكيد وملف PDF جديد قابل للبحث في مجلدك.

## أسئلة شائعة وحالات خاصة

**ماذا لو كانت الصورة ملونة؟**  
EasyOCR يعمل مع الصور بالرمادي والملونة، لكن تحويلها إلى رمادي (`pil_image.convert("L")`) قد يحسن الدقة في المسحات الضوضائية.

**هل يمكنني معالجة ملفات PDF متعددة الصفحات؟**  
نعم—قم بالتكرار على كل صورة صفحة، شغّل خطوات OCR، وأضف كل صفحة إلى نفس كائن `FPDF`. فقط تذكر إعادة ضبط المؤشر (`self.add_page()`) لكل صورة جديدة.

**هل هناك طريقة للحفاظ على طبقة النص الأصلية بدلاً من النص الأبيض غير المرئي؟**  
إذا كنت تحتاج إلى PDF “نص‑تحت‑الصورة” حقيقي (مثلاً لأغراض الوصول)، فكر في استخدام `pdfminer` أو `pikepdf` لدمج طبقة نص مخفية مع وسوم PDF صحيحة. هذا أكثر تقدمًا، لكن المبدأ يبقى نفسه: صورة خلفية + نص متراكب.

**ماذا لو كانت ثقة OCR منخفضة؟**  
يمكنك تصفية الكلمات ذات الثقة المنخفضة:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## الخلاصة – ما حققناه

بدأنا بصورة إيصال بسيطة، **نفذنا OCR على الصورة**، استخرجنا السلاسل المُعترف بها، وأخيرًا **أنشأنا PDF قابل للبحث** يتصرف كأي مستند ممسوح ضوئيًا احترافي. غطى العملية جميع الكلمات الثانوية—**تحويل OCR إلى PDF**، **استخراج النص من الصورة**، **تحويل الصورة إلى PDF**، و**تنفيذ OCR على الصورة**—وبالتالي لديك الآن صندوق أدوات قابل لإعادة الاستخدام لأي مشروع مماثل.

### الخطوات التالية

- جرّب لغات أخرى بتمرير رموز ISO الخاصة بها إلى `easyocr.Reader(['en', 'es'])`.  
- استبدل EasyOCR بـ Tesseract إذا كنت تحتاج حلًا يعمل بالكامل دون اتصال؛ باقي خط الأنابيب يبقى كما هو.  
- أضف تصورًا لثقة OCR (ارسم صناديق الإحاطة على الصورة) لتصحيح المسحات المشكلة.  

هل لديك تعديل ترغب بمشاركته؟ اترك تعليقًا، أو قم بعمل fork

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}