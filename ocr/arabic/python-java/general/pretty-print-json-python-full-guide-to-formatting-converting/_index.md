---
category: general
date: 2026-06-16
description: اطبع JSON في بايثون بشكل جميل بسرعة وتعلم كيفية تحويل JSON إلى dict أو
  تحميل سلسلة JSON في بايثون للتعامل مع البيانات. دليل خطوة بخطوة.
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: ar
og_description: تنسيق JSON في بايثون بشكل جميل وشاهد فورًا كيفية تحويل JSON إلى dict
  أو تحميل سلسلة JSON في بايثون. إتقان التعامل مع JSON في دقائق.
og_title: تنسيق جميل لJSON في بايثون – دليل كامل للتنسيق والتحويل
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: طباعة منسقة لملف JSON في بايثون – دليل كامل للتنسيق والتحويل
url: /ar/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pretty Print JSON Python – دليل كامل للتنسيق والتحويل

هل احتجت يومًا إلى **pretty print JSON Python** وتساءلت لماذا يكون الإخراج دائمًا في سطر واحد غير قابل للقراءة؟ لست وحدك. في العديد من المشاريع تكون سلسلة JSON الخام فوضى متشابكة، مما يجعل عملية تصحيح الأخطاء تشبه البحث عن إبرة في كومة قش.  

الأخبار السارة؟ باستخدام عدد قليل فقط من الدوال المدمجة يمكنك تحويل تلك الكتلة الفوضوية إلى عرض منسق بشكل جميل، ثم **convert JSON to dict** لمعالجة سلسة في المراحل اللاحقة. في هذا الدرس سنستعرض كل خطوة — من تحميل سلسلة JSON في بايثون إلى التكرار على بياناتها — لتتمكن من التركيز على المنطق بدلاً من القتال مع التنسيق.

## ما يغطيه هذا الدرس

- كيفية **pretty print JSON Python** باستخدام `json.dumps` مع معامل `indent`.  
- الطريقة الدقيقة لـ **load JSON string Python** إلى قاموس أصلي.  
- تحويل القاموس الناتج إلى كائنات بايثون مفيدة، بما في ذلك مثال عملي يطبع كل كلمة مع درجة الثقة الخاصة بها.  
- المشكلات الشائعة (مثل التعامل مع الأحرف غير ASCII) والحلول السريعة.  
- سكريبت كامل قابل للتنفيذ يمكنك نسخه ولصقه وتعديله فورًا.

بنهاية هذا الدليل ستتمكن من تحويل أي حمولة JSON إلى صيغة قابلة للقراءة للإنسان والتعامل معها باستخدام بايثون النقي — دون الحاجة إلى مكتبات خارجية.

---

## المتطلبات الأساسية

- Python 3.8 أو أحدث (وحدة `json` جزء من المكتبة القياسية).  
- فهم أساسي للقواميس والحلقات.  
- اختياريًا، محرك OCR أو أي خدمة تُرجع JSON—مثالنا يستخدم استدعاء `engine.recognize()` وهمي، لكن يمكنك استبداله بمصدر البيانات الخاص بك.

---

## الخطوة 1: Perform OCR (or Any JSON‑Generating) Recognition

أولًا، تحتاج إلى نتيجة متوافقة مع JSON. في العديد من سير عمل الرؤية الحاسوبية يُخرج محرك OCR كائنًا منظمًا يمكن تسلسله إلى JSON. إليك مثالًا بسيطًا كبديل:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **لماذا هذه الخطوة مهمة:**  
> حتى إذا لم تكن تقوم بعملية OCR، غالبًا ما تستقبل بيانات من API أو ملف أو طابور رسائل. يجب أن يكون الكائن قابلًا للتسلسل إلى JSON قبل أن نتمكن من **pretty print**ه.

---

## الخطوة 2: Pretty Print JSON Python

الآن نحول البيانات الخام إلى سلسلة منسقة بشكل جميل. معامل `indent` هو المسؤول عن ذلك.

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

سيظهر الإخراج هكذا:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **نصيحة احترافية:** استخدم `indent=4` إذا كنت تفضّل مسافات أوسع، أو أضف `sort_keys=True` لترتيب المفاتيح أبجديًا.

---

## الخطوة 3: Load JSON String Python → Native Dictionary

السلسلة المنسقة مفيدة للبشر، لكن بايثون يفضّل القواميس للعمل الفعلي. هنا نـ **load JSON string Python** إلى بنية أصلية.

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

سترى:

```
✅ Loaded dict type: <class 'dict'>
```

> **لماذا نفعل ذلك:**  
> القواميس تمنحك عمليات بحث O(1)، بيانات قابلة للتعديل، وتكامل سلس مع بقية نظام بايثون. محاولة العمل مباشرةً مع سلسلة JSON ستجبرك على تحليل نصي مرهق.

---

## الخطوة 4: Iterate Over Recognized Words – A Real‑World Use Case

لنستخرج كل كلمة ودرجة ثقتها. هذا يوضح كلًا من **convert json to dict** (القاموس الذي لدينا) والتكرار العملي.

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

الإخراج المتوقع:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **نصيحة لحالات الحافة:** إذا كان من الممكن أن يفتقد JSON المفتاح `"words"`، احمِ نفسك من `KeyError`:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## الخطوة 5: Handling Non‑ASCII Characters (Unicode Support)

غالبًا ما تُعيد محركات OCR أحرفًا مثل “é” أو “ü”. الدالة `json.dumps` الافتراضية تهربها كـ `\u00e9`. لجعلها قابلة للقراءة، مرّر `ensure_ascii=False`.

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

الآن يظهر الإخراج **café** بدلاً من النسخة المهربة. هذا أمر أساسي عندما تقوم بـ **convert json to dict** لاحقًا؛ القاموس سيحتوي على سلاسل Unicode صحيحة.

---

## الخطوة 6: Saving and Reloading the Pretty‑Printed JSON (Optional)

أحيانًا تريد حفظ JSON المنسق إلى ملف لفحصه لاحقًا.

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

سيحتوي الملف على JSON المنسق بشكل جميل، وستقوم `json.load` بتحليله تلقائيًا إلى قاموس مرة أخرى.

---

## الخطوة 7: Putting It All Together – A One‑File Solution

فيما يلي سكريبت مستقل يدمج كل خطوة تم مناقشتها. يمكنك وضعه في ملف باسم `pretty_json_demo.py` وتشغيله.

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

شغّله:

```bash
python pretty_json_demo.py
```

سترى JSON المنسق، نوع القاموس، كل كلمة مع درجة الثقة، وإصدار صديق للـ Unicode محفوظ في `pretty_output.json`.  

**هذه هي القصة كاملة** — من مخرجات OCR الخام إلى قاموس بايثون نظيف وقابل للتعامل.

---

## الأسئلة المتكررة (FAQs)

| السؤال | الجواب |
|----------|--------|
| **هل أحتاج إلى مكتبة خارجية؟** | لا. وحدة `json` المدمجة تتعامل مع كل من التنسيق والتحميل. |
| **ماذا لو كان JSON كبيرًا؟** | استخدم `json.dump` مع مقبض ملف لتجنب تحميل كل شيء في الذاكرة؛ لا يزال بإمكانك ضبط `indent` للحصول على ملف منسق. |
| **هل يمكنني فرز المفاتيح؟** | نعم—أضف `sort_keys=True` إلى `json.dumps` للحصول على ترتيب حتمي، مما يساعد في الاختبارات القائمة على الفروقات. |
| **كيف أتعامل مع JSON غير صالح؟** | غلف `json.loads` في كتلة `try/except json.JSONDecodeError` وسجّل السلسلة المسببة للمشكلة. |
| **هل هناك بديل أسرع؟** | للحمولات الضخمة، المكتبات مثل `orjson` أو `ujson` أسرع، لكنها لا تدعم `indent` خارج‑ |

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)
- [كيفية استخدام Aspose OCR للحصول على نتائج JSON في التعرف على الصور](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [كيفية استخدام Aspose OCR لنتائج JSON في التعرف على الصور](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}