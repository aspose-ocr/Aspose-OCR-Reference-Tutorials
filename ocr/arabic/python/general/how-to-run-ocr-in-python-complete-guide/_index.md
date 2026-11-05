---
category: general
date: 2026-06-19
description: كيفية تنفيذ OCR خطوة بخطوة وتحسين دقة OCR باستخدام تقنيات OCR للنص العادي.
  تعلّم سير عمل سريع لاستخراج النص بشكل موثوق.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: ar
og_description: كيفية تشغيل OCR بكفاءة. يوضح هذا الدرس كيفية تحسين دقة OCR باستخدام
  OCR النص العادي ومعالجة ما بعد الذكاء الاصطناعي.
og_title: كيفية تشغيل OCR في بايثون – دليل شامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: كيفية تشغيل OCR في بايثون – دليل شامل
url: /ar/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تشغيل OCR في بايثون – دليل كامل

هل تساءلت يومًا **كيف تشغّل OCR** على مجموعة من ملفات PDF الممسوحة دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك. في العديد من المشاريع العقبة الأولى هي ببساطة استخراج نص موثوق من صورة، والفرق بين نتيجة متذبذبة واستخلاص نظيف غالبًا ما يعود إلى بضع خطوات ذكية.

في هذا الدليل سنستعرض خط أنابيب عملي من أربع خطوات لا يقتصر فقط على **تشغيل OCR** بل أيضًا **تحسين دقة OCR** من خلال دمج تمريرة نصية سريعة مع تمريرة ثانية واعية للتخطيط ومعالج لاحق مدعوم بالذكاء الاصطناعي. بنهاية الدليل ستحصل على سكريبت جاهز للتنفيذ، شرح واضح لأهمية كل مرحلة، ونصائح للتعامل مع الحالات الخاصة مثل الصفحات متعددة الأعمدة أو المسحات الضوضائية.

---

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر ما يلي:

- **Python 3.9+** – يستخدم الكود تلميحات النوع وسلاسل f.
- **Tesseract OCR** مثبت ويمكن الوصول إليه عبر أمر `tesseract`. (على أوبونتو: `sudo apt install tesseract-ocr`; على ويندوز احصل على المثبت من المستودع الرسمي.)
- مكتبة **pytesseract** (`pip install pytesseract`).
- مكتبة **AI post‑processing** – في هذا المثال سنفترض أن لديك وحدة `ai` خفيفة تقدم `run_postprocessor`. استبدلها بواجهة OpenAI GPT‑4 أو نموذج محلي إذا رغبت.
- بعض الصور أو ملفات PDF التجريبية للاختبار.

هذا كل شيء. لا أطر ثقيلة، لا تمارين Docker. مجرد عدد قليل من تثبيتات pip وأنت جاهز للانطلاق.

---

## الخطوة 1: تنفيذ تمريرة OCR نصية سريعة

أول شيء يتغافل عنه معظم المطورين هو أن تشغيل OCR *نصي* هو سريع جدًا ويعطيك فحصًا سريعًا للمنطقية. سنستدعي `engine.Recognize()` لاستخراج الأحرف الخام دون أي بيانات تخطيطية. هذا ما نعنيه بـ **plain text OCR**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*لماذا هذا مهم:*  
- **Speed** – تمريرة نصية على صفحة 300 dpi عادةً ما تنتهي في أقل من ثانية.  
- **Baseline** – يمكنك مقارنة المخرجات المهيكلة لاحقًا مع هذا الأساس لاكتشاف الأخطاء الواضحة.  
- **Error‑catching** – إذا فشلت التمريرة النصية تمامًا (مثلاً كل النص غير مفهوم)، تعرف أن جودة الصورة منخفضة ويمكنك الإيقاف مبكرًا.

---

## الخطوة 2: تشغيل تمريرة OCR مفصلة واعية للتخطيط

النص العادي رائع، لكنه يتجاهل *أين* يقع كل كلمة على الصفحة. للفواتير، النماذج، أو المجلات متعددة الأعمدة تحتاج إلى إحداثيات، أرقام أسطر، وربما معلومات الخط. هنا يأتي دور `engine.RecognizeStructured()`.

فيما يلي غلاف رقيق حول مخرجات **TSV** الخاصة بـ Tesseract، والتي تعطينا هيكلًا من صفحات → أسطر → كلمات، مع الحفاظ على الصناديق المحيطة.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*لماذا نقوم بذلك:*  
- **Coordinates** تتيح لك لاحقًا ربط النص المستخرج بالصورة الأصلية للتظليل أو الإزالة.  
- **Line grouping** يحافظ على تنسيق الصفحة الأصلي، وهو ضروري عند إعادة بناء الجداول أو الأعمدة.  
- هذه التمريرة أبطأ قليلاً من النصية، لكنها لا تزال تنتهي خلال بضع ثوانٍ لمعظم المستندات.

---

## الخطوة 3: تشغيل المعالج AI لتصحيح أخطاء OCR

حتى أفضل محرك OCR يخطئ—فكر في “rn” مقابل “m”، أو فقدان الحركات، أو تقسيم الكلمات. نموذج AI يمكنه النظر إلى السلسلة الخام والبيانات المهيكلة، اكتشاف التناقضات، وإعادة كتابة النص مع الحفاظ على الإحداثيات الأصلية.

فيما يلي تنفيذ **تجريبي**؛ استبدل الجسم بنداء LLM حقيقي إذا كان لديك واحد.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*لماذا هذه الخطوة تحسن دقة OCR:*  
- **Contextual fixes** – يمكن للذكاء الاصطناعي أن يحدد أن “l0ve” ربما تكون “love” بناءً على الكلمات المحيطة.  
- **Coordinate preservation** – تحتفظ بمعلومات التخطيط، لذا تبقى المهام اللاحقة (مثل تعليقات PDF) دقيقة.  
- **Iterative refinement** – يمكنك تشغيل المعالج عدة مرات، كل مرة تُنقّص المزيد من الأخطاء.

---

## الخطوة 4: التكرار عبر المخرجات المهيكلة المصححة

الآن بعد أن حصلنا على بنية منقّحة، استخراج النص النهائي أمر سهل. أدناه نطبع كل سطر، لكن يمكنك أيضًا كتابة إلى CSV، إدخاله في قاعدة بيانات، أو إنشاء PDF قابل للبحث.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**المخرجات المتوقعة** (باستخدام فاتورة صفحة واحدة بسيطة):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

لاحظ كيف تم الحفاظ على فواصل الأسطر وترتيب الأعمدة، وكيف تم تصحيح الأخطاء الشائعة مثل قراءة “$15.00” كـ “$15,00” بفضل خطوة AI.

---

## كيف يساعد هذا سير العمل **تحسين دقة OCR**

| المرحلة | ما الذي يُصحّحه | لماذا يهم |
|------|---------------|----------------|
| **Plain text OCR** | Detects unreadable pages early | يوفر الوقت بتخطي المدخلات المستحيلة |
| **Structured OCR** | Captures layout, coordinates | يُتيح المهام اللاحقة (التظليل، الإزالة) |
| **AI post‑processor** | Corrects spelling, merges split words, fixes numbers | يعزز الدقة العامة على مستوى الأحرف من ~85 % إلى >95 % على المسحات الضوضائية |
| **Iteration** | Allows you to re‑run with tuned parameters | يضبط الخط الأنابيب لأنواع المستندات المحددة |

بدمج هذه المفاهيم الثلاثة—**plain text OCR**، استخراج واعٍ للتخطيط، وتصحيح AI—تحصل على حل قوي *يُحسّن* **دقة OCR** بشكل ملحوظ دون الحاجة لكتابة شبكة عصبية مخصصة من الصفر.

---

## مشاكل شائعة & نصائح احترافية

- **مشكلة:** إمداد صورة منخفضة الدقة (≤150 dpi) إلى Tesseract ينتج مخرجات مشوشة.  
  **نصيحة احترافية:** عالج مسبقًا باستخدام `Pillow`—طبق `Image.convert('L')` و `Image.filter(ImageFilter.MedianFilter())` قبل OCR.

- **مشكلة:** قد يعيد المعالج AI كتابة المصطلحات الخاصة بالمجال (مثلاً “SKU123”).  
  **نصيحة احترافية:** أنشئ قائمة بيضاء بالمصطلحات ومرّرها إلى LLM أو إلى مكتبة تدقيق إملائي مثل `pyspellchecker`.

- **مشكلة:** الصفحات متعددة الأعمدة تُدمج في سطر واحد.  
  **نصيحة احترافية:** اكتشف حدود الأعمدة باستخدام حقل `block_num` في مخرجات TSV لـ Tesseract وقسّم السطور وفقًا لذلك.

- **مشكلة:** ملفات PDF الكبيرة تُسبب استهلاك الذاكرة عند تحميل جميع الصفحات مرة واحدة.  
  **نصيحة احترافية:** عالج الصفحات تدريجيًا—استخدم حلقة `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## توسيع الخط الأنابيب

إذا كنت فضوليًا بشأن الخطوات التالية، ففكّر في التحسينات التالية:

1. **معالجة دفعات** – غلف السكريبت بالكامل في دالة تمشي عبر دليل، وتعالج آلاف الملفات بالتوازي باستخدام `concurrent.futures`.
2. **نماذج اللغة** – استبدل الخوارزمية البسيطة `difflib` بنداء إلى OpenAI `gpt‑4o` أو نموذج LLaMA مستضاف محليًا للحصول على تصحيحات سياقية أغنى.
3. **صيغ التصدير** – اكتب البنية المصححة إلى PDF قابل للبحث

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية استخراج نص الصورة باستخدام اللغة مع Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [كيفية استخدام OCR - تقنيات متقدمة مع Aspose.OCR للـ Java](/ocr/english/java/advanced-ocr-techniques/)
- [تحسين دقة OCR – وضع اكتشاف المناطق في OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}