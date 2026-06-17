---
category: general
date: 2026-04-29
description: استخراج النص من ملف PDF باستخدام Aspose OCR في بايثون. تعلم معالجة ملفات
  PDF دفعةً باستخدام OCR، تحويل نص PDF الممسوح ضوئياً، ومعالجة الصفحات ذات الثقة المنخفضة.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: ar
og_description: استخراج النص من ملف PDF باستخدام Aspose OCR في بايثون. يوضح هذا الدليل
  معالجة دفعات OCR لملفات PDF، تحويل نص PDF الممسوح ضوئياً، والتعامل مع النتائج ذات
  الثقة المنخفضة.
og_title: استخراج النص من PDF – التعرف الضوئي على الأحرف في PDF باستخدام بايثون
tags:
- OCR
- Python
- PDF processing
title: استخراج النص من PDF – OCR PDF باستخدام بايثون
url: /ar/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من PDF – OCR PDF باستخدام Python

هل احتجت يوماً إلى **استخراج النص من PDF** لكن الملف مجرد صورة ممسوحة ضوئياً؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحاولون تحويل ملفات PDF إلى بيانات قابلة للبحث. الخبر السار؟ باستخدام Aspose OCR for Python يمكنك تحويل نص PDF الممسوح في بضع أسطر فقط، وحتى تشغيل **معالجة دفعة OCR لملفات PDF** عندما يكون لديك عشرات الملفات للتعامل معها.

في هذا الدرس سنستعرض سير العمل بالكامل: إعداد المكتبة، تشغيل OCR على ملف PDF واحد، توسيع العملية إلى دفعة، والتعامل مع الصفحات ذات الثقة المنخفضة حتى تعرف متى تحتاج إلى مراجعة يدوية. في النهاية ستحصل على سكريبت جاهز للتنفيذ يستخرج النص من أي PDF ممسوح، وستفهم سبب كل خطوة.

## ما ستحتاجه

قبل أن نبدأ، تأكد من وجود التالي:

- Python 3.8 أو أحدث (الكود يستخدم f‑strings، لذا 3.6+ يعمل، لكن يفضَّل 3.8+)
- رخصة Aspose OCR for Python أو مفتاح تجربة مجانية (يمكنك الحصول عليه من موقع Aspose)
- مجلد يحتوي على ملف PDF ممسوح أو أكثر تريد معالجته
- مساحة تخزين معتدلة لتقارير *.txt* التي سيتم إنشاؤها

هذا كل شيء—لا توجد تبعيات خارجية ثقيلة، ولا تمارين OpenCV. محرك Aspose OCR يتولى كل العمل الشاق نيابةً عنك.

## إعداد البيئة

أولاً، قم بتثبيت حزمة Aspose OCR من PyPI:

```bash
pip install aspose-ocr
```

إذا كان لديك ملف ترخيص (`Aspose.OCR.lic`)، ضعّه في جذر المشروع وفعل الترخيص كالتالي:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **نصيحة احترافية:** احتفظ بملف الترخيص خارج نظام التحكم في الإصدارات؛ أضفه إلى `.gitignore` لتجنب كشفه عن طريق الخطأ.

## تنفيذ OCR على PDF واحد

الآن لنستخرج النص من PDF ممسوح واحد. الخطوات الأساسية هي:

1. إنشاء كائن `OcrEngine`.
2. توجيهه إلى ملف PDF.
3. استرجاع `OcrResult` لكل صفحة.
4. كتابة الناتج النصي إلى القرص.
5. تحرير المحرك لتحرير الموارد الأصلية.

إليك السكريبت الكامل القابل للتنفيذ:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**ما ستراه:** لكل صفحة يطبع السكريبت شيئاً مثل `Page 1: confidence 97.45%`. إذا كانت الصفحة تحت عتبة الـ 80 %، سيظهر تحذير يُخبرك أن الـ OCR قد يكون قد فاته بعض الأحرف.

### لماذا يعمل هذا؟

- **`OcrEngine`** هو البوابة إلى مكتبة Aspose OCR الأصلية؛ يتعامل مع كل شيء من معالجة الصور إلى التعرف على الأحرف.
- **`extract_from_pdf`** يقوم تلقائياً بتحويل كل صفحة PDF إلى صورة نقطية، لذا لا تحتاج إلى تحويل PDF إلى صور بنفسك.
- **درجات الثقة** تتيح لك أتمتة فحوصات الجودة—وذلك أمر حاسم عندما تعالج مستندات قانونية أو طبية حيث الدقة مهمة.

## معالجة دفعة OCR لملفات PDF باستخدام Python

معظم المشاريع الواقعية تتعامل مع أكثر من ملف واحد. لنُوسِّع سكريبت الملف الواحد إلى **خط أنابيب معالجة دفعة OCR لملفات PDF** يتجول عبر دليل، يعالج كل PDF، ويخزن النتائج في مجلد فرعي مطابق.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### كيف يساعدك هذا؟

- **القابلية للتوسع:** الدالة تتجول في المجلد مرة واحدة، وتُنشئ مجلد إخراج مخصص لكل PDF. هذا يحافظ على التنظيم عندما يكون لديك عشرات المستندات.
- **إعادة الاستخدام:** يمكن استدعاء `ocr_pdf_file` من سكريبتات أخرى (مثل خدمة ويب) لأنها دالة نقية.
- **معالجة الأخطاء:** يطبع السكريبت رسالة ودية إذا كان دليل الإدخال فارغاً، مما يحفظك من فشل صامت.

## تحويل نص PDF ممسوح – التعامل مع الحالات الخاصة

بينما يعمل الكود أعلاه لمعظم ملفات PDF، قد تواجه بعض الخصائص الغريبة:

| الحالة | لماذا يحدث ذلك | كيفية التخفيف |
|-----------|----------------|-----------------|
| **PDFs مشفرة** | الملف محمي بكلمة مرور. | مرّر كلمة المرور إلى `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **مستندات متعددة اللغات** | Aspose OCR يفرض اللغة الإنجليزية افتراضياً. | عيّن `ocr_engine.language = "spa"` للإسبانية، أو قدّم قائمة للغات المختلطة. |
| **PDFs ضخمة جداً (>500 صفحة)** | استهلاك الذاكرة يرتفع لأن كل صفحة تُحمَّل في الذاكرة. | عالج الـ PDF على دفعات باستخدام `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` داخل حلقة. |
| **جودة مسح ضعيفة** | DPI منخفض أو ضوضاء عالية تقلل من الثقة. | عالج الصورة مسبقاً عبر `engine.image_preprocessing = True` أو زد الـ DPI إلى `engine.dpi = 300`. |

> **احذر:** تفعيل معالجة الصورة مسبقاً قد يزيد من زمن استهلاك الـ CPU بشكل ملحوظ. إذا كنت تُجري دفعة ليلية، احرص على جدولة وقت كافٍ أو تشغيل عامل منفصل.

## التحقق من المخرجات

بعد انتهاء السكريبت، ستجد بنية مجلد مشابهة لـ:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

افتح أي ملف `.txt`؛ يجب أن ترى نصاً نظيفاً بترميز UTF‑8 يعكس المحتوى الممسوح الأصلي. إذا لاحظت أحرفاً مشوهة، تحقق مرة أخرى من إعدادات لغة الـ PDF وتأكد من تثبيت حزم الخطوط المناسبة على الجهاز.

## تنظيف الموارد

يعتمد Aspose OCR على ملفات DLL أصلية، لذا من الضروري استدعاء `engine.dispose()` بمجرد الانتهاء. نسيان هذه الخطوة قد يؤدي إلى تسرب الذاكرة، خصوصاً في وظائف دفعات طويلة التشغيل.

```python
# Always the last line of your script
engine.dispose()
```

## مثال كامل من البداية إلى النهاية

لنجمع كل شيء معاً، إليك مثالاً واحداً

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}