---
category: general
date: 2026-06-25
description: รับอักขระที่รองรับ OCR อย่างรวดเร็วด้วยไลบรารี aocr. เรียนรู้วิธีแสดงรายการอักขระ
  OCR, ตั้งค่าภาษา, และดีบักเอนจิน OCR ของคุณใน Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: th
og_description: รับอักขระที่รองรับ OCR ด้วย aocr. คู่มือนี้จะแสดงวิธีการแสดงรายการอักขระ
  OCR, เลือกภาษา, และจัดการกรณีขอบใน Python.
og_title: รับอักขระที่รองรับโดย OCR ใน Python – คู่มือเต็ม
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
title: รับอักขระที่รองรับโดย OCR ใน Python – คู่มือฉบับสมบูรณ์
url: /th/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับตัวอักษรที่รองรับ OCR ใน Python – คู่มือครบถ้วน

เคยสงสัยหรือไม่ว่า **จะรับตัวอักษรที่รองรับ OCR** สำหรับภาษาที่ต้องการอย่างไรเมื่อคุณกำลังทดลองกับเครื่องมือ OCR? คุณไม่ได้อยู่คนเดียว ไม่ว่าคุณจะกำลังสร้างสแกนเนอร์ใบเสร็จหรือเครื่องแยกเอกสารหลายภาษา การรู้ว่าตัวอักษรใดบ้างที่เครื่องของคุณสามารถจดจำได้เป็นสิ่งที่ช่วยชีวิต ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด—การติดตั้งไลบรารี, การตั้งค่าภาษา, และสุดท้ายการแสดงรายการตัวอักษรเหล่านั้น—เพื่อให้คุณสามารถดีบักและปรับแต่ง pipeline OCR ของคุณได้ในไม่กี่นาที

เราจะใช้ไลบรารี **aocr** ซึ่งเป็น engine OCR ขนาดเบาที่ทำให้การสอบถามความสามารถของภาษาเป็นเรื่องง่าย หลังจากอ่านคู่มือนี้แล้วคุณจะสามารถ **แสดงรายการตัวอักษร OCR**, สลับระหว่าง **ภาษาที่รองรับ OCR**, และแม้กระทั่งตรวจพบช่องว่างของการสนับสนุนก่อนที่มันจะส่งผลกระทบต่อการผลิต

---

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมี:

* Python 3.8 หรือใหม่กว่า (แพ็กเกจ aocr ไม่รองรับ 3.7)
* เทอร์มินัลหรือ command prompt ที่เชื่อมต่ออินเทอร์เน็ต
* ความคุ้นเคยพื้นฐานกับการเขียนสคริปต์ Python (ถ้าคุณเคยใช้ `print()` มาก่อนก็พร้อม)

ไม่มีการพึ่งพาไลบรารีภายนอกที่หนัก—เพียงแพ็กเกจ `aocr` จาก pip เท่านั้น

---

## ติดตั้งไลบรารี aocr (OCR Engine Python)

สิ่งแรกที่คุณต้องการคือการติดตั้ง **OCR engine Python** ที่ทำงานได้ ไลบรารี aocr มีอยู่บน PyPI ดังนั้นคำสั่ง pip เพียงหนึ่งบรรทัดก็เพียงพอ:

```bash
pip install aocr
```

หากคุณใช้ virtual environment (ขอแนะนำอย่างยิ่ง) ให้เปิดใช้งานก่อน:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **เคล็ดลับ:** ระบุเวอร์ชัน (`pip install aocr==1.2.4`) เพื่อหลีกเลี่ยงการเปลี่ยนแปลง API ที่ไม่คาดคิดในภายหลัง

---

## เลือกภาษา (Supported OCR Languages)

aocr มาพร้อมกับชุดภาษาที่ฝังมาในตัวหลายชุด แต่ละชุดกำหนดชุด Unicode code point ที่ engine สามารถจดจำได้ เพื่อสอบถามชุดเหล่านี้คุณต้องตั้งค่า attribute `language` บน instance ของ engine

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

คุณสามารถเปลี่ยน `aocr.Language.ENGLISH` เป็นค่า enum ใดก็ได้ (`FRENCH`, `GERMAN` เป็นต้น) หากคุณพยายามกำหนดภาษาที่ไม่ได้รวมอยู่ในแพ็กเกจ aocr จะเกิด `ValueError` นั่นคือเหตุผลที่ควรตรวจสอบ **รายการภาษาที่รองรับ OCR** ก่อน:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## ดึงชุดตัวอักษร (Get OCR Supported Characters)

ต่อไปคือหัวใจของบทแนะนำ: **รับตัวอักษรที่รองรับ OCR** จริง ๆ Engine มีเมธอดที่สะดวกชื่อ `get_supported_characters()` ซึ่งจะคืนค่าเป็นรายการของสตริงตัวอักษรเดี่ยว

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

เบื้องหลัง aocr จะอ่านไฟล์ JSON ที่บรรจุอยู่ในแพ็กเกจภาษาและแปลงแต่ละ Unicode code point ให้เป็นสตริง Python ผลลัพธ์จะเป็นแบบ deterministic หมายความว่าคุณจะได้รายการเดียวกันทุกครั้งที่รันสคริปต์บนเวอร์ชันภาษาเดียวกัน

---

## แสดงจำนวนตัวอักษรที่รองรับ

การรู้จำนวนช่วยให้คุณประเมินขอบเขตการครอบคลุมได้อย่างรวดเร็ว สำหรับภาษาอังกฤษคุณมักจะเห็นหลายพันตัวอักษร (รวมถึงเครื่องหมายวรรคตอนและตัวเลข)

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

การเรียก `len()` มีค่า O(1) เพราะ Python เก็บความยาวของรายการไว้ภายในอยู่แล้ว จึงไม่มีผลกระทบต่อประสิทธิภาพแม้กับอักษรจำนวนมาก

---

## แสดงตัวอย่าง 100 ตัวอักษรแรกที่รองรับ

การตรวจสอบแบบมองเห็นอย่างรวดเร็วสามารถบ่งบอกว่า engine มีสัญลักษณ์ที่คุณต้องการหรือไม่ (เช่นสัญลักษณ์ยูโรหรือเครื่องหมายอัญประกาศอัจฉริยะ) ให้พิมพ์ตัวอักษรแรกร้อยตัว:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

การทำ `join` จะเชื่อมสไลซ์เป็นสตริงเดียว ซึ่งอ่านง่ายกว่าการพิมพ์รายการ Python

---

## สคริปต์เต็ม – ทุกขั้นตอนในที่เดียว

ด้านล่างเป็นตัวอย่างที่ทำงานได้ครบถ้วนซึ่งเชื่อมทุกขั้นตอนเข้าด้วยกัน บันทึกเป็น `list_supported_chars.py` แล้วรันด้วย `python list_supported_chars.py` จากเทอร์มินัลของคุณ

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

**ผลลัพธ์ที่คาดหวัง (ตัดทอนเพื่อความกระชับ):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

จำนวนที่แน่นอนอาจแตกต่างกันเล็กน้อยขึ้นอยู่กับเวอร์ชัน aocr แต่คุณจะเห็นอักษรจำนวนมากพร้อมเครื่องหมายวรรคตอนทั่วไปเสมอ

---

## การจัดการกรณีขอบ

### ถ้าแพ็กเกจภาษาไม่มีอยู่?

หากคุณร้องขอภาษาที่ไม่ได้บรรจุในแพ็กเกจ `aocr.Language` จะไม่มี enum นั้นและคุณจะเจอ `AttributeError` ป้องกันด้วยการตรวจสอบอย่างง่าย:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### รายการตัวอักษรว่าง

บางภาษาที่หายากอาจคืนรายการว่าง หากข้อมูลการฝึกไม่ครบ ในกรณีนั้นคุณสามารถ fallback ไปยังค่าเริ่มต้น (เช่นอังกฤษ) หรือให้คำเตือน:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### การทำ Normalization ของ Unicode

รายการอาจมีตัวอักษรที่รวมกัน (เช่น “é” เป็น `e` + acute accent) หากขั้นตอนต่อไปของคุณคาดหวัง glyph ที่ประกอบไว้ล่วงหน้า ให้ทำขั้นตอน Normalization:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## เคล็ดลับสำหรับโครงการจริง

* **แคชรายการตัวอักษร** – หากคุณประมวลผลภาพหลายพันภาพ การเรียก `get_supported_characters()` ทุกรอบจะเพิ่มภาระที่ไม่จำเป็น เก็บรายการไว้ในตัวแปรระดับโมดูลหรือบันทึกเป็น JSON เพื่อใช้ซ้ำในภายหลัง
* **ตรวจสอบความสอดคล้องข้ามภาษา** – เมื่อรองรับหลายภาษาในแอปเดียวกัน ให้ทำ intersect ชุดตัวอักษรเพื่อหา subset ที่ใช้ร่วมกัน ช่วยออกแบบ UI ที่สอดคล้องในทุก locale
* **ดีบักความล้มเหลวของ OCR** – หาก engine จำแนก glyph ผิด ให้เปรียบเทียบอักขระที่ผิดพลาดกับผลลัพธ์ของ `list_supported_chars` หากไม่มีในรายการคุณได้พบช่องว่างของการครอบคลุมที่อาจต้องฝึกโมเดลใหม่
* **ผสานกับฟอนต์ที่กำหนดเอง** – aocr เคารพช่วง Unicode แต่คุณภาพการแสดงผลอาจแตกต่างตามฟอนต์ ทดสอบตัวอักษรที่รองรับด้วยฟอนต์เดียวกับที่ใช้ใน production เพื่อหลีกเลี่ยงความประหลาดใจ

---

## คำถามที่พบบ่อย

**ถาม: วิธีนี้ทำงานกับ aocr เวอร์ชัน 2.x ได้หรือไม่?**  
ตอบ: ใช่, เมธอด `get_supported_characters()` มีความเสถียรระหว่าง 1.x และ 2.x การเปลี่ยนแปลงเดียวคือ enum ของภาษาได้ย้ายไปที่ `aocr.languages`

**ถาม: ฉันจะรับ Unicode code point ของแต่ละตัวอักษรได้อย่างไร?**  
ตอบ: ทำได้เลย ใช้ `ord(ch)` ภายใน list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**ถาม: แล้วสคริปต์สำหรับภาษาเขียนจากขวาไปซ้ายอย่าง Arabic ล่ะ?**  
ตอบ: aocr มี enum `ARABIC` รายการตัวอักษรจะมี glyph ของ Arabic แต่คุณอาจต้องเปิดใช้งานการเรนเดอร์ RTL ใน UI ของคุณ

---

## สรุป

คุณได้เรียนรู้ **วิธีรับตัวอักษรที่รองรับ OCR** ด้วยไลบรารี aocr ใน Python, วิธีสลับระหว่าง **ภาษาที่รองรับ OCR**, และเหตุผลที่ **การแสดงรายการตัวอักษร OCR** มีความสำคัญต่อ pipeline การรับรู้ข้อความที่แข็งแรง ด้วยสคริปต์เต็มและเคล็ดลับข้างต้น คุณสามารถตรวจสอบการครอบคลุมของภาษา, ดีบัก glyph ที่หายไป, และสร้างแอปพลิเคชันที่ขับเคลื่อนด้วย OCR ได้อย่างฉลาด

พร้อมก้าวต่อไปหรือยัง? ลองจับคู่รายการตัวอักษรนี้กับฟิลเตอร์ word‑list แบบกำหนดเอง, หรือทดลองกับ engine OCR อื่น (Tesseract, EasyOCR) แล้วเปรียบเทียบผลลัพธ์ ยิ่งคุณสำรวจมากเท่าไหร่ โซลูชัน OCR ของคุณก็จะยิ่งดีขึ้น

ขอให้เขียนโค้ดสนุกและตัวอักษรของคุณครบถ้วนเสมอ!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่นในโปรเจกต์ของคุณ

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}