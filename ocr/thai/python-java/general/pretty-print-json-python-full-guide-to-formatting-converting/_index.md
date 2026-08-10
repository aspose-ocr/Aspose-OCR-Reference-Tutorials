---
category: general
date: 2026-06-16
description: พรีตีพริ้นท์ JSON ด้วย Python อย่างรวดเร็วและเรียนรู้วิธีแปลง JSON เป็น
  dict หรือโหลดสตริง JSON ด้วย Python เพื่อการจัดการข้อมูล ขั้นตอนแบบทีละขั้นตอน
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: th
og_description: ทำการพิมพ์ JSON ใน Python อย่างสวยงามและดูวิธีแปลง JSON เป็น dict
  หรือโหลดสตริง JSON ใน Python ได้ทันที เรียนรู้การจัดการ JSON อย่างเชี่ยวชาญในไม่กี่นาที
og_title: การพิมพ์สวย JSON ด้วย Python – คู่มือการจัดรูปแบบและการแปลงอย่างครบถ้วน
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
title: การพิมพ์สวย JSON ด้วย Python – คู่มือเต็มเรื่องการจัดรูปแบบและการแปลง
url: /th/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การพิมพ์ JSON Python อย่างสวยงาม – คู่มือเต็มสำหรับการจัดรูปแบบและการแปลง

เคยต้องการ **pretty print JSON Python** แล้วสงสัยว่าทำไมผลลัพธ์มักออกมาเป็นบรรทัดเดียวที่อ่านไม่ออกหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการสตริง JSON ดิบมักเป็นกองรกที่ทำให้การดีบักเหมือนการหาสิ่งที่หายไปในกองหญ้า  

ข่าวดีคือ? ด้วยฟังก์ชันในตัวไม่กี่ตัวคุณก็สามารถเปลี่ยนข้อมูลกองรกนั้นให้เป็นมุมมองที่จัดย่อหน้าอย่างสวยงาม แล้ว **convert JSON to dict** เพื่อการประมวลผลต่อเนื่องที่ราบรื่น ในบทแนะนำนี้เราจะเดินผ่านทุกขั้นตอน—from การโหลดสตริง JSON ใน Python ไปจนถึงการวนลูปข้อมูล—เพื่อให้คุณมุ่งเน้นที่ตรรกะแทนการต่อสู้กับรูปแบบ

## สิ่งที่บทแนะนำนี้ครอบคลุม

- วิธี **pretty print JSON Python** ด้วย `json.dumps` พร้อมอาร์กิวเมนต์ `indent`  
- วิธี **load JSON string Python** ให้เป็นดิกชันนารีพื้นเมือง  
- การแปลงดิกชันนารีที่ได้เป็นอ็อบเจ็กต์ Python ที่ใช้งานได้ รวมตัวอย่างที่พิมพ์แต่ละคำพร้อมคะแนนความเชื่อมั่น  
- จุดบกพร่องทั่วไป (เช่น การจัดการอักขระที่ไม่ใช่ ASCII) และวิธีแก้อย่างรวดเร็ว  
- สคริปต์เต็มที่สามารถคัดลอก‑วางและปรับใช้ได้ทันที

เมื่ออ่านจบคุณจะสามารถแปลง payload JSON ใด ๆ ให้เป็นรูปแบบที่มนุษย์อ่านได้และจัดการด้วย Python ธรรมดา—ไม่ต้องพึ่งไลบรารีภายนอก

---

## ข้อกำหนดเบื้องต้น

- Python 3.8 หรือใหม่กว่า (โมดูล `json` เป็นส่วนหนึ่งของไลบรารีมาตรฐาน)  
- ความเข้าใจพื้นฐานเกี่ยวกับดิกชันนารีและลูป  
- ตัวเลือก: เครื่อง OCR หรือบริการใด ๆ ที่คืนค่าเป็น JSON—ตัวอย่างของเราจะใช้การเรียก `engine.recognize()` จำลองเท่านั้น แต่คุณสามารถแทนที่ด้วยแหล่งข้อมูลของคุณเองได้

---

## ขั้นตอนที่ 1: ทำ OCR (หรือการสร้าง JSON) ใด ๆ

ก่อนอื่นคุณต้องมีผลลัพธ์ที่เข้ากันได้กับ JSON ในหลาย workflow ของคอมพิวเตอร์วิชั่นเครื่อง OCR จะส่งออกอ็อบเจ็กต์ที่มีโครงสร้างซึ่งสามารถซีเรียลไลซ์เป็น JSON ได้ นี่คือตัวอย่าง placeholder ขั้นต่ำ:

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

> **ทำไมขั้นตอนนี้ถึงสำคัญ:**  
> แม้ว่าคุณจะไม่ได้ทำ OCR ก็ตาม คุณมักจะได้รับข้อมูลจาก API, ไฟล์, หรือคิวข้อความ อ็อบเจ็กต์ต้องสามารถซีเรียลไลซ์เป็น JSON ก่อนที่เราจะ **pretty print** ได้

---

## ขั้นตอนที่ 2: Pretty Print JSON Python

ตอนนี้เราจะเปลี่ยนข้อมูลดิบให้เป็นสตริงที่จัดย่อหน้าอย่างสวยงาม พารามิเตอร์ `indent` ทำหน้าที่หลัก

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

ผลลัพธ์จะเป็นดังนี้:

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

> **เคล็ดลับ:** ใช้ `indent=4` หากต้องการช่องว่างกว้างขึ้น หรือเพิ่ม `sort_keys=True` เพื่อเรียงคีย์ตามตัวอักษร

---

## ขั้นตอนที่ 3: Load JSON String Python → ดิกชันนารีพื้นเมือง

สตริงที่จัดย่อหน้าแล้วเหมาะกับมนุษย์ แต่ Python ชอบดิกชันนารีสำหรับการทำงานจริง นี่คือจุดที่เราจะ **load JSON string Python** ให้เป็นโครงสร้างพื้นเมือง

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

คุณจะเห็น:

```
✅ Loaded dict type: <class 'dict'>
```

> **ทำไมเราต้องทำเช่นนี้:**  
> ดิกชันนารีให้การค้นหา O(1), ข้อมูลที่แก้ไขได้, และการบูรณาการที่ราบรื่นกับระบบนิเวศของ Python การทำงานโดยตรงกับสตริง JSON จะทำให้ต้องพาร์สสตริงที่ยุ่งยาก

---

## ขั้นตอนที่ 4: วนลูปคำที่ถูกจดจำ – กรณีใช้งานจริง

เราจะดึงแต่ละคำและคะแนนความเชื่อมั่นของมัน ตัวอย่างนี้แสดงทั้ง **convert json to dict** (ดิกชันนารีที่เรามีอยู่แล้ว) และการวนลูปที่ใช้งานได้จริง

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

ผลลัพธ์ที่คาดหวัง:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **เคล็ดลับกรณีขอบ:** หาก JSON อาจไม่มีคีย์ `"words"` ให้ป้องกัน `KeyError`:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## ขั้นตอนที่ 5: การจัดการอักขระที่ไม่ใช่ ASCII (รองรับ Unicode)

เครื่อง OCR มักคืนอักขระเช่น “é” หรือ “ü” ค่าเริ่มต้นของ `json.dumps` จะเอสเคปเป็น `\u00e9` เพื่อให้แสดงได้อย่างอ่านง่าย ให้ส่ง `ensure_ascii=False`

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

ตอนนี้ผลลัพธ์จะแสดง **café** แทนเวอร์ชันที่เอสเคป นี่สำคัญเมื่อคุณ **convert json to dict** ต่อไป; ดิกชันนารีจะมีสตริง Unicode ที่ถูกต้อง

---

## ขั้นตอนที่ 6: บันทึกและโหลด JSON ที่จัดย่อหน้า (ทางเลือก)

บางครั้งคุณอาจต้องการเก็บ JSON ที่จัดย่อหน้าไว้ในไฟล์เพื่อการตรวจสอบในภายหลัง

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

ไฟล์จะมี JSON ที่จัดย่อหน้าอย่างสวยงาม และ `json.load` จะพาร์สกลับเป็นดิกชันนารีโดยอัตโนมัติ

---

## ขั้นตอนที่ 7: รวมทุกอย่างไว้ในไฟล์เดียว – โซลูชันแบบ One‑File

ด้านล่างเป็นสคริปต์อิสระที่รวมทุกขั้นตอนที่อธิบายไว้ คุณสามารถวางลงในไฟล์ชื่อ `pretty_json_demo.py` แล้วรันได้

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

รันสคริปต์:

```bash
python pretty_json_demo.py
```

คุณจะเห็น JSON ที่จัดย่อหน้า, ประเภทดิกชันนารี, แต่ละคำพร้อมคะแนนความเชื่อมั่น, และเวอร์ชันที่รองรับ Unicode ที่บันทึกไว้ใน `pretty_output.json`  

**นี่คือทั้งหมด** — ตั้งแต่ผลลัพธ์ OCR ดิบจนถึงดิกชันนารี Python ที่สะอาดและใช้งานได้

---

## คำถามที่พบบ่อย (FAQs)

| คำถาม | คำตอบ |
|----------|--------|
| **ต้องใช้ไลบรารีภายนอกหรือไม่?** | ไม่จำเป็น โมดูล `json` ที่มาพร้อม Python จัดการการพิมพ์สวยและการโหลดได้ทั้งหมด |
| **ถ้า JSON ของฉันมีขนาดใหญ่จะทำอย่างไร?** | ใช้ `json.dump` พร้อมไฟล์แฮนด์เดิลเพื่อหลีกเลี่ยงการโหลดทั้งหมดเข้าสู่หน่วยความจำ; ยังคงตั้ง `indent` เพื่อให้ไฟล์สวย |
| **สามารถเรียงคีย์ได้หรือไม่?** | ได้ — เพิ่ม `sort_keys=True` ให้กับ `json.dumps` เพื่อให้คีย์เรียงตามลำดับอักษร ซึ่งช่วยในการทดสอบแบบ diff |
| **จะจัดการกับ JSON ที่ผิดรูปแบบอย่างไร?** | ห่อ `json.loads` ด้วย `try/except json.JSONDecodeError` แล้วบันทึกสตริงที่มีปัญหา |
| **มีทางเลือกที่เร็วกว่าไหม?** | สำหรับ payload ขนาดมหาศาล ไลบรารีอย่าง `orjson` หรือ `ujson` เร็วกว่า แต่ไม่มีการสนับสนุน `indent` |

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้เกี่ยวกับหัวข้อที่ใกล้เคียงและต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cómo usar Aspose OCR para obtener resultados JSON en reconocimiento de imágenes](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Wie man Aspose OCR für JSON‑Ergebnisse bei der Bilderkennung verwendet](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}