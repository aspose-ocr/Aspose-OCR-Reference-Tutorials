---
category: general
date: 2026-06-25
description: احصل على الأحرف المدعومة في OCR بسرعة باستخدام مكتبة aocr. تعلم كيفية
  سرد أحرف OCR، وتعيين اللغات، وتصحيح أخطاء محرك OCR الخاص بك في بايثون.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: ar
og_description: احصل على الأحرف المدعومة في OCR باستخدام aocr. يوضح لك هذا الدليل
  كيفية سرد أحرف OCR، اختيار اللغات، ومعالجة الحالات الخاصة في بايثون.
og_title: احصل على الأحرف المدعومة في OCR باستخدام بايثون – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: احصل على الأحرف المدعومة في OCR باستخدام بايثون – دليل كامل
url: /ar/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# احصل على الأحرف المدعومة من OCR في بايثون – دليل كامل

هل تساءلت يوماً كيف **get OCR supported characters** للغة معينة عندما تلعب بمحرك OCR؟ لست وحدك. سواءً كنت تبني ماسح فواتير أو محلل مستندات متعدد اللغات، معرفة الأحرف التي يستطيع محركك التعرف عليها بدقة تُعد منقذاً للوقت. في هذا الدرس سنستعرض العملية بالكامل — تثبيت المكتبة، ضبط اللغة، وأخيراً سرد تلك الأحرف — لتتمكن من تصحيح وضبط خط أنابيب OCR الخاص بك في دقائق.

سنستخدم مكتبة **aocr**، محرك OCR خفيف الوزن للبايثون يجعل من السهل الاستعلام عن قدرات اللغة. بنهاية هذا الدليل ستتمكن من **list OCR characters**، التبديل بين **supported OCR languages**، وحتى اكتشاف الفجوات في التغطية قبل أن تؤثر على الإنتاج.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* Python 3.8 أو أحدث (حزمة aocr توقفت عن دعم 3.7)
* طرفية أو موجه أوامر مع اتصال بالإنترنت
* إلمام أساسي ببرمجة بايثون (إذا كتبت `print()` من قبل، فأنت جاهز)

لا توجد تبعيات خارجية ثقيلة — فقط حزمة `aocr` عبر pip.

---

## تثبيت مكتبة aocr (محرك OCR للبايثون)

أول شيء تحتاجه هو تثبيت **OCR engine Python** يعمل. حزمة aocr متوفرة على PyPI، لذا أمر pip واحد يكفي:

```bash
pip install aocr
```

إذا كنت تستخدم بيئة افتراضية (مستحسن جداً)، فعّلها أولاً:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **نصيحة احترافية:** ثبّت نسخة محددة (`pip install aocr==1.2.4`) لتجنب تغييرات غير متوقعة في الـ API لاحقاً.

---

## اختيار لغة (Supported OCR Languages)

تأتي aocr مع مجموعة من حزم اللغات المدمجة. كل حزمة تحدد مجموعة نقاط Unicode التي يستطيع المحرك التعرف عليها. لاستعلام هذه الحزم عليك ضبط الخاصية `language` على كائن المحرك.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

يمكنك استبدال `aocr.Language.ENGLISH` بأي قيمة enum أخرى (`FRENCH`, `GERMAN`, إلخ). إذا حاولت تعيين لغة غير موجودة في الحزمة، ستطرح aocr استثناء `ValueError`. لهذا من الجيد فحص قائمة **supported OCR languages** أولاً:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## استرجاع مجموعة الأحرف (Get OCR Supported Characters)

الآن نصل إلى جوهر الدرس: **get OCR supported characters** فعلياً. يوفر المحرك طريقة مفيدة تسمى `get_supported_characters()` تُعيد قائمة بسلاسل أحرف مفردة.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

في الخلفية، تقرأ aocr ملف JSON مرفق بحزمة اللغة وتحوّل كل نقطة Unicode إلى سلسلة بايثون. النتيجة حتمية، أي ستحصل على نفس القائمة في كل مرة تشغّل فيها السكريبت على نفس نسخة اللغة.

---

## إظهار عدد الأحرف المدعومة

معرفة العدد تساعدك على تقدير مدى التغطية بسرعة. للإنجليزية، عادةً ما ترى بضعة آلاف من الأحرف (بما في ذلك علامات الترقيم والأرقام).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

استدعاء `len()` هو O(1) لأن بايثون يخزن طول القائمة داخلياً، لذا لا توجد تكلفة أداء حتى مع الأبجديات الكبيرة.

---

## معاينة أول 100 حرف مدعوم

فحص بصري سريع يمكن أن يكشف ما إذا كان المحرك يحتوي على الرموز التي تحتاجها (مثل علامة اليورو أو الاقتباسات الذكية). لنطبع أول مائة حرف:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

عملية `join` تجمع الشريحة في سلسلة واحدة، مما يجعل العرض أكثر قابلية للقراءة مقارنة بطباعة قائمة بايثون.

---

## السكريبت الكامل – جميع الخطوات في مكان واحد

فيما يلي مثال كامل قابل للتنفيذ يربط كل ما سبق. احفظه باسم `list_supported_chars.py` وشغّله عبر `python list_supported_chars.py` من الطرفية.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**الناتج المتوقع (مقتطع للاختصار):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

قد يختلف العدد الدقيق قليلاً حسب نسخة aocr، لكنك ستلاحظ دائماً أبجدية طويلة مع علامات الترقيم الشائعة.

---

## معالجة الحالات الخاصة

### ماذا لو كانت حزمة اللغة مفقودة؟

إذا طلبت لغة غير موجودة في الحزمة، لن يحتوي `aocr.Language` على الـ enum، وستواجه استثناء `AttributeError`. احمِ نفسك بفحص بسيط:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### قائمة أحرف فارغة

بعض اللغات النادرة قد تُعيد قائمة فارغة إذا كانت بيانات التدريب غير مكتملة. في هذه الحالة، يمكنك الرجوع إلى لغة افتراضية (مثل الإنجليزية) أو رفع تحذير:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### تطبيع Unicode

قد تحتوي القائمة على أحرف مركبة (مثال: “é” كـ `e` + علامة حادة). إذا كانت عملياتك اللاحقة تتوقع أحرفاً مركبة مسبقاً، نفّذ خطوة تطبيع:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## نصائح احترافية للمشاريع الواقعية

* **Cache the character list** – إذا كنت تعالج آلاف الصور، فإن استدعاء `get_supported_characters()` في كل تكرار يضيف عبئاً غير ضروري. احفظ القائمة في متغيّر على مستوى الوحدة أو سِرّتها إلى JSON لإعادة الاستخدام لاحقاً.
* **Cross‑language validation** – عندما تدعم عدة لغات في تطبيق واحد، تقاطع مجموعات الأحرف للعثور على مجموعة مشتركة. هذا يساعدك على تصميم عناصر واجهة مستخدم متسقة عبر اللغات.
* **Debugging OCR failures** – إذا أخطأ المحرك في تصنيف حرف ما، قارن الحرف المخطئ مع ناتج `list_supported_chars`. إذا كان مفقوداً، فقد حددت فجوة تغطية قد تتطلب تدريباً مخصصاً.
* **Combine with custom fonts** – aocr تحترم نطاق Unicode، لكن جودة العرض قد تختلف حسب الخط. اختبر الأحرف المدعومة بالخط الذي ستستخدمه في الإنتاج لتجنب المفاجآت.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع نسخة aocr 2.x؟**  
ج: نعم، طريقة `get_supported_characters()` ثابتة بين 1.x و 2.x. التغيير الوحيد هو أن enums اللغات نُقلت إلى `aocr.languages`.

**س: هل يمكنني الحصول على نقطة Unicode لكل حرف؟**  
ج: بالتأكيد. استخدم `ord(ch)` داخل تعبير قائمة:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**س: ماذا عن اللغات من اليمين إلى اليسار مثل العربية؟**  
ج: aocr تتضمن enum `ARABIC`. ستحتوي قائمة الأحرف على رموز عربية، لكن قد تحتاج إلى تفعيل عرض RTL في واجهة المستخدم اللاحقة.

---

## الخلاصة

أنت الآن تعرف **how to get OCR supported characters** باستخدام مكتبة aocr في بايثون، وكيفية التبديل بين **supported OCR languages**، ولماذا تُعد **listing OCR characters** خطوة أساسية لبناء خطوط أنابيب التعرف على النصوص بشكل موثوق. armed with the full script and the tips above, you can quickly verify language coverage, debug missing glyphs, and build smarter OCR‑driven applications.

هل أنت مستعد للخطوة التالية؟ جرّب ربط قائمة الأحرف هذه بفلتر قائمة كلمات مخصص، أو جرب محرك OCR آخر (Tesseract, EasyOCR) وقارن النتائج. كلما استكشفت أكثر، كلما تحسنت حلول OCR الخاصة بك.

Happy coding, and may your character sets always be complete!

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شاملة مع شروحات خطوة‑بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}