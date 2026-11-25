---
category: general
date: 2026-06-06
description: 'دليل مجموعة أحرف OCR: تعلم كيفية استخدام محرك OCR لسرد الأحرف المدعومة
  للخطوط اللاتينية والسيريلية مع أمثلة بايثون كاملة.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: ar
og_description: 'دليل مجموعة أحرف OCR: اكتشف كيفية استخدام محرك OCR في بايثون لسرد
  الأحرف المدعومة لمختلف النصوص، مع كود ونصائح كاملة.'
og_title: مجموعة أحرف OCR – استرجاع واستخدام محرك OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: مجموعة أحرف OCR – استرجاع واستخدام محرك OCR في بايثون
url: /ar/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# مجموعة أحرف OCR – استرجاع واستخدام محرك OCR في بايثون

هل تريد معرفة **ocr character set** التي تدعمها مكتبتك؟ في هذا الدرس سنوضح لك كيفية **use OCR engine** لاستعلام الأحرف المدعومة لمختلف الأنظمة الكتابية، ولماذا هذا مهم للمشاريع الواقعية.

إذا سبق لك أن حدقت في شاشة فارغة متسائلًا لماذا بعض الحروف لا تظهر أبدًا بعد معالجة OCR، فأنت لست وحدك. غالبًا ما يكون الجواب مخفيًا في مجموعة الأحرف التي يعرفها المحرك. بنهاية هذا الدليل ستتمكن من:

* سرد كل حرف يمكن لمحرك OCR التعرف عليه لنظام كتابة معين.  
* التعامل مع الحالات التي لا يكون فيها نظام الكتابة مدعومًا.  
* دمج معلومات مجموعة الأحرف في التحقق اللاحق أو منطق واجهة المستخدم.

لا حيل سحرية في صندوق أسود—فقط بايثون عادي، بضع أسطر من الشيفرة، وقليل من الشرح.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من أن لديك:

* تثبيت Python 3.8+ (الكود يستخدم f‑strings).  
* مكتبة OCR التي توفر `ocr.OcrEngine` — في هذا المثال سنفترض أن الحزمة المسماة `ocr` مثبتة بالفعل عبر `pip install ocr-lib`.  
* إلمام أساسي بنظام الاستيراد في بايثون وطباعة القيم.

إذا كنت تفتقد المكتبة، شغّل:

```bash
pip install ocr-lib
```

هذا كل شيء—لا حاجة إلى ملفات ثنائية إضافية أو تبعيات أصلية لاستعلام مجموعة الأحرف الأساسية التي سنجريها.

## الخطوة 1: تهيئة كائن محرك OCR

إنشاء كائن المحرك هو أول شيء تقوم به عندما **use OCR engine**. فكر فيه كتشغيل الماسح؛ بدون ذلك لا يمكنك طرح أي أسئلة.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

فئة `OcrEngine` هي غلاف خفيف الوزن حول محرك التعرف الأساسي. لا يبدأ معالجة ثقيلة حتى تطلب شيئًا، لذا فإن تكلفة بدء التشغيل ضئيلة.

> **نصيحة محترف:** إذا كان تطبيقك ينشئ العديد من كائنات المحرك، أعد استخدام كائن واحد. هذا يوفر الذاكرة ويقلل من زمن التهيئة.

## الخطوة 2: استعلام مجموعة أحرف OCR لنظام كتابة محدد

الآن بعد أن لدينا محركًا، يمكننا سؤاله عن الأحرف التي يعرفها لنظام كتابة معين. الطريقة `get_supported_characters(script_name)` تُرجع قائمة Python `list` من أحرف Unicode.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

تشغيل المقتطف أعلاه يطبع شيئًا مثل:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

المخرجات الدقيقة تعتمد على نسخة مكتبة OCR، لكنك ستحصل دائمًا على قائمة مسطحة من الأحرف. إذا كنت تحتاج إلى الأحرف الكبيرة والصغيرة معًا، ما عليك سوى طلب نظام `"Latin"` ثم تطبيق `.lower()` على كل عنصر، أو استعلام نظام منفصل `"Latin‑lower"` إذا كانت المكتبة تميزهما.

### لماذا هذا مهم؟

عند تمرير صورة تحتوي على علامات تشكيل غير شائعة (مثل “ñ” أو “ø”)، قد يستبدل محرك OCR هذه الأحرف بصمت بمكان حامل أو يتجاهلها تمامًا. معرفة **ocr character set** مسبقًا يتيح لك التحقق المسبق من الإدخال، تحذير المستخدمين، أو اللجوء إلى محرك مختلف.

## الخطوة 3: استرجاع الأحرف لنظام كتابة آخر – مثال على السيريلي

تعمل نفس الطريقة مع أي نظام كتابة يدعي المحرك دعمه. لنرى ما يحدث مع السيريلي.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

مخرجات نموذجية:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

إذا كان المحرك **لا** يدعم النظام المطلوب، عادةً ما يرفع استثناء `ValueError` (أو يُرجع قائمة فارغة حسب التنفيذ). دعنا نحمي الكود من ذلك.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

## الخطوة 4: تصور مجموعة أحرف OCR (اختياري)

أحيانًا تساعد الصورة السريعة، خاصةً عندما تحتاج إلى إظهار أصحاب المصلحة أي الأحرف مغطاة. أدناه مثال بسيط يستخدم `matplotlib` لرسم شبكة من الأحرف.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Image alt text:** ![مخطط مجموعة أحرف OCR](ocr_character_set.png){alt="نظرة عامة على مجموعة أحرف OCR"}

المخطط ليس ضروريًا للحل الأساسي، لكنه يوضح كيف يمكنك **use OCR engine** للبيانات الوصفية بعيدًا عن الطباعة العادية.

## الخطوة 5: دمج مجموعة الأحرف في سير العمل الواقعي

الآن بعد أن يمكننا استرجاع **ocr character set**، لنرى سيناريو عملي: التحقق من مخرجات OCR قبل تخزينها في قاعدة البيانات.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

هذا النمط يمنع تسرب البيانات غير الصالحة إلى الأنابيب اللاحقة، وهو نقطة ألم شائعة عند التعامل مع مستندات متعددة اللغات.

## الأخطاء الشائعة والحالات الحدية

| المشكلة | سبب حدوثها | كيفية التجنب |
|---------|------------|--------------|
| **خطأ في اسم النظام الكتابي** (مثال: `"Cyrillic "` مع مساحة زائدة) | المحرك يتعامل مع السلسلة حرفيًا ولا يستطيع العثور على النظام الكتابي. | قم بإزالة المسافات: `script.strip()` قبل استدعاء `get_supported_characters`. |
| **قائمة أحرف فارغة** | بعض المحركات تعرض نظام كتابة لكنه لم يتم تحميل نموذج اللغة بعد. | استدعِ `engine.load_language_model(script)` إذا كانت المكتبة توفر هذه الطريقة، أو تأكد من وجود ملفات النموذج. |
| **مشكلات تطبيع Unicode** | قد تظهر أحرف مثل “é” مركبة (`\u00E9`) أو مفككة (`e\u0301`). | قم بتطبيع السلاسل باستخدام `unicodedata.normalize('NFC', text)` قبل التحقق. |
| **الأداء مع الأنظمة الكبيرة** (مثال: الصينية) | استرجاع آلاف الأحرف قد يكون بطيئًا. | احفظ النتيجة في الذاكرة بعد الاستدعاء الأول؛ معظم التطبيقات تحتاج القائمة مرة واحدة فقط. |

## مثال كامل يعمل

وضع كل شيء معًا، إليك سكربت واحد يمكنك نسخه ولصقه وتشغيله:

```python
import ocr
import matplotlib.pyplot as plt

def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose OCR Tutorial – Optical Character Recognition](/ocr/english/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}