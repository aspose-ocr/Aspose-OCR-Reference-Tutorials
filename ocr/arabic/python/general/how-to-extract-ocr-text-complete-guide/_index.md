---
category: general
date: 2026-02-22
description: تعلم كيفية استخراج نص OCR وتحسين دقة OCR باستخدام المعالجة اللاحقة بالذكاء
  الاصطناعي. نظّف نص OCR بسهولة في بايثون مع مثال خطوة بخطوة.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: ar
og_description: اكتشف كيفية استخراج نص OCR، تحسين دقة OCR، وتنظيف نص OCR باستخدام
  سير عمل بسيط بلغة بايثون مع معالجة ما بعد الذكاء الاصطناعي.
og_title: كيفية استخراج نص OCR – دليل خطوة بخطوة
tags:
- OCR
- AI
- Python
title: كيفية استخراج نص OCR – دليل كامل
url: /ar/python/general/how-to-extract-ocr-text-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخراج نص OCR – دليل برمجة كامل

هل تساءلت يومًا **كيف تستخرج OCR** من مستند ممسوح ضوئيًا دون أن ينتهي بك الأمر إلى فوضى من الأخطاء الإملائية والأسطر المكسورة؟ أنت لست وحدك. في العديد من المشاريع الواقعية، يبدو الناتج الخام من محرك OCR كفقرة مشوشة، وتنظيفه يبدو مهمة شاقة.  

الأخبار السارة؟ باتباع هذا الدليل سترى طريقة عملية لاستخلاص بيانات OCR منظمة، تشغيل معالج ما بعد الذكاء الاصطناعي، والحصول على **نص OCR نظيف** جاهز للتحليل اللاحق. سنستعرض أيضًا تقنيات **تحسين دقة OCR** لتكون النتائج موثوقة من المرة الأولى.  

في الدقائق القليلة القادمة سنغطي كل ما تحتاجه: المكتبات المطلوبة، سكريبت كامل قابل للتنفيذ، ونصائح لتجنب الأخطاء الشائعة. لا اختصارات غامضة مثل “انظر الوثائق” — فقط حل كامل ومستقل يمكنك نسخه ولصقه وتشغيله.

## ما ستحتاجه

- Python 3.9+ (الكود يستخدم تلميحات النوع لكنه يعمل على إصدارات 3.x الأقدم)
- محرك OCR يمكنه إرجاع نتيجة منظمة (مثل Tesseract عبر `pytesseract` مع العلمة `--psm 1`، أو واجهة برمجة تطبيقات تجارية توفر بيانات الكتل/الأسطر)
- نموذج معالجة ما بعد الذكاء الاصطناعي – في هذا المثال سنحاكيه بدالة بسيطة، لكن يمكنك استبداله بـ `gpt‑4o-mini` من OpenAI، Claude، أو أي نموذج لغة كبير يقبل نصًا ويعيد ناتجًا مُنظفًا
- بضع صور عينة (PNG/JPG) للاختبار

إذا كان لديك هذه جاهزة، فلنبدأ.

## كيفية استخراج OCR – الاسترجاع الأولي

الخطوة الأولى هي استدعاء محرك OCR وطلب **تمثيل منظم** بدلاً من سلسلة نصية عادية. النتائج المنظمة تحافظ على حدود الكتل والأسطر والكلمات، مما يجعل التنظيف لاحقًا أسهل بكثير.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **لماذا هذا مهم:** من خلال الحفاظ على الكتل والأسطر نتجنب الحاجة لتخمين مكان بدء الفقرات. دالة `recognize_structured` توفر لنا هيكلًا نظيفًا يمكننا لاحقًا إمداده إلى نموذج الذكاء الاصطناعي.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

تشغيل المقتطف يطبع السطر الأول تمامًا كما رآه محرك OCR، والذي غالبًا ما يحتوي على أخطاء مثل “0cr” بدلاً من “OCR”.

## تحسين دقة OCR باستخدام معالجة ما بعد الذكاء الاصطناعي

الآن بعد أن حصلنا على الناتج المنظم الخام، لنمرره إلى معالج ما بعد الذكاء الاصطناعي. الهدف هو **تحسين دقة OCR** عبر تصحيح الأخطاء الشائعة، توحيد علامات الترقيم، وحتى إعادة تقسيم الأسطر عند الحاجة.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **نصيحة احترافية:** إذا لم يكن لديك اشتراك في نموذج لغة كبير، يمكنك استبدال الاستدعاء بمحول محلي (مثل `sentence‑transformers` + نموذج تصحيح مدرب)، أو حتى نهج قائم على القواعد. الفكرة الأساسية هي أن الذكاء الاصطناعي يرى كل سطر على حدة، وهو عادةً كافٍ لـ **تنظيف نص OCR**.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

يجب الآن أن ترى جملة أنظف كثيرًا — تم استبدال الأخطاء الإملائية، إزالة المسافات الزائدة، وإصلاح علامات الترقيم.

## تنظيف نص OCR للحصول على نتائج أفضل

حتى بعد تصحيح الذكاء الاصطناعي، قد ترغب في تطبيق خطوة تنظيف نهائية: إزالة الأحرف غير ASCII، توحيد فواصل الأسطر، وضغط المسافات المتعددة. هذه العملية الإضافية تضمن أن يكون الناتج جاهزًا للمهام اللاحقة مثل معالجة اللغة الطبيعية أو إدخال البيانات إلى قاعدة بيانات.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

دالة `final_cleanup` تعطيك سلسلة نصية عادية يمكنك تمريرها مباشرة إلى فهرس بحث، نموذج لغة، أو تصدير CSV. لأننا حافظنا على حدود الكتل، يبقى هيكل الفقرات محفوظًا.

## الحالات الحدية والسيناريوهات المحتملة

- **تصاميم متعددة الأعمدة:** إذا كان المصدر يحتوي على أعمدة، قد يخلط محرك OCR بين الأسطر. يمكنك اكتشاف إحداثيات الأعمدة من مخرجات TSV وإعادة ترتيب الأسطر قبل إرسالها إلى الذكاء الاصطناعي.
- **نصوص غير لاتينية:** للغات مثل الصينية أو العربية، غيّر موجه النموذج لطلب تصحيح خاص باللغة، أو استخدم نموذجًا مدربًا على تلك الكتابة.
- **مستندات كبيرة:** إرسال كل سطر على حدة قد يكون بطيئًا. اجمع الأسطر في دفعات (مثلاً 10 أسطر لكل طلب) ودع النموذج يرجع قائمة بالأسطر المنظفة. تذكر احترام حدود الرموز.
- **كتل مفقودة:** بعض محركات OCR تُرجع قائمة مسطحة من الكلمات فقط. في هذه الحالة، يمكنك إعادة بناء الأسطر بتجميع الكلمات ذات قيم `line_num` المتشابهة.

## مثال كامل يعمل

بجمع كل شيء معًا، إليك ملفًا واحدًا يمكنك تشغيله من البداية إلى النهاية. استبدل القيم النائبة بمفتاح API الخاص بك ومسار الصورة.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}