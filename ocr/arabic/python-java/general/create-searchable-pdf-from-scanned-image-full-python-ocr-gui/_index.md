---
category: general
date: 2026-07-05
description: إنشاء ملف PDF قابل للبحث باستخدام بايثون. تعلّم كيفية تحويل صورة PNG
  ممسوحة ضوئياً إلى نص باستخدام OCR، وتحويل ملف PDF الممسوح إلى PDF قابل للبحث، والحصول
  على ملف PDF قابل للبحث في دقائق.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: ar
og_description: أنشئ ملف PDF قابل للبحث بسرعة. يوضح هذا الدليل كيفية تحويل صورة PNG
  إلى نص باستخدام OCR، وتحويل ملف PDF الممسوح ضوئياً، وإنتاج ملف PDF قابل للبحث باستخدام
  بايثون.
og_title: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئياً – دليل Python OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: إنشاء ملف PDF قابل للبحث من صورة ممسوحة ضوئياً – دليل كامل لتقنية OCR باستخدام
  بايثون
url: /ar/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إنشاء ملف PDF قابل للبحث من صورة ممسوحة – دليل كامل للتعرف الضوئي على الأحرف (OCR) باستخدام بايثون

هل تساءلت يومًا كيف يمكنك **إنشاء PDF قابل للبحث** من صورة ممسوحة ضوئيًا دون دفع ثمن برامج باهظة؟ لست وحدك. في العديد من المكاتب، تصل ملفات PDF كصور ثابتة—صعبة البحث، ولا يمكن نسخها، وتُعد كابوسًا لتدقيق الامتثال. الخبر السار؟ ببضع أسطر من بايثون يمكنك تحويل تلك الصورة PNG الثابتة إلى PDF قابل للبحث بالكامل، والعملية أسهل مما تتصور.

في هذا الدليل سنستعرض مثالًا كاملًا على **التعرف الضوئي على الأحرف (OCR)**، يغطي كل شيء من تثبيت المكتبة المناسبة إلى كتابة ملف PDF النهائي. بنهاية الدليل ستعرف بالضبط كيفية **تحويل ملفات PDF للصور الممسوحة**، وكيفية **how to ocr pdf** برمجيًا، وستحصل على سكريبت قابل لإعادة الاستخدام يمكنك إدراجه في أي مشروع.

## ما ستتعلمه

- تثبيت وتكوين مكتبة OCR للبايثون (سنستخدم `pytesseract` و `pdf2image`).
- تهيئة محرك OCR وتحديد اللغة.
- تحميل صورة PNG ممسوحة (أو أي صورة) وتشغيل OCR عليها.
- تحويل نتيجة OCR إلى **PDF قابل للبحث** (مصفوفة بايت) وحفظه.
- نصائح للتعامل مع المستندات متعددة الصفحات، اللغات المختلفة، والمشكلات الشائعة.

لا تحتاج إلى خبرة سابقة في OCR—فقط بيئة عمل Python 3 وبعض الفضول.

---

## إنشاء PDF قابل للبحث – نظرة عامة

فيما يلي مخطط تدفق عالي المستوى للخطوات التي سننفذها.  

![مخطط سير عمل إنشاء PDF قابل للبحث](https://example.com/flowchart.png "مخطط سير عمل إنشاء PDF قابل للبحث")

*نص بديل: مخطط سير عمل إنشاء PDF قابل للبحث يُظهر تهيئة المحرك، تحميل الصورة، التعرف الضوئي على الأحرف، تحويل إلى PDF، وكتابة الملف.*

---

## الخطوة 1: تهيئة محرك OCR (how to ocr pdf)

لماذا نحتاج إلى تهيئة أي شيء على الإطلاق؟ محرك OCR هو الدماغ الذي يفسر أنماط البكسل كحروف. بإنشاء نسخة من المحرك وتحديد اللغة صراحةً، نخبر المكتبة أي أبجدية نتوقعها، مما يحسن الدقة بشكل كبير.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**نصيحة احترافية:** إذا كنت بحاجة إلى OCR مستندات بعدة لغات، ثبّت حزم اللغة المناسبة لـ Tesseract ومرّر قائمة مثل `"eng+spa"` إلى `ocr_language`.

---

## الخطوة 2: تحميل الصورة الممسوحة (convert scanned image pdf)

الجزء التالي من اللغز هو جلب بيانات الصورة إلى بايثون. سواء كان لديك PNG واحد أو TIFF متعدد الصفحات، يمكن لفئة `PIL.Image` فتحه. إذا كنت تبدأ من PDF يحتوي بالفعل على صور ممسوحة، سيقوم `pdf2image` بتحويل كل صفحة إلى صورة لنا.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**لماذا هذا مهم:** تحميل الصورة ككائن Pillow يمنحنا الوصول إلى بيانات البكسل الخام، والتي يحتاجها محرك OCR. تخطي هذه الخطوة وإعطاء بايتات خام مباشرة سيسبب أخطاء.

---

## الخطوة 3: تنفيذ التعرف الضوئي على الأحرف على الصورة (ocr recognition example)

الآن الجزء الممتع—السماح للمحرك بقراءة النص. `pytesseract.image_to_pdf_or_hocr` يُعيد تدفق بايتات PDF يحتوي بالفعل على طبقة نص غير مرئية، وهو ما نحتاجه بالضبط لإنشاء **PDF قابل للبحث**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**حالة خاصة:** إذا كانت صورتك منخفضة التباين، فكر في تطبيق عتبة بسيطة قبل OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

يمكن لهذه الخطوة الصغيرة من المعالجة المسبقة أن تعزز الدقة بشكل كبير.

---

## الخطوة 4: كتابة بايتات PDF إلى ملف (convert png searchable pdf)

مكتبة OCR تعطينا مصفوفة بايت—فكر فيها كالمحتوى الخام لملف PDF. كل ما نحتاج إلى القيام به الآن هو كتابة تلك البايتات إلى القرص.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**ما ستلاحظه:** افتح الملف الناتج في أي عارض PDF وحاول البحث عن كلمة تعرف أنها موجودة في الصورة الأصلية. يجب أن ينتقل التحديد مباشرة إلى الموقع، مما يثبت أن طبقة النص غير المرئية تعمل.

---

## الخطوة 5: توسيع إلى مستندات متعددة الصفحات (convert scanned image pdf)

العقود في الواقع غالبًا ما تمتد لعدة صفحات. لتحويل ملفات **convert scanned image pdf** التي تحتوي على عدة صفحات، قم بالتكرار عبر كل صفحة، نفّذ OCR عليها، ثم دمج ملفات PDF الناتجة.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**لماذا الدمج؟** كل استدعاء لـ `image_to_pdf_or_hocr` ينتج PDF مستقل. دمجها يضمن أن المستند النهائي يحافظ على ترتيب الصفحات الأصلي.

---

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا يمكن البحث عن النص بعد فتح PDF | Tesseract لا يجد أي حروف (ناتج فارغ) | تحقق من جودة الصورة، زد DPI، أو طبّق معالجة مسبقة (التباين، التحويل إلى ثنائي). |
| حروف مشوشة (مثال: �) | حزمة لغة خاطئة أو خطوط مفقودة | ثبّت بيانات اللغة الصحيحة (`tesseract‑lang‑eng`) وتأكد من أن `ocr_language` يتطابق. |
| حجم ملف PDF كبير جدًا (>10 MB لصورة صفحة واحدة) | استخدام PNG غير مضغوط كمصدر؛ OCR يضيف صورة بدقة كاملة | قلل حجم الصورة قبل OCR (`image.thumbnail((1240, 1754))` لـ A4). |
| انهيار السكريبت على Windows مع رسالة “tesseract.exe not found” | ملف Tesseract التنفيذي غير موجود في PATH | أضف `pytesseract.pytesseract.tesseract_cmd = r\"C:\\Program Files\\Tesseract-OCR\\tesseract.exe\"` (عدّل المسار). |

---

## سكريبت كامل وجاهز للتنفيذ

بجمع كل ذلك معًا، إليك ملف واحد يمكنك نسخه ولصقه وتشغيله:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

احفظه كـ `create_searchable_pdf.py`، استبدل القيم النائبة بالمسارات الفعلية، ثم شغّله:

```bash
python create_searchable_pdf.py
```

يجب أن ترى

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة من الكود مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية OCR ملف PDF في .NET باستخدام Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [تحويل الصور إلى PDF C# – حفظ نتيجة OCR متعددة الصفحات](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [التعرف الضوئي على مستندات PDF في Aspose.OCR للـ Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}