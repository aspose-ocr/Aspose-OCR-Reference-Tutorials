---
category: general
date: 2026-06-16
description: استخراج النص من ملفات TIFF باستخدام OCR في بايثون. تعلم كيفية تحويل TIFF
  إلى نص خطوة بخطوة، مع التعامل بسهولة مع المستندات متعددة الصفحات.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: ar
og_description: استخراج النص من ملفات TIFF باستخدام OCR في بايثون. اتبع هذا الدليل
  لتحويل ملفات TIFF إلى نص، وتعامل مع المسحات متعددة الصفحات، واحصل على نتائج نظيفة.
og_title: استخراج النص من ملف TIFF – دليل بايثون الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: استخراج النص من ملف TIFF – دليل بايثون الكامل
url: /ar/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من ملفات TIFF – دليل بايثون كامل

هل احتجت يوماً إلى **استخراج النص من صور TIFF** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—الكثير من المطورين يواجهون هذه المشكلة عند التعامل مع الأرشيفات الممسوحة ضوئيًا أو المستندات القديمة. الخبر السار؟ ببضع أسطر من بايثون يمكنك **تحويل TIFF إلى نص** بسرعة، حتى عندما يحتوي الملف على عشرات الصفحات.

في هذا الدرس سنستعرض مثالًا واقعيًا: تحميل ملف TIFF متعدد الصفحات، ضبط لغة OCR إلى الفرنسية، واستخراج النص المعترف به من كل صفحة. بنهاية الدرس ستحصل على سكربت جاهز للتنفيذ، وتفهم سبب أهمية كل خطوة، وتعرف كيف تعدلها للغات أو صيغ صور أخرى.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

- بايثون 3.8 أو أحدث مثبت.
- حزمة `ocr` (أو أي مكتبة OCR متوافقة توفر فئة `OcrEngine`). يمكنك تثبيتها عبر `pip install ocr-lib`—استبدلها باسم الحزمة الفعلي الذي تستخدمه.
- ملف TIFF متعدد الصفحات (مثال: `french-scans.tif`) تريد معالجته.
- إلمام أساسي ببرمجة بايثون.

لا توجد تبعيات ثقيلة، ولا خدمات خارجية—فقط بايثون نقي ومحرك OCR.

---

## الخطوة 1: إعداد محرك OCR **لاستخراج النص من TIFF**

أولاً، نحتاج إلى إنشاء كائن محرك OCR ويجب أن نخبره بأي لغة نريد استخدامها. في حالتنا المادة المصدرية بالفرنسية، لذا سنضبط اللغة وفقًا لذلك.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**لماذا هذا مهم:**  
إعداد اللغة يحسن الدقة بشكل كبير. الأحرف الفرنسية مثل “é” أو “ç” ستُقرأ كرموز عامة إذا كان المحرك يستخدم اللغة الإنجليزية افتراضيًا. باختيار الفرنسية صراحةً، نوفر للمحرك خريطة الأحرف الصحيحة.

> **نصيحة احترافية:** إذا كنت تعالج مستندات بعدة لغات، يمكنك تغيير `engine.language` في الوقت الفعلي قبل كل استدعاء لـ `recognize()`.

---

## الخطوة 2: تحميل ملف TIFF متعدد الصفحات **لتحويل TIFF إلى نص**

يمكن لملف TIFF أن يحتوي على عدة إطارات—اعتبر كل إطار صفحة منفصلة. مكتبة OCR تج abstracts ذلك لنا، لذا نوجهها ببساطة إلى الملف.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**تنبيه حالة حافة:**  
إذا كان مسار الملف غير صحيح أو كان TIFF تالفًا، ستثير طريقة `load_from_file` استثناء. احرص على وضعها داخل كتلة `try/except` في الكود الإنتاجي:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## الخطوة 3: تشغيل OCR على المستند بالكامل – جوهر **استخراج النص من TIFF**

الآن نترك المحرك يقوم بسحره. استدعاء `recognize()` يعالج كل صفحة مرة واحدة ويعيد كائن نتيجة غني.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**ما الذي يحدث خلف الكواليس؟**  
المحرك يمر على كل إطار، يطبق التحسين المسبق (تصحيح الميل، التحويل إلى ثنائي)، يشغل الشبكة العصبية، ويجمع المخرجات. لأننا استدعينا `recognize()` مرة واحدة فقط، يمكن للمكتبة مشاركة الموارد بين الصفحات، مما يكون أسرع من التكرار اليدوي.

---

## الخطوة 4: استخراج النص المعترف به من نتيجة JSON – **تحويل TIFF إلى نص** صفحةً بصفحة

يمكن تسلسل كائن النتيجة إلى JSON. داخل هذا الـ JSON ستجد مصفوفة `pages`، كل عنصر منها يحتوي على حقل `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

الآن لدينا قائمة بايثون نظيفة حيث كل عنصر يمثل نص OCR لصفحة معينة.

---

## الخطوة 5: طباعة أو حفظ النص لكل صفحة – القطعة النهائية من **استخراج النص من TIFF**

لنمر على الصفحات ونعرض النص المستخرج. يمكنك أيضًا كتابة كل صفحة إلى ملف `.txt` منفصل إذا رغبت.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### النتيجة المتوقعة (عينة)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

إذا نجح OCR، سترى كتلة نظيفة من الجمل الفرنسية لكل صفحة. إذا لاحظت رموزًا مشوهة، تحقق من إعداد اللغة أو فكر في زيادة دقة الصورة قبل OCR.

---

## التعامل مع المشكلات الشائعة عند **تحويل TIFF إلى نص**

| المشكلة | السبب | الحل السريع |
|-------|-------|-----------|
| **مصفوفة `pages` فارغة** | لم يتم تحميل TIFF بشكل صحيح أو لا يحتوي على إطارات. | تحقق من مسار الملف وتأكد أن TIFF ليس PNG صفحة واحدة مُقنَّعًا كـ TIFF. |
| **حروف غير مفهومة** | عدم تطابق اللغة أو جودة صورة منخفضة. | اضبط `engine.language` الصحيح وقم بمعالجة الصورة مسبقًا (مثلاً زيادة DPI). |
| **استهلاك الذاكرة عند TIFF كبير** | تحميل جميع الصفحات مرة واحدة يستهلك RAM. | عالج على دفعات: حمّل إطارًا واحدًا، اعترف به، ثم حرّره قبل الانتقال إلى التالي. |
| **أخطاء Unicode عند الطباعة** | ترميز الطرفية لا يدعم الأحرف المت accented. | استخدم `print(page["text"].encode('utf-8').decode('utf-8'))` أو اضبط الطرفية لتدعم UTF‑8. |

---

## توسيع السكربت: من **استخراج النص من TIFF** إلى المعالجة الدفعية

الآن بعد أن لديك أساسًا قويًا، فكر في الخطوات التالية:

1. **تحويل دفعي** – غلف التدفق بالكامل في دالة `def ocr_tiff(path):` وكررها على مجلد من ملفات TIFF.
2. **الإخراج إلى ملفات** – بدلاً من الطباعة، اكتب نص كل صفحة إلى `page_{i}.txt` أو اجمع كل النصوص في مستند واحد.
3. **محركات OCR بديلة** – إذا كنت تحتاج دقة أعلى، استبدل `ocr.OcrEngine()` بـ Tesseract (`pytesseract`) أو Azure Cognitive Services—مع الحفاظ على منطق “استخراج النص من TIFF”.
4. **معالجة ما بعد OCR** – نفّذ تدقيق إملائي، كشف لغة، أو تنظيف regex لتصحيح مخرجات OCR الخام.

---

## السكربت الكامل الجاهز للتنفيذ

فيما يلي الكود الكامل، جاهز للنسخ واللصق. يتضمن معالجة أخطاء أساسية وحفظًا اختياريًا لنص كل صفحة في ملفات منفصلة.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

شغّل هذا السكربت، وجه المتغيّر `tiff_file` إلى مستندك، وسترى وحدة التحكم تمتلئ بجمل فرنسية نظيفة. إذا زوّدت المتغيّر `out_folder`، ستجد أيضًا مجموعة من ملفات `page_#.txt` جاهزة للمعالجة اللاحقة.

---

## الخلاصة

لقد **استخدمنا استخراج النص من ملفات TIFF** باستخدام سير عمل OCR بسيط في بايثون، وتعلمت الآن كيف **تحول TIFF إلى نص** بشكل موثوق. من تهيئة المحرك باللغة المناسبة إلى التكرار على نتيجة JSON لكل صفحة، تم شرح كل خطوة مع توضيح “السبب”، لتتمكن من تعديل النمط للغات أخرى، صيغ صور مختلفة، أو وظائف دفعية أكبر.

ما الخطوة التالية؟ جرّب استبدال محرك OCR بـ Tesseract، جرب حزم لغات مختلفة، أو دمج المخرجات في قاعدة بيانات قابلة للبحث. السماء هي الحد عندما تستطيع تحويل الصور الممسوحة إلى نص قابل للبحث بسهولة.

لا تتردد في ترك تعليق إذا واجهت أي صعوبات أو لديك أفكار لتحسينات إضافية. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}