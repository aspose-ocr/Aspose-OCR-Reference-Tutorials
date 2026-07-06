---
category: general
date: 2026-06-28
description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعيًا في بايثون — استخراج
  النص من الصور وتحويل الصفحات الممسوحة ضوئيًا إلى نص باستخدام معالجة OCR دفعية.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: ar
og_description: تعلّم كيفية تنفيذ التعرف الضوئي على الأحرف (OCR) على دفعات في بايثون،
  استخراج النص من الصور، وتحويل الصفحات الممسوحة ضوئياً إلى نص باستخدام معالجة OCR
  فعّالة على دفعات.
og_title: كيفية تنفيذ OCR دفعيًا في بايثون – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعيًا في بايثون – دليل شامل لاستخراج
  النص من الصور
url: /ar/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في بايثون – دليل كامل لاستخراج النص من الصور

إذا كنت تتساءل **عن كيفية تنفيذ OCR دفعيًا في بايثون**، فأنت في المكان الصحيح. يوضح لك هذا الدرس طريقة سريعة **لاستخراج النص من الصور** و**تحويل الصفحات الممسوحة ضوئيًا إلى نص** باستخدام نسخة واحدة من محرك OCR. لا مزيد من النسخ واللصق ملفًا تلو الآخر—دع الشيفرة تقوم بالعمل الشاق.

سنستعرض كل ما تحتاجه: تثبيت المكتبة، تحميل مجلد كامل من المسحات، تشغيل معالجة OCR دفعيًا، ومعالجة النتائج بسلاسة. في النهاية ستحصل على سكريبت قابل لإعادة الاستخدام يحول مجموعة من ملفات PNG أو JPEG إلى ملفات نصية قابلة للبحث في ثوانٍ.

## ما ستحتاجه

* Python 3.9+ مثبت (الكود يعمل على 3.8 أيضًا، لكن 3.9+ يوفّر أحدث ميزات الـ typing).
* مكتبة OCR حديثة—نحن هنا نستخدم **Aspose.OCR for Python via .NET**، التي تُظهر فئة `OcrEngine` كما في المقتطف الأصلي.  
  ```bash
  pip install aspose-ocr
  ```
* مجلد يحتوي على صفحات ممسوحة ضوئيًا (`page1.png`, `page2.png`, …). أي شيء يمكن لمكتبة Pillow فتحه سيعمل، لذا ملفات PDF أو TIFF أو BMP صالحة أيضًا.
* قليل من الفضول—إذا لم تقم أبدًا بأتمتة تحويل الصورة إلى نص، فأنت على وشك معرفة لماذا يعتبر OCR الدفعي تغييرًا جذريًا.

> **نصيحة احترافية:** إذا كنت تفضّل مكتبة بايثون خالصة، استبدل `OcrEngine` بـ `pytesseract.image_to_string`. يبقى المنطق المحيط كما هو.

## كيفية تنفيذ OCR دفعيًا في بايثون – دليل خطوة بخطوة

فيما يلي السكريبت الكامل القابل للتنفيذ. كل سطر مُعلّق لتتمكن من معرفة *لماذا* كل جزء مهم، وليس فقط *ماذا* يفعل.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### النتيجة المتوقعة

تشغيل السكريبت على مجلد يحتوي على ثلاث مسحات PNG ينتج شيئًا مشابهًا لـ:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

المعاينة تُظهر أول 200 حرف من كل صفحة، والنص الكامل يُخزن في دليل `ocr_output`.

## استخراج النص من الصور باستخدام محرك واحد

لماذا ننشئ **محرك** `OcrEngine` **واحد** ونعيد استخدامه؟ إنشاء المحرك قد يكون مكلفًا لأنه يحمل حزم اللغات وملفات DLL الأصلية. بمشاركة نفس النسخة عبر الدفعة، ستحصل على:

* **توفير الذاكرة** – مجموعة واحدة فقط من الموارد تُخزن في الذاكرة.
* **زيادة السرعة** – يبقى المحرك مُشغَّلًا، متجنبًا إعادة التهيئة المتكررة.
* **الحفاظ على التناسق** – نفس إعدادات التعرف تُطبق على كل صفحة، وهو أمر أساسي عندما تريد **استخراج النص من الصور** التي تشترك في نفس التخطيط.

إذا احتجت إلى تعديل التعرف (مثل تمكين التدقيق الإملائي أو تغيير اللغة)، قم بذلك *قبل* استدعاء `recognize_batch`. جميع الصفحات اللاحقة ستورّث تلك الإعدادات تلقائيًا.

## تحويل الصفحات الممسوحة ضوئيًا إلى نص بكفاءة

جوهر المشكلة—**تحويل الصفحات الممسوحة ضوئيًا إلى نص**—يُحل بواسطة `engine.recognize_batch(images)`. في الخلفية، المكتبة تعالج كل صورة في مجموعة من الخيوط الخلفية، لذا تحصل على توسع شبه خطي على الأجهزة متعددة الأنوية. بعض الأمور التي يجب مراعاتها:

* **جودة الصورة مهمة** – 300 dpi أو أعلى تعطي أفضل النتائج. إذا كانت مسحاتك منخفضة الدقة، فكر في رفع الدقة باستخدام Pillow قبل تمريرها إلى المحرك.
* **اللون مقابل التدرج الرمادي** – عادةً ما تعمل محركات OCR أسرع على صور 8‑bit بالرمادي. يمكنك إضافة خطوة تمهيدية:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **دعم اللغات** – تدعم Aspose.OCR أكثر من 40 لغة. اضبط `engine.language = "eng"` أو `"fra"` قبل استدعاء الدفعة إذا لم تكن تعمل بالإنجليزية.

## أفضل ممارسات معالجة OCR دفعيًا

على الرغم من أن الشيفرة أعلاه مختصرة بالفعل، إلا أن OCR الدفعي على مستوى الإنتاج غالبًا ما يتطلب بعض الضمانات الإضافية:

| القلق | النهج الموصى به |
|---------|----------------------|
| **دفعات كبيرة ( > 500 ملف )** | قسّم إلى أجزاء من 100‑200 صورة للحفاظ على استهلاك الذاكرة منخفضًا. |
| **ملفات تالفة أو غير مدعومة** | المساعد `load_images` يلتقط الاستثناءات بالفعل ويسجل تحذيرًا؛ يمكنك أيضًا كتابة آلية احتياطية لتخطي أو نقل الملفات التالفة. |
| **مراقبة التقدم** | غلف `recognize_batch` في حلقة تُعيد التحكم بعد كل صورة إذا كانت المكتبة توفر ردود نداء per‑image. |
| **معالجة ما بعد** | نفّذ تدقيق إملائي أو تنظيف باستخدام regex على السلاسل الناتجة لتحسين قابلية البحث لاحقًا. |
| **التوازي** | إذا كان لديك إعداد متعدد العقد، وزّع المجلدات على العاملين ودمج مخرجات `.txt` في النهاية. |

## الأسئلة المتكررة

**س: هل يمكنني استخدام هذا مع ملفات PDF مباشرةً؟**  
ج: بالتأكيد. حوّل كل صفحة PDF إلى صورة أولاً (مثلاً باستخدام `pdf2image`) ومرّر القائمة الناتجة إلى `recognize_batch`. يبقى باقي سير العمل دون تغيير

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصورة باستخدام Aspose OCR – دليل خطوة بخطوة](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}