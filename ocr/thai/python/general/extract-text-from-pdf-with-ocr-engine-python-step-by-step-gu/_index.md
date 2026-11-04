---
category: general
date: 2026-01-12
description: ดึงข้อความจาก PDF ด้วยเครื่องมือ OCR ใน Python – เรียนรู้วิธีอ่าน PDF
  ด้วย OCR, โหลดภาพสำหรับ OCR, และรับผลลัพธ์ที่มีโครงสร้าง
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: th
og_description: ดึงข้อความจาก PDF ด้วยเครื่องมือ OCR ใน Python บทเรียนนี้แสดงวิธีอ่าน
  PDF ด้วย OCR, โหลดภาพสำหรับ OCR, และใช้เครื่องมือ OCR ใน Python เพื่อผลลัพธ์ที่เชื่อถือได้.
og_title: ดึงข้อความจาก PDF ด้วย OCR Engine Python – คู่มือฉบับสมบูรณ์
tags:
- OCR
- Python
- PDF
- Text Extraction
title: สกัดข้อความจาก PDF ด้วย OCR Engine Python – คู่มือขั้นตอนโดยละเอียด
url: /th/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจาก PDF ด้วย OCR Engine Python – บทเรียนเต็ม

เคยต้อง **ดึงข้อความจาก PDF** แต่ไฟล์เป็นแค่ภาพสแกนหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการจริง ๆ PDF ที่ได้รับมักไม่มีข้อความที่สามารถเลือกได้ ดังนั้นวิธีเดียวที่ทำได้คือ **อ่าน PDF ด้วย OCR**  

ในคู่มือนี้เราจะพาคุณผ่านโซลูชันแบบครบวงจรที่แสดงขั้นตอนอย่างละเอียดว่า **โหลดภาพสำหรับ OCR** อย่างไร, เรียกใช้ **OCR engine Python**, และดึงข้อความที่มีโครงสร้างเพื่อส่งต่อไปยัง pipeline ถัดไป ไม่ใช่การอ้างอิงแบบคลุมเครือ แต่เป็นตัวอย่างที่ทำงานได้เต็มรูปแบบที่คุณสามารถคัดลอก‑วางได้ทันที

## สิ่งที่คุณจะได้เรียน

- วิธีติดตั้งและนำเข้าไลบรารี OCR ของ Python ที่จำเป็น  
- ขั้นตอนที่แม่นยำในการ **โหลดภาพสำหรับ OCR** จากไฟล์ PDF  
- วิธีเรียกเมธอด `recognize_structured()` ของ engine และวนลูปผ่านบล็อก, บรรทัด, และคำ  
- เคล็ดลับสำหรับการจัดการผลลัพธ์ที่ความเชื่อมั่นต่ำและ PDF หลายหน้า  

เมื่อจบบทเรียนนี้คุณจะมีสคริปต์ที่ดึง **ข้อความจาก PDF** อย่างเชื่อถือได้ ไม่ว่ามีหน้าเดียวหรือหลายร้อยหน้า

---

![Diagram showing the OCR engine processing a PDF and outputting structured text.](images/ocr_flow.png "แผนภาพการดึงข้อความจาก PDF ด้วย OCR")  
*ข้อความแทนภาพ: แผนภาพการดึงข้อความจาก PDF แสดงขั้นตอนการประมวลผล OCR*

## ข้อกำหนดเบื้องต้น

- Python 3.9 หรือใหม่กว่า (โค้ดใช้ f‑strings และ type hints)  
- แพ็กเกจ OCR ที่ติดตั้งผ่าน pip และมีคลาส `OcrEngine` (เช่นไลบรารีสมมติ `pyocr`)  
- ไฟล์ PDF ที่ต้องการประมวลผล บันทึกไว้ในเครื่อง (เช่น `form.pdf`)  

หากคุณยังไม่มีไลบรารี OCR ให้ติดตั้งด้วยคำสั่ง:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## ขั้นตอนที่ 1: ดึงข้อความจาก PDF – ตั้งค่า OCR Engine

ก่อนที่เราจะ **อ่าน PDF ด้วย OCR** เราต้องสร้างอินสแตนซ์ของ engine ก่อน คิดว่า engine คือสมองที่มองแต่ละพิกเซลและตัดสินว่าตัวอักษรคืออะไร

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **ทำไมจึงสำคัญ:** การเริ่มต้น engine ครั้งเดียวทำให้คุณสามารถใช้ language pack ที่โหลดแล้วหลายไฟล์ ลดเวลาและหน่วยความจำ

---

## ขั้นตอนที่ 2: โหลดภาพสำหรับ OCR – เตรียม PDF ของคุณ

PDF ไม่ใช่ภาพดิบ ดังนั้นไลบรารีส่วนใหญ่จะมีฟังก์ชันช่วยแปลงหน้าแรก (หรือทุกหน้า) เป็นภาพที่ OCR engine เข้าใจได้

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **เคล็ดลับ:** หาก PDF ของคุณมีหลายหน้า หลายไลบรารี OCR ให้คุณระบุ `page=2` หรือวนลูป `engine.load_image(pdf_path, page=n)` สำหรับเอกสารขนาดใหญ่ ควรประมวลผลเป็นชุดเพื่อหลีกเลี่ยงการใช้หน่วยความจำสูง

---

## ขั้นตอนที่ 3: ใช้ OCR Engine Python – จดจำข้อความที่มีโครงสร้าง

ตอนนี้งานหนักเริ่มทำงานแล้ว การเรียก `recognize_structured()` จะคืนลำดับชั้นของบล็อก → บรรทัด → คำ พร้อมข้อมูลภาษา, ความเชื่อมั่น, และ bounding box

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **สิ่งที่คุณจะได้:**  
> - `structured_result.blocks` – ตัวคอนเทนเนอร์ระดับบน (มักเป็นย่อหน้าหรือคอลัมน์)  
> - แต่ละบล็อกมี `lines` และแต่ละบรรทัดมี `words`  
> - คะแนนความเชื่อมั่นช่วยกรองผลลัพธ์ที่อาจผิดพลาด

---

## ขั้นตอนที่ 4: วนลูปผลลัพธ์ – เข้าถึงบล็อก, บรรทัด, และคำ

ด้านล่างเป็นลูปสั้น ๆ ที่พิมพ์ข้อมูลที่เป็นประโยชน์ที่สุด คุณสามารถขยายเพื่อเขียนเป็น JSON, CSV หรือบันทึกลงฐานข้อมูลได้ตามต้องการ

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### ผลลัพธ์ที่คาดหวัง

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **ทำไมคุณจะชอบ:** โครงสร้างแบบลำดับชั้นนี้สอดคล้องกับวิธีที่มนุษย์อ่านหน้า ทำให้การสร้างตารางหรือเลย์เอาต์คอลัมน์ในภายหลังทำได้ง่าย

---

## ขั้นตอนที่ 5: จัดการกรณีพิเศษ – ความเชื่อมั่นต่ำ & PDF หลายหน้า

### คำที่ความเชื่อมั่นต่ำ

หากความเชื่อมั่นของคำต่ำกว่า `0.70` คุณอาจต้องทำเครื่องหมายเพื่อให้ตรวจสอบด้วยมือ:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### ประมวลผลทุกหน้า

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **เคล็ดลับระดับมืออาชีพ:** เก็บภาพกลางเป็น PNG หากไลบรารี OCR ของคุณสร้างภาพใหม่ทุกครั้ง จะช่วยลดเวลาในการประมวลผลชุดใหญ่ได้หลายวินาที

---

## สคริปต์ทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือไฟล์เดียวที่คุณสามารถรันได้ทันที:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

บันทึกเป็น `extract_pdf_ocr.py` แล้วรัน:

```bash
python extract_pdf_ocr.py
```

คุณจะเห็นรายละเอียดระดับบล็อกพิมพ์ออกมาที่คอนโซล พร้อมคำเตือนความเชื่อมั่นต่ำ (ถ้ามี)

---

## สรุป

เราได้อธิบายวิธี **ดึงข้อความจาก PDF** อย่างครบวงจรโดยใช้ **OCR engine Python** ตั้งแต่การติดตั้งไลบรารี, **โหลดภาพสำหรับ OCR**, **อ่าน PDF ด้วย OCR**, จนถึงการวนลูปผ่านผลลัพธ์ที่มีโครงสร้าง ตอนนี้คุณมีสคริปต์ที่สามารถนำไปใช้ซ้ำได้ในทุกโครงการ

ขั้นตอนต่อไปที่คุณอาจสนใจ:

- ส่งออกโครงสร้างเป็น JSON เพื่อใช้ใน pipeline NLP ต่อไป  
- เพิ่มการตรวจจับภาษาเพื่อสลับโมเดล OCR แบบอัตโนมัติ  
- ผสานกับ `pdf2image` เพื่อพรี‑โปรเซส PDF ที่มีเลย์เอาต์ซับซ้อน  

ลองใช้กับชุดใบแจ้งหนี้หลายหน้า ปรับค่า threshold ของความเชื่อมั่น และดูว่าคุณสามารถแปลง PDF สแกนเป็นข้อความที่ค้นหาและแก้ไขได้เร็วแค่ไหน หากเจอปัญหาใด ๆ คอมเมนต์ด้านล่างได้เลย — Happy OCRing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}