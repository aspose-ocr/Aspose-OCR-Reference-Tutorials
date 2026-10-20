---
category: general
date: 2026-04-26
description: ปกปิดหมายเลขบัตรเครดิตอย่างรวดเร็วด้วยการประมวลผลหลัง OCR ของ AsposeAI
  เรียนรู้การปฏิบัติตาม PCI, การปกปิดด้วย regular expression, และการทำความสะอาดข้อมูลในบทเรียนแบบขั้นตอนต่อขั้นตอน.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: th
og_description: ปกปิดหมายเลขบัตรเครดิตในผลลัพธ์ OCR ด้วย AsposeAI. บทเรียนนี้ครอบคลุมการปฏิบัติตามมาตรฐาน
  PCI, การปกปิดด้วย regular expression, และการทำความสะอาดข้อมูล.
og_title: ซ่อนหมายเลขบัตรเครดิต – คู่มือการประมวลผลหลัง OCR ด้วย Python อย่างเต็มรูปแบบ
tags:
- OCR
- Python
- security
title: ซ่อนหมายเลขบัตรเครดิตในผลลัพธ์ OCR – คู่มือ Python ฉบับสมบูรณ์
url: /th/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ซ่อนหมายเลขบัตรเครดิต – คู่มือ Python ฉบับสมบูรณ์

เคยต้องการ **ซ่อนหมายเลขบัตรเครดิต** ในข้อความที่มาจากเครื่อง OCR โดยตรงหรือไม่? คุณไม่ได้เป็นคนเดียว ในอุตสาหกรรมที่มีการควบคุม การเปิดเผย PAN (Primary Account Number) เต็มรูปแบบอาจทำให้คุณเจอปัญหากับผู้ตรวจสอบการปฏิบัติตาม PCI ข่าวดีคือ? ด้วยไม่กี่บรรทัดของ Python และ post‑processing hook ของ AsposeAI คุณสามารถซ่อนเลข 8 หลักตรงกลางโดยอัตโนมัติและอยู่ในความปลอดภัย

ในบทแนะนำนี้ เราจะเดินผ่านสถานการณ์จริง: การทำ OCR บนภาพใบเสร็จ แล้วใช้ฟังก์ชัน **OCR post‑processing** แบบกำหนดเองที่ทำความสะอาดข้อมูล PCI ใด ๆ เมื่อเสร็จคุณจะได้สคริปต์ที่นำกลับมาใช้ใหม่ได้ซึ่งสามารถใส่ลงใน workflow ของ AsposeAI ใดก็ได้ พร้อมกับเคล็ดลับเชิงปฏิบัติเพื่อจัดการกับกรณีขอบและการขยายโซลูชัน

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการลงทะเบียน post‑processor แบบกำหนดเองกับ **AsposeAI**.
- ทำไมวิธี **regular expression masking** ถึงเร็วและเชื่อถือได้.
- พื้นฐานของ **PCI compliance** ที่เกี่ยวข้องกับการทำความสะอาดข้อมูล.
- วิธีขยายรูปแบบเพื่อรองรับหลายรูปแบบบัตรหรือหมายเลขระหว่างประเทศ.
- ผลลัพธ์ที่คาดหวังและวิธีตรวจสอบว่าการซ่อนทำงานถูกต้องหรือไม่.

> **Prerequisites** – คุณควรมีสภาพแวดล้อม Python 3 ที่ทำงานได้, ติดตั้งแพคเกจ Aspose.AI for OCR (`pip install aspose-ocr`), และมีภาพตัวอย่าง (เช่น `receipt.png`) ที่มีหมายเลขบัตรเครดิต ไม่จำเป็นต้องใช้บริการภายนอกอื่นใด

---

## ขั้นตอนที่ 1: กำหนด Post‑Processor ที่ซ่อนหมายเลขบัตรเครดิต

หัวใจของวิธีแก้ปัญหาอยู่ในฟังก์ชันเล็ก ๆ ที่รับผลลัพธ์ OCR, รันขั้นตอน **regular expression masking**, และคืนข้อความที่ทำความสะอาดแล้ว

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**ทำไมวิธีนี้ถึงได้ผล:**  
- regex `(\d{4})\d{8}(\d{4})` จะจับตรงกับตัวเลขต่อเนื่อง 16 หลัก ซึ่งเป็นรูปแบบทั่วไปสำหรับ Visa, MasterCard และอื่น ๆ  
- โดยการจับสี่หลักแรกและสี่หลักสุดท้าย (`\1` และ `\2`) เราเก็บข้อมูลเพียงพอสำหรับการดีบัก ในขณะเดียวกันก็สอดคล้องกับกฎ **PCI compliance** ที่ห้ามเก็บ PAN เต็มรูปแบบ  
- การแทนที่ `\1****\2` จะซ่อนเลข 8 หลักตรงกลางที่เป็นข้อมูลสำคัญ ทำให้ `1234567812345678` กลายเป็น `1234****5678`

> **Pro tip:** หากคุณต้องการรองรับหมายเลข American Express ที่มี 15 หลัก ให้เพิ่มรูปแบบที่สองเช่น `r'(\d{4})\d{6}(\d{5})'` และทำการแทนที่ทั้งสองแบบต่อเนื่องกัน

---

## ขั้นตอนที่ 2: เริ่มต้น AsposeAI Engine

ก่อนที่เราจะผูก post‑processor ของเรา เราต้องมีอินสแตนซ์ของ OCR engine. AsposeAI มีโมเดล OCR และ API อย่างง่ายสำหรับการประมวลผลแบบกำหนดเอง

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**ทำไมต้องเริ่มต้นที่นี่?**  
การสร้างอ็อบเจ็กต์ `AsposeAI` ครั้งเดียวและนำกลับมาใช้ใหม่กับหลายภาพจะลดภาระการทำงาน เครื่องยังเก็บโมเดลภาษาไว้ในแคช ซึ่งทำให้การเรียกครั้งต่อไปเร็วขึ้น—สะดวกเมื่อคุณสแกนชุดใบเสร็จหลายใบ

---

## ขั้นตอนที่ 3: ลงทะเบียนฟังก์ชันการซ่อนแบบกำหนดเอง

AsposeAI มีเมธอด `set_post_processor` ที่ให้คุณเชื่อมต่อกับ callable ใดก็ได้ เราจะส่งฟังก์ชัน `mask_pci` ของเราพร้อมกับพจนานุกรมการตั้งค่า (ว่างเปล่าสำหรับตอนนี้)

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**เกิดอะไรขึ้นเบื้องหลัง?**  
เมื่อคุณเรียก `run_postprocessor` ภายหลัง AsposeAI จะส่งผลลัพธ์ OCR ดิบให้กับ `mask_pci`. ฟังก์ชันจะรับอ็อบเจ็กต์น้ำหนักเบา (`data`) ที่มีข้อความที่รับรู้แล้ว และคุณจะคืนสตริงใหม่ การออกแบบนี้ทำให้ส่วนหลักของ OCR ไม่ถูกแก้ไขขณะเดียวกันคุณสามารถบังคับใช้แนวทาง **data sanitization** ในที่เดียว

---

## ขั้นตอนที่ 4: รัน OCR บนภาพใบเสร็จ

ตอนนี้ engine รู้วิธีทำความสะอาดผลลัพธ์แล้ว เราจะส่งภาพเข้าไป เพื่อความสะดวกในบทแนะนำนี้ เราจะสมมติว่าคุณมีอ็อบเจ็กต์ `engine` ที่ตั้งค่าภาษาและความละเอียดแล้ว

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**เคล็ดลับ:** หากคุณไม่มีอ็อบเจ็กต์ที่ตั้งค่าไว้ล่วงหน้า คุณสามารถสร้างได้ด้วย:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

การเรียก `recognize_image` จะคืนอ็อบเจ็กต์ที่มีแอตทริบิวต์ `text` ซึ่งเก็บสตริงดิบที่ยังไม่ได้ซ่อน

---

## ขั้นตอนที่ 5: ใช้ Post‑Processor ที่ลงทะเบียนไว้

เมื่อได้ข้อมูล OCR ดิบแล้ว เราจะส่งต่อให้กับอินสแตนซ์ AI Engine Engine จะรันฟังก์ชัน `mask_pci` ที่เราลงทะเบียนไว้โดยอัตโนมัติ

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**ทำไมต้องใช้ `run_postprocessor` แทนการเรียกฟังก์ชันด้วยตนเอง?**  
การทำเช่นนี้ทำให้ workflow สม่ำเสมอ โดยเฉพาะเมื่อคุณมี post‑processor หลายตัว (เช่น การตรวจสอบการสะกด, การตรวจจับภาษา) AsposeAI จะจัดคิวตามลำดับที่คุณลงทะเบียน เพื่อรับประกันผลลัพธ์ที่กำหนดได้

---

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์ที่ทำความสะอาดแล้ว

สุดท้าย เรามาพิมพ์ข้อความที่ทำความสะอาดแล้วและยืนยันว่าหมายเลขบัตรเครดิตใด ๆ ถูกซ่อนอย่างถูกต้อง

```python
print(final_result.text)
```

**ผลลัพธ์ที่คาดหวัง** (ส่วนย่อย):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

หากใบเสร็จไม่มีหมายเลขบัตร ข้อความจะคงเดิม—ไม่มีอะไรต้องซ่อน ไม่มีอะไรต้องกังวล

---

## การจัดการกรณีขอบและรูปแบบทั่วไป

### หมายเลขบัตรหลายใบในเอกสารเดียว

หากใบเสร็จมี PAN มากกว่าหนึ่ง (เช่น บัตรสมาชิกและบัตรชำระเงิน) regex จะทำงานทั่วทั้งข้อความและซ่อนทุกการจับคู่โดยอัตโนมัติ ไม่ต้องเขียนโค้ดเพิ่มเติม

### รูปแบบที่ไม่เป็นมาตรฐาน

บางครั้ง OCR จะใส่ช่องว่างหรือขีด (`1234 5678 1234 5678` หรือ `1234-5678-1234-5678`). ขยายรูปแบบเพื่อไม่สนใจอักขระเหล่านั้น:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

ส่วนเพิ่ม `[ -]?` จะยอมรับช่องว่างหรือขีดที่เป็นตัวเลือกระหว่างบล็อกตัวเลข

### บัตรระหว่างประเทศ

สำหรับ PAN 19 หลักที่ใช้ในบางภูมิภาค คุณสามารถขยายรูปแบบได้:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

จำไว้ว่า **PCI compliance** ยังต้องการการซ่อนเลขตรงกลาง ไม่ว่าความยาวจะเท่าใด

### การบันทึกค่าที่ซ่อน (ทางเลือก)

หากคุณต้องการบันทึกการตรวจสอบ ให้ส่งแฟล็กผ่าน `custom_settings` และปรับฟังก์ชัน:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

จากนั้นลงทะเบียนด้วย:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## ตัวอย่างทำงานเต็ม (พร้อมคัดลอก‑วาง)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

การรันสคริปต์นี้บนใบเสร็จที่มี `4111111111111111` จะให้ผลลัพธ์:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

นี่คือทั้งหมดของ pipeline—จาก OCR ดิบถึง **data sanitization**—ห่อหุ้มด้วยไม่กี่บรรทัดของ Python ที่สะอาด

---

## สรุป

เราได้แสดงวิธี **ซ่อนหมายเลขบัตรเครดิต** ในผลลัพธ์ OCR ด้วย post‑processing hook ของ AsposeAI, ขั้นตอน regular‑expression ที่กระชับ, และเคล็ดลับปฏิบัติที่ดีที่สุดสำหรับ **PCI compliance**. วิธีแก้ปัญหานี้เป็นอิสระเต็มรูปแบบ ทำงานกับภาพใด ๆ ที่ OCR engine สามารถอ่านได้ และสามารถขยายเพื่อรองรับรูปแบบบัตรที่ซับซ้อนหรือความต้องการบันทึกเพิ่มเติม

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองเชื่อมต่อการซ่อนนี้กับขั้นตอน **database insertion** ที่เก็บเฉพาะสี่หลักสุดท้ายเพื่ออ้างอิง, หรือรวมกับ **batch processor** ที่สแกนโฟลเดอร์ใบเสร็จทั้งหมดในช่วงคืน คุณอาจสำรวจงาน **OCR post‑processing** อื่น ๆ เช่น การทำมาตรฐานที่อยู่หรือการตรวจจับภาษา—แต่ละงานใช้รูปแบบเดียวกับที่เราใช้ที่นี่

มีคำถามเกี่ยวกับกรณีขอบ, ประสิทธิภาพ, หรือวิธีปรับโค้ดให้เข้ากับไลบรารี OCR อื่น? แสดงความคิดเห็นด้านล่างและเราจะสนทนาต่อไป ขอให้เขียนโค้ดอย่างสนุกและปลอดภัย!

![แผนภาพแสดงวิธีการซ่อนหมายเลขบัตรเครดิตทำงานใน pipeline ของ OCR](https://example.com/images/ocr-mask-flow.png "แผนภาพของการซ่อนในขั้นตอน post‑processing ของ OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}